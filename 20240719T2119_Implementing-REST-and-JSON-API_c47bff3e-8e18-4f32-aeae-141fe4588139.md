---
conversation_id: "c47bff3e-8e18-4f32-aeae-141fe4588139"
title: "Implementing REST and JSON API"
create_time: 1721423941.937947
update_time: 1721424478.554971
language_guess: "en"
num_messages: 21
part_index: 1
part_count: 1
---

### system — 2024-07-19T21:19:01.937947+00:00

_(empty)_

### user — 2024-07-19T21:19:01.943325+00:00

.net8を前提として以下のサンプルを提示
・WebAPIを実装する
・処理内容は同じだが、I/FとしてRESTとjsonを提供する
・RESTとjsonのswaggerを提供する

### assistant — 2024-07-19T21:19:27.231630+00:00

_(empty)_

### assistant — 2024-07-19T21:19:27.231715+00:00

.NET 8でWeb APIを実装し、RESTとJSONの両方のインターフェースを提供し、それぞれのSwaggerを提供するサンプルコードを以下に示します。

### プロジェクトの作成

まず、新しいASP.NET Core Web APIプロジェクトを作成します。

```sh
dotnet new webapi -n SampleApi
cd SampleApi
```

### 必要なパッケージのインストール

以下のパッケージをインストールします。

```sh
dotnet add package Swashbuckle.AspNetCore
```

### `Program.cs` の設定

次に、`Program.cs` ファイルを編集してSwaggerの設定を追加します。

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new() { Title = "REST API", Version = "v1" });
    c.SwaggerDoc("v2", new() { Title = "JSON API", Version = "v2" });
});

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "REST API v1");
        c.SwaggerEndpoint("/swagger/v2/swagger.json", "JSON API v2");
    });
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

### コントローラーの作成

`Controllers` フォルダーに新しいコントローラーを追加します。

#### `RestController.cs`

```csharp
using Microsoft.AspNetCore.Mvc;

namespace SampleApi.Controllers
{
    [ApiController]
    [Route("api/v1/[controller]")]
    public class RestController : ControllerBase
    {
        [HttpGet]
        public IActionResult Get()
        {
            return Ok(new { Message = "This is the REST API" });
        }
    }
}
```

#### `JsonController.cs`

```csharp
using Microsoft.AspNetCore.Mvc;

namespace SampleApi.Controllers
{
    [ApiController]
    [Route("api/v2/[controller]")]
    public class JsonController : ControllerBase
    {
        [HttpPost]
        public IActionResult Post([FromBody] object data)
        {
            return Ok(new { Message = "This is the JSON API", Data = data });
        }
    }
}
```

### `launchSettings.json` の設定

開発環境でアプリを起動するために、`Properties` フォルダー内の `launchSettings.json` を編集します。

```json
{
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "https": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "https://localhost:5001",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

### アプリケーションの実行

次に、アプリケーションを実行します。

```sh
dotnet run
```

ブラウザで `https://localhost:5001/swagger` にアクセスすると、REST APIとJSON APIのSwaggerドキュメントが表示されるはずです。

### テスト

REST APIエンドポイント（GETリクエスト）:
```
https://localhost:5001/api/v1/rest
```

JSON APIエンドポイント（POSTリクエスト）:
```
https://localhost:5001/api/v2/json
```

以上の手順で、.NET 8を使用してRESTとJSONの両方のインターフェースを提供するWeb APIを実装し、それぞれのSwaggerドキュメントを提供することができます。

### user — 2024-07-19T21:19:58.272074+00:00

この実装では処理が共通化されていないため別案を提示

### assistant — 2024-07-19T21:20:21.728843+00:00

共通のビジネスロジックを利用するようにして、RESTとJSONのインターフェースを提供するアプローチに変更しましょう。共通のサービスクラスを作成し、各コントローラーでそのサービスを使用することで処理を共通化します。

### プロジェクトの作成とパッケージのインストール

```sh
dotnet new webapi -n SampleApi
cd SampleApi
dotnet add package Swashbuckle.AspNetCore
```

