---
conversation_id: "df6aa67c-2780-465b-8e93-48fcf5a3f51b"
title: "Kestrel gRPC Streaming Sample"
create_time: 1711586294.089958
update_time: 1711586339.629519
language_guess: "en"
num_messages: 4
part_index: 1
part_count: 1
---

### system — 2024-03-28T00:38:14.089958+00:00

_(empty)_

### user — 2024-03-28T00:38:14.090655+00:00

C# kestrel grpc streaming sample

### assistant — 2024-03-28T00:38:58.919335+00:00

To create a gRPC streaming service using Kestrel in C#, you generally need to follow these steps: define your gRPC service in a `.proto` file, implement the service in C#, and then configure Kestrel to host the service. Here's a simple example that demonstrates these steps for both server-side and client-side streaming.

### Step 1: Define the gRPC Service in a .proto File

First, define your gRPC service and messages in a Protocol Buffer (`.proto`) file. This example includes both server streaming and client streaming.

```proto
syntax = "proto3";

option csharp_namespace = "GrpcStreamingSample";

// The greeting service definition.
service Greeter {
  // Server streaming RPC
  rpc SayHelloServerStreaming (HelloRequest) returns (stream HelloReply);
  // Client streaming RPC
  rpc SayHelloClientStreaming (stream HelloRequest) returns (HelloReply);
}

// The request message containing the user's name.
message HelloRequest {
  string name = 1;
}

// The response message containing the greetings.
message HelloReply {
  string message = 1;
}
```

### Step 2: Implement the gRPC Service in C#

Implement your service by inheriting from the base class generated from your `.proto` file. Here's how you might implement both server streaming and client streaming methods.

```csharp
using Grpc.Core;
using GrpcStreamingSample; // Generated from the .proto file
using System.Threading.Tasks;

public class GreeterService : Greeter.GreeterBase
{
    // Server streaming example
    public override async Task SayHelloServerStreaming(HelloRequest request, IServerStreamWriter<HelloReply> responseStream, ServerCallContext context)
    {
        for (int i = 0; i < 5; i++)
        {
            await responseStream.WriteAsync(new HelloReply { Message = "Hello " + request.Name });
            await Task.Delay(1000); // Simulate work
        }
    }

    // Client streaming example
    public override async Task<HelloReply> SayHelloClientStreaming(IAsyncStreamReader<HelloRequest> requestStream, ServerCallContext context)
    {
        while (await requestStream.MoveNext())
        {
            var message = requestStream.Current.Name;
            // Process message
        }
        
        return new HelloReply { Message = "Messages received." };
    }
}
```

### Step 3: Configure Kestrel to Host the gRPC Service

Finally, configure Kestrel in your `Program.cs` or `Startup.cs` to host the gRPC service.

```csharp
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.DependencyInjection;

public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.ConfigureServices(services =>
                {
                    services.AddGrpc(); // Add gRPC services
                });
                webBuilder.Configure(app =>
                {
                    app.UseRouting();

                    app.UseEndpoints(endpoints =>
                    {
                        endpoints.MapGrpcService<GreeterService>(); // Map the GreeterService
                    });
                });
            });
}
```

### Client Implementation

On the client side, you'll use the stubs generated from the `.proto` file to make gRPC calls. Here's a simple example of how a client might interact with the server streaming method:

```csharp
using var channel = GrpcChannel.ForAddress("https://localhost:5001");
var client = new Greeter.GreeterClient(channel);

using var call = client.SayHelloServerStreaming(new HelloRequest { Name = "World" });

await foreach (var reply in call.ResponseStream.ReadAllAsync())
{
    Console.WriteLine("Greeting: " + reply.Message);
}
```

This example should give you a solid starting point for implementing gRPC streaming services using Kestrel in C#. Remember, you need the gRPC NuGet packages (`Grpc`, `Grpc.Tools`, `Google.Protobuf`, and `Grpc.AspNetCore`) for both the server and client projects.
