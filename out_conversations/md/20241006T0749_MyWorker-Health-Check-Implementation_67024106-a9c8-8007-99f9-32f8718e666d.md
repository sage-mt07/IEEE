---
conversation_id: "67024106-a9c8-8007-99f9-32f8718e666d"
title: "MyWorker Health Check Implementation"
create_time: 1728200966.837668
update_time: 1728201249.339405
language_guess: "en"
num_messages: 7
part_index: 1
part_count: 1
---

### system — 2024-10-06T07:49:26.837668+00:00

_(empty)_

### user — 2024-10-06T07:49:26.843735+00:00

using System;
using System.Net.Http;
using System.Text.Json;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
using Npgsql;
using Azure.Monitor.Query;
using Azure.Identity;

public class MyWorker : BackgroundService
{
    private readonly int _executionInterval;
    private readonly string _connectionString;
    private string _subscriptionId;
    private string _resourceGroupName;
    private readonly string _resourceUri;
    private readonly ILogger<MyWorker> _logger;

    public MyWorker(int executionInterval, string connectionString, ILogger<MyWorker> logger)
    {
        _executionInterval = executionInterval;
        _connectionString = connectionString;
        _logger = logger;

        // Initialize resource identifiers by fetching metadata from IMDS
        var metadata = GetAzureInstanceMetadataAsync().GetAwaiter().GetResult();
        _subscriptionId = metadata.subscriptionId;
        _resourceGroupName = metadata.resourceGroupName;

        // PostgreSQLのサーバー名を接続文字列から抽出し、リソースURIを構築
        var postgresqlServerName = ExtractServerNameFromConnectionString(_connectionString);
        if (!string.IsNullOrEmpty(postgresqlServerName))
        {
            _resourceUri = $"/subscriptions/{_subscriptionId}/resourceGroups/{_resourceGroupName}/providers/Microsoft.DBforPostgreSQL/servers/{postgresqlServerName}";
        }
        else
        {
            _logger.LogError("PostgreSQL server name could not be extracted from the connection string.");
        }
    }

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            try
            {
                // PostgreSQLからキャッシュヒット率を取得
                double cacheHitRate = await GetPostgreSqlCacheHitRate(_connectionString);
                _logger.LogInformation($"Cache Hit Rate: {cacheHitRate}%");

                // キャッシュヒット率をAzure Monitorに送信
                await SendMetricToAzureMonitor(cacheHitRate, _resourceUri);

                // 次の実行まで指定秒数待機
                _logger.LogInformation($"Waiting for {_executionInterval} seconds before next execution.");
                await Task.Delay(_executionInterval * 1000, stoppingToken);
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "An error occurred during execution.");
            }
        }
    }

    private async Task<double> GetPostgreSqlCacheHitRate(string connectionString)
    {
        double cacheHitRate = 0;
        using (var conn = new NpgsqlConnection(connectionString))
        {
            await conn.OpenAsync();

            string query = @"
                SELECT blks_hit::float / (blks_hit + blks_read) * 100 AS cache_hit_ratio
                FROM pg_stat_database
                WHERE datname = current_database()";

            using (var cmd = new NpgsqlCommand(query, conn))
            {
                var result = await cmd.ExecuteScalarAsync();
                if (result != null && result != DBNull.Value)
                {
                    cacheHitRate = Convert.ToDouble(result);
                }
            }
        }
        return cacheHitRate;
    }

    private async Task SendMetricToAzureMonitor(double cacheHitRate, string resourceUri)
    {
        var credential = new DefaultAzureCredential();
        var monitorClient = new MetricsClient(credential);

        var metric = new MetricQueryDefinition(
            "CustomMetrics",
            new[]
            {
                new MetricQueryTimeSeriesData(
                    "CacheHitRate",
                    new MetricQueryTimeSeriesDataPoint
                    {
                        Average = cacheHitRate
                    }
                )
            }
        );

        await monitorClient.SendMetricsAsync(resourceUri, metric);
    }

    private string ExtractServerNameFromConnectionString(string connectionString)
    {
        var match = System.Text.RegularExpressions.Regex.Match(connectionString, @"Host=([\w\d\-\.]+)");
        return match.Success ? match.Groups[1].Value : null;
    }

    private async Task<(string subscriptionId, string resourceGroupName)> GetAzureInstanceMetadataAsync()
    {
        using (HttpClient client = new HttpClient())
        {
            client.DefaultRequestHeaders.Add("Metadata", "true");

            var response = await client.GetAsync("http://[[REDACTED_PHONE]]/metadata/instance?api-version=[[REDACTED_PHONE]]");

            if (response.IsSuccessStatusCode)
            {
                var json = await response.Content.ReadAsStringAsync();
                var document = JsonDocument.Parse(json);

                var subscriptionId = document.RootElement.GetProperty("compute").GetProperty("subscriptionId").GetString();
                var resourceGroupName = document.RootElement.GetProperty("compute").GetProperty("resourceGroupName").GetString();

                return (subscriptionId, resourceGroupName);
            }
            else
            {
                _logger.LogError("Failed to retrieve Azure instance metadata.");
                throw new InvalidOperationException("Unable to fetch metadata from Azure Instance Metadata Service.");
            }
        }
    }
}
にへるすちぇくを追加する