### `Program.cs` の設定

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new() { Title = "REST API", Version = "v1" });
    c.SwaggerDoc("v2", new() { Title = "JSON API", Version = "v2" });
});

// Register the service
builder.Services.AddScoped<IMyService, MyService>();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "REST API v1");
        c.SwaggerEndpoint("/swagger/v2/swagger.json", "JSON API v2");
    });
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();

public interface IMyService
{
    string ProcessRequest();
}

public class MyService : IMyService
{
    public string ProcessRequest()
    {
        return "This is the shared logic response.";
    }
}
```

### コントローラーの作成

`Controllers` フォルダーに新しいコントローラーを追加します。

#### `RestController.cs`

```csharp
using Microsoft.AspNetCore.Mvc;

namespace SampleApi.Controllers
{
    [ApiController]
    [Route("api/v1/[controller]")]
    public class RestController : ControllerBase
    {
        private readonly IMyService _myService;

        public RestController(IMyService myService)
        {
            _myService = myService;
        }

        [HttpGet]
        public IActionResult Get()
        {
            var response = _myService.ProcessRequest();
            return Ok(new { Message = response });
        }
    }
}
```

#### `JsonController.cs`

```csharp
using Microsoft.AspNetCore.Mvc;

namespace SampleApi.Controllers
{
    [ApiController]
    [Route("api/v2/[controller]")]
    public class JsonController : ControllerBase
    {
        private readonly IMyService _myService;

        public JsonController(IMyService myService)
        {
            _myService = myService;
        }

        [HttpPost]
        public IActionResult Post([FromBody] object data)
        {
            var response = _myService.ProcessRequest();
            return Ok(new { Message = response, Data = data });
        }
    }
}
```

### `launchSettings.json` の設定

```json
{
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "https": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "https://localhost:5001",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

### アプリケーションの実行

```sh
dotnet run
```

ブラウザで `https://localhost:5001/swagger` にアクセスすると、REST APIとJSON APIのSwaggerドキュメントが表示されるはずです。

### テスト

REST APIエンドポイント（GETリクエスト）:
```
https://localhost:5001/api/v1/rest
```

JSON APIエンドポイント（POSTリクエスト）:
```
https://localhost:5001/api/v2/json
```

この実装では、`MyService` クラスに共通のビジネスロジックを配置し、それを各コントローラーで利用するようにしています。これにより、処理が共通化され、コードの重複を避けることができます。

### user — 2024-07-19T21:20:46.079667+00:00

同じcontrollerを使用して実装する

### assistant — 2024-07-19T21:21:05.494445+00:00

同じコントローラーを使用して、RESTとJSONのインターフェースを提供する方法を示します。これを実現するために、HTTPメソッドとエンドポイントのルーティングを使い分けます。

### プロジェクトの作成とパッケージのインストール

```sh
dotnet new webapi -n SampleApi
cd SampleApi
dotnet add package Swashbuckle.AspNetCore
```

### `Program.cs` の設定

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new() { Title = "REST API", Version = "v1" });
    c.SwaggerDoc("v2", new() { Title = "JSON API", Version = "v2" });
});

// Register the service
builder.Services.AddScoped<IMyService, MyService>();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "REST API v1");
        c.SwaggerEndpoint("/swagger/v2/swagger.json", "JSON API v2");
    });
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();

public interface IMyService
{
    string ProcessRequest();
}

public class MyService : IMyService
{
    public string ProcessRequest()
    {
        return "This is the shared logic response.";
    }
}
```

### コントローラーの作成

`Controllers` フォルダーに新しいコントローラーを追加します。

#### `MyController.cs`

```csharp
using Microsoft.AspNetCore.Mvc;

