+++
title = "Protocol Buffer 编译器安装"
weight = -1
date = 2023-06-02T08:27:56+08:00
description = ""
isCJKLanguage = true
draft = false

+++

# Protocol Buffer Compiler Installation - Protocol Buffer 编译器安装

​	如何安装 Protocol Buffer 编译器？

​	虽然不是强制要求，但 gRPC 应用程序通常使用 [Protocol Buffers](https://developers.google.com/protocol-buffers) 来进行服务定义和数据序列化。本站的大部分示例代码使用 [Protocol Buffer 语言的版本 3 (proto3)](https://protobuf.dev/programming-guides/proto3)。

​	Protocol Buffer 编译器 `protoc` 用于编译包含服务和消息定义的 `.proto` 文件。请按照以下方法之一安装 `protoc`。

### 使用软件包管理器安装

​	你可以使用软件包管理器在 Linux 或 macOS 上安装 protocol 编译器 —— `protoc`，请使用以下命令：

> 警告
>
> ​	安装后，**请检查 `protoc` 的版本**（如下所示）以确保它足够新。某些软件包管理器安装的 `protoc` 版本可能相当旧。
>
> ​	按照[下一节](https://grpc.io/docs/protoc-installation/#binary-install)中所示的预编译二进制文件进行安装，是确保您使用最新版本的 `protoc` 的最佳方式。

- Linux，请使用 `apt` 或 `apt-get`，例如：

  ```sh
  $ apt install -y protobuf-compiler
  $ protoc --version  # Ensure compiler version is 3+
  ```

- MacOS，请使用 [Homebrew](https://brew.sh/):

  ```sh
  $ brew install protobuf
  $ protoc --version  # Ensure compiler version is 3+
  ```



### 安装预编译二进制文件（任何操作系统）

​	要从预编译的二进制文件安装 Protocol 编译器的[最新版本](https://protobuf.dev/downloads#release-packages)，请按照以下说明进行操作：

1. 从 [github.com/google/protobuf/releases](https://github.com/google/protobuf/releases) 手动下载与您的操作系统和计算机架构相对应的 zip 文件（`protoc-<version>-<os>-<arch>.zip`），或使用类似以下的命令来获取文件：

   ```sh
   $ PB_REL="https://github.com/protocolbuffers/protobuf/releases"
   $ curl -LO $PB_REL/download/v3.15.8/protoc-3.15.8-linux-x86_64.zip
   ```

2. 将文件解压缩到 `$HOME/.local` 或您选择的目录下。例如：

   ```sh
   $ unzip protoc-3.15.8-linux-x86_64.zip -d $HOME/.local
   ```

3. 更新您的环境变量路径，将 `protoc` 可执行文件的路径包含在其中。例如：

   ```sh
   $ export PATH="$PATH:$HOME/.local/bin"
   ```

### 其他安装选项

​	如果您想从源代码构建 Protocol 编译器，或者访问旧版本的预编译二进制文件，请参阅 [Download Protocol Buffers](https://protobuf.dev/downloads)。