### assistant — 2024-10-06T07:49:44.615018+00:00

_(empty)_

### assistant — 2024-10-06T07:49:44.615176+00:00

To add a health check to your `MyWorker` service, you can implement a custom health check by following these steps:

1. **Install the necessary package:**
   First, ensure you have the `Microsoft.Extensions.Diagnostics.HealthChecks` NuGet package installed in your project. This package provides health check APIs.

2. **Create a custom health check class:**
   You can create a class that implements the `IHealthCheck` interface. This class will contain the logic to determine the health of your service.

3. **Register the health check in the `Startup` or `Program` class (depending on your project setup):**
   You need to add the custom health check to the service collection and configure the health check endpoint.

Here’s how you can modify your code to include a health check:

### Step 1: Create a custom health check class

```csharp
using Microsoft.Extensions.Diagnostics.HealthChecks;
using System.Threading;
using System.Threading.Tasks;

public class MyWorkerHealthCheck : IHealthCheck
{
    private readonly MyWorker _myWorker;

    public MyWorkerHealthCheck(MyWorker myWorker)
    {
        _myWorker = myWorker;
    }

    public Task<HealthCheckResult> CheckHealthAsync(HealthCheckContext context, CancellationToken cancellationToken = default)
    {
        // Assuming that the health check depends on whether the service has completed StartAsync.
        if (_myWorker.IsStarted)
        {
            return Task.FromResult(HealthCheckResult.Healthy("MyWorker service is running."));
        }
        else
        {
            return Task.FromResult(HealthCheckResult.Unhealthy("MyWorker service has not started yet."));
        }
    }
}
```

### Step 2: Modify your `MyWorker` class to include an `IsStarted` flag

You can add an `IsStarted` property to track when the service has started:

```csharp
public class MyWorker : BackgroundService
{
    private readonly int _executionInterval;
    private readonly string _connectionString;
    private string _subscriptionId;
    private string _resourceGroupName;
    private readonly string _resourceUri;
    private readonly ILogger<MyWorker> _logger;

    public bool IsStarted { get; private set; }

    public MyWorker(int executionInterval, string connectionString, ILogger<MyWorker> logger)
    {
        _executionInterval = executionInterval;
        _connectionString = connectionString;
        _logger = logger;

        var metadata = GetAzureInstanceMetadataAsync().GetAwaiter().GetResult();
        _subscriptionId = metadata.subscriptionId;
        _resourceGroupName = metadata.resourceGroupName;

        var postgresqlServerName = ExtractServerNameFromConnectionString(_connectionString);
        if (!string.IsNullOrEmpty(postgresqlServerName))
        {
            _resourceUri = $"/subscriptions/{_subscriptionId}/resourceGroups/{_resourceGroupName}/providers/Microsoft.DBforPostgreSQL/servers/{postgresqlServerName}";
        }
        else
        {
            _logger.LogError("PostgreSQL server name could not be extracted from the connection string.");
        }
    }

    protected override async Task StartAsync(CancellationToken cancellationToken)
    {
        IsStarted = true; // Set to true when the service starts successfully
        await base.StartAsync(cancellationToken);
    }

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            try
            {
                double cacheHitRate = await GetPostgreSqlCacheHitRate(_connectionString);
                _logger.LogInformation($"Cache Hit Rate: {cacheHitRate}%");

                await SendMetricToAzureMonitor(cacheHitRate, _resourceUri);

                _logger.LogInformation($"Waiting for {_executionInterval} seconds before next execution.");
                await Task.Delay(_executionInterval * 1000, stoppingToken);
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "An error occurred during execution.");
            }
        }
    }

    // Rest of the methods
}
```

