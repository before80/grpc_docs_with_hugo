+++
title = "FAQ"
weight = 3
date = 2023-05-31T10:40:11+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# FAQ



https://grpc.io/docs/what-is-grpc/faq/

Here are some frequently asked questions. Hope you find your answer here :-)

以下是一些常见问题。希望你能在这里找到答案 :-)

### What is gRPC? 什么是 gRPC？

gRPC is a modern, open source remote procedure call (RPC) framework that can run anywhere. It enables client and server applications to communicate transparently, and makes it easier to build connected systems.

gRPC 是一个现代的、开源的远程过程调用 (RPC) 框架，可以运行在任何地方。它使客户端和服务器应用程序能够透明地通信，并且更容易构建连接的系统。

Read the longer [Motivation & Design Principles](https://grpc.io/blog/principles/) post for background on why we created gRPC.

阅读更详细的 [Motivation & Design Principles](https://grpc.io/blog/principles/) 文章，了解我们为什么创建了 gRPC。

### What does gRPC stand for? gRPC 是什么的缩写？

**g**RPC **R**emote **P**rocedure **C**alls, of course!

### Why would I want to use gRPC? 为什么我要使用 gRPC？

The main usage scenarios:

主要的使用场景包括：

- Low latency, highly scalable, distributed systems.
- Developing mobile clients which are communicating to a cloud server.
- Designing a new protocol that needs to be accurate, efficient and language independent.
- Layered design to enable extension eg. authentication, load balancing, logging and monitoring etc.
- 低延迟、高可扩展性的分布式系统。
- 开发与云服务器通信的移动客户端。
- 设计一个需要准确、高效和语言无关的新协议。
- 分层设计以实现扩展，例如身份验证、负载均衡、日志记录和监控等。

### Who’s using this and why? 谁在使用它以及为什么？

gRPC is a [Cloud Native Computing Foundation](https://cncf.io/) (CNCF) project.

gRPC 是 [Cloud Native Computing Foundation](https://cncf.io/) (CNCF) 的项目。

Google has been using a lot of the underlying technologies and concepts in gRPC for a long time. The current implementation is being used in several of Google’s cloud products and Google externally facing APIs. It is also being used by [Square](https://corner.squareup.com/2015/02/grpc.html), [Netflix](https://github.com/Netflix/ribbon), [CoreOS](https://blog.gopheracademy.com/advent-2015/etcd-distributed-key-value-store-with-grpc-http2/), [Docker](https://blog.docker.com/2015/12/containerd-daemon-to-control-runc/), [CockroachDB](https://github.com/cockroachdb/cockroach), [Cisco](https://github.com/CiscoDevNet/grpc-getting-started), [Juniper Networks](https://github.com/Juniper/open-nti) and many other organizations and individuals.

Google 长期以来一直在使用许多 gRPC 的底层技术和概念。当前的实现被应用于 Google 的多个云产品和 Google 外部面向 API。它还被 [Square](https://corner.squareup.com/2015/02/grpc.html)、[Netflix](https://github.com/Netflix/ribbon)、[CoreOS](https://blog.gopheracademy.com/advent-2015/etcd-distributed-key-value-store-with-grpc-http2/)、[Docker](https://blog.docker.com/2015/12/containerd-daemon-to-control-runc/)、[CockroachDB](https://github.com/cockroachdb/cockroach)、[Cisco](https://github.com/CiscoDevNet/grpc-getting-started)、[Juniper Networks](https://github.com/Juniper/open-nti) 等许多组织和个人所使用。

### Which programming languages are supported? 支持哪些编程语言？

See [Officially supported languages and platforms](https://grpc.io/about/#officially-supported-languages-and-platforms).

请参阅 [Officially supported languages and platforms](https://grpc.io/about/#officially-supported-languages-and-platforms)。

### How do I get started using gRPC? 如何开始使用 gRPC？

You can start with installation of gRPC by following instructions [here](https://grpc.io/docs/quickstart/). Or head over to the [gRPC GitHub org page](https://github.com/grpc), pick the runtime or language you are interested in, and follow the README instructions.

你可以按照[这里](https://grpc.io/docs/quickstart/)的说明安装 gRPC。或者前往 [gRPC GitHub 组织页面](https://github.com/grpc)，选择你感兴趣的运行时或语言，并按照 README 中的说明进行操作。

### Which license is gRPC under? gRPC 使用哪种许可证？

All implementations are licensed under [Apache 2.0](https://github.com/grpc/grpc/blob/master/LICENSE).

所有实现都使用 [Apache 2.0 许可证](https://github.com/grpc/grpc/blob/master/LICENSE)。

### How can I contribute? 我如何做出贡献？

[Contributors](https://grpc.io/community/#contribute) are highly welcome and the repositories are hosted on GitHub. We look forward to community feedback, additions and bugs. Both individual contributors and corporate contributors need to sign our CLA. If you have ideas for a project around gRPC, read guidelines and submit [here](https://github.com/grpc/grpc-contrib/blob/master/CONTRIBUTING.md). We have a growing list of projects under the [gRPC Ecosystem](https://github.com/grpc-ecosystem) organization on GitHub.

非常欢迎 [贡献者](https://grpc.io/community/#contribute)，代码库托管在 GitHub 上。我们期待社区的反馈、补充和错误报告。个人贡献者和公司贡献者都需要签署我们的贡献者许可协议 (CLA)。如果你有关于 gRPC 的项目想法，请阅读指南并提交 [这里](https://github.com/grpc/grpc-contrib/blob/master/CONTRIBUTING.md)。我们在 GitHub 上的 [gRPC 生态系统](https://github.com/grpc-ecosystem) 组织下有一个不断增长的项目列表。

### Where is the documentation? 文档在哪里？

Check out the [documentation](https://grpc.io/docs/) right here on grpc.io.

请查阅 [grpc.io 上的文档](https://grpc.io/docs/)。

### What is the road map? 路线图是什么？

The gRPC project has an RFC process, through which new features are designed and approved for implementation. They are tracked in [this repository](https://github.com/grpc/proposal).

gRPC 项目有一个 RFC 流程，通过该流程设计并批准实施新功能。这些功能在 [该代码库](https://github.com/grpc/proposal) 中进行跟踪。

### How long are gRPC releases supported for? gRPC 的版本支持有多久？

The gRPC project does not do LTS releases. Given the rolling release model above, we support the current, latest release and the release prior to that. Support here means bug fixes and security fixes.

gRPC 项目没有长期支持 (LTS) 版本。根据上述滚动发布模型，我们支持当前的最新版本和之前的版本。支持意味着修复错误和安全问题。

### What is the gRPC versioning policy? gRPC 的版本控制策略是什么？

See the gRPC versioning policy [here](https://github.com/grpc/grpc/blob/master/doc/versioning.md).

请参阅 gRPC 的版本控制策略 [此处](https://github.com/grpc/grpc/blob/master/doc/versioning.md)。

### What is the latest gRPC Version? 最新的 gRPC 版本是多少？

The latest release tag is v1.55.0.

最新的发布标签是 v1.55.0。

### When do gRPC releases happen? gRPC 的发布时间是什么时候？

The gRPC project works in a model where the tip of the master branch is stable at all times. The project (across the various runtimes) targets to ship checkpoint releases every 6 weeks on a best effort basis. See the release schedule [here](https://github.com/grpc/grpc/blob/master/doc/grpc_release_schedule.md).

gRPC 项目采用的模式是主分支的 tip 在任何时候都是稳定的。该项目（在各种运行时中）目标是以尽力而为的方式每隔 6 周发布一个checkpoint 版本。请参阅发布计划 [此处](https://github.com/grpc/grpc/blob/master/doc/grpc_release_schedule.md)。

### How can I report a security vulnerability in gRPC? 我如何报告 gRPC 中的安全漏洞？

To report a security vulnerability in gRPC, please follow the process documented [here](https://github.com/grpc/proposal/blob/master/P4-grpc-cve-process.md).

如果要报告 gRPC 中的安全漏洞，请按照[此处](https://github.com/grpc/proposal/blob/master/P4-grpc-cve-process.md)的文档流程进行操作。

### Can I use it in the browser? 是否可以在浏览器中使用它？

The [gRPC-Web](https://github.com/grpc/grpc-web) project is Generally Available.

[gRPC-Web](https://github.com/grpc/grpc-web) 项目已经正式可用。

### Can I use gRPC with my favorite data format (JSON, Protobuf, Thrift, XML) ? 我可以在 gRPC 中使用我喜欢的数据格式（JSON、Protobuf、Thrift、XML）吗？

Yes. gRPC is designed to be extensible to support multiple content types. The initial release contains support for Protobuf and with external support for other content types such as FlatBuffers and Thrift, at varying levels of maturity.

可以。gRPC 的设计目标是支持多种内容类型的可扩展性。初始版本包含对 Protobuf 的支持，并在不同程度上支持其他内容类型，如 FlatBuffers 和 Thrift，但这些支持可能具有不同的成熟度水平。

### Can I use gRPC in a service mesh? 我可以在服务网格中使用 gRPC 吗？

Yes. gRPC applications can be deployed in a service mesh like any other application. gRPC also supports [xDS APIs](https://www.envoyproxy.io/docs/envoy/latest/api-docs/xds_protocol) which enables deploying gRPC applications in a service mesh without sidecar proxies. The proxyless service mesh features supported in gRPC are listed [here](https://github.com/grpc/grpc/blob/master/doc/grpc_xds_features.md).

可以。gRPC 应用程序可以像其他应用程序一样部署在服务网格中。gRPC 还支持 [xDS API](https://www.envoyproxy.io/docs/envoy/latest/api-docs/xds_protocol)，可以在服务网格中部署 gRPC 应用程序而无需使用 sidecar 代理。gRPC 支持的无代理服务网格功能可以在 [这里](https://github.com/grpc/grpc/blob/master/doc/grpc_xds_features.md) 查看。

### How does gRPC help in mobile application development? gRPC 如何在移动应用程序开发中发挥作用？

gRPC and Protobuf provide an easy way to precisely define a service and auto generate reliable client libraries for iOS, Android and the servers providing the back end. The clients can take advantage of advanced streaming and connection features which help save bandwidth, do more over fewer TCP connections and save CPU usage and battery life.

gRPC 和 Protobuf 提供了一种精确定义服务并自动生成可靠的 iOS、Android 和后端服务器的客户端库的简便方式。客户端可以利用高级流式和连接功能，帮助节省带宽，通过较少的 TCP 连接完成更多任务，并节省 CPU 使用和电池寿命。

### Why is gRPC better than any binary blob over HTTP/2? 为什么 gRPC 比使用 HTTP/2 传输的二进制数据块更好？

This is largely what gRPC is on the wire. However gRPC is also a set of libraries that will provide higher-level features consistently across platforms that common HTTP libraries typically do not. Examples of such features include:

这在很大程度上是 gRPC 在网络上传输的内容。然而，gRPC 也是一组库，可以在各个平台上提供高级功能，这些功能通常常见的 HTTP 库通常不具备。这些功能的示例包括：

- interaction with flow-control at the application layer
- cascading call-cancellation
- load balancing & failover
- 与应用层流量控制的交互
- 级联的调用取消
- 负载均衡和故障转移

### Why is gRPC better/worse than REST? 为什么 gRPC 比 REST 更好/更差？

gRPC largely follows HTTP semantics over HTTP/2 but we explicitly allow for full-duplex streaming. We diverge from typical REST conventions as we use static paths for performance reasons during call dispatch as parsing call parameters from paths, query parameters and payload body adds latency and complexity. We have also formalized a set of errors that we believe are more directly applicable to API use cases than the HTTP status codes.

gRPC 在很大程度上遵循 HTTP/2 上的 HTTP 语义，但我们明确允许全双工流式传输。我们与典型的 REST 约定有所不同，因为为了性能原因，在调用分派过程中我们使用静态路径，而从路径、查询参数和负载主体解析调用参数会增加延迟和复杂性。我们还正式确定了一组错误，我们认为这些错误与 API 使用情况更直接相关，而不是 HTTP 状态码。

### How do you pronounce gRPC? gRPC 的发音是什么？

Jee-Arr-Pee-See.