---
title: "Testing gRPC #2: How to unit test a gRPC server"
excerpt: "How is a service method implemented, What is the basic anatomy of a server unit test, grasp GrpcCleanupRule, InProcessServer and InProcessChannel. Let’s go ⚡"
permalink: 2024-02-20-testing-grpc-2-how-to-unit-test-a-grpc-server
published: true
image: /assets/images/2024/02/testing-grpc-2.png
canonical_url: "https://newsletter.automationhacks.io/p/testing-grpc-2-how-to-unit-test-a"
categories:
  - "Software Engineering"
  - "Software Testing"
  - "gRPC"
  - "Backend automation"
tags:
  - "Software Engineering"
  - "Software Testing"
  - "gRPC"
---

<figure class="image">
    <img src="assets/images/2024/02/testing-grpc-2.png" alt="Image showing male developers coding APIs with gRPC written on a big screen">
</figure>

Hi folks,

In the previous post, we grasped what gRPC technology is, its features, what are protocol buffers and then spun up an example gRPC server for route guide API and inspected its methods via gRPC web UI.

Please feel free to [read that before](https://newsletter.automationhacks.io/p/testing-grpc-1-set-up-a-grpc-server) this one to build the required context.

In this blog, we’ll dive into how to write a unit test for the server (or the service)

To recap, we have a gRPC server and a client-generated for us for the protobuf compiler automatically.

How will we test it?

There are a few options in front of us:

- We could also write up unit tests to test each functionality
- We could also test integration between services with automated integration tests.
  - Essentially cover cases like Service A depends on Service B and we write a test such that Service A calls Service B (with mocked backend) to verify the two services together will work fine.
- We could write up some API tests to automate the above to test the live API with live backends.
  - While this method is prone to failures and flakiness due to live environments, this is how users would be using your API so this is a must-have in your test strategy.
- We could simulate load on these APIs and test for their resilience, reliability, and performance
- We could exploratory test these APIs by manually passing in different requests and verifying their response, This is a great way to understand the API better and understand the functionality however not scalable with the fast pace of CI/CD

Let’s explore writing a unit test as that is the lowest fidelity and fastest test we can write.

With gRPC, we could write a unit test for the client and the server individually

## Anatomy of a gRPC server unit test

### Method under test

Let’s say we want to test the GetFeature method of our server

Below is how the RouteGuide service looks like:

```java
private static class RouteGuideService extends RouteGuideGrpc.RouteGuideImplBase {
 private final Collection<Feature> features;
 private final ConcurrentMap<Point, List<RouteNote>> routeNotes =
     new ConcurrentHashMap<Point, List<RouteNote>>();

 RouteGuideService(Collection<Feature> features) {
   this.features = features;
 }

 /**
  * Gets the {@link Feature} at the requested {@link Point}. If no feature at that location
  * exists, an unnamed feature is returned at the provided location.
  *
  * @param request the requested location for the feature.
  * @param responseObserver the observer that will receive the feature at the requested point.
  */
 @Override
 public void getFeature(Point request, StreamObserver<Feature> responseObserver) {
   responseObserver.onNext(checkFeature(request));
   responseObserver.onCompleted();
 }

/**
* Gets the feature at the given point.
*
* @param location the location to check.
* @return The feature object at the point. Note that an empty name indicates no feature.
*/
private Feature checkFeature(Point location) {
 for (Feature feature : features) {
   if (feature.getLocation().getLatitude() == location.getLatitude()
       && feature.getLocation().getLongitude() == location.getLongitude()) {
     return feature;
   }
 }

 // No feature was found, return an unnamed feature.
 return Feature.newBuilder().setName("").setLocation(location).build();
}
```

}

What does this method do?

- The getFeature() method accepts a Point and returns a Feature wrapped with StreamObserver on the onNext() method.
- If we navigate to the checkFeature() method, it takes the Point and then iterates in its list of Features:
  - and checks if the Point is present in the list of Features, if it finds the feature then it returns it
  - otherwise it returns a Feature object with name as empty

