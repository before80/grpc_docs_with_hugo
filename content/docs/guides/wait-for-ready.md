+++
title = "等待就绪"
weight = 10
date = 2023-05-31T10:47:45+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Wait-for-Ready 等待就绪

https://grpc.io/docs/guides/wait-for-ready/

Explains how to configure RPCs to wait for the server to be ready before sending the request.

解释了如何配置 RPC，在发送请求之前等待服务器就绪。



### Overview 概述

This is a feature which can be used on a stub which will cause the RPCs to wait for the server to become available before sending the request. This allows for robust batch workflows since transient server problems won’t cause failures. The deadline still applies, so the wait will be interrupted if the deadline is passed.

这是一个可以用于存根（stub）的特性，它会导致 RPC 在发送请求之前等待服务器可用。这样可以实现稳健的批处理工作流，因为临时的服务器问题不会导致失败。仍然适用截止时间（deadline），所以如果超过截止时间，等待将被中断。

When an RPC is created when the channel has failed to connect to the server, without Wait-for-Ready it will immediately return a failure; with Wait-for-Ready it will simply be queued until the connection becomes ready. The default is **without** Wait-for-Ready.

当通道无法连接到服务器时创建 RPC，如果没有设置等待就绪（Wait-for-Ready），它会立即返回失败；如果设置了等待就绪，它将被简单地排队，直到连接就绪。默认情况下是**不使用**等待就绪。

For detailed semantics see [this](https://github.com/grpc/grpc/blob/master/doc/wait-for-ready.md).

有关详细的语义，请参阅[这个文档](https://github.com/grpc/grpc/blob/master/doc/wait-for-ready.md)。

### How to use Wait-for-Ready 如何使用等待就绪

You can specify for a stub whether or not it should use Wait-for-Ready, which will automatically be passed along when an RPC is created.

您可以为存根指定是否应该使用等待就绪，当创建 RPC 时，它会自动传递。

#### Note 注意

The RPC can still fail for other reasons besides the server not being ready, so error handling is still necessary.

除了服务器未就绪之外，RPC 仍然可能因其他原因而失败，因此仍然需要进行错误处理。

The following shows the sequence of events that occur, when a client sends a message to a server, based upon channel state and whether or not Wait-for-Ready is set.

以下是基于通道状态和是否设置了等待就绪的客户端向服务器发送消息时发生的事件序列。

![image-20230531111124821](wait-for-ready_img/image-20230531111124821.png)

The following is a state based view

以下是基于状态的视图

![image-20230531111143792](wait-for-ready_img/image-20230531111143792.png)

### Alternatives 替代方案

- Loop (with exponential backoff) until the RPC stops returning transient failures.
- 循环（使用指数退避）直到 RPC 不再返回临时失败。
  - This could be combined, for efficiency, with implementing an `onReady` Handler *(for languages that support this)*.
  - 这可以与实现`onReady`处理程序（适用于支持此功能的语言）结合使用以提高效率。
- Accept failures that might have been avoided by waiting because you want to fail fast
- 忽略可能因等待而避免的故障，因为您希望尽快失败。



### 语言支持

| 语言   | 示例                                                         |
| ------ | ------------------------------------------------------------ |
| Java   | [Java 示例](https://github.com/grpc/grpc-java/blob/master/examples/src/main/java/io/grpc/examples/waitforready/WaitForReadyClient.java) |
| Go     | [Go 示例](https://github.com/grpc/grpc-go/tree/master/examples/features/name_resolving) |
| Python | [Python 示例](https://github.com/grpc/grpc/tree/master/examples/python/wait_for_ready) |

