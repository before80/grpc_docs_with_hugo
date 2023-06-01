+++
title = "ALTS"
weight = 3
date = 2023-05-31T10:41:43+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# ALTS authentication ALTS身份验证

An overview of gRPC authentication in Go using Application Layer Transport Security (ALTS).

使用应用层传输安全（Application Layer Transport Security，ALTS）在Go中进行gRPC身份验证的概述。



### Overview 概述

Application Layer Transport Security (ALTS) is a mutual authentication and transport encryption system developed by Google. It is used for securing RPC communications within Google’s infrastructure. ALTS is similar to mutual TLS but has been designed and optimized to meet the needs of Google’s production environments. For more information, take a look at the [ALTS whitepaper](https://cloud.google.com/security/encryption-in-transit/application-layer-transport-security).

应用层传输安全（ALTS）是由Google开发的相互认证和传输加密系统，用于保护Google基础架构内的RPC通信。ALTS类似于相互TLS，但经过设计和优化以满足Google生产环境的需求。有关更多信息，请参阅[ALTS白皮书](https://cloud.google.com/security/encryption-in-transit/application-layer-transport-security)。

ALTS in gRPC has the following features:

gRPC中的ALTS具有以下功能：

- Create gRPC servers & clients with ALTS as the transport security protocol.
- ALTS connections are end-to-end protected with privacy and integrity.
- Applications can access peer information such as the peer service account.
- Client authorization and server authorization support.
- Minimal code changes to enable ALTS.
- 使用ALTS作为传输安全协议创建gRPC服务器和客户端。
- ALTS连接具有端到端的隐私和完整性保护。
- 应用程序可以访问对等方信息，例如对等方服务帐号。
- 支持客户端授权和服务器授权。
- 最小的代码更改以启用ALTS。

gRPC users can configure their applications to use ALTS as a transport security protocol with few lines of code.

gRPC用户可以配置其应用程序以使用ALTS作为传输安全协议，只需几行代码。

Note that ALTS is fully functional if the application runs on [Google Cloud Platform](https://cloud.google.com/). ALTS could be run on any platforms with a pluggable [ALTS handshaker service](https://github.com/grpc/grpc/blob/7e367da22a137e2e7caeae8342c239a91434ba50/src/proto/grpc/gcp/handshaker.proto#L224-L234).

请注意，如果应用程序在[Google Cloud Platform](https://cloud.google.com/)上运行，则ALTS是完全功能的。ALTS可以在任何平台上运行，只需具备可插拔的[ALTS握手服务](https://github.com/grpc/grpc/blob/7e367da22a137e2e7caeae8342c239a91434ba50/src/proto/grpc/gcp/handshaker.proto#L224-L234)。

### gRPC Client with ALTS Transport Security Protocol 使用ALTS传输安全协议的gRPC客户端

gRPC clients can use ALTS credentials to connect to servers, as illustrated in the following code excerpt:

gRPC客户端可以使用ALTS凭据连接到服务器，如下面的代码摘录所示：

```go
import (
  "google.golang.org/grpc"
  "google.golang.org/grpc/credentials/alts"
)

altsTC := alts.NewClientCreds(alts.DefaultClientOptions())
conn, err := grpc.Dial(serverAddr, grpc.WithTransportCredentials(altsTC))
```

### gRPC Server with ALTS Transport Security Protocol 使用ALTS传输安全协议的gRPC服务器

gRPC servers can use ALTS credentials to allow clients to connect to them, as illustrated next:

gRPC服务器可以使用ALTS凭据允许客户端连接到它们，如下所示：

```go
import (
  "google.golang.org/grpc"
  "google.golang.org/grpc/credentials/alts"
)

altsTC := alts.NewServerCreds(alts.DefaultServerOptions())
server := grpc.NewServer(grpc.Creds(altsTC))
```

### Server Authorization 服务器授权

gRPC has built-in server authorization support using ALTS. A gRPC client using ALTS can set the expected server service accounts prior to establishing a connection. Then, at the end of the handshake, server authorization guarantees that the server identity matches one of the service accounts specified by the client. Otherwise, the connection fails.

gRPC使用ALTS具有内置的服务器授权支持。使用ALTS的gRPC客户端可以在建立连接之前设置预期的服务器服务帐号。然后，在握手结束时，服务器授权保证服务器标识与客户端指定的服务帐号之一匹配。否则，连接将失败。

```go
import (
  "google.golang.org/grpc"
  "google.golang.org/grpc/credentials/alts"
)

clientOpts := alts.DefaultClientOptions()
clientOpts.TargetServiceAccounts = []string{expectedServerSA}
altsTC := alts.NewClientCreds(clientOpts)
conn, err := grpc.Dial(serverAddr, grpc.WithTransportCredentials(altsTC))
```

### Client Authorization 客户端授权

On a successful connection, the peer information (e.g., client’s service account) is stored in the [AltsContext](https://github.com/grpc/grpc/blob/master/src/proto/grpc/gcp/altscontext.proto). gRPC provides a utility library for client authorization check. Assuming that the server knows the expected client identity (e.g., `foo@iam.gserviceaccount.com`), it can run the following example codes to authorize the incoming RPC.

在成功建立连接后，对等方信息（例如，客户端的服务帐号）将存储在[AltsContext](https://github.com/grpc/grpc/blob/master/src/proto/grpc/gcp/altscontext.proto)中。gRPC提供了一个用于客户端授权检查的实用库。假设服务器知道预期的客户端身份（例如，`foo@iam.gserviceaccount.com`），它可以运行以下示例代码来对传入的RPC进行授权。

```go
import (
  "google.golang.org/grpc"
  "google.golang.org/grpc/credentials/alts"
)

err := alts.ClientAuthorizationCheck(ctx, []string{"foo@iam.gserviceaccount.com"})
```