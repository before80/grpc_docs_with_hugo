+++
title = "compression"
date = 2023-05-31T10:44:47+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Compression

How to compress the data sent over the wire while using gRPC.



### Overview

Compression is used to reduce the amount of bandwidth used when communicating between peers and can be enabled or disabled based on call or message level for all languages. For some languages, it is also possible to control compression settings at the channel level. Different languages also support different compression algorithms, including a customized compressor.

### Compression Method Asymmetry Between Peers

gRPC allows asymmetrically compressed communication, whereby a response may be compressed differently with the request, or not compressed at all. A gRPC peer may choose to respond using a different compression method to that of the request, including not performing any compression, regardless of channel and RPC settings (for example, if compression would result in small or negative gains).

If a client message is compressed by an algorithm that is not supported by a server, the message will result in an `UNIMPLEMENTED` error status on the server. The server will include a `grpc-accept-encoding` header to the response which specifies the algorithms that the server accepts.

If the client message is compressed using one of the algorithms from the `grpc-accept-encoding` header and an `UNIMPLEMENTED` error status is returned from the server, the cause of the error won’t be related to compression.

Note that a peer may choose to not disclose all the encodings it supports. However, if it receives a message compressed in an undisclosed but supported encoding, it will include said encoding in the response’s `grpc-accept-encoding` header.

For every message a server is requested to compress using an algorithm it knows the client doesn’t support (as indicated by the last `grpc-accept-encoding` header received from the client), it will send the message uncompressed.

### Specific Disabling of Compression

If the user requests to disable compression, the next message will be sent uncompressed. This is instrumental in preventing [BEAST](https://en.wikipedia.org/wiki/Transport_Layer_Security#BEAST_attack) and [CRIME](https://en.wikipedia.org/wiki/CRIME) attacks. This applies to both the unary and streaming cases.

### Language guides and examples

| Language | Example                                                      | Documentation                                                |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| C++      | [C++ Example](https://github.com/grpc/grpc/tree/master/examples/cpp/compression) | [C++ Documentation](https://github.com/grpc/grpc/tree/master/examples/cpp/compression) |
| Go       | [Go Example](https://github.com/grpc/grpc-go/tree/master/examples/features/compression) | [Go Documentation](https://github.com/grpc/grpc-go/blob/master/Documentation/compression.md) |
| Java     | [Java Example](https://github.com/grpc/grpc-java/tree/master/examples/src/main/java/io/grpc/examples/experimental) | [Java Documentation](https://grpc.github.io/grpc-java/javadoc/io/grpc/CallOptions.html#withCompression-java.lang.String-) |
| Python   | [Python Example](https://github.com/grpc/grpc/tree/master/examples/python/compression) | [Python Documentation](https://github.com/grpc/grpc/tree/master/examples/python/compression) |

### Additional Resources

- [gRPC Compression](https://github.com/grpc/grpc/blob/master/doc/compression.md)
- [gRPC (Core) Compression Cookbook](https://github.com/grpc/grpc/blob/master/doc/compression_cookbook.md#per-call-settings)
- [gRFC for Python Compression API](https://github.com/grpc/proposal/blob/master/L46-python-compression-api.md)