namespace SampleApi.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class MyController : ControllerBase
    {
        private readonly IMyService _myService;

        public MyController(IMyService myService)
        {
            _myService = myService;
        }

        // REST APIエンドポイント
        [HttpGet]
        [Route("v1/rest")]
        public IActionResult GetRest()
        {
            var response = _myService.ProcessRequest();
            return Ok(new { Message = response });
        }

        // JSON APIエンドポイント
        [HttpPost]
        [Route("v2/json")]
        public IActionResult PostJson([FromBody] object data)
        {
            var response = _myService.ProcessRequest();
            return Ok(new { Message = response, Data = data });
        }
    }
}
```

### `launchSettings.json` の設定

```json
{
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "https": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "https://localhost:5001",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

### アプリケーションの実行

```sh
dotnet run
```

ブラウザで `https://localhost:5001/swagger` にアクセスすると、REST APIとJSON APIのSwaggerドキュメントが表示されるはずです。

### テスト

REST APIエンドポイント（GETリクエスト）:
```
https://localhost:5001/api/my/v1/rest
```

JSON APIエンドポイント（POSTリクエスト）:
```
https://localhost:5001/api/my/v2/json
```

この実装では、同じコントローラー `MyController` を使用して、異なるエンドポイントとHTTPメソッドによってRESTとJSONの両方のインターフェースを提供しています。これにより、コードの重複を避けながら、単一のコントローラーで複数のインターフェースを管理できます。

### user — 2024-07-19T21:21:33.450554+00:00

APIはすべてPostで処理を行うものとする

### assistant — 2024-07-19T21:22:00.099915+00:00

すべてのAPIリクエストをPOSTメソッドで処理し、RESTとJSONの両方のインターフェースを提供する方法を以下に示します。この場合も、共通のビジネスロジックを持つサービスを使用して処理を共通化します。

### プロジェクトの作成とパッケージのインストール

```sh
dotnet new webapi -n SampleApi
cd SampleApi
dotnet add package Swashbuckle.AspNetCore
```

### `Program.cs` の設定

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new() { Title = "REST API", Version = "v1" });
    c.SwaggerDoc("v2", new() { Title = "JSON API", Version = "v2" });
});

// Register the service
builder.Services.AddScoped<IMyService, MyService>();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "REST API v1");
        c.SwaggerEndpoint("/swagger/v2/swagger.json", "JSON API v2");
    });
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();

public interface IMyService
{
    string ProcessRequest();
}

public class MyService : IMyService
{
    public string ProcessRequest()
    {
        return "This is the shared logic response.";
    }
}
```

### コントローラーの作成

`Controllers` フォルダーに新しいコントローラーを追加します。

#### `MyController.cs`

```csharp
using Microsoft.AspNetCore.Mvc;

namespace SampleApi.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class MyController : ControllerBase
    {
        private readonly IMyService _myService;

        public MyController(IMyService myService)
        {
            _myService = myService;
        }

        // REST APIエンドポイント
        [HttpPost]
        [Route("v1/rest")]
        public IActionResult PostRest([FromBody] object data)
        {
            var response = _myService.ProcessRequest();
            return Ok(new { Message = "This is the REST API response", Data = data, Response = response });
        }

        // JSON APIエンドポイント
        [HttpPost]
        [Route("v2/json")]
        public IActionResult PostJson([FromBody] object data)
        {
            var response = _myService.ProcessRequest();
            return Ok(new { Message = "This is the JSON API response", Data = data, Response = response });
        }
    }
}
```

### `launchSettings.json` の設定

```json
{
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "https": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "https://localhost:5001",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

### アプリケーションの実行

```sh
dotnet run
```

ブラウザで `https://localhost:5001/swagger` にアクセスすると、REST APIとJSON APIのSwaggerドキュメントが表示されるはずです。

### テスト

REST APIエンドポイント（POSTリクエスト）:
```
https://localhost:5001/api/my/v1/rest
```

JSON APIエンドポイント（POSTリクエスト）:
```
https://localhost:5001/api/my/v2/json
```

この実装では、単一のコントローラー `MyController` を使用して、異なるルート (`v1/rest` および `v2/json`) によってRESTとJSONの両方のインターフェースを提供し、POSTメソッドで処理を行います。共通のビジネスロジックは `MyService` クラスに配置されています。

### user — 2024-07-19T21:22:52.446128+00:00

Attributeを利用して処理を共通化する

### assistant — 2024-07-19T21:23:16.672867+00:00

属性（Attribute）を使用して、処理を共通化する方法を以下に示します。この方法では、カスタム属性を作成し、アクションメソッドに共通の処理を適用します。

### プロジェクトの作成とパッケージのインストール

```sh
dotnet new webapi -n SampleApi
cd SampleApi
dotnet add package Swashbuckle.AspNetCore
```

### カスタム属性の作成

まず、共通の処理を行うカスタム属性を作成します。

#### `Attributes/CustomProcessingAttribute.cs`

```csharp
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.Filters;

namespace SampleApi.Attributes
{
    public class CustomProcessingAttribute : ActionFilterAttribute
    {
        public override void OnActionExecuting(ActionExecutingContext context)
        {
            var service = (IMyService)context.HttpContext.RequestServices.GetService(typeof(IMyService));
            var response = service.ProcessRequest();
            context.HttpContext.Items["ProcessedResponse"] = response;
            base.OnActionExecuting(context);
        }
    }
}
```

### ビジネスロジックのサービスを作成

次に、ビジネスロジックを含むサービスを作成します。

#### `Services/MyService.cs`

```csharp
namespace SampleApi
{
    public interface IMyService
    {
        string ProcessRequest();
    }

    public class MyService : IMyService
    {
        public string ProcessRequest()
        {
            return "This is the shared logic response.";
        }
    }
}
```

### `Program.cs` の設定

`Program.cs` ファイルを設定して、サービスとSwaggerを登録します。

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using SampleApi;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new() { Title = "REST API", Version = "v1" });
    c.SwaggerDoc("v2", new() { Title = "JSON API", Version = "v2" });
});

