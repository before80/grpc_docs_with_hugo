+++
title = "认证"
weight = 1
date = 2023-05-31T10:44:25+08:00
description = ""
isCJKLanguage = true
draft = false

+++

# Authentication 认证

https://grpc.io/docs/guides/auth/

An overview of gRPC authentication, including built-in auth mechanisms, and how to plug in your own authentication systems.

gRPC 认证概述，包括内置的认证机制以及如何插入自己的认证系统。



### Overview 概述

gRPC is designed to work with a variety of authentication mechanisms, making it easy to safely use gRPC to talk to other systems. You can use our supported mechanisms - SSL/TLS with or without Google token-based authentication - or you can plug in your own authentication system by extending our provided code.

gRPC 设计用于与各种认证机制配合工作，使得通过 gRPC 安全地与其他系统进行通信变得容易。您可以使用我们支持的机制 - SSL/TLS（可选使用 Google 基于令牌的认证） - 或者通过扩展我们提供的代码来插入自己的认证系统。

gRPC also provides a simple authentication API that lets you provide all the necessary authentication information as `Credentials` when creating a channel or making a call.

gRPC 还提供了一个简单的认证 API，允许您在创建通道或进行调用时提供所有必要的认证信息作为 `Credentials`。

### Supported auth mechanisms 支持的认证机制

The following authentication mechanisms are built-in to gRPC:

以下认证机制已内置到 gRPC 中：

