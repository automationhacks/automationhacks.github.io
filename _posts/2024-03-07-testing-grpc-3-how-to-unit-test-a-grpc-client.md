---
title: "Testing gRPC #3: How to unit test a gRPC client"
excerpt: "Grasp internals of how a client is written, and unit test it with a positive and negative case with a fake service implementation."
permalink: 2024-03-07-testing-grpc-3-how-to-unit-test-a-grpc-client
published: true
image: /assets/images/2024/03/testing-grpc-3.png
canonical_url: "https://newsletter.automationhacks.io/p/testing-grpc-3-how-to-unit-test-a-grpc-client"
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
    <img src="assets/images/2024/03/testing-grpc-3.png" alt="Image showing male and female developers coding APIs with a screen at the back and some icons like Java etc">
    <figcaption>Image powered by DALL-E 3</figcaption>
</figure>

⏪ Recap:

In the previous blog, we understood how to write a unit test for a gRPC server using InProcessChannel, and InProcessServer and how to set automatic cleanup using GrpcCleanupRule. In case you missed it, please feel free to read it [here](https://automationhacks.io/2024-02-20-testing-grpc-2-how-to-unit-test-a-grpc-server)

⏩ What we’ll learn:

In this blog, we’ll understand how a client could be written for our Grpc service and also how can we unit test that.

Let’s go ⚡

## System under test

Before we understand how the client is written, let’s first grasp how the service is implemented for this method since we have to write a client method for essentially this.

You can see the complete **listFeatures()** method in **RouteGuideServer.java**  below:

```java
RouteGuideServer.java

@Override
public void listFeatures(Rectangle request, StreamObserver<Feature> responseObserver) {
 int left = min(request.getLo().getLongitude(), request.getHi().getLongitude());
 int right = max(request.getLo().getLongitude(), request.getHi().getLongitude());
 int top = max(request.getLo().getLatitude(), request.getHi().getLatitude());
 int bottom = min(request.getLo().getLatitude(), request.getHi().getLatitude());

 for (Feature feature : features) {
   if (!RouteGuideUtil.exists(feature)) {
     continue;
   }

   int lat = feature.getLocation().getLatitude();
   int lon = feature.getLocation().getLongitude();
   if (lon >= left && lon <= right && lat >= bottom && lat <= top) {
     responseObserver.onNext(feature);
   }
 }
 responseObserver.onCompleted();
}
```

Let’s walk through the code and grasp how this server method is implemented

If you observe the method signature, We pass in a `Rectangle request` and `StreamObserver<Feature> responseObserver`

We know from **route_guide.proto**, that **Rectangle** is a collection of 2 **Point** (lo and hi), such that each point has a **latitude** and **longitude**. This represents a bounding rectangle in a map. Think of a rectangle that covers the central part of Bangalore (of course, there could be much better representation to create a geofence but for the sake of simplicity let’s go with this 😏)

Below is the proto in case you need a recap.

route_guide.proto

```java
// Points are represented as latitude-longitude pairs in the E7 representation
// (degrees multiplied by 10**7 and rounded to the nearest integer).
// Latitudes should be in the range +/- 90 degrees and longitude should be in
// the range +/- 180 degrees (inclusive).
message Point {
 int32 latitude = 1;
 int32 longitude = 2;
}

// A latitude-longitude rectangle, represented as two diagonally opposite
// points "lo" and "hi".
message Rectangle {
 // One corner of the rectangle.
 Point lo = 1;

 // The other corner of the rectangle.
 Point hi = 2;
}
```

We also pass in `StreamObserver<Feature> responseObserver` which is used to return a stream of **Feature** objects to the client. The stream could loosely be understood as an array that the client can read either all at once or one object at a time.

```java
public void listFeatures(Rectangle request, StreamObserver<Feature> responseObserver)
```

Let’s look at the service methods body, We then extract 4 corners of the rectangle by finding min and max values from lo and hi longitude and latitudes to get an integer that represents each corner.

```java
 int left = min(request.getLo().getLongitude(), request.getHi().getLongitude());
 int right = max(request.getLo().getLongitude(), request.getHi().getLongitude());
 int top = max(request.getLo().getLatitude(), request.getHi().getLatitude());
 int bottom = min(request.getLo().getLatitude(), request.getHi().getLatitude());
```

Nice, We then iterate in the features already stored in our database (in this example, the features are stored in an in-memory Collection but in a real application this could be any other data store) and check if a feature exists

```java
for (Feature feature : features) {
   if (!RouteGuideUtil.exists(feature)) {
     continue;
   }
```

If you see the **exists()** it just checks if the feature has a valid name

```java
RouteGuideUtil.java

/**
* Indicates whether the given feature exists (i.e. has a valid name).
*/
public static boolean exists(Feature feature) {
 return feature != null && !feature.getName().isEmpty();
}
```

If the feature exists then we check

* if that feature longitude lies between left and right ranges
* and latitude lies between the bottom and top ranges

if we find such a feature then we add it to the responseObserver’s **onNext** method

```java
int lat = feature.getLocation().getLatitude();
   int lon = feature.getLocation().getLongitude();
   if (lon >= left && lon <= right && lat >= bottom && lat <= top) {
     responseObserver.onNext(feature);
   }
```

Finally, we call the **responseObserver.onCompleted();** method to indicate that the rpc call is complete.

## How to Implement a Client

So now we understand what our service is actually doing.

Let’s understand how a client method could be written for `listFeatures()` method

Any client for a service method/operation usually performs 3 functions:

* Construct the request for the service
* Call the service method using either a **blockingStub** or an **asyncStub**(in other words either sync or async call)
* Logs or return the response back for further processing

With above context, We can write a gRPC client for this **listFeatures()** method like below

```java
RouteGuideClient.java

public class RouteGuideClient {
 private static final Logger logger = Logger.getLogger(RouteGuideClient.class.getName());

 private final RouteGuideBlockingStub blockingStub;
 private final RouteGuideStub asyncStub;

 private Random random = new Random();
 private TestHelper testHelper;

 /** Construct client for accessing RouteGuide server using the existing channel. */
 public RouteGuideClient(Channel channel) {
   blockingStub = RouteGuideGrpc.newBlockingStub(channel);
   asyncStub = RouteGuideGrpc.newStub(channel);
 }

/**
* Blocking server-streaming example. Calls listFeatures with a rectangle of interest. Prints each
* response feature as it arrives.
*/
public void listFeatures(int lowLat, int lowLon, int hiLat, int hiLon) {
 info("*** ListFeatures: lowLat={0} lowLon={1} hiLat={2} hiLon={3}", lowLat, lowLon, hiLat,
     hiLon);

 Rectangle request =
     Rectangle.newBuilder()
         .setLo(Point.newBuilder().setLatitude(lowLat).setLongitude(lowLon).build())
         .setHi(Point.newBuilder().setLatitude(hiLat).setLongitude(hiLon).build()).build();

 Iterator<Feature> features;
 try {
   features = blockingStub.listFeatures(request);

   for (int i = 1; features.hasNext(); i++) {
     Feature feature = features.next();
     info("Result #" + i + ": {0}", feature);
     if (testHelper != null) {
       testHelper.onMessage(feature);
     }
   }
 } catch (StatusRuntimeException e) {
   warning("RPC failed: {0}", e.getStatus());
   if (testHelper != null) {
     testHelper.onRpcError(e);
   }
 }
}}
```

### Initialize client

Let’s unpack the client and understand how it works

We start with Initialising our client class `RouteGuideClient` and setup our logger using standard`java.util.logging.Logger;`

```java
public class RouteGuideClient {
 private static final Logger logger = Logger.getLogger(RouteGuideClient.class.getName());
```

Next, We declare a **RouteGuideBlockingStub** and a **RouteGuideStub** to make desired sync or async calls to the server and also initialize few other utilities like **Random** and **TestHelper** which may be used

```java
 private final RouteGuideBlockingStub blockingStub;
 private final RouteGuideStub asyncStub;
 private Random random = new Random();
 private TestHelper testHelper;
```

We then pass in the channel to the client constructor and then initialize our blocking and async stubs using method from **RouteGuideGrpc**

```java
/** Construct client for accessing RouteGuide server using the existing channel. */
 public RouteGuideClient(Channel channel) {
   blockingStub = RouteGuideGrpc.newBlockingStub(channel);
   asyncStub = RouteGuideGrpc.newStub(channel);
 }
```

### listFeatures

We implement our listFeatures client method that accepts 4 int parameters, as we saw before they represent the co-ordinates for bottom left and upper right corners of the bounding rectangle

* lowLat → Latitude for a lower point of the rectangle
* lowLon → Longitude for a lower point of the rectangle
* hiLat → Latitude for the upper point of the rectangle
* hiLon → Longitude for the upper point of the rectangle

```java
public void listFeatures(int lowLat, int lowLon, int hiLat, int hiLon) {
 info("*** ListFeatures: lowLat={0} lowLon={1} hiLat={2} hiLon={3}", lowLat, lowLon, hiLat,
     hiLon);
```

For our client, we prepare our request by constructing the **Rectangle** object that the service expects. We can directly use the **newBuilder()** exposed for each proto and use builder pattern to construct our request

```java
 Rectangle request =
     Rectangle.newBuilder()
         .setLo(Point.newBuilder().setLatitude(lowLat).setLongitude(lowLon).build())
         .setHi(Point.newBuilder().setLatitude(hiLat).setLongitude(hiLon).build()).build();
```

Next, we make the actual request to get our list of features using blockingStub and store it in a collection called `Iterator<Feature>` that we can iterate upon

```java
Iterator<Feature> features;
 try {
   features = blockingStub.listFeatures(request);
```

We then iterate and log each feature found within the specified coordinates. If we catch a **StatusRuntimeException** then we log this as a warning

In a real application, the client might do further processing based on these features but for now, we just log the features received

```java
try {
   features = blockingStub.listFeatures(request);
   for (int i = 1; features.hasNext(); i++) {
     Feature feature = features.next();
     info("Result #" + i + ": {0}", feature);
     if (testHelper != null) {
       testHelper.onMessage(feature);
     }
   }
 } catch (StatusRuntimeException e) {
   warning("RPC failed: {0}", e.getStatus());
   if (testHelper != null) {
     testHelper.onRpcError(e);
   }
 }
```

## How to unit test a client

So now, we understand the basics

* How the service method under test is implemented
* How is the client for such a service written

Let’s come to the fun part.

How will we ensure our client works fine?

Of course, we write a test

You can find the complete test [examples/src/test/java/io/grpc/examples/routeguide/RouteGuideClientTest.java](https://github.com/grpc/grpc-java/blob/v1.60.x/examples/src/test/java/io/grpc/examples/routeguide/RouteGuideClientTest.java) but we’ll focus on how to write a test for listFeatures()

```java
RouteGuideClientTest.java

@RunWith(JUnit4.class)
public class RouteGuideClientTest {
 /**
  * This rule manages automatic graceful shutdown for the registered server at the end of test.
  */
 @Rule
 public final GrpcCleanupRule grpcCleanup = new GrpcCleanupRule();

 private final MutableHandlerRegistry serviceRegistry = new MutableHandlerRegistry();
 private final TestHelper testHelper = mock(TestHelper.class);
 private final Random noRandomness =
     new Random() {
       int index;
       boolean isForSleep;

       /**
        * Returns a number deterministically. If the random number is for sleep time, then return
        * -500 so that {@code Thread.sleep(random.nextInt(1000) + 500)} sleeps 0 ms. Otherwise, it
        * is for list index, then return incrementally (and cyclically).
        */
       @Override
       public int nextInt(int bound) {
         int retVal = isForSleep ? -500 : (index++ % bound);
         isForSleep = ! isForSleep;
         return retVal;
       }
     };
 private RouteGuideClient client;

 @Before
 public void setUp() throws Exception {
   // Generate a unique in-process server name.
   String serverName = InProcessServerBuilder.generateName();
   // Use a mutable service registry for later registering the service impl for each test case.
   grpcCleanup.register(InProcessServerBuilder.forName(serverName)
       .fallbackHandlerRegistry(serviceRegistry).directExecutor().build().start());
   client = new RouteGuideClient(grpcCleanup.register(
       InProcessChannelBuilder.forName(serverName).directExecutor().build()));
   client.setTestHelper(testHelper);
 }

/**
* Example for testing blocking server-streaming.
*/
@Test
public void listFeatures() {
 final Feature responseFeature1 = Feature.newBuilder().setName("feature 1").build();
 final Feature responseFeature2 = Feature.newBuilder().setName("feature 2").build();
 final AtomicReference<Rectangle> rectangleDelivered = new AtomicReference<Rectangle>();

 // implement the fake service
 RouteGuideImplBase listFeaturesImpl =
     new RouteGuideImplBase() {
       @Override
       public void listFeatures(Rectangle rectangle, StreamObserver<Feature> responseObserver) {
         rectangleDelivered.set(rectangle);

         // send two response messages
         responseObserver.onNext(responseFeature1);
         responseObserver.onNext(responseFeature2);

         // complete the response
         responseObserver.onCompleted();
       }
     };
 serviceRegistry.addService(listFeaturesImpl);

 client.listFeatures(1, 2, 3, 4);

 assertEquals(Rectangle.newBuilder()
                  .setLo(Point.newBuilder().setLatitude(1).setLongitude(2).build())
                  .setHi(Point.newBuilder().setLatitude(3).setLongitude(4).build())
                  .build(),
              rectangleDelivered.get());
 verify(testHelper).onMessage(responseFeature1);
 verify(testHelper).onMessage(responseFeature2);
 verify(testHelper, never()).onRpcError(any(Throwable.class));
}

/**
* Example for testing blocking server-streaming.
*/
@Test
public void listFeatures_error() {
 final Feature responseFeature1 =
     Feature.newBuilder().setName("feature 1").build();
 final AtomicReference<Rectangle> rectangleDelivered = new AtomicReference<Rectangle>();
 final StatusRuntimeException fakeError = new StatusRuntimeException(Status.INVALID_ARGUMENT);

 // implement the fake service
 RouteGuideImplBase listFeaturesImpl =
     new RouteGuideImplBase() {
       @Override
       public void listFeatures(Rectangle rectangle, StreamObserver<Feature> responseObserver) {
         rectangleDelivered.set(rectangle);

         // send one response message
         responseObserver.onNext(responseFeature1);

         // let the rpc fail
         responseObserver.onError(fakeError);
       }
     };
 serviceRegistry.addService(listFeaturesImpl);

 client.listFeatures(1, 2, 3, 4);

 assertEquals(Rectangle.newBuilder()
                  .setLo(Point.newBuilder().setLatitude(1).setLongitude(2).build())
                  .setHi(Point.newBuilder().setLatitude(3).setLongitude(4).build())
                  .build(),
              rectangleDelivered.get());
 ArgumentCaptor<Throwable> errorCaptor = ArgumentCaptor.forClass(Throwable.class);
 verify(testHelper).onMessage(responseFeature1);
 verify(testHelper).onRpcError(errorCaptor.capture());
 assertEquals(fakeError.getStatus(), Status.fromThrowable(errorCaptor.getValue()));
}
```

}

I know, its a lot. 🤟

Let’s break it down step by step and grasp how this works

### Test Structure

The code is a test class named **RouteGuideClientTest** designed to test a client for communicating with a service called RouteGuide. It uses JUnit4 as we saw before

```java
@RunWith(JUnit4.class)
public class RouteGuideClientTest {}
```

### Automatic Cleanup

* The **@Rule** annotation tells JUnit to manage an instance of **GrpcCleanupRule**.
* This rule ensures that test servers are automatically shut down after each test, keeping the test environment clean.

```java
/**
  * This rule manages automatic graceful shutdown for the registered server at the end of test.
  */
 @Rule
 public final GrpcCleanupRule grpcCleanup = new GrpcCleanupRule();
```

### Setup

```java
@Before
 public void setUp() throws Exception {
   // Generate a unique in-process server name.
   String serverName = InProcessServerBuilder.generateName();
   // Use a mutable service registry for later registering the service impl for each test case.
   grpcCleanup.register(InProcessServerBuilder.forName(serverName)
       .fallbackHandlerRegistry(serviceRegistry).directExecutor().build().start());
   client = new RouteGuideClient(grpcCleanup.register(
       InProcessChannelBuilder.forName(serverName).directExecutor().build()));
   client.setTestHelper(testHelper);
 }
```

We write **@Before** annotated **setUp** method to ensure each test method starts with a unique instance of the client

We create a unique in-process server (running within the same process)

```java
// Generate a unique in-process server name.
   String serverName = InProcessServerBuilder.generateName();
```

We also use a registry to allow different services to be registered for different test cases.

```java
// Use a mutable service registry for later registering the service impl for each test case.
   grpcCleanup.register(InProcessServerBuilder.forName(serverName) .fallbackHandlerRegistry(serviceRegistry).directExecutor().build().start());
```

We then initialize the client and pass it the channel which is also registered for auto cleanup

```java
client = new RouteGuideClient(grpcCleanup.register(
       InProcessChannelBuilder.forName(serverName).directExecutor().build()));
```

We inject a mock object called **testHelper** for observing calls and verifying behavior. We’ll see that this is an interface that exposes

```java
client.setTestHelper(testHelper);
```

### Tests

We then write 2 unit tests that do below on a high level:

* **listFeatures**: This tests successful communication with the server simulating a positive case
  * Creates a fake service implementation to control server behavior.
  * Calls the client's listFeatures method to initiate communication.
  * Asserts that the correct request was sent and the expected responses were received.
* **listFeatures_error**: Tests how the client handles errors.
  * Set up a fake service that throws an error.
  * Verifies that the client properly propagates the error to the test helper.

#### ✅ Positive case

Let’s unpack the positive case first to understand this a bit better

Below is the complete test at a glance. We will do a walkthrough on it below:

```java
/**
* Example for testing blocking server-streaming.
*/
@Test
public void listFeatures() {
 final Feature responseFeature1 = Feature.newBuilder().setName("feature 1").build();
 final Feature responseFeature2 = Feature.newBuilder().setName("feature 2").build();
 final AtomicReference<Rectangle> rectangleDelivered = new AtomicReference<Rectangle>();

 // implement the fake service
 RouteGuideImplBase listFeaturesImpl =
     new RouteGuideImplBase() {
       @Override
       public void listFeatures(Rectangle rectangle, StreamObserver<Feature> responseObserver) {
         rectangleDelivered.set(rectangle);

         // send two response messages
         responseObserver.onNext(responseFeature1);
         responseObserver.onNext(responseFeature2);

         // complete the response
         responseObserver.onCompleted();
       }
     };
 serviceRegistry.addService(listFeaturesImpl);

 client.listFeatures(1, 2, 3, 4);

 assertEquals(Rectangle.newBuilder()
                  .setLo(Point.newBuilder().setLatitude(1).setLongitude(2).build())
                  .setHi(Point.newBuilder().setLatitude(3).setLongitude(4).build())
                  .build(),
              rectangleDelivered.get());
 verify(testHelper).onMessage(responseFeature1);
 verify(testHelper).onMessage(responseFeature2);
 verify(testHelper, never()).onRpcError(any(Throwable.class));
}
```

Alright, let’s break this down.

We first annotate our method with **@Test** and then build two feature objects by using the builder as before by passing in the name as “feature 1” and “feature 2”

```java
@Test
public void listFeatures() {
 final Feature responseFeature1 = Feature.newBuilder().setName("feature 1").build();
 final Feature responseFeature2 = Feature.newBuilder().setName("feature 2").build();
```

We create a thread-safe reference to the **Rectangle** object using Java [AtomicReference](https://stackoverflow.com/questions/3964211/when-to-use-atomicreference-in-java)

```java
final AtomicReference<Rectangle> rectangleDelivered = new AtomicReference<Rectangle>();
```

In this test, we are **only interested in testing our client**, thus we create a fake service implementation for **listFeatures** method. This ensures isolation for this unit test.

To do so, we construct **new RouteGuideImplBase()**and define our [anonymous subclass](https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html) by overriding the **listFeatures** method like below

```java
// implement the fake service
 RouteGuideImplBase listFeaturesImpl =
     new RouteGuideImplBase() {
       @Override
       public void listFeatures(Rectangle rectangle, StreamObserver<Feature> responseObserver) {
```

Inside the body, we set the rectangle passed in from the request into the `AtomicReference<Rectangle>` rectangleDelivered we had defined earlier

```java
rectangleDelivered.set(rectangle);
```

We also want the server to stream and return the two features we had earlier created to the client, thus we use the **onNext()** method in **responseObserver** to do so. This is a way for gRPC to provide [server-side streaming](https://grpc.io/docs/what-is-grpc/core-concepts/#server-streaming-rpc)

```java
// send two response messages
responseObserver.onNext(responseFeature1);
responseObserver.onNext(responseFeature2);
```

Finally, we complete the RPC by calling **onCompleted()** method

```java
// complete the response
responseObserver.onCompleted();
```

We can see the complete fake service implementation below.

```java
// implement the fake service
 RouteGuideImplBase listFeaturesImpl =
     new RouteGuideImplBase() {
       @Override
       public void listFeatures(Rectangle rectangle, StreamObserver<Feature> responseObserver) {
         rectangleDelivered.set(rectangle);

         // send two response messages
         responseObserver.onNext(responseFeature1);
         responseObserver.onNext(responseFeature2);

         // complete the response
         responseObserver.onCompleted();
       }
     };
```

Now, we will add this fake service to our **service registry** as below

```java
serviceRegistry.addService(listFeaturesImpl);
```

Awesome, Let’s make our service call via the client. Here 1, 2, 3, and 4 are the lat and longs for the lower left and upper right corner of the rectangle as we saw before.

```java
client.listFeatures(1, 2, 3, 4);
```

After making the call, we should check whether the rectangle object returned from the response matches what we expect with the below

```java
assertEquals(Rectangle.newBuilder()
                  .setLo(Point.newBuilder().setLatitude(1).setLongitude(2).build())
                  .setHi(Point.newBuilder().setLatitude(3).setLongitude(4).build())
                  .build(),
              rectangleDelivered.get());
```

Lastly, we also need to verify if our client actually called our fake service. We can ensure that using [verify() method from Mockito library](https://www.digitalocean.com/community/tutorials/mockito-verify)

We use the **verify()** method from Mockito library to verify interactions with the mocked object **testHelper**as below

```java
verify(testHelper).onMessage(responseFeature1);
verify(testHelper).onMessage(responseFeature2);
```

This interface is defined in **[RouteGuideClient.java](https://github.com/grpc/grpc-java/blob/eb8b1d8379008ab89cade89392d265bed90a2692/examples/src/main/java/io/grpc/examples/routeguide/RouteGuideClient.java#L315)** as below and if we go over its definition, it exposes two methods onMessage() and onRpcError. We can use this to ensure the client calls the **onMessage()** method with **responseFeature1** and then with **responseFeature2**

```java
/**
* Only used for helping unit test.
*/
@VisibleForTesting
interface TestHelper {
 /**
  * Used for verify/inspect message received from server.
  */
 void onMessage(Message message);

 /**
  * Used for verify/inspect error received from server.
  */
 void onRpcError(Throwable exception);
}
```

We also ensure that the **onRpcError()** method was never called since this is a positive case.

```java
verify(testHelper, never()).onRpcError(any(Throwable.class));
```

You can see other examples of verify() and never() method calls and their usages on [mockito docs](https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html#4)

#### ⛔ Negative test

How would we write a negative test for our client?

In this test, We want to check what happens when our service throws an RPC error

The initial setup is identical, except in this case we only prepare one **responseFeature1**

```java
@Test
public void listFeatures_error() {
 final Feature responseFeature1 =
     Feature.newBuilder().setName("feature 1").build();
 final AtomicReference<Rectangle> rectangleDelivered = new AtomicReference<Rectangle>();
```

We initialize a **fakeError** of StatusRuntimeException type and then initialize it with an INVALID_ARGUMENT value

```java
 final StatusRuntimeException fakeError = new StatusRuntimeException(Status.INVALID_ARGUMENT);
```

We again implement our fake service and repeat the same steps as above:

```java
// implement the fake service
RouteGuideImplBase listFeaturesImpl =
   new RouteGuideImplBase() {
     @Override
     public void listFeatures(Rectangle rectangle, StreamObserver<Feature> responseObserver) {
       rectangleDelivered.set(rectangle);

       // send one response message
       responseObserver.onNext(responseFeature1);

       // let the rpc fail
       responseObserver.onError(fakeError);
     }
   };
```

Notice, the last step. 🔵

We now use the onError method to return the fake error that we had created earlier. In a production app, the service may use this to communicate to the client that something went wrong in processing.

```java
responseObserver.onError(fakeError);
```

We then register our service, call our client with the same input, and assert that the API returns us the similar output by asserting on the rectangle object

```java
serviceRegistry.addService(listFeaturesImpl);

client.listFeatures(1, 2, 3, 4);

assertEquals(Rectangle.newBuilder()
                .setLo(Point.newBuilder().setLatitude(1).setLongitude(2).build())
                .setHi(Point.newBuilder().setLatitude(3).setLongitude(4).build())
                .build(),
            rectangleDelivered.get());
```

To verify the service works for our negative scenario

We perform below 4 steps:

* Set up a capture mechanism for errors.
* Verify that a message was received by the service (likely before the error).
* Verify that an RPC error occurred and capture the specific error.
* Assert that the captured error's status matches the expected error status.

Let’s see how this could be implemented using the Mockito library

We check that the **onMessage()** method of the mocked object **testHelper** was invoked with the specific argument **responseFeature1**

```java
verify(testHelper).onMessage(responseFeature1);
```

We define the [ArgumentCaptor](https://www.baeldung.com/mockito-argumentcaptor) class from Mockito to capture any exception of type **Throwable** to our mocked method

```java
ArgumentCaptor<Throwable> errorCaptor = ArgumentCaptor.forClass(Throwable.class);
```

Then, we ensure that **onRpcError()** method of mocked **testHelper** is called and by using **capture()** method of **ArgumentCaptor,**we capture the error returned by the GRPC service

```java
verify(testHelper).onRpcError(errorCaptor.capture());
```

We also assert that the captured error status matches expected **fakeError.getStatus()**by retrieving the captured **Throwable** using **errorCaptor.getValue()** and convert it into a GRPC Status object using **Status.fromThrowable()**

```java
assertEquals(fakeError.getStatus(), Status.fromThrowable(errorCaptor.getValue()));
```

## Conclusion

Let’s recap what we learned in this post:

* We understood how listFeature() method is implemented and how can a gRPC server return a streaming response
* We understood how the client method is written for this service
* Later, we dove into how can we unit test the client
  * We looked into how to write a fake service
  * We implemented a positive case and checked if calls were made using Mockito verify()
  * We implemented a negative case and then checked if error was returned using Mockito ArgumentCaptor

That was lot of ground 🌆, and this wraps up what I wanted to cover with unit testing. There are other aspects to it but I’ll leave that to you to explore with other methods.

Please let me know if you have questions or thoughts in the comments.

In the next post, we will grasp how to write a **functional API test** for this to get confidence that the service works when dealing with live data.

Thanks for the time you spent reading this 🙌. If you found this post helpful, please share it and follow me (**@automationhacks**) for more such insights in Software **Testing** and **Automation**. Until next time 👋, Happy Testing 🕵🏻 and Learning! 🌱| [Newsletter](https://newsletter.automationhacks.io/) | [YouTube](https://www.youtube.com/@automationhacks) | [Blog](https://automationhacks.io/) | [LinkedIn](https://www.linkedin.com/in/automationhacks/) | [Twitter](https://twitter.com/automationhacks).