// Register the service
builder.Services.AddScoped<IMyService, MyService>();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "REST API v1");
        c.SwaggerEndpoint("/swagger/v2/swagger.json", "JSON API v2");
    });
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

### コントローラーの作成

次に、コントローラーを作成し、カスタム属性を使用して共通処理を適用します。

#### `Controllers/MyController.cs`

```csharp
using Microsoft.AspNetCore.Mvc;
using SampleApi.Attributes;

namespace SampleApi.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class MyController : ControllerBase
    {
        // REST APIエンドポイント
        [HttpPost]
        [Route("v1/rest")]
        [CustomProcessing]
        public IActionResult PostRest([FromBody] object data)
        {
            var response = HttpContext.Items["ProcessedResponse"];
            return Ok(new { Message = "This is the REST API response", Data = data, Response = response });
        }

        // JSON APIエンドポイント
        [HttpPost]
        [Route("v2/json")]
        [CustomProcessing]
        public IActionResult PostJson([FromBody] object data)
        {
            var response = HttpContext.Items["ProcessedResponse"];
            return Ok(new { Message = "This is the JSON API response", Data = data, Response = response });
        }
    }
}
```

### `launchSettings.json` の設定

```json
{
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "https": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "https://localhost:5001",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

### アプリケーションの実行

```sh
dotnet run
```

ブラウザで `https://localhost:5001/swagger` にアクセスすると、REST APIとJSON APIのSwaggerドキュメントが表示されるはずです。

### テスト

REST APIエンドポイント（POSTリクエスト）:
```
https://localhost:5001/api/my/v1/rest
```

JSON APIエンドポイント（POSTリクエスト）:
```
https://localhost:5001/api/my/v2/json
```

この実装では、`CustomProcessingAttribute` を使用して共通のビジネスロジックを適用し、各アクションメソッドでその結果を使用しています。これにより、コードの重複を避けつつ、共通の処理を一箇所に集約することができます。

### user — 2024-07-19T21:23:47.065859+00:00

AttributeにはRouting要素を追加し、v1はrest,v2はjson形式とする

### assistant — 2024-07-19T21:24:18.267886+00:00

カスタム属性にルーティング要素を追加し、`v1` は REST、`v2` は JSON 形式とする方法を示します。この場合、カスタム属性のコンストラクターでルーティングを受け取り、その情報に基づいて処理を分岐します。

### カスタム属性の作成

まず、ルーティング要素を含むカスタム属性を作成します。

#### `Attributes/CustomProcessingAttribute.cs`

