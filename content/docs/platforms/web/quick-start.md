+++
title = "快速入门"
weight = 1
date = 2023-05-31T10:43:26+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Quick start - 快速入门

​	这个指南通过一个简单的工作示例让你开始使用 gRPC-Web。



### 先决条件

- Docker 和支持 [Docker Compose 文件版本 3](https://docs.docker.com/compose/compose-file/compose-versioning) 的 `docker-compose`。安装说明请参见 [安装 Compose](https://docs.docker.com/compose/install/#install-compose)。

### 获取示例代码

​	该示例代码是 [grpc-web](https://github.com/grpc/grpc-web) 仓库中的一部分。

1. [下载该仓库的 zip 文件](https://github.com/grpc/grpc-web/archive/master.zip) 并解压，或者克隆该仓库：

   ```sh
   $ git clone https://github.com/grpc/grpc-web
   ```

2. 切换到该仓库的根目录：

   ```sh
   $ cd grpc-web
   ```


### 从浏览器中运行 Echo 示例！

​	在 `grpc-web` 目录：

1. 获取所需的包和工具：

   ```sh
   $ docker-compose pull prereqs node-server envoy commonjs-client
   ```

   #### 注意

   收到以下警告？你可以忽略它，以便运行该示例应用程序：

   ```nocode
   WARNING: Some service image(s) must be built from source
   ```

3. 启动服务作为后台进程：

   ```sh
   $ docker-compose up -d node-server envoy commonjs-client
   ```

4. 在你的浏览器中：

   - 访问 [localhost:8081/echotest.html](http://localhost:8081/echotest.html)。
   - 在文本输入框中输入消息，如"Hello"。
   - 点击 **Send** 按钮。
   
   你将在输入框下方看到服务器返回的消息。

​	恭喜！你刚刚使用 gRPC 运行了一个客户端-服务端（client-server）应用程序。

​	一旦完成后，您可通过运行以下命令关闭之前启动的服务：

```sh
$ docker-compose down
```

### 发生了什么？

​	这个示例应用程序有三个关键组件（components）：

1. `node-server` 是一个使用 Node 实现的标准 gRPC 服务端。该服务端在端口 `:9090` 上监听，并实现应用程序的业务逻辑（回显客户端消息）。
3. `envoy` 是 Envoy 代理。它在端口 `:8080` 上监听，并将浏览器的 gRPC-Web 请求转发到端口 `:9090`。
5. `commonjs-client`：该组件使用 `protoc-gen-grpc-web` protoc 插件生成客户端存根（stub）类，使用 `webpack` 编译所有的 JS 依赖项，并使用一个简单的 Web 服务器在端口 `:8081` 上托管静态内容（`echotest.html` 和 `dist/main.js`）。从网页中输入的用户消息将作为 gRPC-web 请求发送到 Envoy 代理。

### 下一步

- 完成 [基础教程](https://grpc.io/docs/platforms/web/basics/)。