---
conversation_id: "fbf795d2-c1bf-4525-a78e-9adb8b005d04"
title: "Net8 WebAPI Swagger Entaid"
create_time: 1719568554.8734
update_time: 1719568759.51325
language_guess: "en"
num_messages: 9
part_index: 1
part_count: 1
---

### system — 2024-06-28T09:55:54.873400+00:00

_(empty)_

### user — 2024-06-28T09:55:54.880219+00:00

webapi,swaggerをnet8で作成し、entraidを両方に適用する設定とコードをnet8で

### assistant — 2024-06-28T09:56:31.741423+00:00

_(empty)_

### assistant — 2024-06-28T09:56:31.741516+00:00

.NET 8でSwaggerを使用してWeb APIを作成し、エンドツーエンドの暗号化（Entra ID, Azure Active Directory B2Cなど）を適用する手順とコード例を以下に示します。

## 1. プロジェクトの作成

まず、.NET 8 Web APIプロジェクトを作成します。

```bash
dotnet new webapi -n MyApi
cd MyApi
```

## 2. 必要なパッケージの追加

SwaggerとMicrosoft.Identity.Webを使用するために必要なNuGetパッケージを追加します。

```bash
dotnet add package Swashbuckle.AspNetCore
dotnet add package Microsoft.Identity.Web
dotnet add package Microsoft.Identity.Web.UI
dotnet add package Microsoft.AspNetCore.Authentication.OpenIdConnect
```

## 3. Startup.csの設定

`Program.cs`を編集してSwaggerと認証の設定を追加します。

```csharp
using Microsoft.AspNetCore.Authentication.JwtBearer;
using Microsoft.Identity.Web;
using Microsoft.OpenApi.Models;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddMicrosoftIdentityWebApi(builder.Configuration.GetSection("AzureAd"));

builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new OpenApiInfo { Title = "My API", Version = "v1" });

    // Bearer token 認証の設定
    var securityScheme = new OpenApiSecurityScheme
    {
        Name = "Authorization",
        Type = SecuritySchemeType.Http,
        Scheme = "bearer",
        BearerFormat = "JWT",
        In = ParameterLocation.Header,
        Description = "JWT Authorization header using the Bearer scheme.",
        Reference = new OpenApiReference
        {
            Type = ReferenceType.SecurityScheme,
            Id = "Bearer"
        }
    };

    c.AddSecurityDefinition("Bearer", securityScheme);
    c.AddSecurityRequirement(new OpenApiSecurityRequirement
    {
        {
            new OpenApiSecurityScheme
            {
                Reference = new OpenApiReference
                {
                    Type = ReferenceType.SecurityScheme,
                    Id = "Bearer"
                }
            },
            new string[] {}
        }
    });
});

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
    });
}

app.UseHttpsRedirection();

app.UseAuthentication();
app.UseAuthorization();

app.MapControllers();

app.Run();
```

## 4. appsettings.jsonの設定

Azure AD認証の設定を追加します。

```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "Domain": "yourdomain.onmicrosoft.com",
    "TenantId": "your-tenant-id",
    "ClientId": "your-client-id",
    "ClientSecret": "your-client-secret"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```

`ClientId`、`TenantId`、`ClientSecret`はAzure ADでアプリケーションを登録した際に取得したものを使用します。

## 5. コントローラーの作成

最後に、コントローラーを作成します。

```csharp
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;

namespace MyApi.Controllers
{
    [Authorize]
    [ApiController]
    [Route("[controller]")]
    public class WeatherForecastController : ControllerBase
    {
        private static readonly string[] Summaries = new[]
        {
            "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
        };

        private readonly ILogger<WeatherForecastController> _logger;

        public WeatherForecastController(ILogger<WeatherForecastController> logger)
        {
            _logger = logger;
        }

        [HttpGet(Name = "GetWeatherForecast")]
        public IEnumerable<WeatherForecast> Get()
        {
            return Enumerable.Range(1, 5).Select(index => new WeatherForecast
            {
                Date = DateOnly.FromDateTime(DateTime.Now.AddDays(index)),
                TemperatureC = Random.Shared.Next(-20, 55),
                Summary = Summaries[Random.Shared.Next(Summaries.Length)]
            })
            .ToArray();
        }
    }
}
```

これで、.NET 8でSwaggerを使ったWeb APIとAzure ADによるエンドツーエンドの暗号化認証が設定されました。プロジェクトを実行して、Swagger UIにアクセスし、認証が適用されたエンドポイントをテストできます。