```csharp
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.Filters;

namespace SampleApi.Attributes
{
    public enum ApiVersion
    {
        V1,
        V2
    }

    public class CustomProcessingAttribute : ActionFilterAttribute
    {
        private readonly ApiVersion _apiVersion;

        public CustomProcessingAttribute(ApiVersion apiVersion)
        {
            _apiVersion = apiVersion;
        }

        public override void OnActionExecuting(ActionExecutingContext context)
        {
            var service = (IMyService)context.HttpContext.RequestServices.GetService(typeof(IMyService));
            var response = service.ProcessRequest();

            if (_apiVersion == ApiVersion.V1)
            {
                context.HttpContext.Items["ProcessedResponse"] = new { Message = "This is the REST API response", Response = response };
            }
            else if (_apiVersion == ApiVersion.V2)
            {
                context.HttpContext.Items["ProcessedResponse"] = new { Message = "This is the JSON API response", Response = response };
            }

            base.OnActionExecuting(context);
        }
    }
}
```

### ビジネスロジックのサービスを作成

次に、ビジネスロジックを含むサービスを作成します。

#### `Services/MyService.cs`

```csharp
namespace SampleApi
{
    public interface IMyService
    {
        string ProcessRequest();
    }

    public class MyService : IMyService
    {
        public string ProcessRequest()
        {
            return "This is the shared logic response.";
        }
    }
}
```

### `Program.cs` の設定

`Program.cs` ファイルを設定して、サービスとSwaggerを登録します。

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using SampleApi;
using SampleApi.Attributes;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new() { Title = "REST API", Version = "v1" });
    c.SwaggerDoc("v2", new() { Title = "JSON API", Version = "v2" });
});

// Register the service
builder.Services.AddScoped<IMyService, MyService>();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "REST API v1");
        c.SwaggerEndpoint("/swagger/v2/swagger.json", "JSON API v2");
    });
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

### コントローラーの作成

次に、コントローラーを作成し、カスタム属性を使用して共通処理を適用します。

#### `Controllers/MyController.cs`

```csharp
using Microsoft.AspNetCore.Mvc;
using SampleApi.Attributes;

namespace SampleApi.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class MyController : ControllerBase
    {
        // REST APIエンドポイント
        [HttpPost]
        [Route("v1/rest")]
        [CustomProcessing(ApiVersion.V1)]
        public IActionResult PostRest([FromBody] object data)
        {
            var response = HttpContext.Items["ProcessedResponse"];
            return Ok(new { Data = data, response });
        }

        // JSON APIエンドポイント
        [HttpPost]
        [Route("v2/json")]
        [CustomProcessing(ApiVersion.V2)]
        public IActionResult PostJson([FromBody] object data)
        {
            var response = HttpContext.Items["ProcessedResponse"];
            return Ok(new { Data = data, response });
        }
    }
}
```

### `launchSettings.json` の設定

```json
{
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "https": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "https://localhost:5001",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

### アプリケーションの実行

```sh
dotnet run
```

ブラウザで `https://localhost:5001/swagger` にアクセスすると、REST APIとJSON APIのSwaggerドキュメントが表示されるはずです。

### テスト

REST APIエンドポイント（POSTリクエスト）:
```
https://localhost:5001/api/my/v1/rest
```

JSON APIエンドポイント（POSTリクエスト）:
```
https://localhost:5001/api/my/v2/json
```

この実装では、`CustomProcessingAttribute` を使用して共通のビジネスロジックを適用し、各アクションメソッドでその結果を使用しています。属性にはルーティング要素が追加され、`v1` ではREST形式、`v2` ではJSON形式のレスポンスを返します。

### user — 2024-07-19T21:24:57.237774+00:00

PostRest,PostJsonを一つのI/Fで表現する

### assistant — 2024-07-19T21:25:22.841648+00:00

`PostRest` と `PostJson` のエンドポイントを統合し、1つのインターフェースで表現する方法を示します。エンドポイントごとに異なるルートと属性を使用して、バージョンに基づいて処理を分岐させます。

### カスタム属性の作成

