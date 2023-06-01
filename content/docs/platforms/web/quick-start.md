+++
title = "快速入门"
weight = 1
date = 2023-05-31T10:43:26+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Quick start 快速入门

This guide gets you started with gRPC-Web with a simple working example.

这个指南通过一个简单的工作示例让你开始使用 gRPC-Web。



### Prerequisites 先决条件

- Docker and `docker-compose` supporting [Docker Compose file version 3](https://docs.docker.com/compose/compose-file/compose-versioning). For installation instructions see [Install Compose](https://docs.docker.com/compose/install/#install-compose).
- Docker 和支持 [Docker Compose 文件版本 3](https://docs.docker.com/compose/compose-file/compose-versioning) 的 `docker-compose`。安装说明请参见 [安装 Compose](https://docs.docker.com/compose/install/#install-compose)。

### Get the example code 获取示例代码

The example code is part of the [grpc-web](https://github.com/grpc/grpc-web) repo.

示例代码包含在 [grpc-web](https://github.com/grpc/grpc-web) 仓库中。

1. [Download the repo as a zip file](https://github.com/grpc/grpc-web/archive/master.zip) and unzip it, or clone the repo:

2. [下载仓库的 zip 文件](https://github.com/grpc/grpc-web/archive/master.zip) 并解压，或者克隆仓库：

   ```sh
   $ git clone https://github.com/grpc/grpc-web
   ```

3. Change to the repo’s root directory:

4. 切换到仓库的根目录：

   ```sh
   $ cd grpc-web
   ```

### Run an Echo example from your browser! 从浏览器中运行 Echo 示例！

From the `grpc-web` directory:

从 `grpc-web` 目录：

1. Fetch required packages and tools:

2. 获取所需的包和工具：

   ```sh
   $ docker-compose pull prereqs node-server envoy commonjs-client
   ```

   #### Note 注意

   Getting the following warning? You can ignore it for the purpose of running the example app:

   收到以下警告？你可以忽略它，以便运行示例应用程序：

   ```nocode
   WARNING: Some service image(s) must be built from source
   ```

3. Launch services as background processes: 启动服务作为后台进程：

   ```sh
   $ docker-compose up -d node-server envoy commonjs-client
   ```

4. From your browser: 在你的浏览器中：

   - Visit [localhost:8081/echotest.html](http://localhost:8081/echotest.html).
   - Enter a message, like “Hello”, in the text-input box.
   - Press the **Send** button.
   - 访问 [localhost:8081/echotest.html](http://localhost:8081/echotest.html)。
   - 在文本输入框中输入消息，如“Hello”。
   - 点击 **Send** 按钮。

   You’ll see your message echoed by the server below the input box.

   你将在输入框下方看到服务器返回的消息。

Congratulations! You’ve just run a client-server application with gRPC.

恭喜！你刚刚使用 gRPC 运行了一个客户端-服务器应用程序。

Once you are done, shutdown the services that you launched earlier by running the following command:

完成后，通过运行以下命令关闭之前启动的服务：

```sh
$ docker-compose down
```

### What is happening? 发生了什么？

This example app has three key components:

这个示例应用程序有三个关键组件：

1. `node-server` is a standard gRPC server, implemented in Node. This server listens at port `:9090`, and implements the app’s business logic (echoing client messages).
2. `node-server` 是一个使用 Node 实现的标准 gRPC 服务器。该服务器在端口 `:9090` 上监听，并实现应用程序的业务逻辑（回显客户端消息）。
3. `envoy` is the Envoy proxy. It listens at `:8080` and forwards the browser’s gRPC-Web requests to port `:9090`.
4. `envoy` 是 Envoy 代理。它在端口 `:8080` 上监听，并将浏览器的 gRPC-Web 请求转发到端口 `:9090`。
5. `commonjs-client`: this component generates the client stub class using the `protoc-gen-grpc-web` protoc plugin, compiles all the JS dependencies using `webpack`, and hosts the static content (`echotest.html` and `dist/main.js`) at port `:8081` using a simple web server. User messages entered from the webpage are sent to the Envoy proxy as gRPC-web requests.
6. `commonjs-client`：该组件使用 `protoc-gen-grpc-web` protoc 插件生成客户端存根类，使用 `webpack` 编译所有的 JS 依赖项，并使用一个简单的 Web 服务器在端口 `:8081` 上托管静态内容（`echotest.html` 和 `dist/main.js`）。从网页中输入的用户消息将作为 gRPC-web 请求发送到 Envoy 代理。

### What’s next 下一步

- Work through the [Basics tutorial](https://grpc.io/docs/platforms/web/basics/).
- 完成 [基础教程](https://grpc.io/docs/platforms/web/basics/)。