### user — 2024-06-28T09:56:49.235251+00:00

clientsecretは使用しない

### assistant — 2024-06-28T09:57:27.351426+00:00

ClientSecretを使用しない設定に変更する場合、Azure AD B2CやEntra IDを使用してトークンを取得し、トークンを使った認証を行う設定に変更します。

## 1. プロジェクトの作成

前述の手順と同様に、.NET 8 Web APIプロジェクトを作成します。

```bash
dotnet new webapi -n MyApi
cd MyApi
```

## 2. 必要なパッケージの追加

SwaggerとMicrosoft.Identity.Webを使用するために必要なNuGetパッケージを追加します。

```bash
dotnet add package Swashbuckle.AspNetCore
dotnet add package Microsoft.Identity.Web
dotnet add package Microsoft.Identity.Web.UI
dotnet add package Microsoft.AspNetCore.Authentication.OpenIdConnect
```

## 3. `Program.cs`の設定

`Program.cs`を編集してSwaggerと認証の設定を追加します。

```csharp
using Microsoft.AspNetCore.Authentication.JwtBearer;
using Microsoft.Identity.Web;
using Microsoft.OpenApi.Models;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddMicrosoftIdentityWebApi(builder.Configuration.GetSection("AzureAdB2C"));

builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new OpenApiInfo { Title = "My API", Version = "v1" });

    // Bearer token 認証の設定
    var securityScheme = new OpenApiSecurityScheme
    {
        Name = "Authorization",
        Type = SecuritySchemeType.Http,
        Scheme = "bearer",
        BearerFormat = "JWT",
        In = ParameterLocation.Header,
        Description = "JWT Authorization header using the Bearer scheme.",
        Reference = new OpenApiReference
        {
            Type = ReferenceType.SecurityScheme,
            Id = "Bearer"
        }
    };

    c.AddSecurityDefinition("Bearer", securityScheme);
    c.AddSecurityRequirement(new OpenApiSecurityRequirement
    {
        {
            new OpenApiSecurityScheme
            {
                Reference = new OpenApiReference
                {
                    Type = ReferenceType.SecurityScheme,
                    Id = "Bearer"
                }
            },
            new string[] {}
        }
    });
});

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
    });
}

app.UseHttpsRedirection();

app.UseAuthentication();
app.UseAuthorization();

app.MapControllers();

app.Run();
```

## 4. `appsettings.json`の設定

Azure AD B2C認証の設定を追加します。ClientSecretは不要です。

```json
{
  "AzureAdB2C": {
    "Instance": "https://{your-tenant-name}.b2clogin.com/",
    "ClientId": "your-client-id",
    "Domain": "your-domain",
    "SignUpSignInPolicyId": "your-sign-up-sign-in-policy-id"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```

`Instance`, `ClientId`, `Domain`, `SignUpSignInPolicyId`はAzure AD B2Cで設定した値を使用します。

## 5. コントローラーの作成

最後に、コントローラーを作成します。

```csharp
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;

namespace MyApi.Controllers
{
    [Authorize]
    [ApiController]
    [Route("[controller]")]
    public class WeatherForecastController : ControllerBase
    {
        private static readonly string[] Summaries = new[]
        {
            "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
        };

        private readonly ILogger<WeatherForecastController> _logger;

        public WeatherForecastController(ILogger<WeatherForecastController> logger)
        {
            _logger = logger;
        }

        [HttpGet(Name = "GetWeatherForecast")]
        public IEnumerable<WeatherForecast> Get()
        {
            return Enumerable.Range(1, 5).Select(index => new WeatherForecast
            {
                Date = DateOnly.FromDateTime(DateTime.Now.AddDays(index)),
                TemperatureC = Random.Shared.Next(-20, 55),
                Summary = Summaries[Random.Shared.Next(Summaries.Length)]
            })
            .ToArray();
        }
    }
}
```

これで、.NET 8でSwaggerを使ったWeb APIとAzure AD B2Cによるエンドツーエンドの暗号化認証が設定されました。プロジェクトを実行して、Swagger UIにアクセスし、認証が適用されたエンドポイントをテストできます。

### user — 2024-06-28T09:58:36.485288+00:00

このコードではclientidを使用していない

### assistant — 2024-06-28T09:59:19.242697+00:00