ルーティング要素を含むカスタム属性を作成します。

#### `Attributes/CustomProcessingAttribute.cs`

```csharp
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.Filters;

namespace SampleApi.Attributes
{
    public enum ApiVersion
    {
        V1,
        V2
    }

    public class CustomProcessingAttribute : ActionFilterAttribute
    {
        private readonly ApiVersion _apiVersion;

        public CustomProcessingAttribute(ApiVersion apiVersion)
        {
            _apiVersion = apiVersion;
        }

        public override void OnActionExecuting(ActionExecutingContext context)
        {
            var service = (IMyService)context.HttpContext.RequestServices.GetService(typeof(IMyService));
            var response = service.ProcessRequest();

            if (_apiVersion == ApiVersion.V1)
            {
                context.HttpContext.Items["ProcessedResponse"] = new { Message = "This is the REST API response", Response = response };
            }
            else if (_apiVersion == ApiVersion.V2)
            {
                context.HttpContext.Items["ProcessedResponse"] = new { Message = "This is the JSON API response", Response = response };
            }

            base.OnActionExecuting(context);
        }
    }
}
```

### ビジネスロジックのサービスを作成

次に、ビジネスロジックを含むサービスを作成します。

#### `Services/MyService.cs`

```csharp
namespace SampleApi
{
    public interface IMyService
    {
        string ProcessRequest();
    }

    public class MyService : IMyService
    {
        public string ProcessRequest()
        {
            return "This is the shared logic response.";
        }
    }
}
```

### `Program.cs` の設定

`Program.cs` ファイルを設定して、サービスとSwaggerを登録します。

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using SampleApi;
using SampleApi.Attributes;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new() { Title = "REST API", Version = "v1" });
    c.SwaggerDoc("v2", new() { Title = "JSON API", Version = "v2" });
});

// Register the service
builder.Services.AddScoped<IMyService, MyService>();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "REST API v1");
        c.SwaggerEndpoint("/swagger/v2/swagger.json", "JSON API v2");
    });
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

### コントローラーの作成

次に、単一のエンドポイントを作成し、カスタム属性を使用して処理を分岐させます。

#### `Controllers/MyController.cs`

```csharp
using Microsoft.AspNetCore.Mvc;
using SampleApi.Attributes;

namespace SampleApi.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class MyController : ControllerBase
    {
        // 共通エンドポイント
        [HttpPost]
        [Route("process")]
        public IActionResult PostProcess([FromQuery] ApiVersion version, [FromBody] object data)
        {
            var service = (IMyService)HttpContext.RequestServices.GetService(typeof(IMyService));
            var response = service.ProcessRequest();

            if (version == ApiVersion.V1)
            {
                return Ok(new { Message = "This is the REST API response", Data = data, Response = response });
            }
            else if (version == ApiVersion.V2)
            {
                return Ok(new { Message = "This is the JSON API response", Data = data, Response = response });
            }

            return BadRequest(new { Message = "Invalid API version" });
        }
    }
}
```

### `launchSettings.json` の設定

```json
{
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "https": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "https://localhost:5001",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

### アプリケーションの実行

```sh
dotnet run
```

ブラウザで `https://localhost:5001/swagger` にアクセスすると、REST APIとJSON APIのSwaggerドキュメントが表示されるはずです。

### テスト

共通のエンドポイント（POSTリクエスト）:
```
https://localhost:5001/api/my/process?version=V1
https://localhost:5001/api/my/process?version=V2
```

この実装では、単一のエンドポイント `PostProcess` を使用して、クエリパラメーター `version` に基づいて処理を分岐させています。`version` が `V1` の場合はREST形式、`version` が `V2` の場合はJSON形式のレスポンスを返します。これにより、1つのインターフェースで複数のAPIバージョンを処理できます。

### user — 2024-07-19T21:26:20.800062+00:00

returnの処理が分岐しているため、共通化する

### assistant — 2024-07-19T21:26:45.480673+00:00

共通化されたreturn処理を持つように、単一のエンドポイントで処理を行い、APIバージョンに基づいてレスポンスのフォーマットを動的に変更します。以下はその実装例です。

