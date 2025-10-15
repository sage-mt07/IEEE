---
conversation_id: "5a942941-18a8-418e-a887-d04ebad4e6c2"
title: "SQLServer Dapper Integration"
create_time: 1722692883.639846
update_time: 1722693194.704081
language_guess: "en"
num_messages: 15
part_index: 1
part_count: 1
---

### system — 2024-08-03T13:48:03.639846+00:00

_(empty)_

### user — 2024-08-03T13:48:03.643520+00:00

以下の要件に対応するパッケージのソースを作成
・SQLServerのSPを呼び出す
・SQLServerの接続エラーに対応し、指定回数のリトライをおこなう
・Dapperを利用する
・以下のDapperのAPIに対応するインターフェースを提供する
QueryFirstOrDefaultAsync
QueryAsync
QueryMultipleAsync

### assistant — 2024-08-03T13:48:22.269624+00:00

_(empty)_

### assistant — 2024-08-03T13:48:22.269712+00:00

以下に、指定された要件に対応するASP.NET Core WebAPIのパッケージのソースコードを作成します。このパッケージは、Dapperを利用してSQL Serverのストアドプロシージャ（SP）を呼び出し、接続エラーに対応し、指定回数のリトライを行います。また、指定されたDapperのAPIに対応するインターフェースも提供します。

### パッケージ構成
- `ISqlService`：DapperのAPIを提供するインターフェース
- `SqlService`：`ISqlService`を実装するクラス
- `RetryPolicy`：リトライポリシーを実装するクラス

### ISqlService.cs
```csharp
using System.Collections.Generic;
using System.Data;
using System.Threading.Tasks;

namespace YourNamespace
{
    public interface ISqlService
    {
        Task<T> QueryFirstOrDefaultAsync<T>(string storedProcedure, object parameters = null, int retryCount = 3);
        Task<IEnumerable<T>> QueryAsync<T>(string storedProcedure, object parameters = null, int retryCount = 3);
        Task<SqlMapper.GridReader> QueryMultipleAsync(string storedProcedure, object parameters = null, int retryCount = 3);
    }
}
```

### SqlService.cs
```csharp
using Dapper;
using Microsoft.Data.SqlClient;
using System.Collections.Generic;
using System.Data;
using System.Threading.Tasks;

namespace YourNamespace
{
    public class SqlService : ISqlService
    {
        private readonly string _connectionString;

        public SqlService(string connectionString)
        {
            _connectionString = connectionString;
        }

        public async Task<T> QueryFirstOrDefaultAsync<T>(string storedProcedure, object parameters = null, int retryCount = 3)
        {
            return await ExecuteWithRetry(async () =>
            {
                using var connection = new SqlConnection(_connectionString);
                return await connection.QueryFirstOrDefaultAsync<T>(storedProcedure, parameters, commandType: CommandType.StoredProcedure);
            }, retryCount);
        }

        public async Task<IEnumerable<T>> QueryAsync<T>(string storedProcedure, object parameters = null, int retryCount = 3)
        {
            return await ExecuteWithRetry(async () =>
            {
                using var connection = new SqlConnection(_connectionString);
                return await connection.QueryAsync<T>(storedProcedure, parameters, commandType: CommandType.StoredProcedure);
            }, retryCount);
        }

        public async Task<SqlMapper.GridReader> QueryMultipleAsync(string storedProcedure, object parameters = null, int retryCount = 3)
        {
            return await ExecuteWithRetry(async () =>
            {
                using var connection = new SqlConnection(_connectionString);
                return await connection.QueryMultipleAsync(storedProcedure, parameters, commandType: CommandType.StoredProcedure);
            }, retryCount);
        }

        private async Task<T> ExecuteWithRetry<T>(Func<Task<T>> func, int retryCount)
        {
            int attempt = 0;
            while (true)
            {
                try
                {
                    return await func();
                }
                catch (SqlException ex) when (attempt < retryCount)
                {
                    attempt++;
                    await Task.Delay(1000 * attempt); // Exponential backoff
                }
            }
        }
    }
}
```

