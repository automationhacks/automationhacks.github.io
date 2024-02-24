---
title: "Testing gRPC #1: Set up a gRPC server and make an API call via gRPC UI"
excerpt: "What is gRPC, its basic nuts and bolts, how to setup a server and explore APIs via gRPC web UI"
permalink: 2024-02-17-testing-grpc-set-up-server-and-hit-api-using-grpcui
published: true
image: /assets/images/2024/02/testing-grpc-2.png
canonical_url: "https://newsletter.automationhacks.io/p/testing-grpc-1-set-up-a-grpc-server"
categories:
  - Software Engineering
  - Software Testing
  - gRPC
tags:
  - "Software Engineering"
  - "Software Testing"
  - "gRPC"
---

<figure class="image">
    <img src="assets/images/2024/02/testing-grpc-1.png" alt="Image showing a male and female developer coding APIs with gRPC written at the back of their laptop">
</figure>

Hi everyone,

I’ve been busy testing and automating some gRPC APIs at work for the past 6 months and I’ve found this technology fascinating.

While HTTP APIs are discussed extensively in blogs and conference talks, curiously gRPC is still a less talked about technology in the Quality engineering space. Let’s change that, shall we?

## Why should you read this? ❓

In this blog series, we’ll take a deeper look at gRPC from the lens of a Software Engineer looking to test all the different aspects. If your org uses gRPC this may help solidify its concepts and help you to test better. If not, who knows you may come across this technology in the future and can come back to this series

What will we learn in this series?

- gRPC concepts such as client stub, protocol buffers, blocking, and async calls
- Set up a gRPC server and a client for an example service
- How to do unit testing
- How to do functional API testing
- Performance test these APIs

By the end of this series, I want to personally have a deeper intuition of how to approach all testing at these different layers and take you along with me on this learning journey.

This will be a ton of fun 💖.

I hope you are as excited to start on this learning journey with me. 🏃

## What is gRPC?

