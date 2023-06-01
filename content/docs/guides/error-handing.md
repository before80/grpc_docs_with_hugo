+++
title = "错误处理"
weight = 6
date = 2023-05-31T10:45:57+08:00
description = ""
isCJKLanguage = true
draft = false

+++

# Error handling 错误处理

https://grpc.io/docs/guides/error/

How gRPC deals with errors, and gRPC error codes.

介绍了gRPC如何处理错误以及gRPC的错误代码。



### Standard error model 标准错误模型

As you’ll have seen in our concepts document and examples, when a gRPC call completes successfully the server returns an `OK` status to the client (depending on the language the `OK` status may or may not be directly used in your code). But what happens if the call isn’t successful?

正如您在我们的概念文档和示例中所看到的，当gRPC调用成功完成时，服务器将向客户端返回一个`OK`状态（根据语言，`OK`状态可能会或可能不会直接在您的代码中使用）。但是如果调用不成功会发生什么呢？

If an error occurs, gRPC returns one of its error status codes instead, with an optional string error message that provides further details about what happened. Error information is available to gRPC clients in all supported languages.

如果发生错误，gRPC会返回其中一个错误状态码，并可选地提供一个字符串错误消息，该消息提供了更多关于发生的情况的详细信息。所有支持的语言的gRPC客户端都可以获取错误信息。

### Richer error model 更丰富的错误模型

The error model described above is the official gRPC error model, is supported by all gRPC client/server libraries, and is independent of the gRPC data format (whether protocol buffers or something else). You may have noticed that it’s quite limited and doesn’t include the ability to communicate error details.

上述的错误模型是官方的gRPC错误模型，由所有gRPC客户端/服务器库支持，并且与gRPC的数据格式（无论是协议缓冲区还是其他格式）无关。您可能已经注意到它相当有限，并且没有包含传递错误详细信息的能力。

