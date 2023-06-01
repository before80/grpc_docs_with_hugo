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

An introduction to gRPC and protocol buffers.

​	gRPC 和协议缓冲区（protocol buffers）的简介。



This page introduces you to gRPC and protocol buffers. gRPC can use protocol buffers as both its Interface Definition Language (**IDL**) and as its underlying message interchange format. If you’re new to gRPC and/or protocol buffers, read this! If you just want to dive in and see gRPC in action first, [select a language](https://grpc.io/docs/languages/) and try its **Quick start**.

本页面向您介绍了 gRPC 和协议缓冲区。gRPC 可以将协议缓冲区用作其接口定义语言（**IDL**）和基础消息交换格式。如果您对 gRPC 和/或协议缓冲区还不熟悉，请先阅读本文！如果您只想立即深入了解 gRPC 并进行实践，[选择一种语言](https://grpc.io/docs/languages/)，并尝试其中的**快速入门**。

## Overview 概述

In gRPC, a client application can directly call a method on a server application on a different machine as if it were a local object, making it easier for you to create distributed applications and services. As in many RPC systems, gRPC is based around the idea of defining a service, specifying the methods that can be called remotely with their parameters and return types. On the server side, the server implements this interface and runs a gRPC server to handle client calls. On the client side, the client has a stub (referred to as just a client in some languages) that provides the same methods as the server.

在 gRPC 中，客户端应用程序可以直接调用不同机器上的服务器应用程序的方法，就像调用本地对象一样，这使得您更容易创建分布式应用程序和服务。与许多 RPC 系统一样，gRPC 基于定义服务的思想，指定可以使用其参数和返回类型远程调用的方法。在服务器端，服务器实现此接口并运行 gRPC 服务器来处理客户端调用。在客户端端，客户端具有一个存根（在某些语言中仅称为客户端），它提供与服务器相同的方法。



![Concept Diagram](introduction_img/landing-2.svg)



gRPC clients and servers can run and talk to each other in a variety of environments - from servers inside Google to your own desktop - and can be written in any of gRPC’s supported languages. So, for example, you can easily create a gRPC server in Java with clients in Go, Python, or Ruby. In addition, the latest Google APIs will have gRPC versions of their interfaces, letting you easily build Google functionality into your applications.

gRPC 客户端和服务器可以在各种环境中运行和相互通信，从 Google 内部的服务器到您自己的桌面，并且可以使用 gRPC 支持的任何语言进行编写。因此，例如，您可以轻松地在 Java 中创建一个 gRPC 服务器，并使用 Go、Python 或 Ruby 中的客户端。此外，最新的 Google API 将具有 gRPC 版本的接口，让您可以轻松地将 Google 功能集成到您的应用程序中。

### Working with Protocol Buffers 使用协议缓冲区

By default, gRPC uses [Protocol Buffers](https://protobuf.dev/overview), Google’s mature open source mechanism for serializing structured data (although it can be used with other data formats such as JSON). Here’s a quick intro to how it works. If you’re already familiar with protocol buffers, feel free to skip ahead to the next section.

默认情况下，gRPC 使用 [协议缓冲区](https://protobuf.dev/overview)，这是 Google 成熟的开源机制，用于序列化结构化数据（尽管它也可以与其他数据格式如 JSON 一起使用）。下面是它的工作原理的简要介绍。如果您已经熟悉协议缓冲区，请随时跳到下一节。

The first step when working with protocol buffers is to define the structure for the data you want to serialize in a *proto file*: this is an ordinary text file with a `.proto` extension. Protocol buffer data is structured as *messages*, where each message is a small logical record of information containing a series of name-value pairs called *fields*. Here’s a simple example:

在使用协议缓冲区时的第一步是在一个名为 *proto 文件* 的文件中定义要序列化的数据的结构：这是一个带有 `.proto` 扩展名的普通文本文件。协议缓冲区数据被结构化为 *消息*，其中每个消息是包含一系列名值对（称为 *字段*）的小型逻辑记录的信息。以下是

```proto
message Person {
  string name = 1;
  int32 id = 2;
  bool has_ponycopter = 3;
}
```

Then, once you’ve specified your data structures, you use the protocol buffer compiler `protoc` to generate data access classes in your preferred language(s) from your proto definition. These provide simple accessors for each field, like `name()` and `set_name()`, as well as methods to serialize/parse the whole structure to/from raw bytes. So, for instance, if your chosen language is C++, running the compiler on the example above will generate a class called `Person`. You can then use this class in your application to populate, serialize, and retrieve `Person` protocol buffer messages.

一旦您指定了数据结构，您就可以使用协议缓冲区编译器 `protoc` 根据您的 proto 定义生成所需语言的数据访问类。这些类提供了对每个字段的简单访问器，如 `name()` 和 `set_name()`，以及将整个结构序列化/解析为原始字节的方法。例如，如果您选择的语言是 C++，在上面的示例上运行编译器将生成一个名为 `Person` 的类。然后，您可以在应用程序中使用此类来填充、序列化和检索 `Person` 协议缓冲区消息。

You define gRPC services in ordinary proto files, with RPC method parameters and return types specified as protocol buffer messages:

您可以在普通的 proto 文件中定义 gRPC 服务，其中 RPC 方法的参数和返回类型指定为协议缓冲区消息：

```proto
// The greeter service definition. Greeter 服务定义。
service Greeter {
  // Sends a greeting 发送问候
  rpc SayHello (HelloRequest) returns (HelloReply) {}
}

// The request message containing the user's name. 包含用户姓名的请求消息。
message HelloRequest {
  string name = 1;
}

// The response message containing the greetings 包含问候语的响应消息。
message HelloReply {
  string message = 1;
}
```

gRPC uses `protoc` with a special gRPC plugin to generate code from your proto file: you get generated gRPC client and server code, as well as the regular protocol buffer code for populating, serializing, and retrieving your message types. To learn more about protocol buffers, including how to install `protoc` with the gRPC plugin in your chosen language, see the [protocol buffers documentation](https://protobuf.dev/overview).

gRPC 使用带有特殊 gRPC 插件的 `protoc` 从您的 proto 文件生成代码：您将获得生成的 gRPC 客户端和服务器代码，以及用于填充、序列化和检索消息类型的常规协议缓冲区代码。要了解有关协议缓冲区的更多信息，包括如何在所选语言中安装带有 gRPC 插件的 `protoc`，请参阅 [协议缓冲区文档](https://protobuf.dev/overview)。

## Protocol buffer versions 协议缓冲区版本

While [protocol buffers](https://protobuf.dev/overview) have been available to open source users for some time, most examples from this site use protocol buffers version 3 (proto3), which has a slightly simplified syntax, some useful new features, and supports more languages. Proto3 is currently available in Java, C++, Dart, Python, Objective-C, C#, a lite-runtime (Android Java), Ruby, and JavaScript from the [protocol buffers GitHub repo](https://github.com/google/protobuf/releases), as well as a Go language generator from the [golang/protobuf official package](https://pkg.go.dev/google.golang.org/protobuf), with more languages in development. You can find out more in the [proto3 language guide](https://protobuf.dev/programming-guides/proto3) and the [reference documentation](https://protobuf.dev/reference) available for each language. The reference documentation also includes a [formal specification](https://protobuf.dev/reference/protobuf/proto3-spec) for the `.proto` file format.

虽然[协议缓冲区](https://protobuf.dev/overview)已经可供开源用户使用一段时间了，但本网站的大多数示例使用协议缓冲区版本 3（proto3），它具有稍微简化的语法、一些有用的新功能，并支持更多语言。Proto3 目前可在 Java、C++、Dart、Python、Objective-C、C#、轻量级运行时（Android Java）、Ruby 和 JavaScript 中使用，这些版本可以从 [协议缓冲区 GitHub 仓库](https://github.com/google/protobuf/releases)获取，还有一个来自 [golang/protobuf 官方包](https://pkg.go.dev/google.golang.org/protobuf) 的 Go 语言生成器，同时还有更多语言正在开发中。您可以在每种语言的 [proto3 语言指南](https://protobuf.dev/programming-guides/proto3) 和 [参考文档](https://protobuf.dev/reference) 中了解更多信息。参考文档还包括 `.proto` 文件格式的 [正式规范](https://protobuf.dev/reference/protobuf/proto3-spec)。

In general, while you can use proto2 (the current default protocol buffers version), we recommend that you use proto3 with gRPC as it lets you use the full range of gRPC-supported languages, as well as avoiding compatibility issues with proto2 clients talking to proto3 servers and vice versa.

总的来说，尽管您可以使用 proto2（当前默认的协议缓冲区版本），但我们建议您使用 proto3 与 gRPC 结合使用，因为它可以让您使用完整范围的 gRPC 支持的语言，同时避免 proto2 客户端与 proto3 服务器之间的兼容性问题。