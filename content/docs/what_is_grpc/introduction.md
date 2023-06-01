+++
title = "gRPC 简介"
weight = 1
date = 2023-05-31T10:39:36+08:00
description = "gRPC 和协议缓冲区（protocol buffers）的简介。"
isCJKLanguage = true
draft = false

+++

# Introduction to gRPC - gRPC 简介

> 原文：[https://grpc.io/docs/what-is-grpc/introduction/](https://grpc.io/docs/what-is-grpc/introduction/)

​	gRPC 和协议缓冲区（protocol buffers）的简介。

​	本页面向您介绍了 gRPC 和协议缓冲区。gRPC 可以将协议缓冲区用作其接口定义语言（**IDL**）和基础消息交换格式。如果您对 gRPC 和/或协议缓冲区还不熟悉，请先阅读本文！如果您只想立即深入了解 gRPC 并进行实践，[选择一种语言]({{< ref "/docs/languages">}})，并尝试其中的**快速入门**。

## 概述

​	在 gRPC 中，客户端应用程序可以直接调用不同机器上的服务端应用程序的方法，就像调用本地对象一样，这使得您更容易创建分布式应用程序和服务。与许多 RPC 系统一样，gRPC 基于定义服务的思想，指定可远程调用的方法及其参数和返回类型。在服务端，服务端实现此接口并运行 gRPC 服务端来处理客户端调用。在客户端，客户端具有一个*存根（stub）*（在某些语言中仅称为客户端），它提供与服务端相同的方法。



![Concept Diagram](introduction_img/landing-2.svg)



​	gRPC 客户端和服务端可以在各种环境中运行和相互通信，从 Google 内部的服务器到您自己的笔记本电脑，并且可以使用 gRPC 支持的任何语言进行编写。因此，例如，您可以轻松地在 Java 中创建一个 gRPC 服务端，并使用 Go、Python 或 Ruby 编写客户端。此外，最新的 Google API 将具有 gRPC 版本的接口，让您可以轻松地将 Google 功能集成到您的应用程序中。

### 使用协议缓冲区

​	默认情况下，gRPC 使用 [协议缓冲区（Protocol Buffers）](https://protobuf.dev/overview)，这是 Google 成熟的开源机制（Google’s mature open source mechanism），用于序列化结构化数据（尽管它也可以与其他数据格式如 JSON 一起使用）。下面是它的工作原理的简要介绍。如果您已经熟悉协议缓冲区，请随时跳到下一节。

​	在使用协议缓冲区时的第一步是在一个 *proto 文件* 的文件中定义要序列化的数据的结构：这是一个带有 `.proto` 扩展名的普通文本文件。协议缓冲区数据被结构化为 *消息（messages）*，其中每个消息是包含一系列名值对（称为 *字段（fields）*）的小型逻辑记录的信息。下面是一个简单的例子：

```proto
message Person {
  string name = 1;
  int32 id = 2;
  bool has_ponycopter = 3;
}
```

​	一旦您指定了数据结构，您就可以使用协议缓冲区编译器 `protoc` 根据您的 proto 定义生成所需语言的数据访问类。这些类提供了对每个字段的简单访问器，如 `name()` 和 `set_name()`，以及将整个结构序列化/解析为原始字节的方法。例如，如果您选择的语言是 C++，在上面的示例上运行编译器将生成一个名为 `Person` 的类。然后，您可以在应用程序中使用此类来填充（populate）、序列化（serialize）和检索（retrieve） `Person` 协议缓冲区消息。

​	您可以在普通的 proto 文件中定义 gRPC 服务，其中 RPC 方法的参数和返回类型被指定为协议缓冲区消息：

```proto
// The greeter service definition. - Greeter 服务定义。
service Greeter {
  // Sends a greeting 发送问候
  rpc SayHello (HelloRequest) returns (HelloReply) {}
}

// The request message containing the user's name. 包含用户 name 的请求消息。
message HelloRequest {
  string name = 1;
}

// The response message containing the greetings 包含问候语的响应消息。
message HelloReply {
  string message = 1;
}
```

​	gRPC 使用带有特殊 gRPC 插件的 `protoc` 从您的 proto 文件生成代码：您将获得生成的 gRPC 客户端和服务端代码，以及用于填充（populating）、序列化（serializing）和检索（retrieving ）消息类型的常规协议缓冲区代码。要了解有关协议缓冲区的更多信息，包括如何在所选语言中安装带有 gRPC 插件的 `protoc`，请参阅 [协议缓冲区文档](https://protobuf.dev/overview)。

## 协议缓冲区版本

​	虽然[协议缓冲区](https://protobuf.dev/overview)已经可供开源用户使用一段时间了，但本站的大多数示例使用协议缓冲区版本 3（proto3），它具有稍微简化的语法、一些有用的新功能，并支持更多语言。proto3 目前可在 Java、C++、Dart、Python、Objective-C、C#、轻量级运行时（Android Java）、Ruby 和 JavaScript 中使用，这些版本可以从 [协议缓冲区 GitHub 仓库](https://github.com/google/protobuf/releases)获取，还有一个来自 [golang/protobuf 官方包](https://pkg.go.dev/google.golang.org/protobuf) 的 Go 语言生成器，同时还有更多语言正在开发中。您可以在每种语言的 [proto3 语言指南](https://protobuf.dev/programming-guides/proto3) 和 [参考文档](https://protobuf.dev/reference) 中了解更多信息。参考文档还包括 `.proto` 文件格式的 [正式规范](https://protobuf.dev/reference/protobuf/proto3-spec)。

​	总的来说，尽管您可以使用 proto2（当前默认的协议缓冲区版本），但我们建议您在使用gRPC时使用proto3，因为它可以让您使用完整范围的 gRPC 支持的编程语言，同时避免 proto2 客户端与 proto3 服务端之间的兼容性问题。