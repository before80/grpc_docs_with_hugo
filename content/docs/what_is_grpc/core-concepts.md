+++
title = "核心概念"
weight = 2
date = 2023-05-31T10:39:59+08:00
description = "介绍关键的 gRPC 概念，概述 gRPC 的架构和 RPC 生命周期。"
isCJKLanguage = true
draft = false
+++

# Core concepts, architecture and lifecycle 核心概念、架构和生命周期

> 原文：https://grpc.io/docs/what-is-grpc/core-concepts/

An introduction to key gRPC concepts, with an overview of gRPC architecture and RPC life cycle.

介绍关键的 gRPC 概念，概述 gRPC 的架构和 RPC 生命周期。



Not familiar with gRPC? First read [Introduction to gRPC](https://grpc.io/docs/what-is-grpc/introduction/). For language-specific details, see the quick start, tutorial, and reference documentation for your language of choice.

对 gRPC 不熟悉吗？首先阅读[入门指南](https://grpc.io/docs/what-is-grpc/introduction/)。对于特定语言的详细信息，请参阅您选择的语言的快速入门、教程和参考文档。

### Overview 概述

#### Service definition 服务定义

Like many RPC systems, gRPC is based around the idea of defining a service, specifying the methods that can be called remotely with their parameters and return types. By default, gRPC uses [protocol buffers](https://developers.google.com/protocol-buffers) as the Interface Definition Language (IDL) for describing both the service interface and the structure of the payload messages. It is possible to use other alternatives if desired.

与许多 RPC 系统类似，gRPC 基于定义服务的概念，指定可以远程调用的方法以及它们的参数和返回类型。默认情况下，gRPC 使用[协议缓冲区](https://developers.google.com/protocol-buffers)作为接口定义语言 (IDL)，用于描述服务接口和有效负载消息的结构。如果需要，也可以使用其他替代方案。

```proto
service HelloService {
  rpc SayHello (HelloRequest) returns (HelloResponse);
}

message HelloRequest {
  string greeting = 1;
}

message HelloResponse {
  string reply = 1;
}
```

gRPC lets you define four kinds of service method:

gRPC 允许您定义四种类型的服务方法：

- Unary RPCs where the client sends a single request to the server and gets a single response back, just like a normal function call.

- 一元 RPC：客户端向服务器发送单个请求并获取单个响应，就像普通函数调用一样。

  ```proto
  rpc SayHello(HelloRequest) returns (HelloResponse);
  ```

- Server streaming RPCs where the client sends a request to the server and gets a stream to read a sequence of messages back. The client reads from the returned stream until there are no more messages. gRPC guarantees message ordering within an individual RPC call.

- 服务器流式 RPC：客户端向服务器发送请求并获取一个流以读取一系列的消息。客户端从返回的流中读取，直到没有更多的消息为止。gRPC 保证在单个 RPC 调用中消息的顺序。

  ```proto
  rpc LotsOfReplies(HelloRequest) returns (stream HelloResponse);
  ```

- Client streaming RPCs where the client writes a sequence of messages and sends them to the server, again using a provided stream. Once the client has finished writing the messages, it waits for the server to read them and return its response. Again gRPC guarantees message ordering within an individual RPC call.

- 客户端流式 RPC：客户端编写一系列消息并将它们发送到服务器，再次使用提供的流。客户端完成写入消息后，等待服务器读取它们并返回响应。同样，gRPC 保证在单个 RPC 调用中消息的顺序。

  ```proto
  rpc LotsOfGreetings(stream HelloRequest) returns (HelloResponse);
  ```

- Bidirectional streaming RPCs where both sides send a sequence of messages using a read-write stream. The two streams operate independently, so clients and servers can read and write in whatever order they like: for example, the server could wait to receive all the client messages before writing its responses, or it could alternately read a message then write a message, or some other combination of reads and writes. The order of messages in each stream is preserved.

- 双向流式 RPC：双方都使用读写流发送一系列的消息。两个流独立运行，因此客户端和服务器可以以任何顺序进行读写操作：例如，服务器可以在写入响应之前等待接收所有客户端消息，或者可以交替读取消息然后写入消息，或者进行其他读写组合。每个流中的消息顺序保持不变。

  ```proto
  rpc BidiHello(stream HelloRequest) returns (stream HelloResponse);
  ```

You’ll learn more about the different types of RPC in the [RPC life cycle](https://grpc.io/docs/what-is-grpc/core-concepts/#rpc-life-cycle) section below.

您将在下面的[RPC 生命周期](https://grpc.io/docs/what-is-grpc/core-concepts/#rpc-life-cycle)章节中了解更多关于不同类型的 RPC。

#### Using the API 使用 API

Starting from a service definition in a `.proto` file, gRPC provides protocol buffer compiler plugins that generate client- and server-side code. gRPC users typically call these APIs on the client side and implement the corresponding API on the server side.

从 `.proto` 文件中的服务定义开始，gRPC 提供了协议缓冲区编译器插件，用于生成客户端和服务器端代码。gRPC 用户通常在客户端调用这些 API，并在服务器端实现相应的 API。

- On the server side, the server implements the methods declared by the service and runs a gRPC server to handle client calls. The gRPC infrastructure decodes incoming requests, executes service methods, and encodes service responses.
- 在服务器端，服务器实现了服务声明的方法，并运行 gRPC 服务器来处理客户端调用。gRPC 基础设施解码传入的请求，执行服务方法，并编码服务响应。
- On the client side, the client has a local object known as *stub* (for some languages, the preferred term is *client*) that implements the same methods as the service. The client can then just call those methods on the local object, and the methods wrap the parameters for the call in the appropriate protocol buffer message type, send the requests to the server, and return the server’s protocol buffer responses.
- 在客户端，客户端有一个称为 *stub*（对于某些语言，首选术语是 *client*）的本地对象，实现了与服务相同的方法。然后，客户端只需在本地对象上调用这些方法，方法会将调用的参数封装为适当的协议缓冲区消息类型，将请求发送到服务器，并返回服务器的协议缓冲区响应。

#### Synchronous vs. asynchronous 同步 vs. 异步

Synchronous RPC calls that block until a response arrives from the server are the closest approximation to the abstraction of a procedure call that RPC aspires to. On the other hand, networks are inherently asynchronous and in many scenarios it’s useful to be able to start RPCs without blocking the current thread.

同步的 RPC 调用会阻塞，直到从服务器接收到响应，这是对 RPC 所追求的过程调用抽象的最接近的近似。另一方面，网络本质上是异步的，在许多场景中，能够在不阻塞当前线程的情况下启动 RPC 是很有用的。

The gRPC programming API in most languages comes in both synchronous and asynchronous flavors. You can find out more in each language’s tutorial and reference documentation (complete reference docs are coming soon).

大多数语言中的 gRPC 编程 API 都提供同步和异步两种方式。您可以在各语言的教程和参考文档中了解更多信息（完整的参考文档即将推出）。

### RPC life cycle RPC 生命周期

In this section, you’ll take a closer look at what happens when a gRPC client calls a gRPC server method. For complete implementation details, see the language-specific pages.

在本节中，您将更详细地了解当 gRPC 客户端调用 gRPC 服务器方法时发生的情况。有关完整的实现细节，请参阅特定语言的页面。

#### Unary RPC 一元 RPC

First consider the simplest type of RPC where the client sends a single request and gets back a single response.

首先考虑最简单类型的 RPC，即客户端发送一个请求并收到一个响应。

1. Once the client calls a stub method, the server is notified that the RPC has been invoked with the client’s [metadata](https://grpc.io/docs/what-is-grpc/core-concepts/#metadata) for this call, the method name, and the specified [deadline](https://grpc.io/docs/what-is-grpc/core-concepts/#deadlines) if applicable.
2. 客户端调用存根方法后，服务器会收到有关此调用的客户端[元数据](https://grpc.io/docs/what-is-grpc/core-concepts/#metadata)，方法名称以及指定的[截止时间](https://grpc.io/docs/what-is-grpc/core-concepts/#deadlines)（如果适用）的通知。
3. The server can then either send back its own initial metadata (which must be sent before any response) straight away, or wait for the client’s request message. Which happens first, is application-specific.
4. 然后，服务器可以立即发送自己的初始元数据（必须在任何响应之前发送），或者等待客户端的请求消息。先发生哪个取决于应用程序的具体情况。
5. Once the server has the client’s request message, it does whatever work is necessary to create and populate a response. The response is then returned (if successful) to the client together with status details (status code and optional status message) and optional trailing metadata.
6. 一旦服务器收到客户端的请求消息，它会执行必要的工作来创建和填充响应。然后将响应（如果成功）与状态详细信息（状态代码和可选状态消息）以及可选的尾部元数据一起返回给客户端。
7. If the response status is OK, then the client gets the response, which completes the call on the client side.
8. 如果响应状态为 OK，则客户端接收到响应，这样在客户端上就完成了调用。

#### Server streaming RPC 服务器流式 RPC

A server-streaming RPC is similar to a unary RPC, except that the server returns a stream of messages in response to a client’s request. After sending all its messages, the server’s status details (status code and optional status message) and optional trailing metadata are sent to the client. This completes processing on the server side. The client completes once it has all the server’s messages.

服务器流式 RPC 类似于一元 RPC，只是服务器以流的形式返回多个消息作为对客户端请求的响应。在发送完所有消息后，服务器将其状态详细信息（状态代码和可选状态消息）以及可选的尾部元数据发送给客户端。这样在服务器端完成处理。客户端在接收到所有服务器的消息后完成。

#### Client streaming RPC 客户端流式 RPC

A client-streaming RPC is similar to a unary RPC, except that the client sends a stream of messages to the server instead of a single message. The server responds with a single message (along with its status details and optional trailing metadata), typically but not necessarily after it has received all the client’s messages.

客户端流式 RPC 类似于一元 RPC，只是客户端向服务器发送一系列消息，而不是单个消息。服务器以单个消息作为响应（连同其状态详细信息和可选的尾部元数据）进行响应，通常是在接收到客户端的所有消息之后，但不一定是这样。

#### Bidirectional streaming RPC 双向流式 RPC

In a bidirectional streaming RPC, the call is initiated by the client invoking the method and the server receiving the client metadata, method name, and deadline. The server can choose to send back its initial metadata or wait for the client to start streaming messages.

在双向流式 RPC 中，调用由客户端发起方法调用，服务器接收客户端的元数据、方法名称和截止时间。服务器可以选择发送初始元数据，或者等待客户端开始流式传输消息。

Client- and server-side stream processing is application specific. Since the two streams are independent, the client and server can read and write messages in any order. For example, a server can wait until it has received all of a client’s messages before writing its messages, or the server and client can play “ping-pong” – the server gets a request, then sends back a response, then the client sends another request based on the response, and so on.

客户端和服务器端流处理是特定于应用程序的。由于这两个流是独立的，因此客户端和服务器可以以任何顺序读取和写入消息。例如，服务器可以等待接收到所有客户端的消息后再写入其消息，或者服务器和客户端可以进行“乒乓”式的交互——服务器接收请求，然后发送响应，然后客户端根据响应发送另一个请求，依此类推。

#### Deadlines/Timeouts 截止时间/超时

gRPC allows clients to specify how long they are willing to wait for an RPC to complete before the RPC is terminated with a `DEADLINE_EXCEEDED` error. On the server side, the server can query to see if a particular RPC has timed out, or how much time is left to complete the RPC.

gRPC 允许客户端指定在 RPC 完成之前愿意等待的时间长度，超过这个时间长度将终止 RPC 并返回 `DEADLINE_EXCEEDED` 错误。在服务器端，服务器可以查询特定 RPC 是否已超时，或者还剩多少时间来完成 RPC。

Specifying a deadline or timeout is language specific: some language APIs work in terms of timeouts (durations of time), and some language APIs work in terms of a deadline (a fixed point in time) and may or may not have a default deadline.

指定截止时间或超时是特定于语言的：某些语言的 API 使用超时（时间段），而某些语言的 API 使用截止时间（固定时间点），可能有默认的截止时间，也可能没有。

#### RPC termination RPC 终止

In gRPC, both the client and server make independent and local determinations of the success of the call, and their conclusions may not match. This means that, for example, you could have an RPC that finishes successfully on the server side (“I have sent all my responses!”) but fails on the client side (“The responses arrived after my deadline!”). It’s also possible for a server to decide to complete before a client has sent all its requests.

在 gRPC 中，客户端和服务器都独立并本地确定调用的成功与否，它们的结论可能不一致。这意味着，例如，你可能有一个在服务器端成功完成的 RPC（“我已发送完所有响应！”），但在客户端端失败（“响应在我的截止时间之后到达！”）。服务器也可以在客户端发送完所有请求之前决定完成。

#### Cancelling an RPC 取消 RPC

Either the client or the server can cancel an RPC at any time. A cancellation terminates the RPC immediately so that no further work is done.

客户端或服务器可以随时取消 RPC。取消操作会立即终止 RPC，不再进行进一步的工作。

#### Warning 警告

Changes made before a cancellation are not rolled back.

在取消操作之前所做的更改不会回滚。

#### Metadata 元数据

Metadata is information about a particular RPC call (such as [authentication details](https://grpc.io/docs/guides/auth/)) in the form of a list of key-value pairs, where the keys are strings and the values are typically strings, but can be binary data.

元数据是关于特定 RPC 调用的信息（例如 [身份验证细节](https://grpc.io/docs/guides/auth/)），以键值对的形式表示，其中键是字符串，值通常是字符串，但也可以是二进制数据。

Keys are case insensitive and consist of ASCII letters, digits, and special characters `-`, `_`, `.` and must not start with `grpc-` (which is reserved for gRPC itself). Binary-valued keys end in `-bin` while ASCII-valued keys do not.

键是不区分大小写的，并由 ASCII 字母、数字和特殊字符 `-`、`_`、`.` 组成，且不能以 `grpc-` 开头（这是为 gRPC 保留的）。以二进制值结尾的键以 `-bin` 结尾，而以 ASCII 值结尾的键则不以此结尾。

User-defined metadata is not used by gRPC, which allows the client to provide information associated with the call to the server and vice versa.

gRPC 不使用用户定义的元数据，这允许客户端提供与调用相关的信息给服务器，反之亦然。

Access to metadata is language dependent.

访问元数据是依赖于语言的。

#### Channels 通道

A gRPC channel provides a connection to a gRPC server on a specified host and port. It is used when creating a client stub. Clients can specify channel arguments to modify gRPC’s default behavior, such as switching message compression on or off. A channel has state, including `connected` and `idle`.

gRPC 通道提供与指定主机和端口上的 gRPC 服务器的连接。在创建客户端存根时使用它。客户端可以指定通道参数以修改 gRPC 的默认行为，例如打开或关闭消息压缩。通道具有状态，包括 `connected` 和 `idle`。

How gRPC deals with closing a channel is language dependent. Some languages also permit querying channel state.

gRPC 如何处理关闭通道取决于语言。某些语言还允许查询通道状态。