### Step 3: Register the health check in your `Program` or `Startup` class

Now, you need to register the health check in your `Program` or `Startup` class:

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureServices((hostContext, services) =>
            {
                services.AddHostedService<MyWorker>();

                // Register the health check
                services.AddHealthChecks()
                        .AddCheck<MyWorkerHealthCheck>("MyWorker Health Check");
            });
}
```

### Step 4: Configure health check endpoints

You can expose the health check endpoint by adding the following code in `Startup.cs` or in the `Program.cs` for minimal APIs:

```csharp
app.UseEndpoints(endpoints =>
{
    endpoints.MapHealthChecks("/health");
});
```

### Step 5: Test the health check

You can now access the `/health` endpoint in your browser or through a tool like `curl` to check the health of your service:

```bash
curl http://localhost:5000/health
```

This will return either a healthy or unhealthy status based on the state of your service.

### user — 2024-10-06T07:53:51.636828+00:00

ポート番号が5000はどこで設定しているのか

### assistant — 2024-10-06T07:54:08.726370+00:00

ポート番号 5000 は、ASP.NET Core アプリケーションの既定の Kestrel サーバーの設定によって決定されます。特に、ポート番号は次の場所で設定される可能性があります。

### 1. **`launchSettings.json` ファイル**
Visual Studio を使用している場合、`Properties` フォルダ内にある `launchSettings.json` ファイルで、デフォルトのポート設定が指定されています。このファイルで、アプリケーションがどのポートで実行されるかが設定されている場合があります。

例えば、以下のような `launchSettings.json` の一部があります：

```json
{
  "profiles": {
    "MyApp": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "http://localhost:5000;https://localhost:5001",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

ここで、`applicationUrl` に `http://localhost:5000` と `https://localhost:5001` が指定されており、これがアプリケーションのポート設定です。これを変更することで、別のポート番号でアプリケーションを実行することができます。

### 2. **環境変数**
ポート番号は環境変数 `ASPNETCORE_URLS` でも設定できます。この環境変数を設定することで、アプリケーションのリッスンする URL やポートを指定できます。

例えば、Linux や Windows のコマンドラインで環境変数を設定する方法は以下の通りです：

#### Linux/MacOS:
```bash
export ASPNETCORE_URLS="http://localhost:6000"
```

#### Windows コマンドプロンプト:
```cmd
set ASPNETCORE_URLS=http://localhost:6000
```

#### Windows PowerShell:
```powershell
$env:ASPNETCORE_URLS="http://localhost:6000"
```

### 3. **`Program.cs`（または `Startup.cs`）内での設定**
Kestrel サーバーの設定は、`Program.cs` や `Startup.cs` で直接指定することも可能です。特に `Program.cs` に次のように Kestrel の設定を記述することで、ポート番号を指定できます。

```csharp
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
                webBuilder.UseStartup<Startup>();

                // ポートを 5000 に設定
                webBuilder.UseUrls("http://localhost:5000");
            });
}
```

このコードでは、`UseUrls` メソッドを使用して Kestrel サーバーに `http://localhost:5000` でリッスンするように指示しています。

### 4. **Docker コンテナの設定**
アプリケーションが Docker コンテナでホストされている場合、`Dockerfile` や `docker-compose.yml` ファイルでポートが設定されている可能性もあります。

例えば、`docker-compose.yml` では次のように設定します：

```yaml
services:
  myapp:
    image: myappimage
    ports:
      - "5000:80"  # コンテナの内部ポート 80 をホストの 5000 ポートにマッピング
```

この場合、Docker コンテナ内ではアプリケーションがポート 80 で実行されていますが、ホストマシンのポート 5000 に公開されています。

### 結論
ポート番号 5000 は、`launchSettings.json`、環境変数、`Program.cs` や `Startup.cs` の中で設定されている可能性があります。これらを確認・変更することで、アプリケーションのポート番号を制御できます。