### カスタム属性の作成

まず、ルーティング要素を含むカスタム属性を作成します。

#### `Attributes/CustomProcessingAttribute.cs`

```csharp
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.Filters;

namespace SampleApi.Attributes
{
    public enum ApiVersion
    {
        V1,
        V2
    }

    public class CustomProcessingAttribute : ActionFilterAttribute
    {
        private readonly ApiVersion _apiVersion;

        public CustomProcessingAttribute(ApiVersion apiVersion)
        {
            _apiVersion = apiVersion;
        }

        public override void OnActionExecuting(ActionExecutingContext context)
        {
            var service = (IMyService)context.HttpContext.RequestServices.GetService(typeof(IMyService));
            var response = service.ProcessRequest();

            if (_apiVersion == ApiVersion.V1)
            {
                context.HttpContext.Items["ProcessedResponse"] = new { Message = "This is the REST API response", Response = response };
            }
            else if (_apiVersion == ApiVersion.V2)
            {
                context.HttpContext.Items["ProcessedResponse"] = new { Message = "This is the JSON API response", Response = response };
            }

            base.OnActionExecuting(context);
        }
    }
}
```

### ビジネスロジックのサービスを作成

次に、ビジネスロジックを含むサービスを作成します。

#### `Services/MyService.cs`

```csharp
namespace SampleApi
{
    public interface IMyService
    {
        string ProcessRequest();
    }

    public class MyService : IMyService
    {
        public string ProcessRequest()
        {
            return "This is the shared logic response.";
        }
    }
}
```

### `Program.cs` の設定

`Program.cs` ファイルを設定して、サービスとSwaggerを登録します。

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using SampleApi;
using SampleApi.Attributes;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new() { Title = "REST API", Version = "v1" });
    c.SwaggerDoc("v2", new() { Title = "JSON API", Version = "v2" });
});

// Register the service
builder.Services.AddScoped<IMyService, MyService>();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "REST API v1");
        c.SwaggerEndpoint("/swagger/v2/swagger.json", "JSON API v2");
    });
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

### コントローラーの作成

次に、単一のエンドポイントを作成し、カスタム属性を使用して処理を分岐させます。

#### `Controllers/MyController.cs`

```csharp
using Microsoft.AspNetCore.Mvc;
using SampleApi.Attributes;

namespace SampleApi.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class MyController : ControllerBase
    {
        // 共通エンドポイント
        [HttpPost]
        [Route("process")]
        [CustomProcessing(ApiVersion.V1)]
        [CustomProcessing(ApiVersion.V2)]
        public IActionResult PostProcess([FromQuery] ApiVersion version, [FromBody] object data)
        {
            var response = HttpContext.Items["ProcessedResponse"];
            return Ok(new { Data = data, response });
        }
    }
}
```

### `launchSettings.json` の設定

```json
{
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "https": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "https://localhost:5001",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

### アプリケーションの実行

```sh
dotnet run
```

ブラウザで `https://localhost:5001/swagger` にアクセスすると、REST APIとJSON APIのSwaggerドキュメントが表示されるはずです。

### テスト

共通のエンドポイント（POSTリクエスト）:
```
https://localhost:5001/api/my/process?version=V1
https://localhost:5001/api/my/process?version=V2
```

この実装では、単一のエンドポイント `PostProcess` を使用して、クエリパラメーター `version` に基づいて処理を分岐させています。`version` が `V1` の場合はREST形式、`version` が `V2` の場合はJSON形式のレスポンスを返します。これにより、1つのインターフェースで複数のAPIバージョンを処理し、共通化されたreturn処理を実現しています。

### user — 2024-07-19T21:27:33.150483+00:00

これをswaggerで表示するとどのようになるのか

### assistant — 2024-07-19T21:27:58.015014+00:00

Swaggerで表示する場合、エンドポイントが一つなので、単一のエンドポイントに対して複数のバージョンがあるようには見えません。しかし、クエリパラメーターを使ってAPIのバージョンを指定する方法をSwaggerに明示することはできます。