- **SSL/TLS**: gRPC has SSL/TLS integration and promotes the use of SSL/TLS to authenticate the server, and to encrypt all the data exchanged between the client and the server. Optional mechanisms are available for clients to provide certificates for mutual authentication.
- **SSL/TLS**: gRPC 具有 SSL/TLS 集成，并推广使用 SSL/TLS 对服务器进行身份验证，并对客户端和服务器之间交换的所有数据进行加密。对于客户端提供证书以进行互相认证，可提供可选机制。
- **ALTS**: gRPC supports [ALTS](https://cloud.google.com/security/encryption-in-transit/application-layer-transport-security) as a transport security mechanism, if the application is running on [Google Cloud Platform (GCP)](https://cloud.google.com/). For details, see one of the following language-specific pages: [ALTS in C++](https://grpc.io/docs/languages/cpp/alts/), [ALTS in Go](https://grpc.io/docs/languages/go/alts/), [ALTS in Java](https://grpc.io/docs/languages/java/alts/), [ALTS in Python](https://grpc.io/docs/languages/python/alts/).
- **ALTS**: 如果应用程序在 [Google Cloud Platform (GCP)](https://cloud.google.com/) 上运行，gRPC 支持 [ALTS](https://cloud.google.com/security/encryption-in-transit/application-layer-transport-security) 作为传输安全机制。有关详细信息，请参阅以下特定语言的页面：[C++ 中的 ALTS](https://grpc.io/docs/languages/cpp/alts/)，[Go 中的 ALTS](https://grpc.io/docs/languages/go/alts/)，[Java 中的 ALTS](https://grpc.io/docs/languages/java/alts/)，[Python 中的 ALTS](https://grpc.io/docs/languages/python/alts/)。
- **Token-based authentication with Google**: gRPC provides a generic mechanism (described below) to attach metadata based credentials to requests and responses. Additional support for acquiring access tokens (typically OAuth2 tokens) while accessing Google APIs through gRPC is provided for certain auth flows: you can see how this works in our code examples below. In general this mechanism must be used *as well as* SSL/TLS on the channel - Google will not allow connections without SSL/TLS, and most gRPC language implementations will not let you send credentials on an unencrypted channel.
- **使用 Google 的基于令牌的身份验证**: gRPC 提供了一种通用机制（下文描述），用于将基于元数据的凭据附加到请求和响应中。在通过 gRPC 访问 Google API 时，还提供了获取访问令牌（通常是 OAuth2 令牌）的其他支持，您可以在下面的代码示例中查看其工作原理。通常情况下，此机制必须与通道上的 SSL/TLS 一起使用 - Google 不允许在没有 SSL/TLS 的情况下建立连接，大多数 gRPC 语言实现也不允许您在未加密的通道上发送凭据。

#### Warning 警告

Google credentials should only be used to connect to Google services. Sending a Google issued OAuth2 token to a non-Google service could result in this token being stolen and used to impersonate the client to Google services.

Google 凭据应仅用于连接到 Google 服务。将由 Google 发行的 OAuth2 令牌发送到非 Google 服务可能导致该令牌被窃取并用于冒充客户端访问 Google 服务。

### Authentication API 认证 API

gRPC provides a simple authentication API based around the unified concept of Credentials objects, which can be used when creating an entire gRPC channel or an individual call.

gRPC 提供了一个简单的认证 API，基于 Credentials 对象的统一概念，可以在创建整个 gRPC 通道或单个调用时使用。

#### Credential types 凭据类型

Credentials can be of two types:

凭据可以分为两种类型： 

- **Channel credentials**, which are attached to a `Channel`, such as SSL credentials.
- **Call credentials**, which are attached to a call (or `ClientContext` in C++).
- **通道凭据**，附加到 `Channel` 上的凭据，例如 SSL 凭据。
- **调用凭据**，附加到调用（或 C++ 中的 `ClientContext`）上的凭据。

You can also combine these in a `CompositeChannelCredentials`, allowing you to specify, for example, SSL details for the channel along with call credentials for each call made on the channel. A `CompositeChannelCredentials` associates a `ChannelCredentials` and a `CallCredentials` to create a new `ChannelCredentials`. The result will send the authentication data associated with the composed `CallCredentials` with every call made on the channel.

您还可以将它们组合在 `CompositeChannelCredentials` 中，允许您为通道指定 SSL 详细信息以及每个在通道上进行的调用的调用凭据，例如。`CompositeChannelCredentials` 将 `ChannelCredentials` 和 `CallCredentials` 关联起来，以创建新的 `ChannelCredentials`。结果将使用与组合的 `CallCredentials` 相关联的身份验证数据发送到通道上进行的每个调用。

For example, you could create a `ChannelCredentials` from an `SslCredentials` and an `AccessTokenCredentials`. The result when applied to a `Channel` would send the appropriate access token for each call on this channel.

例如，您可以使用 `SslCredentials` 和 `AccessTokenCredentials` 创建一个 `ChannelCredentials`。将其应用于通道时，结果将为该通道上的每个调用发送适当的访问令牌。

Individual `CallCredentials` can also be composed using `CompositeCallCredentials`. The resulting `CallCredentials` when used in a call will trigger the sending of the authentication data associated with the two `CallCredentials`.

还可以使用 `CompositeCallCredentials` 组合单独的 `CallCredentials`。在调用中使用生成的 `CallCredentials` 将触发与这两个 `CallCredentials` 相关联的身份验证数据的发送。

#### Using client-side SSL/TLS 使用客户端 SSL/TLS

Now let’s look at how `Credentials` work with one of our supported auth mechanisms. This is the simplest authentication scenario, where a client just wants to authenticate the server and encrypt all data. The example is in C++, but the API is similar for all languages: you can see how to enable SSL/TLS in more languages in our Examples section below.

现在让我们看一下 `Credentials` 如何与我们支持的一种认证机制配合工作。这是最简单的认证场景，其中客户端只想对服务器进行认证并加密所有数据。以下示例是用 C++ 编写的，但 API 在所有语言中的用法类似：您可以在下面的示例部分中查看如何在其他语言中启用 SSL/TLS。

```cpp
// Create a default SSL ChannelCredentials object. 创建一个默认的 SSL ChannelCredentials 对象。
auto channel_creds = grpc::SslCredentials(grpc::SslCredentialsOptions());
// Create a channel using the credentials created in the previous step. 使用前面创建的凭据创建一个通道。
auto channel = grpc::CreateChannel(server_name, channel_creds);
// Create a stub on the channel. 在通道上创建一个存根。
std::unique_ptr<Greeter::Stub> stub(Greeter::NewStub(channel));
// Make actual RPC calls on the stub. 在存根上进行实际的 RPC 调用。
grpc::Status s = stub->sayHello(&context, *request, response);
```

For advanced use cases such as modifying the root CA or using client certs, the corresponding options can be set in the `SslCredentialsOptions` parameter passed to the factory method.

对于诸如修改根 CA 或使用客户端证书之类的高级用例，可以在传递给工厂方法的 `SslCredentialsOptions` 参数中设置相应的选项。

#### Note 注意

Non-POSIX-compliant systems (such as Windows) need to specify the root certificates in `SslCredentialsOptions`, since the defaults are only configured for POSIX filesystems.

非 POSIX 兼容的系统（例如 Windows）需要在 `SslCredentialsOptions` 中指定根证书，因为默认值仅针对 POSIX 文件系统进行了配置。

#### Using Google token-based authentication 使用基于 Google 令牌的身份验证

gRPC applications can use a simple API to create a credential that works for authentication with Google in various deployment scenarios. Again, our example is in C++ but you can find examples in other languages in our Examples section.

gRPC 应用程序可以使用简单的 API 创建适用于在各种部署场景下与 Google 进行身份验证的凭据。以下示例再次以 C++ 为例，但您可以在我们的示例部分中找到其他语言的示例。

```cpp
auto creds = grpc::GoogleDefaultCredentials();
// Create a channel, stub and make RPC calls (same as in the previous example) 创建一个通道、存根并进行 RPC 调用（与前面的示例相同）
auto channel = grpc::CreateChannel(server_name, creds);
std::unique_ptr<Greeter::Stub> stub(Greeter::NewStub(channel));
grpc::Status s = stub->sayHello(&context, *request, response);
```

This channel credentials object works for applications using Service Accounts as well as for applications running in [Google Compute Engine (GCE)](https://cloud.google.com/compute/). In the former case, the service account’s private keys are loaded from the file named in the environment variable `GOOGLE_APPLICATION_CREDENTIALS`. The keys are used to generate bearer tokens that are attached to each outgoing RPC on the corresponding channel.

此通道凭据对象适用于使用服务账号以及在 [Google Compute Engine (GCE)](https://cloud.google.com/compute/) 上运行的应用程序。对于前一种情况，服务账号的私钥将从环境变量 `GOOGLE_APPLICATION_CREDENTIALS` 中指定的文件中加载。这些密钥用于生成附加到相应通道上的每个传出 RPC 的承载令牌。

For applications running in GCE, a default service account and corresponding OAuth2 scopes can be configured during VM setup. At run-time, this credential handles communication with the authentication systems to obtain OAuth2 access tokens and attaches them to each outgoing RPC on the corresponding channel.

对于在 GCE 上运行的应用程序，可以在虚拟机设置期间配置默认服务账号和相应的 OAuth2 范围。在运行时，该凭据与身份验证系统进行通信，获取 OAuth2 访问令牌，并将其附加到相应通道上的每个传出 RPC。

#### Extending gRPC to support other authentication mechanisms 扩展 gRPC 支持其他身份验证机制

The Credentials plugin API allows developers to plug in their own type of credentials. This consists of:

Credentials 插件 API 允许开发人员插入自己的凭据类型。这包括以下内容：

- The `MetadataCredentialsPlugin` abstract class, which contains the pure virtual `GetMetadata` method that needs to be implemented by a sub-class created by the developer.
- The `MetadataCredentialsFromPlugin` function, which creates a `CallCredentials` from the `MetadataCredentialsPlugin`.
- `MetadataCredentialsPlugin` 抽象类，其中包含由开发人员创建的子类需要实现的纯虚拟 `GetMetadata` 方法。
- `MetadataCredentialsFromPlugin` 函数，从 `MetadataCredentialsPlugin` 创建一个 `CallCredentials`。

Here is example of a simple credentials plugin which sets an authentication ticket in a custom header.

以下是一个简单的凭据插件示例，它在自定义标头中设置身份验证票据。

```cpp
class MyCustomAuthenticator : public grpc::MetadataCredentialsPlugin {
 public:
  MyCustomAuthenticator(const grpc::string& ticket) : ticket_(ticket) {}

  grpc::Status GetMetadata(
      grpc::string_ref service_url, grpc::string_ref method_name,
      const grpc::AuthContext& channel_auth_context,
      std::multimap<grpc::string, grpc::string>* metadata) override {
    metadata->insert(std::make_pair("x-custom-auth-ticket", ticket_));
    return grpc::Status::OK;
  }

 private:
  grpc::string ticket_;
};

auto call_creds = grpc::MetadataCredentialsFromPlugin(
    std::unique_ptr<grpc::MetadataCredentialsPlugin>(
        new MyCustomAuthenticator("super-secret-ticket")));
```

A deeper integration can be achieved by plugging in a gRPC credentials implementation at the core level. gRPC internals also allow switching out SSL/TLS with other encryption mechanisms.

通过在核心级别插入 gRPC 凭据实现，可以实现更深入的集成。gRPC 内部还允许将 SSL/TLS 替换为其他加密机制。

### Examples 示例

These authentication mechanisms will be available in all gRPC’s supported languages. The following sections demonstrate how authentication and authorization features described above appear in each language: more languages are coming soon.

这些身份验证机制将适用于所有 gRPC 支持的语言。以下部分展示了每种语言中上述身份验证和授权功能的示例：更多语言即将推出。

#### Go

##### Base case - no encryption or authentication 基本情况 - 无加密或身份验证

Client:

```go
conn, _ := grpc.Dial("localhost:50051", grpc.WithTransportCredentials(insecure.NewCredentials()))
// error handling omitted
client := pb.NewGreeterClient(conn)
// ...
```

Server:

```go
s := grpc.NewServer()
lis, _ := net.Listen("tcp", "localhost:50051")
// error handling omitted
s.Serve(lis)
```

##### With server authentication SSL/TLS 使用服务器身份验证 SSL/TLS

Client:

```go
creds, _ := credentials.NewClientTLSFromFile(certFile, "")
conn, _ := grpc.Dial("localhost:50051", grpc.WithTransportCredentials(creds))
// error handling omitted 省略错误处理
client := pb.NewGreeterClient(conn)
// ...
```

Server:

```go
creds, _ := credentials.NewServerTLSFromFile(certFile, keyFile)
s := grpc.NewServer(grpc.Creds(creds))
lis, _ := net.Listen("tcp", "localhost:50051")
// error handling omitted 省略错误处理
s.Serve(lis)
```

##### Authenticate with Google 使用 Google 进行身份验证

```go
pool, _ := x509.SystemCertPool()
// error handling omitted 省略错误处理
creds := credentials.NewClientTLSFromCert(pool, "")
perRPC, _ := oauth.NewServiceAccountFromFile("service-account.json", scope)
conn, _ := grpc.Dial(
	"greeter.googleapis.com",
	grpc.WithTransportCredentials(creds),
	grpc.WithPerRPCCredentials(perRPC),
)
// error handling omitted 省略错误处理
client := pb.NewGreeterClient(conn)
// ...
```

#### Ruby

##### Base case - no encryption or authentication 基本情况 - 无加密或身份验证

```ruby
stub = Helloworld::Greeter::Stub.new('localhost:50051', :this_channel_is_insecure)
...
```

##### With server authentication SSL/TLS 使用服务器身份验证 SSL/TLS

```ruby
creds = GRPC::Core::ChannelCredentials.new(load_certs)  # load_certs typically loads a CA roots file   - load_certs 通常加载 CA 根证书文件
stub = Helloworld::Greeter::Stub.new('myservice.example.com', creds)
```

##### Authenticate with Google 使用 Google 进行身份验证

```ruby
require 'googleauth'  # from http://www.rubydoc.info/gems/googleauth/0.1.0
...
ssl_creds = GRPC::Core::ChannelCredentials.new(load_certs)  # load_certs typically loads a CA roots file - load_certs 通常加载 CA 根证书文件
authentication = Google::Auth.get_application_default()
call_creds = GRPC::Core::CallCredentials.new(authentication.updater_proc)
combined_creds = ssl_creds.compose(call_creds)
stub = Helloworld::Greeter::Stub.new('greeter.googleapis.com', combined_creds)
```

#### C++

##### Base case - no encryption or authentication 基本情况 - 无加密或身份验证

```cpp
auto channel = grpc::CreateChannel("localhost:50051", InsecureChannelCredentials());
std::unique_ptr<Greeter::Stub> stub(Greeter::NewStub(channel));
...
```

##### With server authentication SSL/TLS 使用服务器身份验证 SSL/TLS

```cpp
auto channel_creds = grpc::SslCredentials(grpc::SslCredentialsOptions());
auto channel = grpc::CreateChannel("myservice.example.com", channel_creds);
std::unique_ptr<Greeter::Stub> stub(Greeter::NewStub(channel));
...
```

##### Authenticate with Google 使用 Google 进行身份验证

```cpp
auto creds = grpc::GoogleDefaultCredentials();
auto channel = grpc::CreateChannel("greeter.googleapis.com", creds);
std::unique_ptr<Greeter::Stub> stub(Greeter::NewStub(channel));
...
```

#### Python

##### Base case - No encryption or authentication 基本情况 - 无加密或身份验证

```python
import grpc
import helloworld_pb2

channel = grpc.insecure_channel('localhost:50051')
stub = helloworld_pb2.GreeterStub(channel)
```

##### With server authentication SSL/TLS 使用服务器身份验证 SSL/TLS

Client:

```python
import grpc
import helloworld_pb2

with open('roots.pem', 'rb') as f:
    creds = grpc.ssl_channel_credentials(f.read())
channel = grpc.secure_channel('myservice.example.com:443', creds)
stub = helloworld_pb2.GreeterStub(channel)
```

Server:

```python
import grpc
import helloworld_pb2
from concurrent import futures

server = grpc.server(futures.ThreadPoolExecutor(max_workers=10))
with open('key.pem', 'rb') as f:
    private_key = f.read()
with open('chain.pem', 'rb') as f:
    certificate_chain = f.read()
server_credentials = grpc.ssl_server_credentials( ( (private_key, certificate_chain), ) )
# Adding GreeterServicer to server omitted
server.add_secure_port('myservice.example.com:443', server_credentials)
server.start()
# Server sleep omitted
```

##### Authenticate with Google using a JWT 使用 Google 进行身份验证使用 JWT

```python
import grpc
import helloworld_pb2

from google import auth as google_auth
from google.auth import jwt as google_auth_jwt
from google.auth.transport import grpc as google_auth_transport_grpc

credentials, _ = google_auth.default()
jwt_creds = google_auth_jwt.OnDemandCredentials.from_signing_credentials(
    credentials)
channel = google_auth_transport_grpc.secure_authorized_channel(
    jwt_creds, None, 'greeter.googleapis.com:443')
stub = helloworld_pb2.GreeterStub(channel)
```

##### Authenticate with Google using an Oauth2 token 使用 Google 进行身份验证使用 OAuth2 令牌

```python
import grpc
import helloworld_pb2

from google import auth as google_auth
from google.auth.transport import grpc as google_auth_transport_grpc
from google.auth.transport import requests as google_auth_transport_requests

credentials, _ = google_auth.default(scopes=(scope,))
request = google_auth_transport_requests.Request()
channel = google_auth_transport_grpc.secure_authorized_channel(
    credentials, request, 'greeter.googleapis.com:443')
stub = helloworld_pb2.GreeterStub(channel)
```

##### With server authentication SSL/TLS and a custom header with token 使用服务器身份验证 SSL/TLS 和带有令牌的自定义标头

Client:

```python
import grpc
import helloworld_pb2

class GrpcAuth(grpc.AuthMetadataPlugin):
    def __init__(self, key):
        self._key = key

    def __call__(self, context, callback):
        callback((('rpc-auth-header', self._key),), None)

with open('path/to/root-cert', 'rb') as fh:
    root_cert = fh.read()

channel = grpc.secure_channel(
    'myservice.example.com:443',
    grpc.composite_channel_credentials(
        grpc.ssl_channel_credentials(root_cert),
        grpc.metadata_call_credentials(
            GrpcAuth('access_key')
        )
    )
)

stub = helloworld_pb2.GreeterStub(channel)
```

Server:

```python
from concurrent import futures

import grpc
import helloworld_pb2

class AuthInterceptor(grpc.ServerInterceptor):
    def __init__(self, key):
        self._valid_metadata = ('rpc-auth-header', key)

        def deny(_, context):
            context.abort(grpc.StatusCode.UNAUTHENTICATED, 'Invalid key')

        self._deny = grpc.unary_unary_rpc_method_handler(deny)

    def intercept_service(self, continuation, handler_call_details):
        meta = handler_call_details.invocation_metadata

        if meta and meta[0] == self._valid_metadata:
            return continuation(handler_call_details)
        else:
            return self._deny

server = grpc.server(
    futures.ThreadPoolExecutor(max_workers=10),
    interceptors=(AuthInterceptor('access_key'),)
)
with open('key.pem', 'rb') as f:
    private_key = f.read()
with open('chain.pem', 'rb') as f:
    certificate_chain = f.read()
server_credentials = grpc.ssl_server_credentials( ( (private_key, certificate_chain), ) )
# Adding GreeterServicer to server omitted
server.add_secure_port('myservice.example.com:443', server_credentials)
server.start()
# Server sleep omitted
```

#### Java

##### Base case - no encryption or authentication 基本情况 - 无加密或身份验证

```java
ManagedChannel channel = Grpc.newChannelBuilder(
        "localhost:50051", InsecureChannelCredentials.create())
    .build();
GreeterGrpc.GreeterStub stub = GreeterGrpc.newStub(channel);
```

##### With server authentication SSL/TLS 使用服务器身份验证 SSL/TLS

In Java we recommend that you use netty-tcnative with BoringSSL when using gRPC over TLS. You can find details about installing and using netty-tcnative and other required libraries for both Android and non-Android Java in the gRPC Java [Security](https://github.com/grpc/grpc-java/blob/master/SECURITY.md#transport-security-tls) documentation.

在 Java 中，我们建议您在使用 TLS 的 gRPC 时使用 netty-tcnative 和 BoringSSL。您可以在 gRPC Java [Security](https://github.com/grpc/grpc-java/blob/master/SECURITY.md#transport-security-tls) 文档中找到有关安装和使用 netty-tcnative 以及其他所需库的详细信息，适用于 Android 和非 Android Java。

To enable TLS on a server, a certificate chain and private key need to be specified in PEM format. Such private key should not be using a password. The order of certificates in the chain matters: more specifically, the certificate at the top has to be the host CA, while the one at the very bottom has to be the root CA. The standard TLS port is 443, but we use 8443 below to avoid needing extra permissions from the OS.

要在服务器上启用 TLS，需要以 PEM 格式指定证书链和私钥。此类私钥不应使用密码。证书链中证书的顺序很重要：具体来说，顶部的证书必须是主机 CA，而底部的证书必须是根 CA。标准的 TLS 端口是 443，但为了避免需要额外的操作系统权限，下面使用了 8443。

```java
ServerCredentials creds = TlsServerCredentials.create(certChainFile, privateKeyFile);
Server server = Grpc.newServerBuilderForPort(8443, creds)
    .addService(TestServiceGrpc.bindService(serviceImplementation))
    .build();
server.start();
```

If the issuing certificate authority is not known to the client then it can be configured using `TlsChannelCredentials.newBuilder()`.

如果客户端不知道颁发证书的机构，则可以使用 `TlsChannelCredentials.newBuilder()` 进行配置。

On the client side, server authentication with SSL/TLS looks like this:

在客户端上，使用 SSL/TLS 进行服务器身份验证的代码如下：

```java
// With server authentication SSL/TLS
ManagedChannel channel = Grpc.newChannelBuilder(
        "myservice.example.com:443", TlsChannelCredentials.create())
    .build();
GreeterGrpc.GreeterStub stub = GreeterGrpc.newStub(channel);

// With server authentication SSL/TLS; custom CA root certificates
ChannelCredentials creds = TlsChannelCredentials.newBuilder()
    .trustManager(new File("roots.pem"))
    .build();
ManagedChannel channel = Grpc.newChannelBuilder("myservice.example.com:443", creds)
    .build();
GreeterGrpc.GreeterStub stub = GreeterGrpc.newStub(channel);
```

##### Authenticate with Google 使用 Google 进行身份验证

The following code snippet shows how you can call the [Google Cloud PubSub API](https://cloud.google.com/pubsub/overview) using gRPC with a service account. The credentials are loaded from a key stored in a well-known location or by detecting that the application is running in an environment that can provide one automatically, e.g. Google Compute Engine. While this example is specific to Google and its services, similar patterns can be followed for other service providers.

以下代码片段显示了如何使用 gRPC 调用 [Google Cloud PubSub API](https://cloud.google.com/pubsub/overview)，并使用服务帐号进行身份验证。凭据从存储在众所周知的位置的密钥加载，或者通过检测应用程序在可以自动提供凭据的环境中运行（例如 Google Compute Engine）进行加载。尽管此示例特定于 Google 及其服务，但可以针对其他服务提供商采用类似的模式。

```java
ChannelCredentials creds = CompositeChannelCredentials.create(
    TlsChannelCredentials.create(),
    MoreCallCredentials.from(GoogleCredentials.getApplicationDefault()));
ManagedChannel channel = ManagedChannelBuilder.forTarget("greeter.googleapis.com", creds)
    .build();
GreeterGrpc.GreeterStub stub = GreeterGrpc.newStub(channel);
```

#### Node.js

##### Base case - No encryption/authentication 基本情况 - 无加密/身份验证

```js
var stub = new helloworld.Greeter('localhost:50051', grpc.credentials.createInsecure());
```

##### With server authentication SSL/TLS  使用服务器身份验证 SSL/TLS

```js
const root_cert = fs.readFileSync('path/to/root-cert');
const ssl_creds = grpc.credentials.createSsl(root_cert);
const stub = new helloworld.Greeter('myservice.example.com', ssl_creds);
```

##### Authenticate with Google 使用 Google 进行身份验证

```js
// Authenticating with Google 使用 Google 进行身份验证
var GoogleAuth = require('google-auth-library'); // from https://www.npmjs.com/package/google-auth-library
...
var ssl_creds = grpc.credentials.createSsl(root_certs);
(new GoogleAuth()).getApplicationDefault(function(err, auth) {
  var call_creds = grpc.credentials.createFromGoogleCredential(auth);
  var combined_creds = grpc.credentials.combineChannelCredentials(ssl_creds, call_creds);
  var stub = new helloworld.Greeter('greeter.googleapis.com', combined_credentials);
});
```

##### Authenticate with Google using Oauth2 token (legacy approach) 使用 OAuth2 令牌对 Google 进行身份验证（传统方法）

```js
var GoogleAuth = require('google-auth-library'); // from https://www.npmjs.com/package/google-auth-library
...
var ssl_creds = grpc.Credentials.createSsl(root_certs); // load_certs typically loads a CA roots file -load_certs 通常加载一个 CA 根证书文件
var scope = 'https://www.googleapis.com/auth/grpc-testing';
(new GoogleAuth()).getApplicationDefault(function(err, auth) {
  if (auth.createScopeRequired()) {
    auth = auth.createScoped(scope);
  }
  var call_creds = grpc.credentials.createFromGoogleCredential(auth);
  var combined_creds = grpc.credentials.combineChannelCredentials(ssl_creds, call_creds);
  var stub = new helloworld.Greeter('greeter.googleapis.com', combined_credentials);
});
```

##### With server authentication SSL/TLS and a custom header with token 使用服务器身份验证 SSL/TLS 和带有令牌的自定义标头

```js
const rootCert = fs.readFileSync('path/to/root-cert');
const channelCreds = grpc.credentials.createSsl(rootCert);
const metaCallback = (_params, callback) => {
    const meta = new grpc.Metadata();
    meta.add('custom-auth-header', 'token');
    callback(null, meta);
}
const callCreds = grpc.credentials.createFromMetadataGenerator(metaCallback);
const combCreds = grpc.credentials.combineChannelCredentials(channelCreds, callCreds);
const stub = new helloworld.Greeter('myservice.example.com', combCreds);
```

#### PHP

##### Base case - No encryption/authorization 基本情况 - 无加密/授权

```php
$client = new helloworld\GreeterClient('localhost:50051', [
    'credentials' => Grpc\ChannelCredentials::createInsecure(),
]);
```

##### With server authentication SSL/TLS 使用服务器身份验证 SSL/TLS

```php
$client = new helloworld\GreeterClient('myservice.example.com', [
    'credentials' => Grpc\ChannelCredentials::createSsl(file_get_contents('roots.pem')),
]);
```

##### Authenticate with Google 使用 Google 进行身份验证

```php
function updateAuthMetadataCallback($context)
{
    $auth_credentials = ApplicationDefaultCredentials::getCredentials();
    return $auth_credentials->updateMetadata($metadata = [], $context->service_url);
}
$channel_credentials = Grpc\ChannelCredentials::createComposite(
    Grpc\ChannelCredentials::createSsl(file_get_contents('roots.pem')),
    Grpc\CallCredentials::createFromPlugin('updateAuthMetadataCallback')
);
$opts = [
  'credentials' => $channel_credentials
];
$client = new helloworld\GreeterClient('greeter.googleapis.com', $opts);
```

##### Authenticate with Google using Oauth2 token (legacy approach) 使用 Google 进行身份验证，使用 OAuth2 令牌（传统方法）

```php
// the environment variable "GOOGLE_APPLICATION_CREDENTIALS" needs to be set
$scope = "https://www.googleapis.com/auth/grpc-testing";
$auth = Google\Auth\ApplicationDefaultCredentials::getCredentials($scope);
$opts = [
  'credentials' => Grpc\Credentials::createSsl(file_get_contents('roots.pem'));
  'update_metadata' => $auth->getUpdateMetadataFunc(),
];
$client = new helloworld\GreeterClient('greeter.googleapis.com', $opts);
```

#### Dart

##### Base case - no encryption or authentication 使用 Google 进行身份验证，使用 OAuth2 令牌（传统方法）

```dart
final channel = new ClientChannel('localhost',
      port: 50051,
      options: const ChannelOptions(
          credentials: const ChannelCredentials.insecure()));
final stub = new GreeterClient(channel);
```

##### With server authentication SSL/TLS 使用服务器身份验证 SSL/TLS

```dart
// Load a custom roots file. 加载自定义的根证书文件。
final trustedRoot = new File('roots.pem').readAsBytesSync();
final channelCredentials =
    new ChannelCredentials.secure(certificates: trustedRoot);
final channelOptions = new ChannelOptions(credentials: channelCredentials);
final channel = new ClientChannel('myservice.example.com',
    options: channelOptions);
final client = new GreeterClient(channel);
```

##### Authenticate with Google 使用 Google 进行身份验证

```dart
// Uses publicly trusted roots by default. 默认情况下使用公开信任的根证书。
final channel = new ClientChannel('greeter.googleapis.com');
final serviceAccountJson =
     new File('service-account.json').readAsStringSync();
final credentials = new JwtServiceAccountAuthenticator(serviceAccountJson);
final client =
    new GreeterClient(channel, options: credentials.toCallOptions);
```

##### Authenticate a single RPC call 对单个 RPC 调用进行身份验证

```dart
// Uses publicly trusted roots by default. 默认情况下使用公开信任的根证书。
final channel = new ClientChannel('greeter.googleapis.com');
final client = new GreeterClient(channel);
...
final serviceAccountJson =
     new File('service-account.json').readAsStringSync();
final credentials = new JwtServiceAccountAuthenticator(serviceAccountJson);
final response =
    await client.sayHello(request, options: credentials.toCallOptions);
```