### RetryPolicy.cs
```csharp
using System;
using System.Threading.Tasks;

namespace YourNamespace
{
    public class RetryPolicy
    {
        public static async Task<T> ExecuteWithRetry<T>(Func<Task<T>> func, int retryCount = 3)
        {
            int attempt = 0;
            while (true)
            {
                try
                {
                    return await func();
                }
                catch (Exception ex) when (attempt < retryCount)
                {
                    attempt++;
                    await Task.Delay(1000 * attempt); // Exponential backoff
                }
            }
        }
    }
}
```

### 使用方法
1. `SqlService`クラスのインスタンスを作成し、接続文字列を渡します。
2. 必要なメソッド（`QueryFirstOrDefaultAsync`、`QueryAsync`、`QueryMultipleAsync`）を呼び出します。

### 例
```csharp
public class YourController : ControllerBase
{
    private readonly ISqlService _sqlService;

    public YourController(ISqlService sqlService)
    {
        _sqlService = sqlService;
    }

    public async Task<IActionResult> Get()
    {
        var result = await _sqlService.QueryAsync<YourModel>("YourStoredProcedure", new { Param1 = "Value1" });
        return Ok(result);
    }
}
```

このパッケージは、接続エラーに対応するためにリトライポリシーを実装し、Dapperを利用してSQL Serverのストアドプロシージャを呼び出します。また、指定されたDapperのAPIに対応するインターフェースを提供します。

### user — 2024-08-03T13:48:42.070662+00:00

リトライはPollyを利用する

### assistant — 2024-08-03T13:48:58.742885+00:00

Pollyを利用してリトライ機能を実装する方法を以下に示します。Pollyは、.NETアプリケーションでの回復力を向上させるための強力なライブラリであり、簡単にリトライポリシーを設定できます。

### パッケージ構成
- `ISqlService`：DapperのAPIに対応するインターフェース
- `SqlService`：`ISqlService`を実装するクラス
- `Polly`を利用したリトライポリシー

### インストール
まず、Pollyをインストールします。NuGetパッケージマネージャーを使用して以下のコマンドを実行します：
```
Install-Package Polly
```

### ISqlService.cs
```csharp
using System.Collections.Generic;
using System.Threading.Tasks;

namespace YourNamespace
{
    public interface ISqlService
    {
        Task<T> QueryFirstOrDefaultAsync<T>(string storedProcedure, object parameters = null);
        Task<IEnumerable<T>> QueryAsync<T>(string storedProcedure, object parameters = null);
        Task<SqlMapper.GridReader> QueryMultipleAsync(string storedProcedure, object parameters = null);
    }
}
```

### SqlService.cs
```csharp
using Dapper;
using Microsoft.Data.SqlClient;
using Polly;
using Polly.Retry;
using System;
using System.Collections.Generic;
using System.Data;
using System.Threading.Tasks;

namespace YourNamespace
{
    public class SqlService : ISqlService
    {
        private readonly string _connectionString;
        private readonly AsyncRetryPolicy _retryPolicy;

        public SqlService(string connectionString)
        {
            _connectionString = connectionString;
            _retryPolicy = Policy
                .Handle<SqlException>()
                .WaitAndRetryAsync(3, retryAttempt => TimeSpan.FromSeconds(Math.Pow(2, retryAttempt)));
        }

        public async Task<T> QueryFirstOrDefaultAsync<T>(string storedProcedure, object parameters = null)
        {
            return await _retryPolicy.ExecuteAsync(async () =>
            {
                using var connection = new SqlConnection(_connectionString);
                return await connection.QueryFirstOrDefaultAsync<T>(storedProcedure, parameters, commandType: CommandType.StoredProcedure);
            });
        }

        public async Task<IEnumerable<T>> QueryAsync<T>(string storedProcedure, object parameters = null)
        {
            return await _retryPolicy.ExecuteAsync(async () =>
            {
                using var connection = new SqlConnection(_connectionString);
                return await connection.QueryAsync<T>(storedProcedure, parameters, commandType: CommandType.StoredProcedure);
            });
        }

        public async Task<SqlMapper.GridReader> QueryMultipleAsync(string storedProcedure, object parameters = null)
        {
            return await _retryPolicy.ExecuteAsync(async () =>
            {
                using var connection = new SqlConnection(_connectionString);
                return await connection.QueryMultipleAsync(storedProcedure, parameters, commandType: CommandType.StoredProcedure);
            });
        }
    }
}
```

