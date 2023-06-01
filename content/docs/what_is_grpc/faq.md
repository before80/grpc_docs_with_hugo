+++
title = "FAQ"
weight = 3
date = 2023-05-31T10:40:11+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# FAQ - 常见问题



https://grpc.io/docs/what-is-grpc/faq/

​	以下是一些常见问题。希望你能在这里找到答案 :-)

### What is gRPC? 什么是 gRPC？

​	gRPC 是一个现代的、开源的远程过程调用 (RPC) 框架，可以运行在任何地方。它使客户端和服务端应用程序能够透明地进行通信，并且更容易构建连接的系统。

​	阅读更详细的 [动机和设计原则（Motivation & Design Principles）](https://grpc.io/blog/principles/) 文章，了解我们为什么创建gRPC的背景。

### gRPC 是什么的缩写？

​	**g**RPC **R**emote **P**rocedure **C**alls, of course!

### 为什么我要使用 gRPC？

​	主要的使用场景包括：

- 低延迟、高可扩展性的分布式系统。
- 开发与云服务端通信的移动客户端。
- 设计一个需要准确、高效和语言无关的新协议。
- 分层设计以实现扩展，例如认证、负载均衡、日志记录和监控等。

### 谁在使用它以及为什么？

​	gRPC 是 [云原生计算基金会（Cloud Native Computing Foundation）](https://cncf.io/) (CNCF) 的项目。

​	Google 长期以来一直在使用许多 gRPC 的底层技术和概念。当前的实现被应用于 Google 的多个云产品和 Google 外部 API。它还被 [Square](https://corner.squareup.com/2015/02/grpc.html)、[Netflix](https://github.com/Netflix/ribbon)、[CoreOS](https://blog.gopheracademy.com/advent-2015/etcd-distributed-key-value-store-with-grpc-http2/)、[Docker](https://blog.docker.com/2015/12/containerd-daemon-to-control-runc/)、[CockroachDB](https://github.com/cockroachdb/cockroach)、[Cisco](https://github.com/CiscoDevNet/grpc-getting-started)、[Juniper Networks](https://github.com/Juniper/open-nti) 等许多组织和个人所使用。

### 支持哪些编程语言？

​	请参阅 [官方支持的语言和平台（Officially supported languages and platforms）](https://grpc.io/about/#officially-supported-languages-and-platforms)。

### 如何开始使用 gRPC？

​	你可以按照[这里](https://grpc.io/docs/quickstart/)的说明安装 gRPC。或者前往 [gRPC GitHub 组织页面](https://github.com/grpc)，选择你感兴趣的运行时或语言，并按照 README 中的说明进行操作。

### gRPC 使用哪种许可证？

​	所有实现都使用 [Apache 2.0 许可证](https://github.com/grpc/grpc/blob/master/LICENSE)。

### 我如何做出贡献？

​	非常欢迎 [贡献者](https://grpc.io/community/#contribute)，代码库托管在 GitHub 上。我们期待社区的反馈、补充和错误报告。个人贡献者和公司贡献者都需要签署我们的贡献者许可协议 (CLA)。如果你有关于 gRPC 的项目想法，请阅读指南并提交到 [这里](https://github.com/grpc/grpc-contrib/blob/master/CONTRIBUTING.md)。我们在 GitHub 上的 [gRPC 生态系统](https://github.com/grpc-ecosystem) 组织下有一个不断增长的项目列表。

### 文档在哪里？

​	请查阅 [grpc.io 上的文档]({{< ref "/docs">}})。

### What is the road map? 

​	gRPC 项目有一个 RFC 过程，通过该过程设计和批准新功能的实现。这些功能在 [该代码库](https://github.com/grpc/proposal) 中进行跟踪。

### gRPC 的版本支持有多久？

​	gRPC 项目没有长期支持 (LTS) 版本。根据上述滚动发布模型，我们支持当前的最新版本和上一个版本。这里的支持意味着修复错误和安全问题。

### gRPC 的版本控制策略是什么？

​	请参阅 gRPC 的版本控制策略 [此处](https://github.com/grpc/grpc/blob/master/doc/versioning.md)。

### 最新的 gRPC 版本是多少？

​	最新的发布标签是 v1.55.0。

### gRPC 的发布时间是什么时候？

​	gRPC 项目采用的模式是主分支的 tip 在任何时候都是稳定的。该项目（在各种运行时中）目标是以尽力而为的方式每隔 6 周发布一个checkpoint 版本。请参阅[此处](https://github.com/grpc/grpc/blob/master/doc/grpc_release_schedule.md)的发布计划 。

### 我如何报告 gRPC 中的安全漏洞？

​	如果要报告 gRPC 中的安全漏洞，请按照[此处](https://github.com/grpc/proposal/blob/master/P4-grpc-cve-process.md)的文档流程进行操作。

### 是否可以在浏览器中使用它？

​	[gRPC-Web](https://github.com/grpc/grpc-web) 项目已经正式可用。

### 我可以在 gRPC 中使用我喜欢的数据格式（JSON、Protobuf、Thrift、XML）吗？

​	可以。gRPC 的设计目标是支持多种内容类型的可扩展性。初始版本包含对 Protobuf 的支持，并在不同程度上支持其他内容类型，如 FlatBuffers 和 Thrift，但这些支持可能具有不同的成熟度水平。

### 我可以在服务网格（service mesh）中使用 gRPC 吗？

​	可以。gRPC 应用程序可以像其他应用程序一样部署在服务网格中。gRPC 还支持 [xDS API](https://www.envoyproxy.io/docs/envoy/latest/api-docs/xds_protocol)，可以在服务网格中部署 gRPC 应用程序而无需使用 sidecar 代理。gRPC 支持的无代理服务网格功能可以在 [这里](https://github.com/grpc/grpc/blob/master/doc/grpc_xds_features.md) 查看。

### gRPC 如何在移动应用程序开发中发挥作用？

​	gRPC和Protobuf提供了一种精确定义服务并自动生成可靠的iOS、Android客户端库以及提供后端的服务端的简便方法。客户端可以利用高级的流式传输和连接功能，帮助节省带宽，通过较少的TCP连接实现更多功能，并节省CPU使用和电池寿命。

### 为什么 gRPC 比使用 HTTP/2 传输的二进制数据块更好？

​	这主要是gRPC在通信中的作用。然而，gRPC也是一组库，在各个平台上提供高级功能，这些功能通常是常见的HTTP库所不具备的。此类功能的示例包括：

- 与应用层流量控制的交互
- 级联的调用取消
- 负载均衡和故障转移

### 为什么 gRPC 比 REST 更好/更差？

​	gRPC 在很大程度上遵循 HTTP/2 上的 HTTP 语义，但我们明确允许全双工流式传输。我们与典型的 REST 约定有所不同，因为为了性能原因，我们在调用分派过程中使用静态路径，从路径、查询参数和有效载荷主体中解析调用参数会增加延迟和复杂性。我们还形成了一套错误集，我们认为这些错误集与API用例更直接相关，而不是HTTP状态码。

### gRPC 的发音是怎样的？

​	Jee-Arr-Pee-See.