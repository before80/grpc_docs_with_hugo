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

​	本页面描述了使用 [grpc插件](https://pkg.go.dev/google.golang.org/grpc/cmd/protoc-gen-go-grpc)，即`protoc-gen-go-grpc`，在使用`protoc`编译`.proto`文件时生成的代码。

​	您可以在[服务定义]({{< ref "/docs/what_is_grpc/core-concepts#服务定义">}})中了解如何在`.proto`文件中定义gRPC服务。

**Thread-safety**: note that client-side RPC invocations and server-side RPC handlers *are thread-safe* and are meant to be run on concurrent goroutines. But also note that for *individual streams*, incoming and outgoing data is bi-directional but serial; so e.g. *individual streams* do not support *concurrent reads* or *concurrent writes* (but reads are safely concurrent *with* writes).

**线程安全性（Thread-safety）**：请注意，客户端的RPC调用和服务端的RPC处理程序是*线程安全（thread-safe）*的，并且可以在并发的goroutine上运行。但是，请注意对于**单个流（individual streams）**而言，传入和传出的数据是双向但串行的；因此，例如，*单个流*不支持*并发读取*或*并发写入*（但读取与写入之间是安全并发的）。

## 生成的服务端接口上的方法

​	在服务端，`.proto`文件中的每个`service Bar`都会生成以下函数：

```
func RegisterBarServer(s *grpc.Server, srv BarServer)
```

​	该应用程序可以定义`BarServer`接口的具体实现，并使用此函数将其注册到`grpc.Server`实例上（在启动服务端实例之前）。

### 一元方法

​	这些方法在生成的服务接口上具有以下签名：

```
Foo(context.Context, *MsgA) (*MsgB, error)
```

​	在这个上下文中，`MsgA`是从客户端发送的Protobuf消息，`MsgB`是从服务端返回的Protobuf消息。

### 服务端流式方法

​	这些方法在生成的服务接口上具有以下签名：

```
Foo(*MsgA, <ServiceName>_FooServer) error
```

​	在这个上下文中，`MsgA`是来自客户端的单个请求，`<ServiceName>_FooServer`参数表示`MsgB`消息的服务端到客户端的流。

​	`<ServiceName>_FooServer`嵌入了`grpc.ServerStream`和以下接口：

```go
type <ServiceName>_FooServer interface {
	Send(*MsgB) error
	grpc.ServerStream
}
```

​	服务端处理程序可以通过此参数的`Send`方法向客户端发送一系列的Protobuf消息。服务端到客户端的流通过处理程序方法的`return`语句来结束。

### 客户端流式方法

​	这些方法在生成的服务接口上具有以下签名：

```
Foo(<ServiceName>_FooServer) error
```

​	在这个上下文中，`<ServiceName>_FooServer`既可以用于读取客户端到服务端的消息流，也可以用于发送单个服务端响应消息。

​	`<ServiceName>_FooServer`嵌入了`grpc.ServerStream`和以下接口：

```go
type <ServiceName>_FooServer interface {
	SendAndClose(*MsgA) error
	Recv() (*MsgB, error)
	grpc.ServerStream
}
```

​	服务端处理程序可以重复调用此参数上的`Recv`方法，以接收来自客户端的完整消息流。一旦达到流的末尾，`Recv`将返回`(nil, io.EOF)`。通过在`<ServiceName>_FooServer`参数上调用`SendAndClose`方法，可以发送来自服务端的单个响应消息。请注意，`SendAndClose`方法必须且只能被调用一次。

### 双向流式方法

​	这些方法在生成的服务接口上具有以下签名：

```
Foo(<ServiceName>_FooServer) error
```

​	在这个上下文中，`<ServiceName>_FooServer`可用于访问客户端到服务端的消息流和服务端到客户端的消息流。`<ServiceName>_FooServer`嵌入了`grpc.ServerStream`和以下接口：

```go
type <ServiceName>_FooServer interface {
	Send(*MsgA) error
	Recv() (*MsgB, error)
	grpc.ServerStream
}
```

​	服务端处理程序可以重复调用此参数上的`Recv`方法，以读取客户端到服务端的消息流。一旦达到客户端到服务端流的末尾，`Recv`方法将返回`(nil, io.EOF)`。通过重复调用`<ServiceName>_FooServer`参数上的`Send`方法，可以发送服务端到客户端的响应消息流。服务端到客户端的流通过双向方法处理程序的`return`语句来结束。

## 生成的客户端接口上的方法

​	对于客户端用法，`.proto`文件中的每个`service Bar`还会生成函数：`func BarClient(cc *grpc.ClientConn) BarClient`，该函数返回`BarClient`接口的具体实现（该具体实现也位于生成的`.pb.go`文件中）。

### 一元方法

​	在生成的客户端存根（stub）上，这些方法具有以下签名：

```
(ctx context.Context, in *MsgA, opts ...grpc.CallOption) (*MsgB, error)
```

​	在这个上下文中，`MsgA`是客户端发送到服务端的单个请求，`MsgB`包含了服务端发送回来的响应。

### 服务端流式方法

​	在生成的客户端存根（stub）上，这些方法具有以下签名：

```
Foo(ctx context.Context, in *MsgA, opts ...grpc.CallOption) (<ServiceName>_FooClient, error)
```

In this context, `<ServiceName>_FooClient` represents the server-to-client `stream` of `MsgB` messages.

​	在这个上下文中，`<ServiceName>_FooClient`表示服务端到客户端的`stream`，其中包含`MsgB`消息。

​	这个流嵌入了`grpc.ClientStream`和以下接口：

```go
type <ServiceName>_FooClient interface {
	Recv() (*MsgB, error)
	grpc.ClientStream
}
```

​	这个流开始于，当客户端在存根（stub）上调用`Foo`方法时。然后，客户端可以重复调用返回的`<ServiceName>_FooClient` *stream* 上的`Recv`方法，以读取服务端到客户端的响应流。一旦完全读取了服务端到客户端的流，`Recv`方法将返回`(nil, io.EOF)`。

### 客户端流式方法

​	在生成的客户端存根（stub）上，这些方法具有以下签名：

```
Foo(ctx context.Context, opts ...grpc.CallOption) (<ServiceName>_FooClient, error)
```

In this context, `<ServiceName>_FooClient` represents the client-to-server `stream` of `MsgA` messages.

​	在这个上下文中，`<ServiceName>_FooClient`表示客户端到服务端的`stream`，其中包含`MsgA`消息。

​	`<ServiceName>_FooClient`嵌入了`grpc.ClientStream`和以下接口：

```go
type <ServiceName>_FooClient interface {
	Send(*MsgA) error
	CloseAndRecv() (*MsgB, error)
	grpc.ClientStream
}
```

​	这个流开始于，当客户端在存根（stub）上调用`Foo`方法时。然后，客户端可以重复调用返回的`<ServiceName>_FooClient`流上的`Send`方法，来发送客户端到服务端的消息流。为了关闭客户端到服务器的流并接收来自服务器的单个响应消息，必须仅调用一次 `CloseAndRecv` 方法。

### 双向流式方法

​	在生成的客户端存根（stub）上，这些方法具有以下签名：

```
Foo(ctx context.Context, opts ...grpc.CallOption) (<ServiceName>_FooClient, error)
```

​	在这个上下文中，`<ServiceName>_FooClient`表示客户端到服务端和服务端到客户端的消息流。

​	`<ServiceName>_FooClient`嵌入了`grpc.ClientStream`和以下接口：

```go
type <ServiceName>_FooClient interface {
	Send(*MsgA) error
	Recv() (*MsgB, error)
	grpc.ClientStream
}
```

​	这个流开始于，当客户端在存根（stub）上调用`Foo`方法时。然后，客户端可以重复调用返回的`<SericeName>_FooClient`流上的`Send`方法，来发送客户端到服务端的消息流。客户端还可以重复调用此流上的`Recv`方法，来接收完整的服务端到客户端的消息流。

​	对于服务器到客户端的流，通过流的 `Recv` 方法返回值为 `(nil, io.EOF)` 来表示流的结束。对于客户端到服务器的流，客户端可以通过在流上调用`CloseSend`方法来表示流结束。

## 包和命名空间

When the `protoc` compiler is invoked with `--go_out=plugins=grpc:`, the `proto package` to Go package translation works the same as when the `protoc-gen-go` plugin is used without the `grpc` plugin. 

​	当使用`protoc`编译器调用`--go_out=plugins=grpc:`时，`proto package` 到 Go 包的转换方式与在没有使用 `grpc` 插件的情况下使用 `protoc-gen-go` 插件时相同。

​	例如，如果`foo.proto`声明其位于`package foo`中，则生成的`foo.pb.go`文件也将位于Go包`foo`中。