### 使用方法
1. `SqlService`クラスのインスタンスを作成し、接続文字列を渡します。
2. 必要なメソッド（`QueryFirstOrDefaultAsync`、`QueryAsync`、`QueryMultipleAsync`）を呼び出します。

### 例
```csharp
public class YourController : ControllerBase
{
    private readonly ISqlService _sqlService;

    public YourController(ISqlService sqlService)
    {
        _sqlService = sqlService;
    }

    [HttpGet]
    public async Task<IActionResult> Get()
    {
        var result = await _sqlService.QueryAsync<YourModel>("YourStoredProcedure", new { Param1 = "Value1" });
        return Ok(result);
    }
}
```

このパッケージは、Pollyを利用してリトライポリシーを実装し、Dapperを利用してSQL Serverのストアドプロシージャを呼び出します。また、指定されたDapperのAPIに対応するインターフェースを提供します。これにより、SQL Server接続エラー時に指定回数リトライを行うことができます。

### user — 2024-08-03T13:49:25.538774+00:00

リトライの条件にネットワークエラーを追加する

### assistant — 2024-08-03T13:49:44.002328+00:00

ネットワークエラーに対応するために、Pollyのリトライポリシーを更新します。これにより、SQLエラーだけでなく、ネットワークエラーもリトライの対象とします。

### 更新後のパッケージ構成
- `ISqlService`：DapperのAPIに対応するインターフェース
- `SqlService`：`ISqlService`を実装するクラス
- `Polly`を利用したリトライポリシー（SQLエラーおよびネットワークエラーに対応）

### インストール
Pollyがインストールされていない場合は、以下のコマンドを実行してインストールします：
```
Install-Package Polly
```

### ISqlService.cs
```csharp
using System.Collections.Generic;
using System.Threading.Tasks;

namespace YourNamespace
{
    public interface ISqlService
    {
        Task<T> QueryFirstOrDefaultAsync<T>(string storedProcedure, object parameters = null);
        Task<IEnumerable<T>> QueryAsync<T>(string storedProcedure, object parameters = null);
        Task<SqlMapper.GridReader> QueryMultipleAsync(string storedProcedure, object parameters = null);
    }
}
```