以下は、実装されたエンドポイントがSwagger UIでどのように表示されるかのイメージと、それを正しく表示させるためのコードです。

### `Program.cs` の設定

まず、Swaggerの設定を追加します。

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using SampleApi;
using SampleApi.Attributes;
using Microsoft.OpenApi.Models;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new OpenApiInfo { Title = "Sample API", Version = "v1" });
    c.SwaggerDoc("v2", new OpenApiInfo { Title = "Sample API", Version = "v2" });

    c.DocInclusionPredicate((version, desc) =>
    {
        if (desc.RelativePath.Contains("v1"))
            return version == "v1";
        else if (desc.RelativePath.Contains("v2"))
            return version == "v2";
        return false;
    });

    c.OperationFilter<RemoveVersionFromParameter>();
    c.DocumentFilter<ReplaceVersionWithExactValueInPath>();
});

// Register the service
builder.Services.AddScoped<IMyService, MyService>();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "Sample API v1");
        c.SwaggerEndpoint("/swagger/v2/swagger.json", "Sample API v2");
    });
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

### Swagger用のフィルターの作成

Swaggerでクエリパラメーターを使ってバージョンを表示するためにフィルターを作成します。

#### `Swagger/RemoveVersionFromParameter.cs`

```csharp
using Microsoft.OpenApi.Models;
using Swashbuckle.AspNetCore.SwaggerGen;

public class RemoveVersionFromParameter : IOperationFilter
{
    public void Apply(OpenApiOperation operation, OperationFilterContext context)
    {
        var versionParameter = operation.Parameters.SingleOrDefault(p => p.Name == "version");
        if (versionParameter != null)
        {
            operation.Parameters.Remove(versionParameter);
        }
    }
}
```

#### `Swagger/ReplaceVersionWithExactValueInPath.cs`

```csharp
using Microsoft.OpenApi.Models;
using Swashbuckle.AspNetCore.SwaggerGen;

public class ReplaceVersionWithExactValueInPath : IDocumentFilter
{
    public void Apply(OpenApiDocument swaggerDoc, DocumentFilterContext context)
    {
        var paths = new OpenApiPaths();
        foreach (var (key, value) in swaggerDoc.Paths)
        {
            paths.Add(key.Replace("{version}", swaggerDoc.Info.Version), value);
        }
        swaggerDoc.Paths = paths;
    }
}
```

### コントローラーの作成

次に、単一のエンドポイントを作成し、カスタム属性を使用して処理を分岐させます。

#### `Controllers/MyController.cs`

```csharp
using Microsoft.AspNetCore.Mvc;
using SampleApi.Attributes;

namespace SampleApi.Controllers
{
    [ApiController]
    [Route("api/v{version:apiVersion}/[controller]")]
    [ApiVersion("1.0")]
    [ApiVersion("2.0")]
    public class MyController : ControllerBase
    {
        // 共通エンドポイント
        [HttpPost]
        [Route("process")]
        public IActionResult PostProcess([FromRoute] string version, [FromBody] object data)
        {
            ApiVersion apiVersion = version == "1.0" ? ApiVersion.V1 : ApiVersion.V2;
            var service = (IMyService)HttpContext.RequestServices.GetService(typeof(IMyService));
            var response = service.ProcessRequest();

            var processedResponse = apiVersion == ApiVersion.V1
                ? new { Message = "This is the REST API response", Response = response }
                : new { Message = "This is the JSON API response", Response = response };

            return Ok(new { Data = data, ProcessedResponse = processedResponse });
        }
    }
}
```

### アプリケーションの実行

```sh
dotnet run
```

### Swagger UIの表示

ブラウザで `https://localhost:5001/swagger` にアクセスすると、以下のように表示されます。

- **Sample API v1**
  - `POST /api/v1/my/process`

- **Sample API v2**
  - `POST /api/v2/my/process`

これにより、Swagger UIで異なるバージョンのAPIがそれぞれ表示され、単一のエンドポイントで複数のバージョンを処理できるようになります。各バージョンに対して異なる処理を行い、クライアントはクエリパラメーターを使ってバージョンを指定できます。
