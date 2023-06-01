+++
title = "保持连接"
weight = 8
date = 2023-05-31T10:46:22+08:00
description = ""
isCJKLanguage = true
draft = false

+++

# Keepalive 保持连接

https://grpc.io/docs/guides/keepalive/

How to use HTTP/2 PING-based keepalives in gRPC.

如何在 gRPC 中使用基于 HTTP/2 PING 的保持连接。

### Overview 概述

HTTP/2 PING-based keepalives are a way to keep an HTTP/2 connection alive even when there is no data being transferred. This is done by periodically sending a [PING frame](https://httpwg.org/specs/rfc7540.html#PING) to the other end of the connection. HTTP/2 keepalives can improve performance and reliability of HTTP/2 connections, but it is important to configure the keepalive interval carefully.

基于 HTTP/2 PING 的保持连接是一种在没有数据传输时保持 HTTP/2 连接活跃的方式。通过定期向连接的另一端发送 [PING 帧](https://httpwg.org/specs/rfc7540.html#PING) 来实现。HTTP/2 保持连接可以提高 HTTP/2 连接的性能和可靠性，但需要仔细配置保持连接间隔。

#### Note 注意

There is a related but separate concern called [Health Checking]. Health checking allows a server to signal whether a *service* is healthy while keepalive is only about the *connection*.

还有一个相关但独立的问题，称为[健康检查](https://grpc.io/docs/guides/concepts/#health-checking)。健康检查允许服务器表示一个*服务*是否健康，而保持连接只涉及*连接*。

### Background 背景

[TCP keepalive](https://en.wikipedia.org/wiki/Keepalive#TCP_keepalive) is a well-known method of maintaining connections and detecting broken connections. When TCP keepalive was enabled, either side of the connection can send redundant packets. Once ACKed by the other side, the connection will be considered as good. If no ACK is received after repeated attempts, the connection is deemed broken.

[TCP keepalive](https://en.wikipedia.org/wiki/Keepalive#TCP_keepalive) 是一种常用的维护连接和检测断开连接的方法。启用 TCP keepalive 后，连接的任一方都可以发送冗余数据包。一旦得到另一方的确认（ACK），连接将被视为正常。如果经过多次尝试仍未收到确认，连接将被视为断开。

Unlike TCP keepalive, gRPC uses HTTP/2 which provides a mandatory [PING frame](https://httpwg.org/specs/rfc7540.html#PING) which can be used to estimate round-trip time, bandwidth-delay product, or test the connection. The interval and retry in TCP keepalive don’t quite apply to PING because the transport is reliable, so they’re replaced with timeout (equivalent to interval * retry) in gRPC PING-based keepalive implementation.

与 TCP keepalive 不同，gRPC 使用的是 HTTP/2 协议，该协议提供了一个强制性的 [PING 帧](https://httpwg.org/specs/rfc7540.html#PING)，可以用于估算往返时间、带宽延迟乘积或测试连接。由于传输是可靠的，TCP keepalive 中的间隔和重试并不适用于 PING，因此在 gRPC 的基于 PING 的保持连接实现中，使用超时（等效于间隔 * 重试次数）来取代。

#### Note 注意

It’s not required for service owners to support keepalive. **Client authors must coordinate with service owners** for whether a particular client-side setting is acceptable. Service owners decide what they are willing to support, including whether they are willing to receive keepalives at all (If the service does not support keepalive, the first few keepalive pings will be ignored, and the server will eventually send a `GOAWAY` message with debug data equal to the ASCII code for `too_many_pings`).

服务所有者并非必须支持保持连接。**客户端作者必须与服务所有者协商**，确定特定的客户端设置是否可接受。服务所有者决定他们愿意支持的内容，包括是否愿意接收保持连接的请求（如果服务不支持保持连接，则前几个保持连接的 PING 将被忽略，服务器最终将发送带有“too_many_pings” ASCII 编码的调试数据的 `GOAWAY` 消息）。

### How configuring keepalive affects a call 配置保持连接如何影响调用

Keepalive is less likely to be triggered for unary RPCs with quick replies. Keepalive is primarily triggered when there is a long-lived RPC, which will fail if the keepalive check fails and the connection is closed.

对于具有快速响应的一元 RPC，不太可能触发保持连接。保持连接主要在存在长时间运行的 RPC 时触发，如果保持连接检查失败并关闭连接，该 RPC 将失败。

For streaming RPCs, if the connection is closed, any in-progress RPCs will fail. If a call is streaming data, the stream will also be closed and any data that has not yet been sent will be lost.

对于流式 RPC，如果连接关闭，任何正在进行中的 RPC 都将失败。如果调用正在流式传输数据，流也将关闭，并且尚未发送的任何数据将丢失。

#### Warning 警告

To avoid DDoSing, it’s important to take caution when setting the keepalive configurations. Thus, it is recommended to avoid enabling keepalive without calls and for clients to avoid configuring their keepalive much below one minute.

为了避免 DDoS 攻击，请在设置保持连接配置时要谨慎。因此，建议在没有调用的情况下避免启用保持连接，并且客户端应避免将保持连接配置得太短，不要低于一分钟。

### Common situations where keepalives can be useful 保持连接可用的常见情况

gRPC HTTP/2 keepalives can be useful in a variety of situations, including but not limited to:

gRPC 的 HTTP/2 保持连接可在多种情况下发挥作用，包括但不限于以下情况：

- When sending data over a long-lived connection which might be considered as idle by proxy or load balancers.
- When the network is less reliable (For example, mobile applications).
- When using a connection after a long period of inactivity.
- 在长时间运行的连接上发送数据，可能会被代理或负载均衡器视为空闲连接。
- 在网络不太可靠时（例如移动应用程序）。
- 在长时间不活动后重新使用连接时。

### Keepalive configuration specification 保持连接配置规范

| 选项                             | 可用性         | 描述                                                         | 客户端默认值    | 服务器默认值       |
| -------------------------------- | -------------- | ------------------------------------------------------------ | --------------- | ------------------ |
| `KEEPALIVE_TIME`                 | 客户端和服务器 | PING 帧之间的间隔（以毫秒为单位）。                          | INT_MAX（禁用） | 27200000（2 小时） |
| `KEEPALIVE_TIMEOUT`              | 客户端和服务器 | PING 帧被确认的超时时间（以毫秒为单位）。如果在此时间内发送方未收到确认，将关闭连接。 | 20000（20 秒）  | 20000（20 秒）     |
| `KEEPALIVE_WITHOUT_CALLS`        | 客户端         | 客户端在没有未完成的流的情况下是否可以发送保持连接的 PING。  | 0（false）      | N/A                |
| `PERMIT_KEEPALIVE_WITHOUT_CALLS` | 服务器         | 服务器在没有未完成的流的情况下是否可以发送保持连接的 PING。  | N/A             | 0（false）         |
| `PERMIT_KEEPALIVE_TIME`          | 服务器         | 服务器在连续接收到 PING 帧而未发送任何数据/头帧之间允许的最小时间间隔。 | N/A             | 300000（5 分钟）   |
| `MAX_CONNECTION_IDLE`            | 服务器         | 通道在没有未完成的 RPC 的情况下允许存在的最长时间，超过该时间后服务器将关闭连接。 | N/A             | INT_MAX（无限制）  |
| `MAX_CONNECTION_AGE`             | 服务器         | 通道允许存在的最长时间。                                     | N/A             | INT_MAX（无限制）  |
| `MAX_CONNECTION_AGE_GRACE`       | 服务器         | 在通道达到最长存活时间后的宽限期。                           | N/A             | INT_MAX（无限制）  |

#### 注意

Some languages may provide additional options, please refer to language examples and additional resource for more details.

某些语言可能提供其他选项，请参考语言示例和其他资源以获取更多详细信息。

### 语言指南和示例

| 语言   | 示例                                                         | 文档                                                         |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| C++    | [C++ 示例](https://github.com/grpc/grpc/tree/master/examples/cpp/keepalive) | [C++ 文档](https://github.com/grpc/grpc/blob/master/doc/keepalive.md) |
| Go     | [Go 示例](https://github.com/grpc/grpc-go/tree/master/examples/features/keepalive) | [Go 文档](https://github.com/grpc/grpc-go/blob/master/Documentation/keepalive.md) |
| Java   | [Java 示例](https://github.com/grpc/grpc-java/tree/master/examples/src/main/java/io/grpc/examples/keepalive) | [Java 文档](https://grpc.github.io/grpc-java/javadoc/io/grpc/ManagedChannelBuilder.html#keepAliveTime-long-java.util.concurrent.TimeUnit-) |
| Python | [Python 示例](https://github.com/grpc/grpc/tree/master/examples/python/keep_alive) | [Python 文档](https://github.com/grpc/grpc/blob/master/doc/keepalive.md) |

### 其他资源

- [客户端保持连接的 gRFC](https://github.com/grpc/proposal/blob/master/A8-client-side-keepalive.md)
- [服务器端连接管理的 gRFC](https://github.com/grpc/proposal/blob/master/A9-server-side-conn-mgt.md)
- [使用 gRPC 进行长时间运行和流式 RPC](https://www.youtube.com/watch?v=Naonb2XD_2Q)