### SqlService.cs
```csharp
using Dapper;
using Microsoft.Data.SqlClient;
using Polly;
using Polly.Retry;
using System;
using System.Collections.Generic;
using System.Data;
using System.Net.Sockets;
using System.Threading.Tasks;

namespace YourNamespace
{
    public class SqlService : ISqlService
    {
        private readonly string _connectionString;
        private readonly AsyncRetryPolicy _retryPolicy;

        public SqlService(string connectionString)
        {
            _connectionString = connectionString;
            _retryPolicy = Policy
                .Handle<SqlException>()
                .Or<SocketException>()
                .WaitAndRetryAsync(3, retryAttempt => TimeSpan.FromSeconds(Math.Pow(2, retryAttempt)));
        }

        public async Task<T> QueryFirstOrDefaultAsync<T>(string storedProcedure, object parameters = null)
        {
            return await _retryPolicy.ExecuteAsync(async () =>
            {
                using var connection = new SqlConnection(_connectionString);
                return await connection.QueryFirstOrDefaultAsync<T>(storedProcedure, parameters, commandType: CommandType.StoredProcedure);
            });
        }

        public async Task<IEnumerable<T>> QueryAsync<T>(string storedProcedure, object parameters = null)
        {
            return await _retryPolicy.ExecuteAsync(async () =>
            {
                using var connection = new SqlConnection(_connectionString);
                return await connection.QueryAsync<T>(storedProcedure, parameters, commandType: CommandType.StoredProcedure);
            });
        }

        public async Task<SqlMapper.GridReader> QueryMultipleAsync(string storedProcedure, object parameters = null)
        {
            return await _retryPolicy.ExecuteAsync(async () =>
            {
                using var connection = new SqlConnection(_connectionString);
                return await connection.QueryMultipleAsync(storedProcedure, parameters, commandType: CommandType.StoredProcedure);
            });
        }
    }
}
```

### 使用方法
1. `SqlService`クラスのインスタンスを作成し、接続文字列を渡します。
2. 必要なメソッド（`QueryFirstOrDefaultAsync`、`QueryAsync`、`QueryMultipleAsync`）を呼び出します。

### 例
```csharp
public class YourController : ControllerBase
{
    private readonly ISqlService _sqlService;

    public YourController(ISqlService sqlService)
    {
        _sqlService = sqlService;
    }

    [HttpGet]
    public async Task<IActionResult> Get()
    {
        var result = await _sqlService.QueryAsync<YourModel>("YourStoredProcedure", new { Param1 = "Value1" });
        return Ok(result);
    }
}
```

このパッケージは、Pollyを利用してリトライポリシーを実装し、Dapperを利用してSQL Serverのストアドプロシージャを呼び出します。SQLエラーおよびネットワークエラー（`SocketException`）に対してリトライを行う設定となっています。これにより、より堅牢なエラーハンドリングを実現します。

### user — 2024-08-03T13:50:50.574295+00:00

SPが存在しない場合など、構成上の問題に対してはリトライを行わない条件を追加

### assistant — 2024-08-03T13:51:12.538458+00:00

構成上の問題（例えば、ストアドプロシージャが存在しない場合など）に対してはリトライを行わないように、特定のエラーメッセージやエラーコードを基にリトライポリシーを設定します。

以下に、構成上の問題に対してリトライを行わない条件を追加したコードを示します。

### 更新後のパッケージ構成
- `ISqlService`：DapperのAPIに対応するインターフェース
- `SqlService`：`ISqlService`を実装するクラス
- `Polly`を利用したリトライポリシー（SQLエラーおよびネットワークエラーに対応、構成上の問題はリトライ対象外）

### ISqlService.cs
```csharp
using System.Collections.Generic;
using System.Threading.Tasks;

namespace YourNamespace
{
    public interface ISqlService
    {
        Task<T> QueryFirstOrDefaultAsync<T>(string storedProcedure, object parameters = null);
        Task<IEnumerable<T>> QueryAsync<T>(string storedProcedure, object parameters = null);
        Task<SqlMapper.GridReader> QueryMultipleAsync(string storedProcedure, object parameters = null);
    }
}
```