You can see the full server implementation [here](https://github.com/grpc/grpc-java/blob/0d39c2c7019645a3e4eb40dfb275b0bcd8efaedf/examples/src/main/java/io/grpc/examples/routeguide/RouteGuideServer.java#L137-L140) in grpc-java GitHub repository

### Let’s see the unit test

You can find the full unit test files in the [grpc-java](https://github.com/grpc/grpc-java/tree/master) repository at this path: [grpc/grpc-java/tree/v1.61.x/examples/src/test/java/io/grpc/examples/routeguide](https://github.com/grpc/grpc-java/tree/v1.61.x/examples/src/test/java/io/grpc/examples/routeguide)

We will use the JUnit4 framework to write this test.

Below is the complete test, don’t worry if its too many details right now, we will unpack this step by step and understand its nuts and bolts

```java
@RunWith(JUnit4.class)
public class RouteGuideServerTest {
 /**
  * This rule manages automatic graceful shutdown for the registered channel at the end of test.
  */
 @Rule
 public final GrpcCleanupRule grpcCleanup = new GrpcCleanupRule();

 private RouteGuideServer server;
 private ManagedChannel inProcessChannel;
 private Collection<Feature> features;

 @Before
 public void setUp() throws Exception {
   // Generate a unique in-process server name.
   String serverName = InProcessServerBuilder.generateName();
   features = new ArrayList<>();
   // Use directExecutor for both InProcessServerBuilder and InProcessChannelBuilder can reduce the
   // usage timeouts and latches in test. But we still add timeout and latches where they would be
   // needed if no directExecutor were used, just for demo purpose.
   server = new RouteGuideServer(
       InProcessServerBuilder.forName(serverName).directExecutor(), 0, features);
   server.start();
   // Create a client channel and register for automatic graceful shutdown.
   inProcessChannel = grpcCleanup.register(
       InProcessChannelBuilder.forName(serverName).directExecutor().build());
 }

 @After
 public void tearDown() throws Exception {
   server.stop();
 }

 @Test
 public void getFeature() {
   Point point = Point.newBuilder().setLongitude(1).setLatitude(1).build();
   Feature unnamedFeature = Feature.newBuilder()
       .setName("").setLocation(point).build();
   RouteGuideGrpc.RouteGuideBlockingStub stub = RouteGuideGrpc.newBlockingStub(inProcessChannel);

   // feature not found in the server
   Feature feature = stub.getFeature(point);

   assertEquals(unnamedFeature, feature);

   // feature found in the server
   Feature namedFeature = Feature.newBuilder()
       .setName("name").setLocation(point).build();
   features.add(namedFeature);

   feature = stub.getFeature(point);

   assertEquals(namedFeature, feature);
 }
}
```

### Code Walkthrough

We create a test class and annotate it with **@RunWith(JUnit4.class)** annotation to indicate this is a Junit test

```java
@RunWith(JUnit4.class)
public class RouteGuideServerTest {}
```

We then want to ensure that the **Managed** **channel** and **InProcessServer** created for this test is created and shut down automatically, we can achieve this by using **GrpcCleanupRule.**To see how GrpcCleanupRule works, you can see its full implementation at [grpc/grpc-java/blob/master/testing/src/main/java/io/grpc/testing/GrpcCleanupRule.java](https://github.com/grpc/grpc-java/blob/master/testing/src/main/java/io/grpc/testing/GrpcCleanupRule.java)

```java
@Rule
public final GrpcCleanupRule grpcCleanup = new GrpcCleanupRule();
```

#### What is a channel?

As per [gRPC docs](https://grpc.io/docs/what-is-grpc/core-concepts/#channels):

> A gRPC channel provides a connection to a gRPC server on a specified host and port. It is used when creating a client stub. Clients can specify channel arguments to modify gRPC’s default behavior, such as switching message compression on or off. A channel has a state, including connected and idle.
> How gRPC deals with closing a channel is language-dependent. Some languages also permit querying channel states.

Let’s move on:

We then init some default variables to be used in the test

Notice, We use the RouteGuideServer class to make use of the actual gRPC server

```java
private RouteGuideServer server;
private ManagedChannel inProcessChannel;
private Collection<Feature> features;
```

How should we structure a unit test?

Following the **[arrange act assert cleanup](https://automationpanda.com/2020/07/07/arrange-act-assert-a-pattern-for-writing-good-tests/)** pattern is a great way to write readable tests, let’s first ensure we can spin up our server before the test by writing a setUp() method annotated with **@Before** to indicate that it should be run before each test

```java
@Before
public void setUp() throws Exception {}
```

Within this setup we will use **[InProcessServerBuilder](https://github.com/grpc/grpc-java/blob/0d39c2c7019645a3e4eb40dfb275b0bcd8efaedf/inprocess/src/main/java/io/grpc/inprocess/InProcessServerBuilder.java#L76)** class to generate a unique server name and init our features to an empty array list

```java
// Generate a unique in-process server name.
String serverName = InProcessServerBuilder.generateName();
features = new ArrayList<>();
```

We then want to start our gRPC server within the unit test, we init a **new RouteGuiderServer()** and pass in the server name with the use of **directExecutor()** and our features, we then call the **start()** method on the server to start it.

```java
// Use directExecutor for both InProcessServerBuilder and InProcessChannelBuilder can reduce the
// usage timeouts and latches in test. But we still add timeout and latches where they would be
// needed if no directExecutor were used, just for demo purpose.
server = new RouteGuideServer(
   InProcessServerBuilder.forName(serverName).directExecutor(), 0, features);
server.start();
```

#### Why use directExecutor()

The `directExecutor()` method, available in InProcessServerBuilder and InProcessChannelBuilder, addresses this non-determinism challenge by providing a single-threaded executor for executing tasks within the in-process gRPC server and client.

This executor offers several benefits:

1. **Sequential Task Execution:** By using a single thread, tasks are executed in a strict order without the potential for interleaving or concurrency issues. This eliminates non-deterministic behavior that could arise from multiple threads accessing shared resources or timing-sensitive operations.
2. **Predictable Behavior:** The use of a single thread makes the execution order of tasks more predictable, leading to consistent test results across multiple runs. This is especially useful when testing gRPC interactions that involve callbacks or asynchronous processing, where timing-dependent behavior can cause test flakiness.
3. **Simplified Test Development:** With the executor handling threading logic, you can focus on writing clearer and more concise test code. You don't need to worry about manually managing threads or synchronizing access to shared resources, as the executor ensures sequential execution by design.

We also create an InProcessChannel and register it with our JUnit rule to enable auto shutdown at the end of the test

```java
// Create a client channel and register for automatic graceful shutdown.
   inProcessChannel = grpcCleanup.register(
       InProcessChannelBuilder.forName(serverName).directExecutor().build());
```

Following the test run we also want the server to shut down, so let’s add the teardown method as well to take care of the cleanup

```java
@After
public void tearDown() throws Exception {
 server.stop();
}
```

#### Testing GetFeature method

Now to test the **GetFeature()**method we want to ensure that if we pass a valid lat long to the server, it can return any available feature at that point.

We start with writing the skeleton of our method

```java
@Test
public void getFeature() {}
```

Then create a **Point**object and set it in the **Feature** object

```java
Point point = Point.newBuilder().setLongitude(1).setLatitude(1).build();
Feature unnamedFeature = Feature.newBuilder()
   .setName("").setLocation(point).build();
```

Note: Using protobufs has the additional advantage of providing convenience builder methods to create a Java object and also provides serialization and deserialization support

Now to make a gRPC request, we have to initialize a stub.

The stub can also be usually understood as a client that facilitates calling gRPC server methods and returning a response over the wire as if it was run locally

We create a sync **RouteGuideBlockingStub**and initialize it with the **inProcessChannel**we created earlier, below is how a stub can be created:

```java
RouteGuideGrpc.RouteGuideBlockingStub stub = RouteGuideGrpc.newBlockingStub(inProcessChannel);
```

If you remember from our service, our service method returns an empty response if it does not find the feature at a given point, let’s assert that in our unit test

```java
// feature not found in the server
Feature feature = stub.getFeature(point);
assertEquals(unnamedFeature, feature);
```

On the other hand, if the given point has a feature then we expect that as a response from the server, to test that we can create a **namedFeature**with a value **“name”**and add it to our **features list**

Now when we again call the server with this the same point, we should expect the server to return us a response similar to **namedFeature**

```java
// feature found in the server
Feature namedFeature = Feature.newBuilder()
   .setName("name").setLocation(point).build();
features.add(namedFeature);

feature = stub.getFeature(point);
assertEquals(namedFeature, feature);
```

#### No mocks?

If you notice above, we did not create any mock but instead created our server with **InProcessServer** and then tested our stub with an **InProcessChannel**

gRPC authors [explain this philosophy](https://github.com/grpc/grpc-java/blob/master/examples/README.md#unit-test-examples) much better below:

> In general, we DO NOT allow overriding the client stub and we DO NOT support mocking final methods in gRPC-Java library. Users should be cautious that using tools like PowerMock or [mockito-inline](https://search.maven.org/search?q=g:org.mockito%20a:mockito-inline) can easily break this rule of thumb. We encourage users to leverage InProcessTransport as demonstrated in the examples to write unit tests. InProcessTransport is lightweight and runs the server and client in the same process without any socket/TCP connection.
> Mocking the client stub provides a false sense of security when writing tests.
> Mocking stubs and responses allow for tests that don't map to reality, causing the tests to pass, but the system-under-test to fail. The gRPC client library is complicated, and accurately reproducing that complexity with mocks is very hard. You will be better off and write less code by using InProcessTransport instead.
> Example bugs not caught by mocked stub tests include:

> - Calling the stub with a null message
> - Not calling close()
> - Sending invalid headers
> - Ignoring deadlines
> - Ignoring cancellation

> For testing a gRPC client, create the client with a real stub using an [InProcessChannel](https://github.com/grpc/grpc-java/blob/master/core/src/main/java/io/grpc/inprocess/InProcessChannelBuilder.java), and test it against an [InProcessServer](https://github.com/grpc/grpc-java/blob/master/core/src/main/java/io/grpc/inprocess/InProcessServerBuilder.java) with a mock/fake service implementation.

> For testing a gRPC server, create the server as an InProcessServer, and test it against a real client stub with an InProcessChannel.

> The `grpc-java` library also provides a JUnit rule, [GrpcCleanupRule](https://github.com/grpc/grpc-java/blob/master/testing/src/main/java/io/grpc/testing/GrpcCleanupRule.java), to do the graceful shutdown boilerplate for you.

#### Does the test pass?

With that said

Let's run these unit tests:

```
./gradlew test --tests RouteGuideServerTest
```

We can see below logs:

```
BUILD SUCCESSFUL in 351ms
9 actionable tasks: 9 up-to-date
```

#### Does it catch bugs?

Assume hypothetically, we introduce a bug wherein our service returns a name when a given point is not present in the list of features, would our unit test catch it?

Let’s tweak the test to change the feature name at the point as **Hola**

```java
Feature unnamedFeature = Feature.newBuilder()
   .setName("Hola").setLocation(point).build();
RouteGuideGrpc.RouteGuideBlockingStub stub = RouteGuideGrpc.newBlockingStub(inProcessChannel);

// feature not found in the server
Feature feature = stub.getFeature(point);

assertEquals(unnamedFeature, feature);
```

And run the test again:

We can see that the 1st test now fails with the below error message:

```shell
io.grpc.examples.routeguide.RouteGuideServerTest > getFeature FAILED
    java.lang.AssertionError: expected:<name: "Hola"
    location {
      latitude: 1
      longitude: 1
    }
    > but was:<location {
      latitude: 1
      longitude: 1
    }
    >
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at io.grpc.examples.routeguide.RouteGuideServerTest.getFeature(RouteGuideServerTest.java:100)
```

Which is precisely what we expected.

Congratulations! 🎀You’ve written your first gRPC unit test for the server. There are examples of testing the other 3 methods exposed by this API. Please feel free to see those [here](https://github.com/grpc/grpc-java/blob/v1.61.x/examples/src/test/java/io/grpc/examples/routeguide/RouteGuideServerTest.java), once you understand the basic anatomy of the test, you’ll see the same format being followed across. We will just change our test basis the server method that we are testing.

In the follow-up post, we will understand how to unit test our client.

Thanks for the time you spent reading this 🙌. If you found this post helpful, please share it with your friends and follow me (**@automationhacks**) for more such insights in Software **Testing** and **Automation**. Until next time, Happy Testing 🕵🏻 and Learning! 🌱| [Newsletter](https://newsletter.automationhacks.io/) | [YouTube](https://www.youtube.com/@automationhacks) | [Blog](https://automationhacks.io/) | [LinkedIn](https://www.linkedin.com/in/automationhacks/) | [Twitter](https://twitter.com/automationhacks).