[gRPC](https://grpc.io/docs/what-is-grpc/) stands for **Google** **Remote Procedure call,** It is a modern framework to design APIs so that a client can call a method with some params on a remote server (running on a different machine) as if it were a local object.

gRPC uses [protocol buffers](https://protobuf.dev/) to define the service and enable serialization/de-serialization. It is essentially an interface definition language (IDL) and we can generate client and server code in any supported language (C++, Java, Python… etc) using a proto compiler.

![gRPC server and client](assets/images/2024/02/grpc-server-client.png)

Source: [Introduction to gRPC](https://grpc.io/docs/what-is-grpc/introduction/)

### Why gRPC?

- Clients (stub) could call any method defined within a service
- gRPC is language agnostic i.e. clients could be written in one language (Ruby, Java) and served in another one (C++)
- gRPC allows for full duplex streaming i.e. client streaming, server streaming, or bi-directional streaming of messages such that clients and servers can issue read or write streams in any order.
- It supports sync and async flows
- Mobile Clients can use advanced streaming and connection features that help save bandwidth and make fewer TCP connections to save battery life and CPU usage
- gRPC provides advanced load balancing and failover, cascading call cancellation, interaction with flow control at the application layer
- Uses static paths in URLs for performance reasons and reducing the cost of parsing query, path, and payload body
- Has formalized set of errors that are more directly applicable to APIs than HTTP status code

If you prefer watching a video, you can watch from ByteByteGo for a quick overview or from IBM Cloud

## Protocol buffers

[Protocol Buffers](https://protobuf.dev/) (protobufs) are used as the **IDL (Interface definition language)** to define the gRPC service, essentially this means we can define what methods would this server/API expose along with what params would be passed in, and what response would be returned.

Protobufs are also used as the **message exchange format** to define the request/response formats and then using a **proto compiler (protoc)**, we can generate client and server code in the supported languages.

What are some advantages of using protocol buffers?

- Compact data storage
- Fast parsing
- Language and platform-neutral
- Extensible data format for structured data
- Protocol buffers support the [addition and deletion of fields without breaking any existing service](https://protobuf.dev/overview/#updating-defs)

How are protocol buffers used?

![How do protocol buffers work](assets/images/2024/02/protocol-buffers-concepts.png)

Source: [How do protocol buffers work](https://protobuf.dev/overview/#work)

For example: below **Person.proto** generates below Java class **Person.java**

```java
Person.proto

message Person {
  optional string name = 1;
  optional int32 id = 2;
  optional string email = 3;
}

Person.java

Person john = Person.newBuilder()
    .setId(1234)
    .setName("John Doe")
    .setEmail("jdoe@example.com")
    .build();
output = new FileOutputStream(args[0]);
john.writeTo(output);
```

To generate client and server code using protoc (protocol buffer compiler), Please read [grpc-java/README.md at master](https://github.com/grpc/grpc-java/blob/master/README.md)

## Setup

Now that we have some idea about gRPC and protocol buffers (at least conceptually), let’s get our hands dirty 🤝 and set up a gRPC server and client for an example service to see how these work practically

We will use the Java programming language and I'll be using Java 17 in this example, we will follow the [official gRPC tutorial](https://grpc.io/docs/languages/java/basics/) to set up this app with the client and server

The service that we will set up is called the **route guide**. You can find the code for that in [/grpc/examples/routeguide](https://github.com/grpc/grpc-java/tree/master/examples/src/main/java/io/grpc/examples/routeguide), we will understand the methods it offers as we set it up.

Let’s clone the code using the below

```shell
git clone -b v1.61.0 --depth 1 https://github.com/grpc/grpc-java
```

Note:

We use the `v1.61.0` branch by specifying `-b` in the clone command and `–depth` to do a shallow clone and only get the latest commit. This is to ensure we don’t pull in all the git history

We will change the directory to

```shell
cd grpc-java/examples
```

## Defining service and request, response in proto file

The service request and response types are specified in the proto file [https://github.com/grpc/grpc-java/blob/v1.61.x/examples/src/main/proto/route_guide.proto](https://github.com/grpc/grpc-java/blob/v1.61.x/examples/src/main/proto/route_guide.proto)

To see the service definition, its methods, and request responses, let’s look at the **service RouteGuide**

```proto
syntax = "proto3";

option java_multiple_files = true;
option java_package = "io.grpc.examples.routeguide";
option java_outer_classname = "RouteGuideProto";
option objc_class_prefix = "RTG";

package routeguide;

// Interface exported by the server.
service RouteGuide {
  // A simple RPC.
  //
  // Obtains the feature at a given position.
  //
  // A feature with an empty name is returned if there's no feature at the given
  // position.
  rpc GetFeature(Point) returns (Feature) {}

  // A server-to-client streaming RPC.
  //
  // Obtains the Features available within the given Rectangle.  Results are
  // streamed rather than returned at once (e.g. in a response message with a
  // repeated field), as the rectangle may cover a large area and contain a
  // huge number of features.
  rpc ListFeatures(Rectangle) returns (stream Feature) {}

  // A client-to-server streaming RPC.
  //
  // Accepts a stream of Points on a route being traversed, returning a
  // RouteSummary when traversal is completed.
  rpc RecordRoute(stream Point) returns (RouteSummary) {}

  // A Bidirectional streaming RPC.
  //
  // Accepts a stream of RouteNotes sent while a route is being traversed,
  // while receiving other RouteNotes (e.g. from other users).
  rpc RouteChat(stream RouteNote) returns (stream RouteNote) {}
}
```

We can see that this service offers 4 different methods

- GetFeature
- ListFeatures
- RecordRoute
- RouteChat.

Each of these provides an example of a different type of RPC call that we can make (simple, server side streaming, client side streaming, bidirectional streaming).

We will grasp them when we test these methods, but for now, you can see that each method accepts a proto and returns either a single proto or a stream of protos (array of protos)

If we look further down in the proto file, we can see how these protos are defined.

- Each proto starts with a keyword **message**
- We specify fields with their appropriate data types like int32, string, or repeated (similar to an array)
- Proto can have other proto messages as its member fields to create a rich representation of data

```proto
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

// A feature names something at a given point.
//
// If a feature could not be named, the name is empty.
message Feature {
  // The name of the feature.
  string name = 1;

  // The point where the feature is detected.
  Point location = 2;
}

// Not used in the RPC.  Instead, this is here for the form serialized to disk.
message FeatureDatabase {
  repeated Feature feature = 1;
}

// A RouteNote is a message sent while at a given point.
message RouteNote {
  // The location from which the message is sent.
  Point location = 1;

  // The message to be sent.
  string message = 2;
}

// A RouteSummary is received in response to a RecordRoute rpc.
//
// It contains the number of individual points received, the number of
// detected features, and the total distance covered as the cumulative sum of
// the distance between each point.
message RouteSummary {
  // The number of points received.
  int32 point_count = 1;

  // The number of known features passed while traversing the route.
  int32 feature_count = 2;

  // The distance covered in metres.
  int32 distance = 3;

  // The duration of the traversal in seconds.
  int32 elapsed_time = 4;
}
```

## Generate server and client code

Given the above service definition, we usually generate client and server interfaces using proto proto-compiler

In the above repo, we can use Gradle to generate these Java classes. You can find these instructions at [https://github.com/grpc/grpc-java/blob/master/README.md](https://github.com/grpc/grpc-java/blob/master/README.md)

We need to ensure the below dependencies are added to our build.gradle file

```groovy
runtimeOnly 'io.grpc:grpc-netty-shaded:1.61.0'
implementation 'io.grpc:grpc-protobuf:1.61.0'
implementation 'io.grpc:grpc-stub:1.61.0'
compileOnly 'org.apache.tomcat:annotations-api:6.0.53' // necessary for Java 9+
```

We need to have below config in our build.gradle file to allow generation of client and server interfaces

```groovy
plugins {
    id 'com.google.protobuf' version '0.9.4'
}

protobuf {
  protoc {
    artifact = "com.google.protobuf:protoc:3.25.1"
  }
  plugins {
    grpc {
      artifact = 'io.grpc:protoc-gen-grpc-java:1.61.0'
    }
  }
  generateProtoTasks {
    all()*.plugins {
      grpc {}
    }
  }
}
```

Note: grpc-java adds config to support both Android and non-android projects and thus the config is slightly more complex. You can see it [here](https://github.com/grpc/grpc-java/blob/v1.61.x/build.gradle#L63-L134)

To ensure latest classes are generated, we should run:

cd examples

```shell
./gradlew installDist -PskipAndroid=true
```

## Running server with reflection and seeing APIs with gRPC UI

And to run the server, run below:

```shell
./build/install/examples/bin/route-guide-server
```

We can now see that we have the server running on **localhost:8980**

```shell
Feb 12, 2024 10:36:08 PM io.grpc.examples.routeguide.RouteGuideServer start
INFO: Server started, listening on 8980
```

Let’s play with these APIs using a command line utility called [grpcui](https://github.com/fullstorydev/grpcui), to install it run below on macOS:

```shell
brew install grpcui
```

Once installed, we can spin up the web app to inspect our gRPC APIs using below:

```shell
grpcui -plaintext localhost:8980
```

When you initially run this, You will see an error message like below, Oh.. no… 🤦

```shell
Failed to compute set of methods to expose: server does not support the reflection API
```

What went wrong here?

The message is pretty self-explanatory.

To play around with APIs with GRPC Web UI you need to enable server reflection support, If curious, read this [tutorial](https://github.com/grpc/grpc-java/blob/master/documentation/server-reflection-tutorial.md) to enable this for the server and understand this in detail

But in short, we need to add package import below and add **ProtoReflectionService** to our **serverBuilder** in `examples/src/main/java/io/grpc/examples/routeguide/RouteGuideServer.java`

```java
import io.grpc.protobuf.services.ProtoReflectionService;

public RouteGuideServer(ServerBuilder<?> serverBuilder, int port, Collection<Feature> features) {
 this.port = port;
 server =
     serverBuilder
         .addService(new RouteGuideService(features))
         .addService(ProtoReflectionService.newInstance())
         .build();
}
```

After making this change, we can again build and run the server as above and start the grpcui

```shell
./gradlew installDist -PskipAndroid=true
./build/install/examples/bin/route-guide-server

# Run this in a different tab that where server is running
grpcui -plaintext localhost:8980
```

We can see that the gRPC UI is up and running. We can see our 4 service methods being available

![API methods for route guide API in GRPC UI](assets/images/2024/02/grpc-web-ui-route-guide-api.png)

We can select the method that we want to test and then select a request payload and call that API directly

Let’s say we want to call GetFeature method with a test latitude and longitude

We can enter a test latitude and longitude in Request Form

![GRPC UI request form](assets/images/2024/02/grpc-web-ui-request-form.png)

Or directly update the request JSON in Raw Request

![GRPC UI raw request](assets/images/2024/02/grpc-web-ui-raw-request.png)

For example, say we want to check any feature at given lat or long

```json
{
  "latitude": -8,
  "longitude": 115
}
```

If there is no feature at the specified location then the API returns an empty name, like below:

```json
{
  "name": "",
  "location": {
    "latitude": -8,
    "longitude": 115
  }
}
```

Congratulations! 🎀 You’ve made your first gRPC API request.

In the follow-up post, we will understand other methods for this API and also understand what a unit test for these API methods looks like

Thanks for the time you spent reading this 🙌. If you found this post helpful, please share it with your friends and follow me (**@automationhacks**) for more such insights in Software **Testing** and **Automation**. Until next time, Happy Testing 🕵🏻 and Learning! 🌱| [Newsletter](https://newsletter.automationhacks.io/) | [YouTube](https://www.youtube.com/@automationhacks) | [Blog](https://automationhacks.io/) | [LinkedIn](https://www.linkedin.com/in/automationhacks/) | [Twitter](https://twitter.com/automationhacks).

## Resources

- Follow [Quick Start Java gRPC](https://grpc.io/docs/languages/java/quickstart/) to understand the components involved
- Read [Introduction to gRPC](https://grpc.io/docs/what-is-grpc/introduction/) and then the [core concepts](https://grpc.io/docs/what-is-grpc/core-concepts/)
- Read [Overview Protocol Buffers Documentation](https://protobuf.dev/overview/) to understand protocol buffers syntax
- Follow [Basics tutorial Java gRPC](https://grpc.io/docs/languages/java/basics/) to understand how to use protocol buffers to define a gRPC service