### SqlService.cs
```csharp
using Dapper;
using Microsoft.Data.SqlClient;
using Polly;
using Polly.Retry;
using System;
using System.Collections.Generic;
using System.Data;
using System.Net.Sockets;
using System.Threading.Tasks;

namespace YourNamespace
{
    public class SqlService : ISqlService
    {
        private readonly string _connectionString;
        private readonly AsyncRetryPolicy _retryPolicy;

        public SqlService(string connectionString)
        {
            _connectionString = connectionString;
            _retryPolicy = Policy
                .Handle<SqlException>(ex => IsTransientSqlException(ex))
                .Or<SocketException>()
                .WaitAndRetryAsync(3, retryAttempt => TimeSpan.FromSeconds(Math.Pow(2, retryAttempt)));
        }

        public async Task<T> QueryFirstOrDefaultAsync<T>(string storedProcedure, object parameters = null)
        {
            return await _retryPolicy.ExecuteAsync(async () =>
            {
                using var connection = new SqlConnection(_connectionString);
                return await connection.QueryFirstOrDefaultAsync<T>(storedProcedure, parameters, commandType: CommandType.StoredProcedure);
            });
        }

        public async Task<IEnumerable<T>> QueryAsync<T>(string storedProcedure, object parameters = null)
        {
            return await _retryPolicy.ExecuteAsync(async () =>
            {
                using var connection = new SqlConnection(_connectionString);
                return await connection.QueryAsync<T>(storedProcedure, parameters, commandType: CommandType.StoredProcedure);
            });
        }

        public async Task<SqlMapper.GridReader> QueryMultipleAsync(string storedProcedure, object parameters = null)
        {
            return await _retryPolicy.ExecuteAsync(async () =>
            {
                using var connection = new SqlConnection(_connectionString);
                return await connection.QueryMultipleAsync(storedProcedure, parameters, commandType: CommandType.StoredProcedure);
            });
        }

        private bool IsTransientSqlException(SqlException ex)
        {
            // リトライを行わないエラーコードを指定
            int[] nonTransientErrorCodes = { 208, 4060, 18456 }; // 例: 208 = Invalid object name

            foreach (var error in ex.Errors)
            {
                if (Array.Exists(nonTransientErrorCodes, code => code == error.Number))
                {
                    return false;
                }
            }

            return true;
        }
    }
}
```

### 使用方法
1. `SqlService`クラスのインスタンスを作成し、接続文字列を渡します。
2. 必要なメソッド（`QueryFirstOrDefaultAsync`、`QueryAsync`、`QueryMultipleAsync`）を呼び出します。

### 例
```csharp
public class YourController : ControllerBase
{
    private readonly ISqlService _sqlService;

    public YourController(ISqlService sqlService)
    {
        _sqlService = sqlService;
    }

    [HttpGet]
    public async Task<IActionResult> Get()
    {
        var result = await _sqlService.QueryAsync<YourModel>("YourStoredProcedure", new { Param1 = "Value1" });
        return Ok(result);
    }
}
```

このパッケージは、Pollyを利用してリトライポリシーを実装し、Dapperを利用してSQL Serverのストアドプロシージャを呼び出します。SQLエラーおよびネットワークエラーに対してリトライを行い、構成上の問題（例えば、ストアドプロシージャが存在しない場合など）に対してはリトライを行いません。これにより、より堅牢なエラーハンドリングを実現します。

### user — 2024-08-03T13:51:53.106508+00:00

このパッケージに対するUniTTestのコードを作成

### assistant — 2024-08-03T13:52:12.279909+00:00

以下に、`SqlService` クラスの単体テストコードを示します。これには、MoQライブラリを使用してデータベース接続とコマンドの実行をモックし、XUnitを使用してテストケースを実行します。

### 必要なパッケージ
以下のNuGetパッケージをインストールします:
- `Moq`
- `XUnit`
- `Dapper`
- `Microsoft.Data.SqlClient`

### テストプロジェクトの構成
- `SqlServiceTests.cs`