If you’re using protocol buffers as your data format, however, you may wish to consider using the richer error model developed and used by Google as described [here](https://cloud.google.com/apis/design/errors#error_model). This model enables servers to return and clients to consume additional error details expressed as one or more protobuf messages. It further specifies a [standard set of error message types](https://github.com/googleapis/googleapis/blob/master/google/rpc/error_details.proto) to cover the most common needs (such as invalid parameters, quota violations, and stack traces). The protobuf binary encoding of this extra error information is provided as trailing metadata in the response.

然而，如果您正在使用协议缓冲区作为数据格式，您可能希望考虑使用由Google开发和使用的更丰富的错误模型，详细信息可以在[这里](https://cloud.google.com/apis/design/errors#error_model)中找到。该模型使得服务器能够返回并且客户端能够消费表示为一个或多个protobuf消息的额外错误详细信息。它进一步指定了一组[标准的错误消息类型](https://github.com/googleapis/googleapis/blob/master/google/rpc/error_details.proto)，以涵盖最常见的需求（例如无效参数、配额超限和堆栈跟踪）。该额外的错误信息的protobuf二进制编码作为响应中的尾部元数据提供。

This richer error model is already supported in the C++, Go, Java, Python, and Ruby libraries, and at least the grpc-web and Node.js libraries have open issues requesting it. Other language libraries may add support in the future if there’s demand, so check their github repos if interested. Note however that the grpc-core library written in C will not likely ever support it since it is purposely data format agnostic.

这种更丰富的错误模型已经在C++、Go、Java、Python和Ruby库中得到支持，至少grpc-web和Node.js库存在请求支持的问题。如果有需求，其他语言库可能在将来添加支持，所以如果感兴趣的话可以查看它们的GitHub存储库。但请注意，以C语言编写的grpc-core库很可能永远不会支持它，因为它有意地与数据格式无关。

You could use a similar approach (put error details in trailing response metadata) if you’re not using protocol buffers, but you’d likely need to find or develop library support for accessing this data in order to make practical use of it in your APIs.

如果您不使用协议缓冲区，您可以采用类似的方法（将错误详细信息放在尾部的响应元数据中），但您可能需要找到或开发库来访问这些数据，以便在API中实际使用它。

There are important considerations to be aware of when deciding whether to use such an extended error model, however, including:

然而，在决定是否使用此扩展错误模型时，有一些重要的注意事项需要注意，包括： 

- Library implementations of the extended error model may not be consistent across languages in terms of requirements for and expectations of the error details payload
- Existing proxies, loggers, and other standard HTTP request processors don’t have visibility into the error details and thus wouldn’t be able to leverage them for monitoring or other purposes
- Additional error detail in the trailers interferes with head-of-line blocking, and will decrease HTTP/2 header compression efficiency due to more frequent cache misses
- Larger error detail payloads may run into protocol limits (like max headers size), effectively losing the original error
- 扩展错误模型的库实现在错误详细信息的要求和期望方面可能在不同的语言之间不一致
- 现有的代理、日志记录器和其他标准HTTP请求处理器无法获取错误详细信息，因此无法利用它们进行监控或其他目的
- 尾部中的附加错误详细信息会干扰首部阻塞，并且由于更频繁的缓存未命中，会降低HTTP/2首部压缩的效率
- 较大的错误详细信息负载可能会超过协议限制（如最大头大小），从而丢失原始错误信息

### Error status codes 错误状态码

Errors are raised by gRPC under various circumstances, from network failures to unauthenticated connections, each of which is associated with a particular status code. The following error status codes are supported in all gRPC languages.

gRPC在各种情况下引发错误，从网络故障到未经身份验证的连接，每种情况都与特定的状态码相关联。以下错误状态码在所有gRPC语言中都受支持。

#### General errors 通用错误

| 案例                                                        | 状态码                          |
| ----------------------------------------------------------- | ------------------------------- |
| 客户端应用程序取消了请求                                    | `GRPC_STATUS_CANCELLED`         |
| 截止时间在服务器返回状态之前过期                            | `GRPC_STATUS_DEADLINE_EXCEEDED` |
| 服务器上找不到该方法                                        | `GRPC_STATUS_UNIMPLEMENTED`     |
| 服务器关闭中                                                | `GRPC_STATUS_UNAVAILABLE`       |
| 服务器抛出异常（或执行了其他操作而不是返回状态码来终止RPC） | `GRPC_STATUS_UNKNOWN`           |



#### Network failures 网络故障

| 案例                                                         | 状态码                          |
| ------------------------------------------------------------ | ------------------------------- |
| 截止时间到期之前未传输任何数据。也适用于在截止时间到期之前传输了一些数据且未检测到其他故障的情况 | `GRPC_STATUS_DEADLINE_EXCEEDED` |
| 在连接断开之前传输了一些数据（例如，请求元数据已写入TCP连接） | `GRPC_STATUS_UNAVAILABLE`       |

#### 协议错误

| 案例                               | 状态码                           |
| ---------------------------------- | -------------------------------- |
| 无法解压缩，但支持压缩算法         | `GRPC_STATUS_INTERNAL`           |
| 客户端使用的压缩机制不被服务器支持 | `GRPC_STATUS_UNIMPLEMENTED`      |
| 流量控制资源限制已达到             | `GRPC_STATUS_RESOURCE_EXHAUSTED` |
| 流量控制协议违规                   | `GRPC_STATUS_INTERNAL`           |
| 解析返回的状态时出错               | `GRPC_STATUS_UNKNOWN`            |
| 未经身份验证：凭据未能获取元数据   | `GRPC_STATUS_UNAUTHENTICATED`    |
| 在授权元数据中设置了无效的主机     | `GRPC_STATUS_UNAUTHENTICATED`    |
| 解析响应协议缓冲区时出错           | `GRPC_STATUS_INTERNAL`           |
| 解析请求协议缓冲区时出错           | `GRPC_STATUS_INTERNAL`           |



### Sample code 示例代码

For sample code illustrating how to handle various gRPC errors, see the [grpc-errors](https://github.com/avinassh/grpc-errors) repo.

有关如何处理各种gRPC错误的示例代码，请参阅[grpc-errors](https://github.com/avinassh/grpc-errors)存储库。