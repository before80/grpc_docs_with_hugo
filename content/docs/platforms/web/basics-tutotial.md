+++
title = "基础教程"
weight = 2
date = 2023-05-31T10:43:40+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Basics tutorial 基础教程

​	gRPC-web 的基础教程介绍。

​	本教程提供了如何在浏览器中使用 gRPC-Web 的基本介绍。

​	通过学习本示例，您将了解如何：

- 在 `.proto` 文件中定义一个服务。
- 使用协议缓冲区编译器生成客户端代码。
- 使用 gRPC-Web API 编写一个简单的服务客户端。

​	本教程假设您对[协议缓冲区](https://protobuf.dev/overview)有基本了解。

### 为什么使用 gRPC 和 gRPC-Web？

​	使用 gRPC，您可以在 `.proto` 文件中定义一次您的服务，并在gRPC支持的任何语言中实现客户端和服务端，这些客户端和服务端可以在从大型数据中心的服务器到您自己的平板电脑等各种环境中运行 ——  gRPC 为不同编程语言和环境之间的通信复杂性提供了便利。您还可以享受使用协议缓冲区的所有优势，包括高效的序列化、简单的接口定义语言和易于更新接口。gRPC-Web 允许您使用符合惯例的 API 从浏览器访问以这种方式构建的 gRPC 服务。

### 定义服务

​	创建 gRPC 服务的第一步是使用协议缓冲区定义服务方法以及它们的请求和响应消息类型。在本示例中，我们在名为 [`echo.proto`](https://github.com/grpc/grpc-web/blob/0.4.0/net/grpc/gateway/examples/echo/echo.proto) 的文件中定义了我们的 `EchoService`。有关协议缓冲区和 proto3 语法的更多信息，请参阅 [protobuf 文档](https://protobuf.dev/)。

```protobuf
message EchoRequest {
  string message = 1;
}

message EchoResponse {
  string message = 1;
}

service EchoService {
  rpc Echo(EchoRequest) returns (EchoResponse);
}
```

### 实现 gRPC 后端服务端

​	接下来，我们使用Node在后端实现了EchoService接口，创建了gRPC的`EchoServer`。它将处理来自客户端的请求。有关详细信息，请参阅文件 [node-server/server.js](https://github.com/grpc/grpc-web/blob/master/net/grpc/gateway/examples/echo/node-server/server.js)。

​	您可以使用 gRPC 支持的任何编程语言来实现服务端。有关详细信息，请参阅[主页]({{< ref "/docs" >}})。

```js
function doEcho(call, callback) {
  callback(null, {message: call.request.message});
}
```

### 配置 Envoy 代理

​	在这个示例中，我们将使用 [Envoy](https://www.envoyproxy.io/) 代理将 gRPC 浏览器请求转发到后端服务端。您可以在 [envoy.yaml](https://github.com/grpc/grpc-web/blob/master/net/grpc/gateway/examples/echo/envoy.yaml) 文件中查看完整的配置文件。

​	为了将 gRPC 请求转发到后端服务端，我们需要添加以下配置块：

```yaml
  listeners:
  - name: listener_0
    address:
      socket_address: { address: 0.0.0.0, port_value: 8080 }
    filter_chains:
    - filters:
      - name: envoy.http_connection_manager
        config:
          codec_type: auto
          stat_prefix: ingress_http
          route_config:
            name: local_route
            virtual_hosts:
            - name: local_service
              domains: ["*"]
              routes:
              - match: { prefix: "/" }
                route: { cluster: echo_service }
          http_filters:
          - name: envoy.grpc_web
          - name: envoy.router
  clusters:
  - name: echo_service
    connect_timeout: 0.25s
    type: logical_dns
    http2_protocol_options: {}
    lb_policy: round_robin
    hosts: [{ socket_address: { address: node-server, port_value: 9090 }}]
```

​	您可能还需要添加一些 CORS 设置，以确保浏览器可以请求跨域内容（cross-origin content）。

​	在这个简单示例中，浏览器向端口 `:8080` 发出 gRPC 请求。Envoy将请求转发到在端口`9090`上监听的后端gRPC服务端。

### 生成 Protobuf 消息和服务客户端 Stub

​	要从我们的 `echo.proto` 生成 protobuf 消息类，请运行以下命令：

```sh
$ protoc -I=$DIR echo.proto \
  --js_out=import_style=commonjs:$OUT_DIR
```

​	传递给`--js_out`标志的`import_style`选项，确保生成的文件将具有CommonJS样式的`require()`语句。

​	要生成gRPC-Web服务的客户端存根（stub），首先需要gRPC-Web protoc插件。要编译`protoc-gen-grpc-web`插件，需要从存储库的根目录运行以下命令：

```sh
$ cd grpc-web
$ sudo make install-plugin
```

​	要生成该服务的客户端存根（stub） 文件，请运行以下命令：

```sh
$ protoc -I=$DIR echo.proto \
  --grpc-web_out=import_style=commonjs,mode=grpcwebtext:$OUT_DIR
```

​	在上述的 `--grpc-web_out` 参数中：

- `mode` 可以是 `grpcwebtext`（默认）或 `grpcweb`
- `import_style` 可以是 `closure`（默认）或 `commonjs`

​	我们的命令会生成客户端存根 (stub)，默认情况下会生成到文件 `echo_grpc_web_pb.js` 中。

### 编写 JS 客户端代码

​	现在，您可以编写一些 JS 客户端代码了。将以下代码放入一个名为 `client.js` 的文件中。

```js
const {EchoRequest, EchoResponse} = require('./echo_pb.js');
const {EchoServiceClient} = require('./echo_grpc_web_pb.js');

var echoService = new EchoServiceClient('http://localhost:8080');

var request = new EchoRequest();
request.setMessage('Hello World!');

echoService.echo(request, {}, function(err, response) {
  // ...
});
```

​	您将需要一个 `package.json` 文件：

```json
{
  "name": "grpc-web-commonjs-example",
  "dependencies": {
    "google-protobuf": "^3.6.1",
    "grpc-web": "^0.4.0"
  },
  "devDependencies": {
    "browserify": "^16.2.2",
    "webpack": "^4.16.5",
    "webpack-cli": "^3.1.0"
  }
}
```

### 编译 JS 库

​	最后，将所有这些内容放在一起，我们可以将所有相关的 JS 文件编译为一个单一（可以在浏览器中使用）的 JS 库。

```sh
$ npm install
$ npx webpack client.js
```

​	现在将 `dist/main.js` 嵌入到您的项目中，并查看它的运行情况！