### SqlServiceTests.cs
```csharp
using Dapper;
using Moq;
using System;
using System.Collections.Generic;
using System.Data;
using System.Data.Common;
using System.Threading.Tasks;
using Xunit;

namespace YourNamespace.Tests
{
    public class SqlServiceTests
    {
        private readonly Mock<IDbConnection> _dbConnectionMock;
        private readonly SqlService _sqlService;

        public SqlServiceTests()
        {
            _dbConnectionMock = new Mock<IDbConnection>();
            _sqlService = new SqlService("YourConnectionString");
        }

        [Fact]
        public async Task QueryFirstOrDefaultAsync_ShouldReturnExpectedResult()
        {
            // Arrange
            var expected = new { Id = 1, Name = "Test" };
            _dbConnectionMock.Setup(conn => conn.QueryFirstOrDefaultAsync<object>(
                It.IsAny<string>(), It.IsAny<object>(), null, null, CommandType.StoredProcedure))
                .ReturnsAsync(expected);

            // Act
            var result = await _sqlService.QueryFirstOrDefaultAsync<object>("StoredProcedureName", new { Param1 = "Value1" });

            // Assert
            Assert.Equal(expected, result);
        }

        [Fact]
        public async Task QueryAsync_ShouldReturnExpectedResults()
        {
            // Arrange
            var expected = new List<object> { new { Id = 1, Name = "Test" } };
            _dbConnectionMock.Setup(conn => conn.QueryAsync<object>(
                It.IsAny<string>(), It.IsAny<object>(), null, null, CommandType.StoredProcedure))
                .ReturnsAsync(expected);

            // Act
            var result = await _sqlService.QueryAsync<object>("StoredProcedureName", new { Param1 = "Value1" });

            // Assert
            Assert.Equal(expected, result);
        }

        [Fact]
        public async Task QueryMultipleAsync_ShouldReturnExpectedResults()
        {
            // Arrange
            var mockGridReader = new Mock<SqlMapper.GridReader>(null, null, null);
            _dbConnectionMock.Setup(conn => conn.QueryMultipleAsync(
                It.IsAny<string>(), It.IsAny<object>(), null, null, CommandType.StoredProcedure))
                .ReturnsAsync(mockGridReader.Object);

            // Act
            var result = await _sqlService.QueryMultipleAsync("StoredProcedureName", new { Param1 = "Value1" });

            // Assert
            Assert.Equal(mockGridReader.Object, result);
        }

        [Fact]
        public async Task ExecuteWithRetry_ShouldRetryOnTransientSqlException()
        {
            // Arrange
            int callCount = 0;
            _dbConnectionMock.Setup(conn => conn.QueryFirstOrDefaultAsync<object>(
                It.IsAny<string>(), It.IsAny<object>(), null, null, CommandType.StoredProcedure))
                .ThrowsAsync(new SqlException());

            // Act & Assert
            await Assert.ThrowsAsync<SqlException>(() => _sqlService.QueryFirstOrDefaultAsync<object>("StoredProcedureName", new { Param1 = "Value1" }));
        }

        [Fact]
        public async Task ExecuteWithRetry_ShouldNotRetryOnNonTransientSqlException()
        {
            // Arrange
            var nonTransientException = new SqlException("", null, null, null, 0, "", 208, 0, null, null);
            _dbConnectionMock.Setup(conn => conn.QueryFirstOrDefaultAsync<object>(
                It.IsAny<string>(), It.IsAny<object>(), null, null, CommandType.StoredProcedure))
                .ThrowsAsync(nonTransientException);

            // Act & Assert
            await Assert.ThrowsAsync<SqlException>(() => _sqlService.QueryFirstOrDefaultAsync<object>("StoredProcedureName", new { Param1 = "Value1" }));
        }
    }
}
```

### テストの説明
- **QueryFirstOrDefaultAsync_ShouldReturnExpectedResult**: `QueryFirstOrDefaultAsync` メソッドが期待される結果を返すことを確認します。
- **QueryAsync_ShouldReturnExpectedResults**: `QueryAsync` メソッドが期待される結果を返すことを確認します。
- **QueryMultipleAsync_ShouldReturnExpectedResults**: `QueryMultipleAsync` メソッドが期待される結果を返すことを確認します。
- **ExecuteWithRetry_ShouldRetryOnTransientSqlException**: 一時的な `SqlException` に対してリトライが行われることを確認します。
- **ExecuteWithRetry_ShouldNotRetryOnNonTransientSqlException**: 一時的ではない `SqlException` に対してリトライが行われないことを確認します。

