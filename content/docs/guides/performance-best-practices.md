+++
title = "性能最佳实践"
weight = 9
date = 2023-05-31T10:47:18+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Performance Best Practices 性能最佳实践

https://grpc.io/docs/guides/performance/

A user guide of both general and language-specific best practices to improve performance.

本文介绍了通用和特定语言的性能最佳实践，以提高性能。

### 通用

- Always **re-use stubs and channels** when possible.

- 本文介绍了一般性和特定语言的性能最佳实践，以提高性能。

- **Use keepalive pings** to keep HTTP/2 connections alive during periods of inactivity to allow initial RPCs to be made quickly without a delay (i.e. C++ channel arg GRPC_ARG_KEEPALIVE_TIME_MS).

- 在不活动期间使用**保持连接的 ping**，以保持 HTTP/2 连接处于活动状态，以便可以快速进行初始 RPC 调用，而无需延迟（例如 C++ 中的通道参数 GRPC_ARG_KEEPALIVE_TIME_MS）。

- **Use streaming RPCs** when handling a long-lived logical flow of data from the client-to-server, server-to-client, or in both directions. Streams can avoid continuous RPC initiation, which includes connection load balancing at the client-side, starting a new HTTP/2 request at the transport layer, and invoking a user-defined method handler on the server side.

- 在处理长时间的客户端到服务器、服务器到客户端或双向数据逻辑流时，**使用流式 RPC**。流可以避免连续的 RPC 启动，其中包括客户端的连接负载均衡，在传输层开始新的 HTTP/2 请求，并在服务器端调用用户定义的方法处理程序。

  Streams, however, cannot be load balanced once they have started and can be hard to debug for stream failures. They also might increase performance at a small scale but can reduce scalability due to load balancing and complexity, so they should only be used when they provide substantial performance or simplicity benefit to application logic. Use streams to optimize the application, not gRPC.

  然而，一旦流开始，就无法进行负载均衡，并且对于流故障的调试可能会很困难。它们在小规模上可能会提高性能，但由于负载均衡和复杂性，可能会降低可扩展性，因此只有在对应用程序逻辑提供实质性性能或简化方面有益时才应使用。使用流来优化应用程序，而不是 gRPC。

  ***Side note:*** *This does not apply to Python (see Python section for details).*

  ***注：*** *这不适用于 Python（请参考 Python 部分了解详细信息）*。

- *(Special topic)* Each gRPC channel uses 0 or more HTTP/2 connections and each connection usually has a limit on the number of concurrent streams. When the number of active RPCs on the connection reaches this limit, additional RPCs are queued in the client and must wait for active RPCs to finish before they are sent. Applications with high load or long-lived streaming RPCs might see performance issues because of this queueing. There are two possible solutions:

- *(特殊主题)* 每个 gRPC 通道使用 0 个或多个 HTTP/2 连接，每个连接通常对并发流的数量有限制。当连接上的活动 RPC 数量达到此限制时，额外的 RPC 将在客户端排队，并在等待活动的 RPC 完成后才会发送。具有高负载或长时间运行的流式 RPC 的应用程序可能会因此排队而出现性能问题。有两种可能的解决方案：

  1. **Create a separate channel for each area of high load** in the application.
  2. 在应用程序中的每个高负载区域**创建一个单独的通道**。
  3. **Use a pool of gRPC channels** to distribute RPCs over multiple connections (channels must have different channel args to prevent re-use so define a use-specific channel arg such as channel number).
  4. 使用**一组 gRPC 通道**将 RPC 分布到多个连接上（通道必须具有不同的通道参数，以防止重用，因此定义一个特定于使用的通道参数，如通道编号）。
  
  ***Side note:*** *The gRPC team has plans to add a feature to fix these performance issues (see [grpc/grpc#21386](https://github.com/grpc/grpc/issues/21386) for more info), so any solution involving creating multiple channels is a temporary workaround that should eventually not be needed.*
  
  ***注：*** *gRPC 团队计划添加一个功能来解决这些性能问题（有关详细信息，请参阅 [grpc/grpc#21386](https://github.com/grpc/grpc/issues/21386)），因此涉及创建多个通道的解决方案是一个临时解决方法，最终可能不再需要*。

### C++

- **Do not use Sync API for performance sensitive servers.** If performance and/or resource consumption are not concerns, use the Sync API as it is the simplest to implement for low-QPS services.

- **对于对性能敏感的服务器，不要使用同步 API**。如果性能和/或资源消耗不是问题，可以使用同步 API，因为它是实现低 QPS 服务最简单的方式。

- **Favor callback API over other APIs for most RPCs**, given that the application can avoid all blocking operations or blocking operations can be moved to a separate thread. The callback API is easier to use than the completion-queue async API but is currently slower for truly high-QPS workloads.

- **对于大多数 RPC，优先使用回调 API**，前提是应用程序可以避免所有阻塞操作，或者阻塞操作可以移到单独的线程中。回调 API 比完成队列异步 API 更易于使用，但在真正高 QPS 的工作负载中，它目前速度较慢。

- If having to use the async completion-queue API, the **best scalability trade-off is having `numcpu`’s threads.** The ideal number of completion queues in relation to the number of threads can change over time (as gRPC C++ evolves), but as of gRPC 1.41 (Sept 2021), using 2 threads per completion queue seems to give the best performance.

- 如果必须使用异步完成队列 API，则在**可扩展性和性能之间进行最佳平衡的方法是使用 `numcpu` 个线程**。关于完成队列数量与线程数之间的理想关系可能会随时间而变化（随着 gRPC C++ 的发展），但截至 gRPC 1.41（2021 年 9 月），每个完成队列使用 2 个线程似乎可以获得最佳性能。

- For the async completion-queue API, make sure to **register enough server requests for the desired level of concurrency** to avoid the server continuously getting stuck in a slow path that results in essentially serial request processing.

- 对于异步完成队列 API，请确保**为所需的并发级别注册足够的服务器请求**，以避免服务器持续陷入导致实质上的串行请求处理的慢路径。

- *(Special topic)* **Enable write batching in streams** if message k + 1 does not rely on responses from message k by passing a WriteOptions argument to Write with buffer_hint set:

- *(特殊主题)* 如果第 k + 1 个消息不依赖于第 k 个消息的响应，则在流中**启用写批处理**，通过传递带有设置了 buffer_hint 的 WriteOptions 参数来实现： 

  `stream_writer->Write(message, WriteOptions().set_buffer_hint());`

- *(Special topic)* [gRPC::GenericStub](https://grpc.github.io/grpc/cpp/grpcpp_2generic_2generic__stub_8h.html) can be useful in certain cases when there is high contention / CPU time spent on proto serialization. This class allows the application to directly send **raw gRPC::ByteBuffer as data** rather than serializing from some proto. This can also be helpful if the same data is being sent multiple times, with one explicit proto-to-ByteBuffer serialization followed by multiple ByteBuffer sends.

- *(特殊主题)* 在某些情况下，当存在高竞争/花费 CPU 时间用于 proto 序列化时，可以使用[gRPC::GenericStub](https://grpc.github.io/grpc/cpp/grpcpp_2generic_2generic__stub_8h.html)。该类允许应用程序直接发送**原始的 gRPC::ByteBuffer 作为数据**，而不是从某个 proto 进行序列化。如果同样的数据被多次发送，通过一个显式的 proto-to-ByteBuffer 序列化，然后进行多次 ByteBuffer 发送，可以提供帮助。

### Java

- **Use non-blocking stubs** to parallelize RPCs.
- **使用非阻塞存根（stubs）**以并行处理 RPC。
- **Provide a custom executor that limits the number of threads, based on your workload** (cached (default), fixed, forkjoin, etc).
- **提供自定义执行器，根据工作负载限制线程数**（缓存（默认），固定，forkjoin 等）。

### Python

- Streaming RPCs create extra threads for receiving and possibly sending the messages, which makes **streaming RPCs much slower than unary RPCs** in gRPC Python, unlike the other languages supported by gRPC.
- 流式 RPC 会创建额外的线程来接收和可能发送消息，这使得在 gRPC Python 中**流式 RPC 比一元 RPC 慢得多**，而其他由 gRPC 支持的语言不会出现这个问题。
- **Using [asyncio](https://grpc.github.io/grpc/python/grpc_asyncio.html)** could improve performance.
- **使用 [asyncio](https://grpc.github.io/grpc/python/grpc_asyncio.html)** 可以改善性能。
- Using the future API in the sync stack results in the creation of an extra thread. **Avoid the future API** if possible.
- 在同步堆栈中使用 future API 会创建额外的线程。**尽可能避免使用 future API**。
- *(Experimental)* An experimental **single-threaded unary-stream implementation** is available via the [SingleThreadedUnaryStream channel option](https://github.com/grpc/grpc/blob/master/src/python/grpcio/grpc/experimental/__init__.py#L38), which can save up to 7% latency per message.
- *(实验性)* 可通过[SingleThreadedUnaryStream 通道选项](https://github.com/grpc/grpc/blob/master/src/python/grpcio/grpc/experimental/__init__.py#L38)获得实验性的**单线程一元流实现**，可节省每个消息高达 7% 的延迟。