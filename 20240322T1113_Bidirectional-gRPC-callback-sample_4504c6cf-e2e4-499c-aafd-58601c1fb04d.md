---
conversation_id: "4504c6cf-e2e4-499c-aafd-58601c1fb04d"
title: "Bidirectional gRPC callback sample"
create_time: 1711105992.457281
update_time: 1711106052.585801
language_guess: "en"
num_messages: 4
part_index: 1
part_count: 1
---

### system — 2024-03-22T11:13:12.457281+00:00

_(empty)_

### user — 2024-03-22T11:13:12.457792+00:00

.net6のgrpc でcallback を利用するサンプル

### assistant — 2024-03-22T11:14:11.387773+00:00

.NET 6でgRPCを使用してコールバックを実装する例を示します。gRPCでは「サーバー・ストリーミングRPC」や「クライアント・ストリーミングRPC」、「双方向ストリーミングRPC」を使用して、サーバーやクライアントからのコールバックのような動作を実現することができます。以下に双方向ストリーミングRPCを使用したサンプルを紹介します。

この例では、クライアントからサーバーへメッセージを送信し、サーバーからの応答を非同期で受け取る方法を示します。

### ステップ 1: gRPC サービスの定義

まず、`Protos/greet.proto`にサービス定義を書きます。

```protobuf
syntax = "proto3";

package greet;

// サービス定義
service Greeter {
  // 双方向ストリーミングRPC
  rpc BidirectionalHello (stream HelloRequest) returns (stream HelloReply);
}

// リクエストメッセージ
message HelloRequest {
  string name = 1;
}

// レスポンスメッセージ
message HelloReply {
  string message = 1;
}
```

### ステップ 2: サーバーの実装

サーバー側で`Greeter`サービスを実装します。`Services/GreeterService.cs`に以下のように記述します。

```csharp
using Grpc.Core;
using System.Threading.Tasks;
using greet;

public class GreeterService : Greeter.GreeterBase
{
    public override async Task BidirectionalHello(IAsyncStreamReader<HelloRequest> requestStream, IServerStreamWriter<HelloReply> responseStream, ServerCallContext context)
    {
        while (await requestStream.MoveNext())
        {
            var name = requestStream.Current.Name;
            await responseStream.WriteAsync(new HelloReply { Message = $"Hello {name}" });
        }
    }
}
```

### ステップ 3: クライアントの実装

クライアント側で双方向ストリーミングRPCを呼び出します。

```csharp
using Grpc.Net.Client;
using greet;
using System;
using System.Threading.Tasks;

class Program
{
    static async Task Main(string[] args)
    {
        using var channel = GrpcChannel.ForAddress("https://localhost:5001");
        var client = new Greeter.GreeterClient(channel);

        using var call = client.BidirectionalHello();

        var responseReaderTask = Task.Run(async () =>
        {
            await foreach (var reply in call.ResponseStream.ReadAllAsync())
            {
                Console.WriteLine("Received: " + reply.Message);
            }
        });

        for (int i = 0; i < 5; i++)
        {
            await call.RequestStream.WriteAsync(new HelloRequest { Name = "World" + i });
        }
        
        await call.RequestStream.CompleteAsync();
        await responseReaderTask;
    }
}
```

この例では、クライアントから5つのリクエストを送信し、サーバーからの応答をコンソールに出力しています。双方向ストリーミングを使用することで、サーバーとクライアントが非同期に通信を行い、一種のコールバックのような挙動を実現しています。
