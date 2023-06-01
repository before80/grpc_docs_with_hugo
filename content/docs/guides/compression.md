+++
title = "压缩"
weight = 3
date = 2023-05-31T10:44:47+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Compression 压缩

How to compress the data sent over the wire while using gRPC.

如何在使用gRPC时压缩通过网络发送的数据。



### Overview 概述

Compression is used to reduce the amount of bandwidth used when communicating between peers and can be enabled or disabled based on call or message level for all languages. For some languages, it is also possible to control compression settings at the channel level. Different languages also support different compression algorithms, including a customized compressor.

压缩用于在对等方之间通信时减少带宽使用量，并且可以基于调用或消息级别在所有语言中启用或禁用。对于某些语言，还可以在通道级别上控制压缩设置。不同的语言还支持不同的压缩算法，包括自定义的压缩器。

### Compression Method Asymmetry Between Peers  对等方之间的压缩方法不对称性

gRPC allows asymmetrically compressed communication, whereby a response may be compressed differently with the request, or not compressed at all. A gRPC peer may choose to respond using a different compression method to that of the request, including not performing any compression, regardless of channel and RPC settings (for example, if compression would result in small or negative gains).

gRPC允许不对称压缩通信，其中响应可以与请求以不同的方式进行压缩，或者根本不进行压缩。不论通道和RPC设置如何，gRPC对等方可以选择使用与请求不同的压缩方法来响应，包括不执行任何压缩（例如，如果压缩会导致较小或负面的收益）。

If a client message is compressed by an algorithm that is not supported by a server, the message will result in an `UNIMPLEMENTED` error status on the server. The server will include a `grpc-accept-encoding` header to the response which specifies the algorithms that the server accepts.

如果客户端消息使用服务器不支持的算法进行压缩，则服务器将在服务器上产生`UNIMPLEMENTED`错误状态。服务器将在响应中包含一个`grpc-accept-encoding`头，该头指定服务器接受的算法。

If the client message is compressed using one of the algorithms from the `grpc-accept-encoding` header and an `UNIMPLEMENTED` error status is returned from the server, the cause of the error won’t be related to compression.

如果客户端消息使用`grpc-accept-encoding`头中的算法之一进行压缩，并且从服务器返回`UNIMPLEMENTED`错误状态，则错误的原因与压缩无关。

Note that a peer may choose to not disclose all the encodings it supports. However, if it receives a message compressed in an undisclosed but supported encoding, it will include said encoding in the response’s `grpc-accept-encoding` header.

注意，对等方可能选择不披露其支持的所有编码。但是，如果它接收到使用未披露但受支持的编码进行压缩的消息，则会在响应的`grpc-accept-encoding`头中包含该编码。

For every message a server is requested to compress using an algorithm it knows the client doesn’t support (as indicated by the last `grpc-accept-encoding` header received from the client), it will send the message uncompressed.

对于服务器被请求使用其知道客户端不支持的算法进行压缩的每个消息，服务器将以未压缩的形式发送该消息，这是根据从客户端接收到的最后一个`grpc-accept-encoding`头指示的。

### Specific Disabling of Compression 明确禁用压缩

If the user requests to disable compression, the next message will be sent uncompressed. This is instrumental in preventing [BEAST](https://en.wikipedia.org/wiki/Transport_Layer_Security#BEAST_attack) and [CRIME](https://en.wikipedia.org/wiki/CRIME) attacks. This applies to both the unary and streaming cases.

如果用户请求禁用压缩，下一条消息将以未压缩的形式发送。这对于防止[BEAST](https://en.wikipedia.org/wiki/Transport_Layer_Security#BEAST_attack)和[CRIME](https://en.wikipedia.org/wiki/CRIME)攻击至关重要。这适用于一元和流式的情况。

### Language guides and examples 语言指南和示例

| 语言   | 示例                                                         | 文档                                                         |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| C++    | [C++ 示例](https://github.com/grpc/grpc/tree/master/examples/cpp/compression) | [C++ 文档](https://github.com/grpc/grpc/tree/master/examples/cpp/compression) |
| Go     | [Go 示例](https://github.com/grpc/grpc-go/tree/master/examples/features/compression) | [Go 文档](https://github.com/grpc/grpc-go/blob/master/Documentation/compression.md) |
| Java   | [Java 示例](https://github.com/grpc/grpc-java/tree/master/examples/src/main/java/io/grpc/examples/experimental) | [Java 文档](https://grpc.github.io/grpc-java/javadoc/io/grpc/CallOptions.html#withCompression-java.lang.String-) |
| Python | [Python 示例](https://github.com/grpc/grpc/tree/master/examples/python/compression) | [Python 文档](https://github.com/grpc/grpc/tree/master/examples/python/compression) |

### Additional Resources 其他资源

- [gRPC 压缩](https://github.com/grpc/grpc/blob/master/doc/compression.md)
- [gRPC（核心）压缩指南](https://github.com/grpc/grpc/blob/master/doc/compression_cookbook.md#per-call-settings)
- [Python 压缩 API 的 gRFC](https://github.com/grpc/proposal/blob/master/L46-python-compression-api.md)