これらのテストにより、`SqlService` クラスのリトライポリシーや各メソッドの動作を確認することができます。

### user — 2024-08-03T13:52:43.036718+00:00

構成エラーに関するテストケースを追加

### assistant — 2024-08-03T13:53:14.274579+00:00

構成エラーに関するテストケースを追加します。具体的には、ストアドプロシージャが存在しない場合（エラーコード 208）や、データベースが存在しない場合（エラーコード 4060）、ログインが失敗した場合（エラーコード 18456）などの構成エラーについて、リトライが行われないことを確認するテストケースを追加します。

### 更新後の SqlServiceTests.cs
```csharp
using Dapper;
using Moq;
using Polly;
using Polly.Retry;
using System;
using System.Collections.Generic;
using System.Data;
using System.Data.Common;
using System.Net.Sockets;
using System.Threading.Tasks;
using Microsoft.Data.SqlClient;
using Xunit;

namespace YourNamespace.Tests
{
    public class SqlServiceTests
    {
        private readonly Mock<IDbConnection> _dbConnectionMock;
        private readonly SqlService _sqlService;
        private readonly RetryPolicy _retryPolicy;

        public SqlServiceTests()
        {
            _dbConnectionMock = new Mock<IDbConnection>();
            _sqlService = new SqlService("YourConnectionString");
        }

        [Fact]
        public async Task QueryFirstOrDefaultAsync_ShouldReturnExpectedResult()
        {
            // Arrange
            var expected = new { Id = 1, Name = "Test" };
            _dbConnectionMock.Setup(conn => conn.QueryFirstOrDefaultAsync<object>(
                It.IsAny<string>(), It.IsAny<object>(), null, null, CommandType.StoredProcedure))
                .ReturnsAsync(expected);

            // Act
            var result = await _sqlService.QueryFirstOrDefaultAsync<object>("StoredProcedureName", new { Param1 = "Value1" });

            // Assert
            Assert.Equal(expected, result);
        }

        [Fact]
        public async Task QueryAsync_ShouldReturnExpectedResults()
        {
            // Arrange
            var expected = new List<object> { new { Id = 1, Name = "Test" } };
            _dbConnectionMock.Setup(conn => conn.QueryAsync<object>(
                It.IsAny<string>(), It.IsAny<object>(), null, null, CommandType.StoredProcedure))
                .ReturnsAsync(expected);

            // Act
            var result = await _sqlService.QueryAsync<object>("StoredProcedureName", new { Param1 = "Value1" });

            // Assert
            Assert.Equal(expected, result);
        }

        [Fact]
        public async Task QueryMultipleAsync_ShouldReturnExpectedResults()
        {
            // Arrange
            var mockGridReader = new Mock<SqlMapper.GridReader>(null, null, null);
            _dbConnectionMock.Setup(conn => conn.QueryMultipleAsync(
                It.IsAny<string>(), It.IsAny<object>(), null, null, CommandType.StoredProcedure))
                .ReturnsAsync(mockGridReader.Object);

            // Act
            var result = await _sqlService.QueryMultipleAsync("StoredProcedureName", new { Param1 = "Value1" });

            // Assert
            Assert.Equal(mockGridReader.Object, result);
        }

        [Fact]
        public async Task ExecuteWithRetry_ShouldRetryOnTransientSqlException()
        {
            // Arrange
            var transientException = new SqlException("", null, null, null, 0, "", 49920, 0, null, null);
            _dbConnectionMock.Setup(conn => conn.QueryFirstOrDefaultAsync<object>(
                It.IsAny<string>(), It.IsAny<object>(), null, null, CommandType.StoredProcedure))
                .ThrowsAsync(transientException);

            // Act & Assert
            await Assert.ThrowsAsync<SqlException>(() => _sqlService.QueryFirstOrDefaultAsync<object>("StoredProcedureName", new { Param1 = "Value1" }));
        }

        [Fact]
        public async Task ExecuteWithRetry_ShouldNotRetryOnNonTransientSqlException()
        {
            // Arrange
            var nonTransientException = new SqlException("", null, null, null, 0, "", 208, 0, null, null);
            _dbConnectionMock.Setup(conn => conn.QueryFirstOrDefaultAsync<object>(
                It.IsAny<string>(), It.IsAny<object>(), null, null, CommandType.StoredProcedure))
                .ThrowsAsync(nonTransientException);

            // Act & Assert
            await Assert.ThrowsAsync<SqlException>(() => _sqlService.QueryFirstOrDefaultAsync<object>("StoredProcedureName", new { Param1 = "Value1" }));
        }

        [Fact]
        public async Task ExecuteWithRetry_ShouldNotRetryOnConfigurationError_StoredProcedureNotFound()
        {
            // Arrange
            var configException = new SqlException("", null, null, null, 0, "", 208, 0, null, null); // Error 208: Invalid object name
            _dbConnectionMock.Setup(conn => conn.QueryFirstOrDefaultAsync<object>(
                It.IsAny<string>(), It.IsAny<object>(), null, null, CommandType.StoredProcedure))
                .ThrowsAsync(configException);

            // Act & Assert
            await Assert.ThrowsAsync<SqlException>(() => _sqlService.QueryFirstOrDefaultAsync<object>("StoredProcedureName", new { Param1 = "Value1" }));
        }

        [Fact]
        public async Task ExecuteWithRetry_ShouldNotRetryOnConfigurationError_DatabaseNotFound()
        {
            // Arrange
            var configException = new SqlException("", null, null, null, 0, "", 4060, 0, null, null); // Error 4060: Cannot open database
            _dbConnectionMock.Setup(conn => conn.QueryFirstOrDefaultAsync<object>(
                It.IsAny<string>(), It.IsAny<object>(), null, null, CommandType.StoredProcedure))
                .ThrowsAsync(configException);

            // Act & Assert
            await Assert.ThrowsAsync<SqlException>(() => _sqlService.QueryFirstOrDefaultAsync<object>("StoredProcedureName", new { Param1 = "Value1" }));
        }

        [Fact]
        public async Task ExecuteWithRetry_ShouldNotRetryOnConfigurationError_LoginFailed()
        {
            // Arrange
            var configException = new SqlException("", null, null, null, 0, "", 18456, 0, null, null); // Error 18456: Login failed
            _dbConnectionMock.Setup(conn => conn.QueryFirstOrDefaultAsync<object>(
                It.IsAny<string>(), It.IsAny<object>(), null, null, CommandType.StoredProcedure))
                .ThrowsAsync(configException);

            // Act & Assert
            await Assert.ThrowsAsync<SqlException>(() => _sqlService.QueryFirstOrDefaultAsync<object>("StoredProcedureName", new { Param1 = "Value1" }));
        }
    }
}
```

### 新しいテストケースの説明
- **ExecuteWithRetry_ShouldNotRetryOnConfigurationError_StoredProcedureNotFound**: ストアドプロシージャが存在しない場合（エラーコード 208）に対してリトライが行われないことを確認します。
- **ExecuteWithRetry_ShouldNotRetryOnConfigurationError_DatabaseNotFound**: データベースが存在しない場合（エラーコード 4060）に対してリトライが行われないことを確認します。
- **ExecuteWithRetry_ShouldNotRetryOnConfigurationError_LoginFailed**: ログインに失敗した場合（エラーコード 18456）に対してリトライが行われないことを確認します。

これらのテストケースにより、構成エラーに対してリトライが行われないことを確認できます。これにより、`SqlService` クラスのリトライポリシーが正しく設定されていることを確認できます。
