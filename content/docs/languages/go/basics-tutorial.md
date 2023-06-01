+++
title = "基础教程"
weight = 2
date = 2023-05-31T10:41:26+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Basics tutorial - 基础教程

https://grpc.io/docs/languages/go/basics/

​	这是关于在 Go 中使用 gRPC 的基础教程。

​	本教程为Go程序员提供了使用gRPC的基础介绍。 

​	通过完成这个示例，您将学会如何：

- 在 `.proto` 文件中定义一个服务。
- 使用协议缓冲区编译器生成服务端和客户端代码。
- 使用 Go gRPC API 为您的服务编写一个简单的客户端和服务端。

​	本教程假设您已经阅读了[gRPC 简介]({{< ref "/docs/what_is_grpc/introduction">}})并熟悉[protocol buffers（协议缓冲区）](https://protobuf.dev/overview)。请注意，本教程中的示例使用的是协议缓冲区语言的**proto3**版本：您可以在[proto3语言指南](https://protobuf.dev/programming-guides/proto3)和[Go生成代码指南](https://protobuf.dev/reference/go/go-generated)中了解更多信息。

### 为什么使用gRPC？

​	我们的示例是一个简单的路由映射应用，它允许客户端获取有关其路由上的特定信息，进而创建这些路由摘要，并让服务端和其他客户端交换路由信息（如路由更新）。

​	使用gRPC，我们可以在一个`.proto`文件中定义我们的服务，并在gRPC支持的任何语言中生成客户端和服务端，这些客户端和服务端可以在各种环境中运行，从大型数据中心的服务器到您自己的平板电脑，gRPC会为不同语言和环境之间的通信复杂性提供支持。我们还可以获得使用协议缓冲区的所有优势，包括高效的序列化、简单的[IDL](https://zh.wikipedia.org/wiki/IDL%E8%AF%AD%E8%A8%80)（Interactive Data Language 交互式数据语言）和易于更新的接口。

### 准备

​	您应该已经安装了生成客户端和服务端接口代码所需的工具 —— 如果尚未安装，请参阅[快速入门]({{< ref "/docs/languages/go/quick-start">}})中的[先决条件]({{< ref "/docs/languages/go/quick-start#先决条件">}})章节的安装说明。

### 获取示例代码

​	该示例代码是[grpc-go](https://github.com/grpc/grpc-go)存储库的一部分。

1. [下载该存储库的zip文件](https://github.com/grpc/grpc-go/archive/v1.55.0.zip)并解压，或者克隆存储库：

   ```sh
   $ git clone -b v1.55.0 --depth 1 https://github.com/grpc/grpc-go
   ```

2. 切换到该示例目录：

   ```sh
   $ cd grpc-go/examples/route_guide
   ```


### 定义服务

​	我们的第一步（正如您从[gRPC 简介]({{< ref "/docs/what_is_grpc/introduction">}})中了解到的）是使用[protocol buffers](https://protobuf.dev/overview)定义gRPC的*服务（service）*以及方法的*请求（request）*和*响应（response）*类型。有关完整的`.proto`文件，请参见[routeguide/route_guide.proto](https://github.com/grpc/grpc-go/blob/master/examples/route_guide/routeguide/route_guide.proto)。

​	要定义一个服务（service），请在您的`.proto`文件中指定一个命名的`service`：

```proto
service RouteGuide {
   ...
}
```

​	然后，在服务（service ）定义内部定义一些`rpc`方法，指定其请求（request ）和响应（response ）类型。gRPC允许您定义四种类型的服务（service ）方法，所有这些方法都可在该`RouteGuide`服务（service ）中使用：

- *简单的RPC（simple RPC）*，其中客户端使用存根（stub ）发送请求到服务端并等待响应返回，就像普通的函数调用一样。

  ```proto
  // 获取给定位置的 feature 。
  rpc GetFeature(Point) returns (Feature) {}
  ```

- *服务端流式RPC（server-side streaming RPC）*，其中的客户端向其服务端发送请求并获得一个流以读取一系列返回的消息。该客户端从返回的流中读取，直到没有更多的消息为止。如我们的示例所示，通过在*响应（response）*类型之前放置`stream`关键字来指定服务端流式方法（server-side streaming method）。

  ```proto
  // Obtains the Features available within the given Rectangle.  Results are
  // streamed rather than returned at once (e.g. in a response message with a
  // repeated field), as the rectangle may cover a large area and contain a
  // huge number of features.
  // 获取给定矩形范围内的可用 Features 。
  // 结果以流式方式传输，而不是一次性返回（例如在带有重复(repeated)字段的响应消息中），
  // 因为该矩形可能涵盖了一个大范围并包含大量 features 。
  rpc ListFeatures(Rectangle) returns (stream Feature) {}
  ```

- *客户端流式RPC（client-side streaming RPC）*，其中的客户端写入一系列消息并将它们发送到其服务端，再次使用提供的流。该客户端完成写入消息后，等待其服务端读取所有消息并返回其响应。通过在*请求（request）*类型之前放置`stream`关键字来指定客户端流式方法（client-side streaming method）。

  ```proto
  // Accepts a stream of Points on a route being traversed, returning a
  // RouteSummary when traversal is completed.
  // 在遍历 route 时，接受一系列 Points 的流，当遍历完成时返回一个RouteSummary。
  rpc RecordRoute(stream Point) returns 
  (RouteSummary) {}
  ```

- *双向流式RPC（bidirectional streaming RPC）*，双方都使用读写流（read-write stream）发送一系列消息。这两个流操作是独立的，因此其客户端们（clients，这里怎么翻译比较合适）和服务端们（servers，这里怎么翻译比较合适）可以按照任意顺序读取和写入：例如，服务端可以在写入响应之前等待接收所有客户端消息，或者它可以交替读取消息然后写入消息，或者其他读取和写入的组合。每个流中消息的顺序保持不变。通过在*请求（request ）*和*响应（response）*之前放置`stream`关键字来指定这种类型的方法。

  ```proto
  // Accepts a stream of RouteNotes sent while a route is being traversed,
  // while receiving other RouteNotes (e.g. from other users).
  // 在遍历 route 时接收一系列发送的 RouteNote，同时接收其他 RouteNote（例如来自其他用户）。
  rpc RouteChat(stream RouteNote) returns (stream RouteNote) {}
  ```

​	我们的`.proto`文件还包含用于服务方法（service methods）中使用的所有请求和响应类型的**protocol buffer消息类型定义** —— 例如，这是`Point`消息类型的定义：

```proto
// Points are represented as latitude-longitude pairs in the E7 representation
// (degrees multiplied by 10**7 and rounded to the nearest integer).
// Latitudes should be in the range +/- 90 degrees and longitude should be in
// the range +/- 180 degrees (inclusive).
// Points 用E7表示法表示为纬度-经度对（度乘以10**7并四舍五入到最接近的整数）。
// 纬度（latitudes）应在+/- 90度范围内，经度（longitude）应在+/- 180度范围内（包括边界）。
message Point {
  int32 latitude = 1;
  int32 longitude = 2;
}
```

### 生成客户端和服务端代码

​	接下来，我们需要从`.proto`服务定义中生成gRPC客户端和服务端接口。我们使用带有特殊gRPC Go插件的protocol buffer编译器`protoc`来实现这一点。这类似于我们在[快速入门]({{< ref "/docs/languages/go/quick-start">}})中所做的。

​	在`examples/route_guide`目录中运行以下命令：

```sh
$ protoc --go_out=. --go_opt=paths=source_relative \
    --go-grpc_out=. --go-grpc_opt=paths=source_relative \
    routeguide/route_guide.proto
```

​	运行此命令将在[routeguide](https://github.com/grpc/grpc-go/blob/master/examples/route_guide/routeguide)目录中生成以下文件：

- `route_guide.pb.go`，其中包含用于填充（populate）、序列化（serialize）和检索（retrieve ）请求和响应消息类型的所有protocol buffer代码。
- `route_guide_grpc.pb.go`，其中包含以下内容： 
  - 一个接口类型（或*存根（stub）*），供客户端调用，其中定义了`RouteGuide`服务中的方法。
  - 一个接口类型，供服务端实现，其中同样定义了`RouteGuide`服务中的方法。

### 创建服务端

​	首先让我们看看如何创建`RouteGuide`服务端。如果您只对创建gRPC客户端感兴趣，可以跳过本节，直接阅读[创建客户端](#创建客户端)（当然您可能还是会觉得有趣！）。

​	使我们的`RouteGuide`服务发挥作用有两个部分（parts）工作要做：

- 实现从我们的服务定义生成的服务接口：它是执行我们的服务的实际"工作（work）"。
- 运行gRPC服务端以侦听来自客户端的请求并将其分派给正确的服务实现。

​	您可以在[server/server.go](https://github.com/grpc/grpc-go/tree/master/examples/route_guide/server/server.go)中找到我们的示例`RouteGuide`服务端。让我们更详细地看看它是如何工作的。

#### 实现RouteGuide

​	正如您所看到的，我们的服务端有一个`routeGuideServer`结构类型，实现了生成的`RouteGuideServer`接口：

```go
type routeGuideServer struct {
        ...
}
...

func (s *routeGuideServer) GetFeature(ctx context.Context, point *pb.Point) (*pb.Feature, error) {
        ...
}
...

func (s *routeGuideServer) ListFeatures(rect *pb.Rectangle, stream pb.RouteGuide_ListFeaturesServer) error {
        ...
}
...

func (s *routeGuideServer) RecordRoute(stream pb.RouteGuide_RecordRouteServer) error {
        ...
}
...

func (s *routeGuideServer) RouteChat(stream pb.RouteGuide_RouteChatServer) error {
        ...
}
...
```

##### 简单RPC

​	该`routeGuideServer`实现了我们所有的服务方法。让我们先看最简单的类型，`GetFeature`，它只是从客户端获取一个`Point`，并从其数据库中（以`Feature`的形式）返回对应的feature信息。

```go
func (s *routeGuideServer) GetFeature(ctx context.Context, point *pb.Point) (*pb.Feature, error) {
  for _, feature := range s.savedFeatures {
    if proto.Equal(feature.Location, point) {
      return feature, nil
    }
  }
  // 未找到feature，返回一个未命名feature
  return &pb.Feature{Location: point}, nil
}
```

​	该方法接收一个用于RPC的上下文对象和客户端的`Point`协议缓冲区请求。它返回一个带有响应信息的`Feature`协议缓冲区对象和一个`error`。在该方法中，我们使用适当的信息填充`Feature`，然后将其与`nil`错误一起`return`，告诉gRPC我们已经完成了对该RPC的处理，并且该`Feature`可以返回给客户端。

##### 服务端流式 RPC

​	现在让我们来看一个流式 RPC 的例子。`ListFeatures` 是一个服务端流式 RPC，因此我们需要向客户端发送多个 `Feature`。

```go
func (s *routeGuideServer) ListFeatures(rect *pb.Rectangle, stream pb.RouteGuide_ListFeaturesServer) error {
  for _, feature := range s.savedFeatures {
    if inRange(feature.Location, rect) {
      if err := stream.Send(feature); err != nil {
        return err
      }
    }
  }
  return nil
}
```

​	如您所见，与在我们的方法参数中获得简单的请求和响应对象不同，这次我们获得了一个请求对象（客户端希望在其中找到`Feature`的`Rectangle`）和一个特殊的`RouteGuide_ListFeaturesServer`对象来编写我们的响应。

​	在这个方法中，我们填充了我们需要返回的许多`Feature`对象，并使用`RouteGuide_ListFeaturesServer`的`Send()`方法将它们写入。最后，就像在我们简单的RPC中一样，我们返回一个`nil`错误，告诉gRPC我们已经完成了响应的编写。如果在此调用中发生任何错误，我们将返回一个非`nil`错误；gRPC层将把它（即非`nil`错误）转换为适当的RPC状态，以发送到网络上。

##### 客户端流式 RPC

​	现在让我们看一些稍微复杂一点的东西：客户端流式方法 `RecordRoute`，我们从客户端获取一系列的 `Point`，并返回一个包含有关他们行程信息的单个 `RouteSummary`。如您所见，这次该方法根本没有请求参数。相反，它获取了一个 `RouteGuide_RecordRouteServer` 流，服务端可以使用该流来读取和写入消息 —— 它可以使用其 `Recv()` 方法接收客户端消息，并使用其 `SendAndClose()` 方法返回单个响应。

```go
func (s *routeGuideServer) RecordRoute(stream pb.RouteGuide_RecordRouteServer) error {
  var pointCount, featureCount, distance int32
  var lastPoint *pb.Point
  startTime := time.Now()
  for {
    point, err := stream.Recv()
    if err == io.EOF {
      endTime := time.Now()
      return stream.SendAndClose(&pb.RouteSummary{
        PointCount:   pointCount,
        FeatureCount: featureCount,
        Distance:     distance,
        ElapsedTime:  int32(endTime.Sub(startTime).Seconds()),
      })
    }
    if err != nil {
      return err
    }
    pointCount++
    for _, feature := range s.savedFeatures {
      if proto.Equal(feature.Location, point) {
        featureCount++
      }
    }
    if lastPoint != nil {
      distance += calcDistance(lastPoint, point)
    }
    lastPoint = point
  }
}
```

​	在该方法体中，我们使用 `RouteGuide_RecordRouteServer` 的 `Recv()` 方法重复地将客户端的请求读取到一个请求对象（在本例中为 `Point`），直到没有更多的消息为止：服务端需要在每次调用后检查从 `Recv()` 返回的错误。如果该错误是 `nil`，则流仍然有效，可以继续读取；如果是 `io.EOF`，则消息流已结束，服务端可以返回其 `RouteSummary`。如果它有任何其他值，我们将原样返回该错误，以便由 gRPC 层将其转换为 RPC 状态。

##### 双向流式 RPC

​	最后，让我们来看一下双向流式 RPC `RouteChat()`。

```go
func (s *routeGuideServer) RouteChat(stream pb.RouteGuide_RouteChatServer) error {
  for {
    in, err := stream.Recv()
    if err == io.EOF {
      return nil
    }
    if err != nil {
      return err
    }
    key := serialize(in.Location)
                ... // look for notes to be sent to client 查找要发送给客户端的注释
    for _, note := range s.routeNotes[key] {
      if err := stream.Send(note); err != nil {
        return err
      }
    }
  }
}
```

​	这次我们获取一个 `RouteGuide_RouteChatServer` 流，就像在客户端流式示例中一样，它可以用于读取和写入消息。但是，这次我们通过方法的流返回值，而客户端仍然在向他们的消息流中写入消息。

​	在这里，读取和写入的语法与我们的客户端流式方法非常相似，只是服务端使用流的 `Send()` 方法而不是 `SendAndClose()`，因为它需要写入多个响应。尽管每一方始终会按照写入的顺序接收到对方的消息，但客户端和服务端都可以按任何顺序读取和写入 —— 这些流操作完全独立。

#### 启动服务端

​	一旦我们实现了所有的方法，我们还需要启动一个 gRPC 服务端，以便客户端可以真正使用我们的服务。下面的代码片段展示了我们如何为我们的 `RouteGuide` 服务做到这一点：

```go
flag.Parse()
lis, err := net.Listen("tcp", fmt.Sprintf("localhost:%d", *port))
if err != nil {
  log.Fatalf("failed to listen: %v", err)
}
var opts []grpc.ServerOption
...
grpcServer := grpc.NewServer(opts...)
pb.RegisterRouteGuideServer(grpcServer, newServer())
grpcServer.Serve(lis)
```

​	要构建和启动服务端，我们需要：

1. 通过 `lis, err := net.Listen(...)` 指定要用于侦听客户端请求的端口。
6. 使用 `grpc.NewServer(...)` 创建一个 gRPC 服务端的实例。
7. 将我们的服务实现注册到 gRPC 服务端（the gRPC server，怎么翻译？暂且翻译为gRPC服务端吧）中。
8. 使用我们的端口详细信息调用服务端的 `Serve()` 方法，以进行阻塞等待，直到其进程被终止或调用了 `Stop()`。

### 创建客户端

​	在本节中，我们将介绍如何为我们的 `RouteGuide` 服务创建一个 Go 客户端。您可以在 [grpc-go/examples/route_guide/client/client.go](https://github.com/grpc/grpc-go/tree/master/examples/route_guide/client/client.go) 中查看我们完整的示例客户端代码。

#### 创建存根

​	要调用服务方法，我们首先需要创建一个 gRPC *通道（channel）*，用于与服务端进行通信。我们通过将服务端地址和端口号传递给 `grpc.Dial()` 来创建通道，代码如下所示：

```go
var opts []grpc.DialOption
...
conn, err := grpc.Dial(*serverAddr, opts...)
if err != nil {
  ...
}
defer conn.Close()
```

​	当服务需要认证凭据（例如，TLS、GCE 凭据或 JWT 凭据）时，您可以使用 `DialOptions` 在 `grpc.Dial` 中设置这些认证凭据。`RouteGuide` 服务不需要任何凭据。

​	一旦设置了 gRPC *通道（channel）*，我们就需要一个客户端 *存根（stub）* 来执行 RPC 调用。我们可以使用从示例 `.proto` 文件生成的 `pb` 包提供的 `NewRouteGuideClient` 方法来获取它（即*存根（stub）*）。

```go
client := pb.NewRouteGuideClient(conn)
```

#### 调用服务方法

​	现在让我们来看一下如何调用我们的服务方法。请注意，在 gRPC-Go 中，RPC 在阻塞/同步模式下运行，这意味着 RPC 调用会等待服务端响应，并且要么返回响应，要么返回错误。

##### 简单 RPC

​	调用简单 RPC `GetFeature` 几乎与调用本地方法一样简单。

```go
feature, err := client.GetFeature(context.Background(), &pb.Point{409146138, -746188906})
if err != nil {
  ...
}
```

​	如您所见，我们在之前获取的存根上调用了该方法。在我们的方法参数中，我们创建并填充了一个请求协议缓冲区对象（在本例中是 `Point`）。我们还传递了一个 `context.Context` 对象，它允许我们在需要时更改 RPC 的行为，比如超时/取消正在进行的 RPC。如果该调用没有返回错误，那么我们可以从第一个返回值中读取来自服务端的响应信息。

```go
log.Println(feature)
```

##### 服务端流式 RPC

​	接下来是调用服务端流式方法 `ListFeatures`，它返回一系列地理（geographical ） `Feature` 流。如果您已经阅读过[创建服务端](#创建服务端)的内容，这其中一些内容可能会非常熟悉 —— 这两者都以类似的方式实现了流式RPC。

```go
rect := &pb.Rectangle{ ... }  // initialize a pb.Rectangle
stream, err := client.ListFeatures(context.Background(), rect)
if err != nil {
  ...
}
for {
    feature, err := stream.Recv()
    if err == io.EOF {
        break
    }
    if err != nil {
        log.Fatalf("%v.ListFeatures(_) = _, %v", client, err)
    }
    log.Println(feature)
}
```

​	与简单的 RPC 类似，我们将上下文和请求传递给该方法。但是，我们不会收到一个响应对象，而是会收到一个`RouteGuide_ListFeaturesClient`的实例。客户端可以使用 `RouteGuide_ListFeaturesClient` 流来读取服务端的响应。

​	我们使用`RouteGuide_ListFeaturesClient`的`Recv()`方法重复读取服务端的响应到一个响应协议缓冲区对象（在本例中为`Feature`）中，直到没有更多的消息为止：客户端需要在每次调用后检查`Recv()`返回的错误`err`。如果是 `nil`，则流仍然有效，可以继续读取；如果是 `io.EOF`，则消息流已经结束；否则，必定存在一个RPC错误，该错误通过`err`传递。

##### 客户端流式 RPC

​	客户端流式方法 `RecordRoute` 与服务端方法类似，只是我们只传递上下文，并获得一个 `RouteGuide_RecordRouteClient` 流，我们用它来同时写入和读取消息。

```go
// Create a random number of random points 创建随机数量的随机点
r := rand.New(rand.NewSource(time.Now().UnixNano()))
pointCount := int(r.Int31n(100)) + 2 // Traverse at least two points 至少遍历两个点
var points []*pb.Point
for i := 0; i < pointCount; i++ {
  points = append(points, randomPoint(r))
}
log.Printf("Traversing %d points.", len(points))
stream, err := client.RecordRoute(context.Background())
if err != nil {
  log.Fatalf("%v.RecordRoute(_) = _, %v", client, err)
}
for _, point := range points {
  if err := stream.Send(point); err != nil {
    log.Fatalf("%v.Send(%v) = %v", stream, point, err)
  }
}
reply, err := stream.CloseAndRecv()
if err != nil {
  log.Fatalf("%v.CloseAndRecv() got error %v, want %v", stream, err, nil)
}
log.Printf("Route summary: %v", reply)
```

​	`RouteGuide_RecordRouteClient` 有一个 `Send()` 方法，我们可以使用它向服务端发送请求。当使用 `Send()` 将客户端的请求写入流中后，我们需要在流上调用 `CloseAndRecv()`，以告知 gRPC 我们已经完成写入并期望接收响应。我们从 `CloseAndRecv()` 返回的 `err` 中获取 RPC 的状态。如果状态是 `nil`，那么 `CloseAndRecv()` 的第一个返回值将是一个有效的服务端响应。

##### 双向流式 RPC

​	最后，让我们看一下双向流式 RPC `RouteChat()`。与 `RecordRoute` 类似，我们只传递上下文对象给该方法，并返回一个流，我们可以使用它来同时写入和读取消息。但是，这次我们通过方法的流返回值，而服务端仍然在向 *它们的* 消息流写入消息。

```go
stream, err := client.RouteChat(context.Background())
waitc := make(chan struct{})
go func() {
  for {
    in, err := stream.Recv()
    if err == io.EOF {
      // read done.
      close(waitc)
      return
    }
    if err != nil {
      log.Fatalf("Failed to receive a note : %v", err)
    }
    log.Printf("Got message %s at point(%d, %d)", in.Message, in.Location.Latitude, in.Location.Longitude)
  }
}()
for _, note := range notes {
  if err := stream.Send(note); err != nil {
    log.Fatalf("Failed to send a note: %v", err)
  }
}
stream.CloseSend()
<-waitc
```

​	在这里，读取和写入的语法与我们的客户端流式方法非常相似，只是在调用完成后，我们使用流的 `CloseSend()` 方法。尽管每一方始终按照写入的顺序获取对方的消息，但客户端和服务端都可以按任意顺序读取和写入 —— 流操作完全独立。

### 试一试！

​	在 `examples/route_guide` 目录执行以下命令：

1. 运行服务端：

   ```sh
   $ go run server/server.go
   ```

2. 在另一个终端中运行客户端：

   ```sh
   $ go run client/client.go
   ```

​	你将看到类似以下的输出：

```nocode
Getting feature for point (409146138, -746188906)
name:"Berkshire Valley Management Area Trail, Jefferson, NJ, USA" location:<latitude:409146138 longitude:-746188906 >
Getting feature for point (0, 0)
location:<>
Looking for features within lo:<latitude:400000000 longitude:-750000000 > hi:<latitude:420000000 longitude:-730000000 >
name:"Patriots Path, Mendham, NJ 07945, USA" location:<latitude:407838351 longitude:-746143763 >
...
name:"3 Hasta Way, Newton, NJ 07860, USA" location:<latitude:410248224 longitude:-747127767 >
Traversing 56 points.
Route summary: point_count:56 distance:497013163
Got message First message at point(0, 1)
Got message Second message at point(0, 2)
Got message Third message at point(0, 3)
Got message First message at point(0, 1)
Got message Fourth message at point(0, 1)
Got message Second message at point(0, 2)
Got message Fifth message at point(0, 2)
Got message Third message at point(0, 3)
Got message Sixth message at point(0, 3)
```

#### 注意

​	我们在本页面展示的客户端和服务端跟踪输出中省略了时间戳。