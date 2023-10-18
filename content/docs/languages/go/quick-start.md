+++
title = "快速入门"
weight = 1
date = 2023-05-31T10:41:03+08:00
description = ""
isCJKLanguage = true
draft = false

+++

# Quick start - 快速入门

https://grpc.io/docs/languages/go/quickstart/

​	本指南将通过一个简单的工作示例帮助您入门使用 Go 中的 gRPC。



### 先决条件

- **[Go](https://golang.org/)**，任意**三个最新主要版本**的 [Go 发行版](https://golang.org/doc/devel/release.html)。

  有关安装说明，请参阅 Go 的 [入门指南](https://golang.org/doc/install)。

- **[Protocol Buffers](https://developers.google.com/protocol-buffers) 编译器** `protoc`，[第 3 版](https://protobuf.dev/programming-guides/proto3)。

  有关安装说明，请参阅 [Protocol Buffer 编译器安装]({{< ref "/docs/ProtocolBufferCompilerInstallation">}})。

- **Go 插件**用于协议编译器：

  1. 使用以下命令安装 Go 的协议编译器插件

     ```sh
     $ go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.28
     $ go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.2
     ```

  2. 更新您的 `PATH`，以便 `protoc` 编译器可以找到这些插件：

     ```sh
     $ export PATH="$PATH:$(go env GOPATH)/bin"
     ```


### 获取示例代码

​	该示例代码是 [grpc-go](https://github.com/grpc/grpc-go) 仓库的一部分。

1. [下载仓库的 zip 文件](https://github.com/grpc/grpc-go/archive/v1.55.0.zip) 并解压，或者克隆仓库：

   ```sh
   $ git clone -b v1.55.0 --depth 1 https://github.com/grpc/grpc-go
   ```

2. 切换到快速入门示例目录：

   ```sh
   $ cd grpc-go/examples/helloworld
   ```


### 运行示例

​	从 `examples/helloworld` 目录开始：

1. 编译并执行服务端代码：

   ```sh
   $ go run greeter_server/main.go
   ```

2. 从另一个终端编译并执行客户端代码，并查看客户端输出：

   ```sh
   $ go run greeter_client/main.go
   Greeting: Hello world
   ```


​	恭喜！您刚刚使用 gRPC 运行了一个客户端-服务端（client-server ）应用程序。

### 更新 gRPC 服务

In this section you’ll update the application with an extra server method. The gRPC service is defined using [protocol buffers](https://developers.google.com/protocol-buffers). To learn more about how to define a service in a `.proto` file see [Basics tutorial](https://grpc.io/docs/languages/go/basics/). For now, all you need to know is that both the server and the client stub have a `SayHello()` RPC method that takes a `HelloRequest` parameter from the client and returns a `HelloReply` from the server, and that the method is defined like this:

​	在本节中，您将使用额外的服务端方法更新应用程序。gRPC 服务使用[Protocol Buffers](https://developers.google.com/protocol-buffers)定义。要了解有关如何在 `.proto` 文件中定义服务的更多信息，请参阅[基础教程]({{< ref "/docs/languages/go/basics-tutorial">}})。目前，您只需要知道服务端和客户端存根都有一个 `SayHello()` 的 RPC 方法，该方法从客户端接收一个 `HelloRequest` 参数，并从服务端返回一个 `HelloReply`，该方法定义如下：

```protobuf
// greeting 服务的定义。
service Greeter {
  // Sends a greeting 发送问候
  rpc SayHello (HelloRequest) returns (HelloReply) {}
}

// 包含用户名称的请求消息。
message HelloRequest {
  string name = 1;
}

// The response message containing the greetings 包含 greetings 的响应消息
message HelloReply {
  string message = 1;
}
```

​	打开 `helloworld/helloworld.proto` 文件，并添加一个新的 `SayHelloAgain()` 方法，使用相同的请求和响应类型：

```protobuf
// greeting 服务的定义。
service Greeter {
  // Sends a greeting 发送问候
  rpc SayHello (HelloRequest) returns (HelloReply) {}
  // Sends another greeting 发送另一个问候
  rpc SayHelloAgain (HelloRequest) returns (HelloReply) {}
}

// 包含用户名称的请求消息。
message HelloRequest {
  string name = 1;
}

// The response message containing the greetings 包含 greetings 的响应消息。
message HelloReply {
  string message = 1;
}
```

​	记得保存文件！

### 重新生成 gRPC 代码

​	在使用新的服务方法之前，您需要重新编译已更新的 `.proto` 文件。

​	仍然位于 `examples/helloworld` 目录中，运行以下命令：

```sh
$ protoc --go_out=. --go_opt=paths=source_relative \
    --go-grpc_out=. --go-grpc_opt=paths=source_relative \
    helloworld/helloworld.proto
```

​	这将重新生成 `helloworld/helloworld.pb.go` 和 `helloworld/helloworld_grpc.pb.go` 文件，其中包含：

- 用于填充、序列化和检索 `HelloRequest` 和 `HelloReply` 消息类型的代码。
- 生成的客户端和服务端代码。

### 更新并运行应用程序

​	您已经重新生成了服务端和客户端代码，但仍需要在该示例应用程序的人工编写部分中实现和调用新的方法。

#### 更新服务端

​	打开 `greeter_server/main.go`，并添加以下函数（这里应该叫做方法吧）：

```go
func (s *server) SayHelloAgain(ctx context.Context, in *pb.HelloRequest) (*pb.HelloReply, error) {
        return &pb.HelloReply{Message: "Hello again " + in.GetName()}, nil
}
```

#### 更新客户端

​	打开 `greeter_client/main.go`，并在 `main()` 函数体的末尾添加以下代码：

```go
r, err = c.SayHelloAgain(ctx, &pb.HelloRequest{Name: *name})
if err != nil {
        log.Fatalf("could not greet: %v", err)
}
log.Printf("Greeting: %s", r.GetMessage())
```

​	记得保存您的更改。

#### 运行！

​	像之前一样运行客户端和服务端。从 `examples/helloworld` 目录执行以下命令：

1. 运行该服务端：

   ```sh
   $ go run greeter_server/main.go
   ```

2. 在另一个终端中运行该客户端。这次，在命令行参数中添加一个名称。

   ```sh
   $ go run greeter_client/main.go --name=Alice
   ```

   您将看到以下输出：

   ```sh
   Greeting: Hello Alice
   Greeting: Hello again Alice
   ```


### 下一步

- 了解 gRPC 的工作原理：[gRPC 简介]({{< ref "/docs/what_is_grpc/introduction" >}})和[核心概念]({{< ref "/docs/what_is_grpc/core-concepts">}})。
- 完成[基础教程]({{< ref "/docs/languages/go/basics-tutorial" >}})。
- 探索[API 参考]({{< ref "/docs/languages/go/api" >}})。