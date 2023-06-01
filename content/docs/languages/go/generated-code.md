+++
title = "生成的代码参考"
weight = 5
date = 2023-05-31T10:42:00+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Generated-code reference 生成的代码参考

https://grpc.io/docs/languages/go/generated-code/



This page describes the code generated with the [grpc plugin](https://pkg.go.dev/google.golang.org/grpc/cmd/protoc-gen-go-grpc), `protoc-gen-go-grpc`, when compiling `.proto` files with `protoc`.

本页面描述了使用 [grpc插件](https://pkg.go.dev/google.golang.org/grpc/cmd/protoc-gen-go-grpc)，即`protoc-gen-go-grpc`，在使用`protoc`编译`.proto`文件时生成的代码。

You can find out how to define a gRPC service in a `.proto` file in [Service definition](https://grpc.io/docs/what-is-grpc/core-concepts/#service-definition).

您可以在[服务定义](https://grpc.io/docs/what-is-grpc/core-concepts/#service-definition)中了解如何在`.proto`文件中定义gRPC服务。

**Thread-safety**: note that client-side RPC invocations and server-side RPC handlers *are thread-safe* and are meant to be run on concurrent goroutines. But also note that for *individual streams*, incoming and outgoing data is bi-directional but serial; so e.g. *individual streams* do not support *concurrent reads* or *concurrent writes* (but reads are safely concurrent *with* writes).

**线程安全性**：请注意，客户端的RPC调用和服务器端的RPC处理程序是*线程安全*的，并且可以在并发的goroutine上运行。但是，请注意对于*单个流*，传入和传出的数据是双向但串行的；因此，例如，*单个流*不支持*并发读取*或*并发写入*（但读取可以与写入安全地并发进行）。

## Methods on generated server interfaces 生成的服务器接口上的方法

On the server side, each `service Bar` in the `.proto` file results in the function:

在服务器端，`.proto`文件中的每个`service Bar`都会生成以下函数：

```
func RegisterBarServer(s *grpc.Server, srv BarServer)
```

The application can define a concrete implementation of the `BarServer` interface and register it with a `grpc.Server` instance (before starting the server instance) by using this function.

应用程序可以定义`BarServer`接口的具体实现，并使用此函数将其注册到`grpc.Server`实例上（在启动服务器实例之前）。

### Unary methods 单向方法

These methods have the following signature on the generated service interface:

这些方法在生成的服务接口上具有以下签名：

```
Foo(context.Context, *MsgA) (*MsgB, error)
```

In this context, `MsgA` is the protobuf message sent from the client, and `MsgB` is the protobuf message sent back from the server.

在此上下文中，`MsgA`是从客户端发送的Protobuf消息，`MsgB`是从服务器返回的Protobuf消息。

### Server-streaming methods 服务器流式方法

These methods have the following signature on the generated service interface: 

在生成的服务接口上，这些方法具有以下签名：

```
Foo(*MsgA, <ServiceName>_FooServer) error
```

In this context, `MsgA` is the single request from the client, and the `<ServiceName>_FooServer` parameter represents the server-to-client stream of `MsgB` messages.

在这个上下文中，`MsgA`是来自客户端的单个请求，`<ServiceName>_FooServer`参数表示`MsgB`消息的服务器到客户端的流。

`<ServiceName>_FooServer` has an embedded `grpc.ServerStream` and the following interface:

`<ServiceName>_FooServer`嵌入了`grpc.ServerStream`和以下接口：

```go
type <ServiceName>_FooServer interface {
	Send(*MsgB) error
	grpc.ServerStream
}
```

The server-side handler can send a stream of protobuf messages to the client through this parameter’s `Send` method. End-of-stream for the server-to-client stream is caused by the `return` of the handler method.

服务器端处理程序可以通过该参数的`Send`方法向客户端发送一系列的Protobuf消息。服务器到客户端的流的结束由处理程序方法的`return`语句引发。

### Client-streaming methods 客户端流式方法

These methods have the following signature on the generated service interface:

在生成的服务接口上，这些方法具有以下签名：

```
Foo(<ServiceName>_FooServer) error
```

In this context, `<ServiceName>_FooServer` can be used both to read the client-to-server message stream and to send the single server response message.

在这个上下文中，`<ServiceName>_FooServer`既可以用于读取客户端到服务器的消息流，也可以用于发送单个服务器响应消息。

`<ServiceName>_FooServer` has an embedded `grpc.ServerStream` and the following interface:

`<ServiceName>_FooServer`嵌入了`grpc.ServerStream`和以下接口：

```go
type <ServiceName>_FooServer interface {
	SendAndClose(*MsgA) error
	Recv() (*MsgB, error)
	grpc.ServerStream
}
```

The server-side handler can repeatedly call `Recv` on this parameter in order to receive the full stream of messages from the client. `Recv` returns `(nil, io.EOF)` once it has reached the end of the stream. The single response message from the server is sent by calling the `SendAndClose` method on this `<ServiceName>_FooServer` parameter. Note that `SendAndClose` must be called once and only once.

服务器端处理程序可以重复调用该参数上的`Recv`方法，以接收来自客户端的完整消息流。一旦达到流的末尾，`Recv`将返回`(nil, io.EOF)`。通过在`<ServiceName>_FooServer`参数上调用`SendAndClose`方法，服务器发送单个响应消息。请注意，`SendAndClose`必须且只能被调用一次。

### Bidi-streaming methods 双向流式方法

These methods have the following signature on the generated service interface:

在生成的服务接口上，这些方法具有以下签名：

```
Foo(<ServiceName>_FooServer) error
```

In this context, `<ServiceName>_FooServer` can be used to access both the client-to-server message stream and the server-to-client message stream. `<ServiceName>_FooServer` has an embedded `grpc.ServerStream` and the following interface:

在这个上下文中，`<ServiceName>_FooServer`可用于访问客户端到服务器的消息流和服务器到客户端的消息流。`<ServiceName>_FooServer`嵌入了`grpc.ServerStream`和以下接口：

```go
type <ServiceName>_FooServer interface {
	Send(*MsgA) error
	Recv() (*MsgB, error)
	grpc.ServerStream
}
```

The server-side handler can repeatedly call `Recv` on this parameter in order to read the client-to-server message stream. `Recv` returns `(nil, io.EOF)` once it has reached the end of the client-to-server stream. The response server-to-client message stream is sent by repeatedly calling the `Send` method of on this `ServiceName>_FooServer` parameter. End-of-stream for the server-to-client stream is indicated by the `return` of the bidi method handler.

服务器端处理程序可以重复调用该参数上的`Recv`方法，以读取客户端到服务器的消息流。一旦达到客户端到服务器流的末尾，`Recv`将返回`(nil, io.EOF)`。通过重复调用`<ServiceName>_FooServer`参数上的`Send`方法，发送服务器到客户端的响应消息流。对于服务器到客户端的流，流的结束由双向方法处理程序的`return`语句指示。

## Methods on generated client interfaces 生成的客户端接口上的方法

For client side usage, each `service Bar` in the `.proto` file also results in the function: `func BarClient(cc *grpc.ClientConn) BarClient`, which returns a concrete implementation of the `BarClient` interface (this concrete implementation also lives in the generated `.pb.go` file).

对于客户端使用，`.proto`文件中的每个`service Bar`还会生成函数：`func BarClient(cc *grpc.ClientConn) BarClient`，该函数返回`BarClient`接口的具体实现（该具体实现也位于生成的`.pb.go`文件中）。

### Unary Methods 一元方法

These methods have the following signature on the generated client stub:

在生成的客户端存根上，这些方法具有以下签名：

```
(ctx context.Context, in *MsgA, opts ...grpc.CallOption) (*MsgB, error)
```

In this context, `MsgA` is the single request from client to server, and `MsgB` contains the response sent back from the server.

在这个上下文中，`MsgA`是客户端发送到服务器的单个请求，`MsgB`包含服务器发送回的响应。

### Server-Streaming methods 服务器流式方法

These methods have the following signature on the generated client stub:

在生成的客户端存根上，这些方法具有以下签名：

```
Foo(ctx context.Context, in *MsgA, opts ...grpc.CallOption) (<ServiceName>_FooClient, error)
```

In this context, `<ServiceName>_FooClient` represents the server-to-client `stream` of `MsgB` messages.

在这个上下文中，`<ServiceName>_FooClient`表示服务器到客户端的`stream`，其中包含`MsgB`消息。

This stream has an embedded `grpc.ClientStream` and the following interface:

该流式具有嵌入的`grpc.ClientStream`和以下接口：

```go
type <ServiceName>_FooClient interface {
	Recv() (*MsgB, error)
	grpc.ClientStream
}
```

The stream begins when the client calls the `Foo` method on the stub. The client can then repeatedly call the `Recv` method on the returned `<ServiceName>_FooClient` *stream* in order to read the server-to-client response stream. This `Recv` method returns `(nil, io.EOF)` once the server-to-client stream has been completely read through.

当客户端在存根上调用`Foo`方法时，流式开始。然后，客户端可以重复调用返回的`<ServiceName>_FooClient` *stream* 上的`Recv`方法，以读取服务器到客户端的响应流。一旦完全读取了服务器到客户端的流，`Recv`方法将返回`(nil, io.EOF)`。

### Client-Streaming methods 客户端流式方法

These methods have the following signature on the generated client stub:

在生成的客户端存根上，这些方法具有以下签名：

```
Foo(ctx context.Context, opts ...grpc.CallOption) (<ServiceName>_FooClient, error)
```

In this context, `<ServiceName>_FooClient` represents the client-to-server `stream` of `MsgA` messages.

在这个上下文中，`<ServiceName>_FooClient`表示客户端到服务器的`stream`，其中包含`MsgA`消息。

`<ServiceName>_FooClient` has an embedded `grpc.ClientStream` and the following interface:

`<ServiceName>_FooClient`具有嵌入的`grpc.ClientStream`和以下接口：

```go
type <ServiceName>_FooClient interface {
	Send(*MsgA) error
	CloseAndRecv() (*MsgB, error)
	grpc.ClientStream
}
```

The stream begins when the client calls the `Foo` method on the stub. The client can then repeatedly call the `Send` method on the returned `<ServiceName>_FooClient` stream in order to send the client-to-server message stream. The `CloseAndRecv` method on this stream must be called once and only once, in order to both close the client-to-server stream and receive the single response message from the server.

当客户端在存根上调用`Foo`方法时，流式开始。然后，客户端可以重复调用返回的`<ServiceName>_FooClient`流上的`Send`方法，以发送客户端到服务器的消息流。必须仅调用一次`CloseAndRecv`方法来关闭客户端到服务器的流，并从服务器接收单个响应消息。

### Bidi-Streaming methods 双向流式方法

These methods have the following signature on the generated client stub:

在生成的客户端存根上，这些方法具有以下签名：

```
Foo(ctx context.Context, opts ...grpc.CallOption) (<ServiceName>_FooClient, error)
```

In this context, `<ServiceName>_FooClient` represents both the client-to-server and server-to-client message streams.

在这个上下文中，`<ServiceName>_FooClient`表示客户端到服务器和服务器到客户端的消息流。

`<ServiceName>_FooClient` has an embedded `grpc.ClientStream` and the following interface:

`<ServiceName>_FooClient`具有嵌入的`grpc.ClientStream`和以下接口：

```go
type <ServiceName>_FooClient interface {
	Send(*MsgA) error
	Recv() (*MsgB, error)
	grpc.ClientStream
}
```

The stream begins when the client calls the `Foo` method on the stub. The client can then repeatedly call the `Send` method on the returned `<SericeName>_FooClient` stream in order to send the client-to-server message stream. The client can also repeatedly call `Recv` on this stream in order to receive the full server-to-client message stream.

当客户端在存根上调用`Foo`方法时，流式开始。然后，客户端可以重复调用返回的`<SericeName>_FooClient`流上的`Send`方法，以发送客户端到服务器的消息流。客户端还可以重复调用此流上的`Recv`方法，以接收完整的服务器到客户端的消息流。

End-of-stream for the server-to-client stream is indicated by a return value of `(nil, io.EOF)` on the `Recv` method of the stream. End-of-stream for the client-to-server stream can be indicated from the client by calling the `CloseSend` method on the stream.

对于服务器到客户端的流，通过流的`Recv`方法返回值为`(nil, io.EOF)`来表示流结束。对于客户端到服务器的流，客户端可以通过在流上调用`CloseSend`方法来表示流结束。

## Packages and Namespaces 包和命名空间

When the `protoc` compiler is invoked with `--go_out=plugins=grpc:`, the `proto package` to Go package translation works the same as when the `protoc-gen-go` plugin is used without the `grpc` plugin.

当使用`protoc`编译器调用`--go_out=plugins=grpc:`时，`proto package`到Go包的转换与使用`protoc-gen-go`插件时相同。

So, for example, if `foo.proto` declares itself to be in `package foo`, then the generated `foo.pb.go` file will also be in the Go package `foo`.

例如，如果`foo.proto`声明其位于`package foo`中，则生成的`foo.pb.go`文件也将位于Go包`foo`中。