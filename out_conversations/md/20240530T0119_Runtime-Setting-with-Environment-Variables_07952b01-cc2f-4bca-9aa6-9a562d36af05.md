---
conversation_id: "07952b01-cc2f-4bca-9aa6-9a562d36af05"
title: "Runtime Setting with Environment Variables"
create_time: 1717031999.519953
update_time: 1717032106.955936
language_guess: "en"
num_messages: 7
part_index: 1
part_count: 1
---

### system — 2024-05-30T01:19:59.519953+00:00

_(empty)_

### user — 2024-05-30T01:19:59.521949+00:00

.netのruntimesetting.json設定は環境変数のできるか

### assistant — 2024-05-30T01:20:17.186126+00:00

_(empty)_

### assistant — 2024-05-30T01:20:17.186289+00:00

`.NET` の `runtimeconfig.json` では、環境変数の設定が直接できるわけではありませんが、環境変数を使ってアプリケーションの設定を行うことは可能です。以下に、環境変数を利用して `runtimeconfig.json` の設定に影響を与える方法を説明します。

## 1. 環境変数の設定
まず、必要な環境変数を設定します。Windows の場合は、コマンドプロンプトまたは PowerShell で以下のように設定できます。

### コマンドプロンプト
```cmd
setx MY_APP_SETTING "my_value"
```

### PowerShell
```powershell
$env:MY_APP_SETTING = "my_value"
```

Linux または macOS では、`export` コマンドを使用して設定します。

```bash
export MY_APP_SETTING="my_value"
```

## 2. アプリケーションで環境変数を読み取る
環境変数をアプリケーションで読み取るには、以下のように `Environment.GetEnvironmentVariable` メソッドを使用します。

```csharp
using System;

class Program
{
    static void Main()
    {
        string setting = Environment.GetEnvironmentVariable("MY_APP_SETTING");
        Console.WriteLine($"Environment variable value: {setting}");
    }
}
```

## 3. `runtimeconfig.json` の使用
`runtimeconfig.json` は、.NET アプリケーションのランタイム設定を記述するためのファイルです。しかし、環境変数の設定自体はこのファイルで行うことはできません。このファイルには、以下のようにランタイム構成情報を記述します。

```json
{
  "runtimeOptions": {
    "tfm": "net5.0",
    "framework": {
      "name": "Microsoft.NETCore.App",
      "version": "5.0.0"
    }
  }
}
```

## 4. 環境変数を使ったアプリケーション設定
多くのアプリケーションでは、環境変数を使って設定を動的に変更できます。例えば、ASP.NET Core アプリケーションでは、`appsettings.json` の設定を環境変数で上書きすることができます。

### `appsettings.json`
```json
{
  "MyAppSetting": "default_value"
}
```

### プログラムコード
```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.AddEnvironmentVariables();
            })
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseStartup<Startup>();
            });
}
```

このように、環境変数を利用してアプリケーションの設定を動的に変更することができます。`.NET` の `runtimeconfig.json` ファイル自体では環境変数を設定することはできませんが、アプリケーション内で環境変数を利用することで、設定を動的に変更することが可能です。

### user — 2024-05-30T01:21:23.411833+00:00

ファイルに書く項目を環境変数にできるのか

### assistant — 2024-05-30T01:21:46.540741+00:00

`.NET` アプリケーションにおいて、ファイルに書かれた項目を環境変数に置き換えることができます。ここでは、`appsettings.json` のような設定ファイルでの設定を環境変数で上書きする方法について説明します。

### 1. `appsettings.json` の設定
まず、`appsettings.json` ファイルにデフォルトの設定を書きます。

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "MyAppSetting": "default_value"
}
```

### 2. 環境変数の設定
次に、環境変数を設定します。以下は Windows の場合の設定方法です。

#### コマンドプロンプト
```cmd
setx Logging__LogLevel__Default "Debug"
setx MyAppSetting "env_value"
```

#### PowerShell
```powershell
$env:Logging__LogLevel__Default = "Debug"
$env:MyAppSetting = "env_value"
```

Linux や macOS では、以下のように設定します。

```bash
export Logging__LogLevel__Default="Debug"
export MyAppSetting="env_value"
```

### 3. アプリケーションコードでの設定
ASP.NET Core アプリケーションでは、環境変数を使用して設定を上書きするために `ConfigureAppConfiguration` メソッドで `AddEnvironmentVariables` を呼び出します。

```csharp
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Hosting;

public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.AddEnvironmentVariables();
            })
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseStartup<Startup>();
            });
}
```

### 4. `Startup.cs` での設定読み取り
`Startup.cs` で設定を読み取る際に、環境変数で上書きされた設定を利用することができます。

```csharp
public class Startup
{
    public Startup(IConfiguration configuration)
    {
        Configuration = configuration;
    }

    public IConfiguration Configuration { get; }

    public void ConfigureServices(IServiceCollection services)
    {
        // 環境変数で上書きされた設定値を取得
        var myAppSetting = Configuration["MyAppSetting"];
        var logLevelDefault = Configuration["Logging:LogLevel:Default"];

        Console.WriteLine($"MyAppSetting: {myAppSetting}");
        Console.WriteLine($"Logging:LogLevel:Default: {logLevelDefault}");

        services.AddControllers();
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }
        else
        {
            app.UseExceptionHandler("/Home/Error");
            app.UseHsts();
        }
        app.UseHttpsRedirection();
        app.UseStaticFiles();
        app.UseRouting();
        app.UseAuthorization();
        app.UseEndpoints(endpoints =>
        {
            endpoints.MapControllers();
        });
    }
}
```

これにより、`appsettings.json` の設定値は環境変数で上書きされ、環境ごとに異なる設定を簡単に管理できるようになります。