クライアントシークレットを使用せず、クライアントIDを使用する設定について説明します。この場合、Azure AD B2Cで発行されたトークンを使用して認証を行います。

## 1. プロジェクトの作成

前述の手順と同様に、.NET 8 Web APIプロジェクトを作成します。

```bash
dotnet new webapi -n MyApi
cd MyApi
```

## 2. 必要なパッケージの追加

SwaggerとMicrosoft.Identity.Webを使用するために必要なNuGetパッケージを追加します。

```bash
dotnet add package Swashbuckle.AspNetCore
dotnet add package Microsoft.Identity.Web
dotnet add package Microsoft.Identity.Web.UI
dotnet add package Microsoft.AspNetCore.Authentication.JwtBearer
```

## 3. `Program.cs`の設定

`Program.cs`を編集してSwaggerと認証の設定を追加します。

```csharp
using Microsoft.AspNetCore.Authentication.JwtBearer;
using Microsoft.Identity.Web;
using Microsoft.OpenApi.Models;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddMicrosoftIdentityWebApi(builder.Configuration.GetSection("AzureAd"));

builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new OpenApiInfo { Title = "My API", Version = "v1" });

    // Bearer token 認証の設定
    var securityScheme = new OpenApiSecurityScheme
    {
        Name = "Authorization",
        Type = SecuritySchemeType.Http,
        Scheme = "bearer",
        BearerFormat = "JWT",
        In = ParameterLocation.Header,
        Description = "JWT Authorization header using the Bearer scheme.",
        Reference = new OpenApiReference
        {
            Type = ReferenceType.SecurityScheme,
            Id = "Bearer"
        }
    };

    c.AddSecurityDefinition("Bearer", securityScheme);
    c.AddSecurityRequirement(new OpenApiSecurityRequirement
    {
        {
            new OpenApiSecurityScheme
            {
                Reference = new OpenApiReference
                {
                    Type = ReferenceType.SecurityScheme,
                    Id = "Bearer"
                }
            },
            new string[] {}
        }
    });
});

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
    });
}

app.UseHttpsRedirection();

app.UseAuthentication();
app.UseAuthorization();

app.MapControllers();

app.Run();
```

## 4. `appsettings.json`の設定

Azure AD B2C認証の設定を追加します。ClientSecretは不要です。

```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "Domain": "yourdomain.onmicrosoft.com",
    "TenantId": "your-tenant-id",
    "ClientId": "your-client-id",
    "SignUpSignInPolicyId": "B2C_1_signupsignin"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```

`ClientId`、`TenantId`、`Domain`、`SignUpSignInPolicyId`はAzure AD B2Cで設定した値を使用します。

## 5. コントローラーの作成

最後に、コントローラーを作成します。

```csharp
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;

namespace MyApi.Controllers
{
    [Authorize]
    [ApiController]
    [Route("[controller]")]
    public class WeatherForecastController : ControllerBase
    {
        private static readonly string[] Summaries = new[]
        {
            "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
        };

        private readonly ILogger<WeatherForecastController> _logger;

        public WeatherForecastController(ILogger<WeatherForecastController> logger)
        {
            _logger = logger;
        }

        [HttpGet(Name = "GetWeatherForecast")]
        public IEnumerable<WeatherForecast> Get()
        {
            return Enumerable.Range(1, 5).Select(index => new WeatherForecast
            {
                Date = DateOnly.FromDateTime(DateTime.Now.AddDays(index)),
                TemperatureC = Random.Shared.Next(-20, 55),
                Summary = Summaries[Random.Shared.Next(Summaries.Length)]
            })
            .ToArray();
        }
    }
}
```

これで、.NET 8でSwaggerを使ったWeb APIとAzure AD B2Cによるエンドツーエンドの暗号化認証が設定されました。プロジェクトを実行して、Swagger UIにアクセスし、認証が適用されたエンドポイントをテストできます。

プロジェクトを実行して、Swagger UIにアクセスし、認証が適用されたエンドポイントをテストできます。プロジェクトの実行後、Swagger UIは`https://localhost:5001/swagger/index.html`でアクセスできます。

プロジェクトをビルドして実行します。

```bash
dotnet run
```

ブラウザで`https://localhost:5001/swagger/index.html`にアクセスしてSwagger UIを確認できます。エンドポイントにアクセスするには、Azure AD B2Cで取得したJWTトークンを使用して認証する必要があります。
