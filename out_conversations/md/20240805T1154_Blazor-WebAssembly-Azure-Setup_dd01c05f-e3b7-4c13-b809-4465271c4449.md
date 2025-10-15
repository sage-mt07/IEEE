---
conversation_id: "dd01c05f-e3b7-4c13-b809-4465271c4449"
title: "Blazor WebAssembly Azure Setup"
create_time: 1722858884.349219
update_time: 1722918504.833749
language_guess: "en"
num_messages: 35
part_index: 1
part_count: 1
---

### system — 2024-08-05T11:54:44.349219+00:00

_(empty)_

### user — 2024-08-05T11:54:44.353506+00:00

Blazor webassemblyとwebapiを同梱したサービスをapp service（linux)でpodでホスティングし、それに対してAzure Testを行う構成を示せ
webapiはEntra IDを利用している

### assistant — 2024-08-05T11:55:27.297107+00:00

_(empty)_

### assistant — 2024-08-05T11:55:27.297181+00:00

Blazor WebAssembly と WebAPI を同梱したサービスを Azure App Service（Linux）でホスティングし、Azure Test を行う構成を示すための手順を以下に示します。この構成では、WebAPI は Entra ID（旧称 Azure AD）を利用しています。

### 1. プロジェクト構成
- **Blazor WebAssembly プロジェクト**
- **ASP.NET Core WebAPI プロジェクト**
- **Azure App Service (Linux)**
- **Azure Test Plans**

### 2. プロジェクトの設定

#### Blazor WebAssembly プロジェクト
Blazor WebAssembly プロジェクトにおいて、Azure AD 認証を設定します。

1. **appsettings.json**
    ```json
    {
      "AzureAd": {
        "Authority": "https://login.microsoftonline.com/{TenantId}",
        "ClientId": "{ClientId}",
        "ValidateAuthority": true
      }
    }
    ```

2. **Program.cs**
    ```csharp
    builder.Services.AddMsalAuthentication(options =>
    {
        builder.Configuration.Bind("AzureAd", options.ProviderOptions.Authentication);
        options.ProviderOptions.DefaultAccessTokenScopes.Add("api://{ApiClientId}/access_as_user");
    });
    ```

#### ASP.NET Core WebAPI プロジェクト
WebAPI プロジェクトにおいても、Azure AD 認証を設定します。

1. **appsettings.json**
    ```json
    {
      "AzureAd": {
        "Instance": "https://login.microsoftonline.com/",
        "Domain": "{YourDomain}",
        "TenantId": "{TenantId}",
        "ClientId": "{ApiClientId}",
        "ClientSecret": "{ClientSecret}",
        "Audience": "api://{ApiClientId}"
      }
    }
    ```

2. **Startup.cs**
    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
            .AddMicrosoftIdentityWebApi(options =>
            {
                Configuration.Bind("AzureAd", options);
                options.TokenValidationParameters.NameClaimType = "name";
            },
            options => { Configuration.Bind("AzureAd", options); });

        services.AddControllers();
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }

        app.UseHttpsRedirection();
        app.UseRouting();
        app.UseAuthentication();
        app.UseAuthorization();
        app.UseEndpoints(endpoints =>
        {
            endpoints.MapControllers();
        });
    }
    ```

### 3. Azure App Service にデプロイ

1. **Azure App Service の作成**
   - Azure Portal で新しい Linux ベースの Azure App Service を作成します。
   - 作成した App Service に Blazor WebAssembly と WebAPI プロジェクトをデプロイします。

2. **GitHub Actions または Azure Pipelines の設定**
   - CI/CD パイプラインを設定し、Azure App Service に自動デプロイを行います。

### 4. Azure Test Plans の設定

1. **Azure DevOps プロジェクトの作成**
   - Azure DevOps で新しいプロジェクトを作成します。

2. **Test Plan の作成**
   - Azure Test Plans で新しいテストプランを作成します。
   - テストケースを定義し、エンドツーエンドのテストを設定します。

3. **テストの実行**
   - テストを実行し、Blazor WebAssembly アプリと WebAPI のエンドポイントが正常に動作することを確認します。

### 5. 図による構成の可視化
以下の図は、構成の概要を示します。

```
+-----------------------------+
|         Azure AD            |
|     (Entra ID)              |
+-------------+---------------+
              |
              v
+-------------+---------------+
|     Azure App Service       |
|      (Linux)                |
|                             |
|  +------------+             |
|  |  Blazor    |             |
|  | WebAssembly|             |
|  +------------+             |
|  +------------+             |
|  |  WebAPI    |             |
|  +------------+             |
+-----------------------------+
              |
              v
+-------------+---------------+
|     Azure Test Plans        |
+-----------------------------+
```

### 6. 追加の設定と注意事項
- **エンドポイントの設定**:
  - Blazor WebAssembly から WebAPI へのエンドポイント URL を適切に設定する。
- **CORS の設定**:
  - WebAPI の CORS 設定を行い、Blazor WebAssembly からのリクエストを許可する。
- **ロギング**:
  - Azure App Service におけるロギングの設定を行い、問題発生時のデバッグを容易にする。

以上の手順に従って、Blazor WebAssembly と WebAPI を同梱したサービスを Azure App Service（Linux）でホスティングし、Azure Test Plans を使用してテストを行う構成を設定できます。

### user — 2024-08-05T11:55:41.362176+00:00

Azure App Service (Linux)はコンテナを利用する

### assistant — 2024-08-05T11:56:32.406069+00:00

Azure App Service (Linux) をコンテナを利用してホスティングする場合の構成手順を示します。この構成では、Blazor WebAssembly と WebAPI を同梱し、WebAPI には Entra ID（旧称 Azure AD）を利用しています。

### 1. プロジェクト構成
- **Blazor WebAssembly プロジェクト**
- **ASP.NET Core WebAPI プロジェクト**
- **Docker コンテナ**
- **Azure App Service (Linux)**
- **Azure Test Plans**

### 2. プロジェクトの Docker 化

#### Dockerfile の作成
Blazor WebAssembly と WebAPI プロジェクトをコンテナ化するために、以下のような Dockerfile を作成します。

**Blazor WebAssembly プロジェクトの Dockerfile**
```Dockerfile
# Stage 1: Build
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["BlazorApp/BlazorApp.csproj", "BlazorApp/"]
RUN dotnet restore "BlazorApp/BlazorApp.csproj"
COPY . .
WORKDIR "/src/BlazorApp"
RUN dotnet build "BlazorApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlazorApp.csproj" -c Release -o /app/publish

# Stage 2: Final
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlazorApp.dll"]
```

**WebAPI プロジェクトの Dockerfile**
```Dockerfile
# Stage 1: Build
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["WebAPI/WebAPI.csproj", "WebAPI/"]
RUN dotnet restore "WebAPI/WebAPI.csproj"
COPY . .
WORKDIR "/src/WebAPI"
RUN dotnet build "WebAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebAPI.csproj" -c Release -o /app/publish

# Stage 2: Final
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebAPI.dll"]
```

### 3. Docker Compose の設定

Blazor WebAssembly と WebAPI を同じネットワークで動作させるために、`docker-compose.yml` を作成します。

```yaml
version: '3.4'

services:
  blazorapp:
    image: blazorapp:latest
    build:
      context: .
      dockerfile: BlazorApp/Dockerfile
    ports:
      - "8080:80"
    depends_on:
      - webapi

  webapi:
    image: webapi:latest
    build:
      context: .
      dockerfile: WebAPI/Dockerfile
    ports:
      - "5000:80"
```

### 4. Azure Container Registry へのプッシュ

1. **Azure Container Registry の作成**
   - Azure Portal で新しい Azure Container Registry (ACR) を作成します。

2. **Docker イメージのビルドとプッシュ**
   - ローカルで Docker イメージをビルドし、ACR にプッシュします。

```bash
# ローカルでビルド
docker-compose build

# ACR にログイン
az acr login --name <your-acr-name>

# イメージをタグ付け
docker tag blazorapp:latest <your-acr-name>.azurecr.io/blazorapp:latest
docker tag webapi:latest <your-acr-name>.azurecr.io/webapi:latest

# ACR にプッシュ
docker push <your-acr-name>.azurecr.io/blazorapp:latest
docker push <your-acr-name>.azurecr.io/webapi:latest
```

### 5. Azure App Service にデプロイ

1. **Azure App Service の作成**
   - Azure Portal で新しい Linux ベースの Azure App Service を作成します。
   - 作成時に Docker コンテナを使用するオプションを選択し、ACR からのイメージを指定します。

2. **App Service の構成**
   - Blazor WebAssembly と WebAPI の両方のイメージを指定し、環境変数やネットワーキングの設定を行います。

### 6. Azure Test Plans の設定

1. **Azure DevOps プロジェクトの作成**
   - Azure DevOps で新しいプロジェクトを作成します。

2. **Test Plan の作成**
   - Azure Test Plans で新しいテストプランを作成します。
   - テストケースを定義し、エンドツーエンドのテストを設定します。

3. **テストの実行**
   - テストを実行し、Blazor WebAssembly アプリと WebAPI のエンドポイントが正常に動作することを確認します。

### 7. 図による構成の可視化

```
+-----------------------------+
|         Azure AD            |
|     (Entra ID)              |
+-------------+---------------+
              |
              v
+-------------+---------------+
| Azure Container Registry    |
+-------------+---------------+
              |
              v
+-------------+---------------+
|     Azure App Service       |
|      (Linux)                |
|                             |
|  +------------+             |
|  |  Blazor    |             |
|  | WebAssembly|             |
|  +------------+             |
|  +------------+             |
|  |  WebAPI    |             |
|  +------------+             |
+-----------------------------+
              |
              v
+-------------+---------------+
|     Azure Test Plans        |
+-----------------------------+
```

この手順に従って、Blazor WebAssembly と WebAPI をコンテナを利用して Azure App Service（Linux）でホスティングし、Azure Test Plans を使用してテストを行う構成を設定できます。

### user — 2024-08-05T11:56:35.853415+00:00

.netはnet8を利用する

### assistant — 2024-08-05T11:57:36.768587+00:00

Blazor WebAssembly と WebAPI を .NET 8 を使用してコンテナでホスティングし、Azure App Service (Linux) にデプロイする手順を示します。以下の手順に従ってください。

### 1. プロジェクトの準備

#### Blazor WebAssembly プロジェクトの作成
.NET 8 をターゲットにした Blazor WebAssembly プロジェクトを作成します。

```bash
dotnet new blazorwasm -o BlazorApp --framework net8.0
```

#### WebAPI プロジェクトの作成
.NET 8 をターゲットにした WebAPI プロジェクトを作成します。

```bash
dotnet new webapi -o WebAPI --framework net8.0
```

### 2. Azure AD 認証の設定

#### Blazor WebAssembly プロジェクト

1. **appsettings.json**
    ```json
    {
      "AzureAd": {
        "Authority": "https://login.microsoftonline.com/{TenantId}",
        "ClientId": "{ClientId}",
        "ValidateAuthority": true
      }
    }
    ```

2. **Program.cs**
    ```csharp
    builder.Services.AddMsalAuthentication(options =>
    {
        builder.Configuration.Bind("AzureAd", options.ProviderOptions.Authentication);
        options.ProviderOptions.DefaultAccessTokenScopes.Add("api://{ApiClientId}/access_as_user");
    });
    ```

#### WebAPI プロジェクト

1. **appsettings.json**
    ```json
    {
      "AzureAd": {
        "Instance": "https://login.microsoftonline.com/",
        "Domain": "{YourDomain}",
        "TenantId": "{TenantId}",
        "ClientId": "{ApiClientId}",
        "ClientSecret": "{ClientSecret}",
        "Audience": "api://{ApiClientId}"
      }
    }
    ```

2. **Program.cs**
    ```csharp
    var builder = WebApplication.CreateBuilder(args);

    builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
        .AddMicrosoftIdentityWebApi(options =>
        {
            builder.Configuration.Bind("AzureAd", options);
            options.TokenValidationParameters.NameClaimType = "name";
        },
        options => { builder.Configuration.Bind("AzureAd", options); });

    builder.Services.AddControllers();

    var app = builder.Build();

    if (app.Environment.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    app.UseHttpsRedirection();
    app.UseRouting();
    app.UseAuthentication();
    app.UseAuthorization();
    app.MapControllers();
    app.Run();
    ```

### 3. Docker 化

#### Blazor WebAssembly プロジェクトの Dockerfile

```Dockerfile
# Stage 1: Build
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["BlazorApp/BlazorApp.csproj", "BlazorApp/"]
RUN dotnet restore "BlazorApp/BlazorApp.csproj"
COPY . .
WORKDIR "/src/BlazorApp"
RUN dotnet build "BlazorApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlazorApp.csproj" -c Release -o /app/publish

# Stage 2: Final
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlazorApp.dll"]
```

#### WebAPI プロジェクトの Dockerfile

```Dockerfile
# Stage 1: Build
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["WebAPI/WebAPI.csproj", "WebAPI/"]
RUN dotnet restore "WebAPI/WebAPI.csproj"
COPY . .
WORKDIR "/src/WebAPI"
RUN dotnet build "WebAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebAPI.csproj" -c Release -o /app/publish

# Stage 2: Final
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebAPI.dll"]
```

### 4. Docker Compose の設定

```yaml
version: '3.4'

services:
  blazorapp:
    image: blazorapp:latest
    build:
      context: .
      dockerfile: BlazorApp/Dockerfile
    ports:
      - "8080:80"
    depends_on:
      - webapi

  webapi:
    image: webapi:latest
    build:
      context: .
      dockerfile: WebAPI/Dockerfile
    ports:
      - "5000:80"
```

### 5. Azure Container Registry へのプッシュ

1. **Azure Container Registry の作成**
   - Azure Portal で新しい Azure Container Registry (ACR) を作成します。

2. **Docker イメージのビルドとプッシュ**
   - ローカルで Docker イメージをビルドし、ACR にプッシュします。

```bash
# ローカルでビルド
docker-compose build

# ACR にログイン
az acr login --name <your-acr-name>

# イメージをタグ付け
docker tag blazorapp:latest <your-acr-name>.azurecr.io/blazorapp:latest
docker tag webapi:latest <your-acr-name>.azurecr.io/webapi:latest

# ACR にプッシュ
docker push <your-acr-name>.azurecr.io/blazorapp:latest
docker push <your-acr-name>.azurecr.io/webapi:latest
```

### 6. Azure App Service にデプロイ

1. **Azure App Service の作成**
   - Azure Portal で新しい Linux ベースの Azure App Service を作成します。
   - 作成時に Docker コンテナを使用するオプションを選択し、ACR からのイメージを指定します。

2. **App Service の構成**
   - Blazor WebAssembly と WebAPI の両方のイメージを指定し、環境変数やネットワーキングの設定を行います。

### 7. Azure Test Plans の設定

1. **Azure DevOps プロジェクトの作成**
   - Azure DevOps で新しいプロジェクトを作成します。

2. **Test Plan の作成**
   - Azure Test Plans で新しいテストプランを作成します。
   - テストケースを定義し、エンドツーエンドのテストを設定します。

3. **テストの実行**
   - テストを実行し、Blazor WebAssembly アプリと WebAPI のエンドポイントが正常に動作することを確認します。

### 8. 図による構成の可視化

```
+-----------------------------+
|         Azure AD            |
|     (Entra ID)              |
+-------------+---------------+
              |
              v
+-------------+---------------+
| Azure Container Registry    |
+-------------+---------------+
              |
              v
+-------------+---------------+
|     Azure App Service       |
|      (Linux)                |
|                             |
|  +------------+             |
|  |  Blazor    |             |
|  | WebAssembly|             |
|  +------------+             |
|  +------------+             |
|  |  WebAPI    |             |
|  +------------+             |
+-----------------------------+
              |
              v
+-------------+---------------+
|     Azure Test Plans        |
+-----------------------------+
```

この手順に従って、Blazor WebAssembly と WebAPI をコンテナを利用して .NET 8 で Azure App Service（Linux）にホスティングし、Azure Test Plans を使用してテストを行う構成を設定できます。

### user — 2024-08-05T11:58:34.108002+00:00

AppServiceへのデプロイはGithub Actionsを利用する

### assistant — 2024-08-05T11:59:39.918925+00:00

GitHub Actions を利用して、Blazor WebAssembly と WebAPI をコンテナ化して .NET 8 で Azure App Service (Linux) にデプロイする手順を示します。

### 1. プロジェクト準備

#### Blazor WebAssembly プロジェクトの作成
```bash
dotnet new blazorwasm -o BlazorApp --framework net8.0
```

#### WebAPI プロジェクトの作成
```bash
dotnet new webapi -o WebAPI --framework net8.0
```

### 2. Docker 化

#### Blazor WebAssembly プロジェクトの Dockerfile

```Dockerfile
# Stage 1: Build
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["BlazorApp/BlazorApp.csproj", "BlazorApp/"]
RUN dotnet restore "BlazorApp/BlazorApp.csproj"
COPY . .
WORKDIR "/src/BlazorApp"
RUN dotnet build "BlazorApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlazorApp.csproj" -c Release -o /app/publish

# Stage 2: Final
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlazorApp.dll"]
```

#### WebAPI プロジェクトの Dockerfile

```Dockerfile
# Stage 1: Build
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["WebAPI/WebAPI.csproj", "WebAPI/"]
RUN dotnet restore "WebAPI/WebAPI.csproj"
COPY . .
WORKDIR "/src/WebAPI"
RUN dotnet build "WebAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebAPI.csproj" -c Release -o /app/publish

# Stage 2: Final
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebAPI.dll"]
```

### 3. Docker Compose の設定

```yaml
version: '3.4'

services:
  blazorapp:
    image: blazorapp:latest
    build:
      context: .
      dockerfile: BlazorApp/Dockerfile
    ports:
      - "8080:80"
    depends_on:
      - webapi

  webapi:
    image: webapi:latest
    build:
      context: .
      dockerfile: WebAPI/Dockerfile
    ports:
      - "5000:80"
```

### 4. Azure Container Registry へのプッシュ

1. **Azure Container Registry の作成**
   - Azure Portal で新しい Azure Container Registry (ACR) を作成します。

2. **Docker イメージのビルドとプッシュ**

```bash
# ローカルでビルド
docker-compose build

# ACR にログイン
az acr login --name <your-acr-name>

# イメージをタグ付け
docker tag blazorapp:latest <your-acr-name>.azurecr.io/blazorapp:latest
docker tag webapi:latest <your-acr-name>.azurecr.io/webapi:latest

# ACR にプッシュ
docker push <your-acr-name>.azurecr.io/blazorapp:latest
docker push <your-acr-name>.azurecr.io/webapi:latest
```

### 5. GitHub Actions の設定

#### GitHub Actions ワークフローの作成
リポジトリのルートに `.github/workflows/deploy.yml` を作成します。

```yaml
name: Build and Deploy to Azure

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2

      - name: Log in to Azure Container Registry
        uses: azure/docker-login@v1
        with:
          login-server: <your-acr-name>.azurecr.io
          username: ${{ secrets.ACR_USERNAME }}
          password: ${{ secrets.ACR_PASSWORD }}

      - name: Build and push BlazorApp image
        run: |
          docker buildx build --push --tag <your-acr-name>.azurecr.io/blazorapp:latest -f BlazorApp/Dockerfile .

      - name: Build and push WebAPI image
        run: |
          docker buildx build --push --tag <your-acr-name>.azurecr.io/webapi:latest -f WebAPI/Dockerfile .

  deploy:
    runs-on: ubuntu-latest
    needs: build

    steps:
      - name: Azure Login
        uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}

      - name: Deploy to Azure Web App
        uses: azure/webapps-deploy@v2
        with:
          app-name: <your-app-service-name>
          images: |
            <your-acr-name>.azurecr.io/blazorapp:latest
            <your-acr-name>.azurecr.io/webapi:latest
```

### 6. Secrets の設定

GitHub リポジトリの Settings > Secrets and variables > Actions で、以下のシークレットを追加します。

- `ACR_USERNAME`: Azure Container Registry のユーザー名
- `ACR_PASSWORD`: Azure Container Registry のパスワード
- `AZURE_CREDENTIALS`: Azure サービスプリンシパルの資格情報。以下のコマンドで生成できます。

```bash
az ad sp create-for-rbac --name "myAppServicePrincipal" --role contributor --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group} --sdk-auth
```

上記コマンドの出力を `AZURE_CREDENTIALS` に設定します。

### 7. Azure App Service の設定

Azure Portal で App Service を作成し、以下の設定を行います。

- **Linux ベースの App Service を作成**。
- **Docker コンテナオプションを選択**し、ACR からイメージを取得するように設定します。
- **ブランチ保護ルール**を設定して、`main` ブランチへのプッシュ時に GitHub Actions ワークフローが実行されるようにします。

### 8. Azure Test Plans の設定

1. **Azure DevOps プロジェクトの作成**
   - Azure DevOps で新しいプロジェクトを作成します。

2. **Test Plan の作成**
   - Azure Test Plans で新しいテストプランを作成します。
   - テストケースを定義し、エンドツーエンドのテストを設定します。

3. **テストの実行**
   - テストを実行し、Blazor WebAssembly アプリと WebAPI のエンドポイントが正常に動作することを確認します。

### 9. 図による構成の可視化

```
+-----------------------------+
|         Azure AD            |
|     (Entra ID)              |
+-------------+---------------+
              |
              v
+-------------+---------------+
| Azure Container Registry    |
+-------------+---------------+
              |
              v
+-------------+---------------+
|     Azure App Service       |
|      (Linux)                |
|                             |
|  +------------+             |
|  |  Blazor    |             |
|  | WebAssembly|             |
|  +------------+             |
|  +------------+             |
|  |  WebAPI    |             |
|  +------------+             |
+-----------------------------+
              |
              v
+-------------+---------------+
|     Azure Test Plans        |
+-----------------------------+
```

以上の手順に従って、Blazor WebAssembly と WebAPI をコンテナを利用して .NET 8 で Azure App Service（Linux）にホスティングし、GitHub Actions を使用して自動デプロイを設定し、Azure Test Plans を使用してテストを行う構成を設定できます。

### user — 2024-08-05T12:00:13.647963+00:00

GitHub Actionsにテストの実行を含める

### assistant — 2024-08-05T12:00:50.971204+00:00

GitHub Actions にテストの実行を含めるための完全なワークフローを作成する手順を示します。このワークフローは、Blazor WebAssembly と WebAPI プロジェクトのビルド、Docker イメージのビルドとプッシュ、Azure App Service へのデプロイ、およびテストの実行を含みます。

### GitHub Actions ワークフローの作成

リポジトリのルートに `.github/workflows/deploy.yml` を作成します。

```yaml
name: Build, Test, and Deploy to Azure

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up .NET
        uses: actions/setup-dotnet@v3
        with:
          dotnet-version: '8.0.x'

      - name: Restore dependencies
        run: dotnet restore

      - name: Build
        run: dotnet build --configuration Release

      - name: Run tests
        run: dotnet test --configuration Release --no-build --verbosity normal

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2

      - name: Log in to Azure Container Registry
        uses: azure/docker-login@v1
        with:
          login-server: <your-acr-name>.azurecr.io
          username: ${{ secrets.ACR_USERNAME }}
          password: ${{ secrets.ACR_PASSWORD }}

      - name: Build and push BlazorApp image
        run: |
          docker buildx build --push --tag <your-acr-name>.azurecr.io/blazorapp:latest -f BlazorApp/Dockerfile .

      - name: Build and push WebAPI image
        run: |
          docker buildx build --push --tag <your-acr-name>.azurecr.io/webapi:latest -f WebAPI/Dockerfile .

  deploy:
    runs-on: ubuntu-latest
    needs: build

    steps:
      - name: Azure Login
        uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}

      - name: Deploy to Azure Web App
        uses: azure/webapps-deploy@v2
        with:
          app-name: <your-app-service-name>
          images: |
            <your-acr-name>.azurecr.io/blazorapp:latest
            <your-acr-name>.azurecr.io/webapi:latest
```

### 追加の手順

1. **Secrets の設定**
   - GitHub リポジトリの Settings > Secrets and variables > Actions で以下のシークレットを追加します。
     - `ACR_USERNAME`: Azure Container Registry のユーザー名
     - `ACR_PASSWORD`: Azure Container Registry のパスワード
     - `AZURE_CREDENTIALS`: Azure サービスプリンシパルの資格情報。以下のコマンドで生成できます。

     ```bash
     az ad sp create-for-rbac --name "myAppServicePrincipal" --role contributor --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group} --sdk-auth
     ```

     上記コマンドの出力を `AZURE_CREDENTIALS` に設定します。

2. **Azure App Service の設定**
   - Azure Portal で App Service を作成し、以下の設定を行います。
     - **Linux ベースの App Service を作成**。
     - **Docker コンテナオプションを選択**し、ACR からイメージを取得するように設定します。

### ワークフローの内容の詳細

1. **ビルドステップ**
   - リポジトリのコードをチェックアウトし、.NET 環境を設定します。
   - 依存関係を復元し、プロジェクトをビルドします。
   - ビルド後、単体テストを実行します。

2. **Docker イメージのビルドとプッシュ**
   - Docker Buildx を設定し、Azure Container Registry にログインします。
   - BlazorApp と WebAPI の Docker イメージをビルドし、ACR にプッシュします。

3. **デプロイステップ**
   - Azure にログインし、Azure Web App にイメージをデプロイします。

このワークフローにより、コードのプッシュ時に自動的にビルド、テスト、Docker イメージのビルドとプッシュ、そして Azure App Service へのデプロイが行われます。

### user — 2024-08-05T12:01:38.774681+00:00

Azure Testではwebapiのテストを想定している。簡易にテストシナリオを作成する方法

### assistant — 2024-08-05T12:02:27.081744+00:00

Azure Test Plans を使用して WebAPI のテストを自動化する方法として、GitHub Actions ワークフローにテストの実行を含める構成を示します。以下の手順で簡易なテストシナリオを作成し、GitHub Actions で実行する方法を説明します。

### 1. API テストシナリオの作成

まず、WebAPI のエンドポイントをテストするための簡単なテストシナリオを作成します。これには、[Postman](https://www.postman.com/) を使用してテストコレクションを作成し、それを [Newman](https://github.com/postmanlabs/newman) で実行する方法が便利です。

#### Postman コレクションの作成

1. **Postman で新しいコレクションを作成**:
   - Postman を開き、「Collections」をクリックして「New Collection」を作成します。
   - コレクションに名前を付け、WebAPI のエンドポイントに対するリクエストを追加します。

2. **リクエストの設定**:
   - 各エンドポイントに対するテストリクエストを追加します（GET, POST, PUT, DELETE など）。
   - 必要に応じてリクエストの認証ヘッダーやボディを設定します。

3. **テストスクリプトの追加**:
   - 各リクエストに対してテストスクリプトを追加し、期待するレスポンスを検証します。
   - 例: ステータスコードが 200 であることを確認するスクリプト
     ```javascript
     pm.test("Status code is 200", function () {
         pm.response.to.have.status(200);
     });
     ```

4. **コレクションのエクスポート**:
   - 完成したコレクションをエクスポートして、JSON ファイルとして保存します。

### 2. GitHub Actions ワークフローの設定

以下のように GitHub Actions ワークフローを設定し、Postman コレクションを使用して WebAPI のテストを実行します。

#### ワークフローの更新

リポジトリのルートにある `.github/workflows/deploy.yml` を以下のように更新します。

```yaml
name: Build, Test, and Deploy to Azure

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up .NET
        uses: actions/setup-dotnet@v3
        with:
          dotnet-version: '8.0.x'

      - name: Restore dependencies
        run: dotnet restore

      - name: Build
        run: dotnet build --configuration Release

      - name: Run unit tests
        run: dotnet test --configuration Release --no-build --verbosity normal

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2

      - name: Log in to Azure Container Registry
        uses: azure/docker-login@v1
        with:
          login-server: <your-acr-name>.azurecr.io
          username: ${{ secrets.ACR_USERNAME }}
          password: ${{ secrets.ACR_PASSWORD }}

      - name: Build and push BlazorApp image
        run: |
          docker buildx build --push --tag <your-acr-name>.azurecr.io/blazorapp:latest -f BlazorApp/Dockerfile .

      - name: Build and push WebAPI image
        run: |
          docker buildx build --push --tag <your-acr-name>.azurecr.io/webapi:latest -f WebAPI/Dockerfile .

  deploy:
    runs-on: ubuntu-latest
    needs: build

    steps:
      - name: Azure Login
        uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}

      - name: Deploy to Azure Web App
        uses: azure/webapps-deploy@v2
        with:
          app-name: <your-app-service-name>
          images: |
            <your-acr-name>.azurecr.io/blazorapp:latest
            <your-acr-name>.azurecr.io/webapi:latest

  post-deploy-test:
    runs-on: ubuntu-latest
    needs: deploy

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Install Newman
        run: npm install -g newman

      - name: Run API tests
        run: |
          newman run path/to/your/postman_collection.json \
            --env-var baseUrl=<your-api-base-url>
        env:
          TEST_ENVIRONMENT: production
```

### 3. Secrets の設定

GitHub リポジトリの Settings > Secrets and variables > Actions で以下のシークレットを追加します。

- `ACR_USERNAME`: Azure Container Registry のユーザー名
- `ACR_PASSWORD`: Azure Container Registry のパスワード
- `AZURE_CREDENTIALS`: Azure サービスプリンシパルの資格情報

### 4. Azure App Service の設定

Azure Portal で App Service を作成し、以下の設定を行います。

- **Linux ベースの App Service を作成**。
- **Docker コンテナオプションを選択**し、ACR からイメージを取得するように設定します。

### 5. テストの実行

GitHub Actions がトリガーされると、以下のステップが実行されます。

1. コードのチェックアウト
2. .NET 環境のセットアップとビルド
3. 単体テストの実行
4. Docker イメージのビルドと ACR へのプッシュ
5. Azure App Service へのデプロイ
6. Postman コレクションを使用した API テストの実行

これにより、GitHub Actions で自動的にビルド、テスト、デプロイが行われ、デプロイ後に API テストが実行されます。

### user — 2024-08-05T12:03:29.013254+00:00

jmeterは利用できるのか

### assistant — 2024-08-05T12:04:18.431734+00:00

はい、GitHub Actions と Apache JMeter を使用して WebAPI のパフォーマンステストを実行することができます。以下に、JMeter を使用して WebAPI のテストを実行するための手順を示します。

### 1. JMeter テスト計画の作成

1. **JMeter をインストール**:
   - [JMeter](https://jmeter.apache.org/download_jmeter.cgi) をダウンロードしてインストールします。

2. **テスト計画の作成**:
   - JMeter を起動し、新しいテスト計画を作成します。
   - テスト計画に Thread Group を追加し、リクエストの数や間隔などを設定します。
   - Thread Group に HTTP Request Sampler を追加し、テストする API エンドポイントの詳細を設定します。
   - 必要に応じて、リスナー（例: View Results Tree, Summary Report）を追加して、結果を確認します。

3. **テスト計画の保存**:
   - 完成したテスト計画を `.jmx` ファイルとして保存します。

### 2. GitHub Actions ワークフローの設定

以下のように GitHub Actions ワークフローを設定し、JMeter を使用して WebAPI のテストを実行します。

#### ワークフローの作成

リポジトリのルートに `.github/workflows/deploy.yml` を作成します。

```yaml
name: Build, Test, and Deploy to Azure

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up .NET
        uses: actions/setup-dotnet@v3
        with:
          dotnet-version: '8.0.x'

      - name: Restore dependencies
        run: dotnet restore

      - name: Build
        run: dotnet build --configuration Release

      - name: Run unit tests
        run: dotnet test --configuration Release --no-build --verbosity normal

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2

      - name: Log in to Azure Container Registry
        uses: azure/docker-login@v1
        with:
          login-server: <your-acr-name>.azurecr.io
          username: ${{ secrets.ACR_USERNAME }}
          password: ${{ secrets.ACR_PASSWORD }}

      - name: Build and push BlazorApp image
        run: |
          docker buildx build --push --tag <your-acr-name>.azurecr.io/blazorapp:latest -f BlazorApp/Dockerfile .

      - name: Build and push WebAPI image
        run: |
          docker buildx build --push --tag <your-acr-name>.azurecr.io/webapi:latest -f WebAPI/Dockerfile .

  deploy:
    runs-on: ubuntu-latest
    needs: build

    steps:
      - name: Azure Login
        uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}

      - name: Deploy to Azure Web App
        uses: azure/webapps-deploy@v2
        with:
          app-name: <your-app-service-name>
          images: |
            <your-acr-name>.azurecr.io/blazorapp:latest
            <your-acr-name>.azurecr.io/webapi:latest

  post-deploy-test:
    runs-on: ubuntu-latest
    needs: deploy

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Install JMeter
        run: |
          sudo apt-get update
          sudo apt-get install -y jmeter

      - name: Run JMeter tests
        run: |
          jmeter -n -t path/to/your/testplan.jmx -l results.jtl -JbaseUrl=<your-api-base-url>

      - name: Upload test results
        uses: actions/upload-artifact@v3
        with:
          name: jmeter-results
          path: results.jtl
```

### 3. Secrets の設定

GitHub リポジトリの Settings > Secrets and variables > Actions で以下のシークレットを追加します。

- `ACR_USERNAME`: Azure Container Registry のユーザー名
- `ACR_PASSWORD`: Azure Container Registry のパスワード
- `AZURE_CREDENTIALS`: Azure サービスプリンシパルの資格情報

### 4. Azure App Service の設定

Azure Portal で App Service を作成し、以下の設定を行います。

- **Linux ベースの App Service を作成**。
- **Docker コンテナオプションを選択**し、ACR からイメージを取得するように設定します。

### 5. テストの実行

GitHub Actions がトリガーされると、以下のステップが実行されます。

1. コードのチェックアウト
2. .NET 環境のセットアップとビルド
3. 単体テストの実行
4. Docker イメージのビルドと ACR へのプッシュ
5. Azure App Service へのデプロイ
6. JMeter を使用した API テストの実行

これにより、GitHub Actions で自動的にビルド、テスト、デプロイが行われ、デプロイ後に JMeter を使用して API テストが実行されます。テスト結果は GitHub Actions のアーティファクトとしてアップロードされるため、後で確認できます。

### user — 2024-08-05T14:49:29.998616+00:00

システムのつながりをdraw.ioで示せ

### assistant — 2024-08-05T14:50:14.504808+00:00

以下は、Blazor WebAssembly と WebAPI をコンテナ化し、.NET 8 を使用して Azure App Service (Linux) にホスティングし、GitHub Actions を利用してデプロイとテストを行うシステム構成図を draw.io で示す方法です。

### 1. draw.io の起動
まず、[draw.io](https://www.draw.io/) を開いてください。

### 2. システム構成図の作成

1. **基本図形の配置**:
   - 左側の図形パレットから「長方形」や「円」を選択し、以下のコンポーネントを表す図形をキャンバスにドラッグします。

2. **コンポーネントの配置**:
   - **GitHub Actions**: CI/CD パイプラインを示す長方形を配置します。
   - **Azure Container Registry (ACR)**: コンテナレジストリを示す長方形を配置します。
   - **Azure App Service (Linux)**: ホスティングサービスを示す長方形を配置します。
   - **Blazor WebAssembly** と **WebAPI**: それぞれのサービスを示す長方形を配置します。
   - **JMeter**: テストツールを示す長方形を配置します。

3. **矢印で接続**:
   - 各コンポーネント間を矢印で接続して、データフローを示します。

### 3. コンポーネントの詳細

以下に、構成図の詳細を示します。

#### 1. GitHub Actions
- **役割**: コードのビルド、テスト、Docker イメージのビルドとプッシュ、Azure App Service へのデプロイ、JMeter テストの実行

#### 2. Azure Container Registry (ACR)
- **役割**: Docker イメージを格納するレジストリ

#### 3. Azure App Service (Linux)
- **役割**: Blazor WebAssembly と WebAPI をホスティングする Linux ベースのサービス

#### 4. Blazor WebAssembly
- **役割**: フロントエンドアプリケーション

#### 5. WebAPI
- **役割**: バックエンド API サービス

#### 6. JMeter
- **役割**: デプロイ後の WebAPI のパフォーマンステストを実行

### 4. システム構成図

以下はシステム構成図の例です。

```plaintext
+-----------------------------+
|         GitHub Actions      |
|                             |
|  +-----------------------+  |
|  |  1. Checkout code     |  |
|  +-----------------------+  |
|  |  2. Build and Test    |  |
|  +-----------------------+  |
|  |  3. Docker Build and  |  |
|  |     Push              |  |
|  +-----------------------+  |
|  |  4. Deploy to Azure   |  |
|  |     App Service       |  |
|  +-----------------------+  |
|  |  5. Run JMeter Tests  |  |
|  +-----------------------+  |
+-----------------------------+
              |
              v
+-------------+---------------+
| Azure Container Registry    |
|  (ACR)                      |
+-------------+---------------+
              |
              v
+-------------+---------------+
|     Azure App Service       |
|      (Linux)                |
|                             |
|  +------------+   +-------+ |
|  |  Blazor    |   | WebAPI| |
|  | WebAssembly|   |       | |
|  +------------+   +-------+ |
+-----------------------------+
              |
              v
+-------------+---------------+
|             JMeter          |
|  (Post-deploy Testing)      |
+-----------------------------+
```

### 5. 完成

この図を draw.io で再現するには、以下の手順に従ってください。

1. 左の図形パレットから「長方形」を選択し、GitHub Actions、ACR、Azure App Service、Blazor WebAssembly、WebAPI、JMeter を表す図形をキャンバスにドラッグします。
2. 各図形に対応するラベルを追加します。
3. 各図形を矢印で接続して、データフローを示します。

この構成図により、システムのつながりが視覚的に理解しやすくなります。

### user — 2024-08-06T02:40:16.006572+00:00

PostManを利用する場合のscopeの作り方

### assistant — 2024-08-06T02:40:43.064741+00:00

Postman を利用して Azure AD 認証を使用する WebAPI をテストする場合、適切なスコープを設定し、アクセストークンを取得して API リクエストに含める必要があります。以下は、その手順です。

### 1. Azure AD アプリの登録

まず、Azure AD にアプリケーションを登録し、必要なスコープと API パーミッションを設定します。

1. **Azure ポータルにサインイン**。
2. **Azure Active Directory** に移動し、「アプリの登録」を選択。
3. **新規登録**をクリックし、アプリケーションを登録。
4. アプリの「クライアント ID」と「テナント ID」を記録。
5. 「API のアクセス許可」に移動し、「API のアクセス許可を追加」をクリック。
6. 「My APIs」を選択し、対象の API を選択。
7. 適切なスコープ（例：`api://<client-id>/access_as_user`）を追加。
8. 「認証」タブでリダイレクト URI を設定（例：`https://oauth.pstmn.io/v1/callback`）。
9. 「証明書とシークレット」タブでクライアントシークレットを作成し、記録。

### 2. Postman の設定

Postman で Azure AD 認証を設定し、アクセストークンを取得します。

1. **Postman を開く**。
2. 新しいコレクションを作成し、そのコレクションの「認証」を設定。

#### 認証設定

1. **Type** を「OAuth 2.0」に設定。
2. **Add auth data to** を「Request Headers」に設定。
3. **Token Name** に任意の名前を入力。
4. **Grant Type** を「Authorization Code」に設定。
5. **Callback URL** に `https://oauth.pstmn.io/v1/callback` を入力。
6. **Auth URL** に以下を入力：
   ```
   https://login.microsoftonline.com/<テナント ID>/oauth2/v2.0/authorize
   ```
7. **Access Token URL** に以下を入力：
   ```
   https://login.microsoftonline.com/<テナント ID>/oauth2/v2.0/token
   ```
8. **Client ID** に Azure AD で取得したクライアント ID を入力。
9. **Client Secret** に Azure AD で取得したクライアントシークレットを入力。
10. **Scope** に以下を入力：
    ```
    api://<クライアント ID>/access_as_user
    ```
11. **State** は空欄のままでOK。
12. **Client Authentication** を「Send as Basic Auth header」に設定。

### 3. トークンの取得

1. **Get New Access Token** をクリック。
2. 認証プロセスが進み、アクセストークンが取得されます。
3. トークンが取得されると、Postman のリクエストに自動的に追加されます。

### 4. API リクエストの設定

1. **新しいリクエスト**を作成し、URL に API のエンドポイントを入力。
2. コレクションまたはリクエストの「認証」タブで、「Type」を「OAuth 2.0」に設定し、先ほど取得したトークンを使用するように設定。
3. リクエストを送信し、API のレスポンスを確認。

### 5. Postman スクリプトでスコープを追加する

アクセストークン取得の際にスコープを追加するための Postman スクリプトを設定します。

#### Pre-request Script

```javascript
pm.environment.set("tenantId", "<テナント ID>");
pm.environment.set("clientId", "<クライアント ID>");
pm.environment.set("clientSecret", "<クライアントシークレット>");
pm.environment.set("scope", "api://<クライアント ID>/access_as_user");
pm.environment.set("authUrl", `https://login.microsoftonline.com/${pm.environment.get("tenantId")}/oauth2/v2.0/token`);

const getTokenRequest = {
    url: pm.environment.get("authUrl"),
    method: 'POST',
    header: {
        'Content-Type': 'application/x-www-form-urlencoded'
    },
    body: {
        mode: 'urlencoded',
        urlencoded: [
            { key: 'grant_type', value: 'client_credentials' },
            { key: 'client_id', value: pm.environment.get("clientId") },
            { key: 'client_secret', value: pm.environment.get("clientSecret") },
            { key: 'scope', value: pm.environment.get("scope") }
        ]
    }
};

pm.sendRequest(getTokenRequest, (err, response) => {
    if (err) {
        console.log(err);
    } else {
        const jsonResponse = response.json();
        pm.environment.set("accessToken", jsonResponse.access_token);
    }
});
```

#### Authorization ヘッダーの設定

リクエストの「Headers」タブで以下のヘッダーを追加します。

```
Authorization: Bearer {{accessToken}}
```

### 6. テストの実行

これで Postman を使用して Azure AD 認証を使用した WebAPI のテストを実行できます。

1. コレクションまたはリクエストを選択し、設定されたトークンを使用してリクエストを送信。
2. API のレスポンスを確認し、必要に応じてテストスクリプトを追加して結果を検証。

この手順を通じて、Postman を使用して Azure AD 認証を介した WebAPI のテストを効果的に実行できます。

### user — 2024-08-06T02:45:25.008987+00:00

PostManの認証設定の場所は

### assistant — 2024-08-06T02:45:44.884958+00:00

Postman で Azure AD 認証を設定する具体的な手順は以下の通りです。

### 1. Postman を開く

まず、Postman を開いてください。

### 2. 新しいコレクションを作成

1. **Collections** タブをクリックします。
2. **New Collection** をクリックして、新しいコレクションを作成します。
3. コレクションに名前を付けます（例: "Azure AD Auth Collection"）。

### 3. 認証設定の追加

1. コレクション名の右側にある **...** をクリックし、「Edit」を選択します。
2. **Authorization** タブをクリックします。
3. 以下の設定を行います：

#### Authorization 設定

1. **Type** を「OAuth 2.0」に設定します。
2. **Add auth data to** を「Request Headers」に設定します。
3. **Token Name** に任意の名前を入力します（例: "AzureADToken"）。
4. **Grant Type** を「Authorization Code」に設定します。
5. **Callback URL** に `https://oauth.pstmn.io/v1/callback` を入力します。
6. **Auth URL** に以下を入力します：
   ```
   https://login.microsoftonline.com/<テナント ID>/oauth2/v2.0/authorize
   ```
7. **Access Token URL** に以下を入力します：
   ```
   https://login.microsoftonline.com/<テナント ID>/oauth2/v2.0/token
   ```
8. **Client ID** に Azure AD で取得したクライアント ID を入力します。
9. **Client Secret** に Azure AD で取得したクライアントシークレットを入力します。
10. **Scope** に以下を入力します：
    ```
    api://<クライアント ID>/access_as_user
    ```
11. **State** は空欄のままでOKです。
12. **Client Authentication** を「Send as Basic Auth header」に設定します。

### 4. トークンの取得

1. 設定が完了したら、**Get New Access Token** をクリックします。
2. ブラウザが開き、Azure AD のサインインページにリダイレクトされます。
3. 認証情報を入力してサインインします。
4. 認証が成功すると、Postman に戻り、アクセストークンが取得されます。
5. **Use Token** をクリックして、トークンをリクエストに使用します。

### 5. リクエストの作成

1. **Collections** タブで、先ほど作成したコレクションを選択します。
2. **Add Request** をクリックして、新しいリクエストを作成します。
3. リクエストに名前を付け、HTTP メソッドと URL を設定します。
4. **Authorization** タブで、「Inherit auth from parent」が選択されていることを確認します。これにより、コレクションで設定した認証情報がこのリクエストにも適用されます。

### 6. リクエストの送信

1. 必要なヘッダーやパラメータを設定したら、リクエストを送信します。
2. API のレスポンスを確認します。

この手順により、Postman で Azure AD 認証を設定し、WebAPI のリクエストにトークンを含めることができます。これにより、Azure AD を使用した API のテストを簡単に実行することができます。

### user — 2024-08-06T03:15:32.577493+00:00

API

### assistant — 2024-08-06T03:16:09.988188+00:00

Postman を使用して Azure AD 認証を通じて WebAPI をテストする場合の手順を詳述します。

### 1. Azure AD アプリの登録

まず、Azure AD にアプリケーションを登録し、必要なスコープと API パーミッションを設定します。

1. **Azure ポータルにサインイン**。
2. **Azure Active Directory** に移動し、「アプリの登録」を選択。
3. **新規登録**をクリックし、アプリケーションを登録。
4. アプリの「クライアント ID」と「テナント ID」を記録。
5. 「API のアクセス許可」に移動し、「API のアクセス許可を追加」をクリック。
6. 「My APIs」を選択し、対象の API を選択。
7. 適切なスコープ（例：`api://<client-id>/access_as_user`）を追加。
8. 「認証」タブでリダイレクト URI を設定（例：`https://oauth.pstmn.io/v1/callback`）。
9. 「証明書とシークレット」タブでクライアントシークレットを作成し、記録。

### 2. Postman の設定

Postman で Azure AD 認証を設定し、アクセストークンを取得します。

#### 認証設定

1. **Postman を開く**。
2. 新しいコレクションを作成し、そのコレクションの「Authorization」を設定します。
   - **Collections** タブをクリック。
   - **New Collection** をクリックして、新しいコレクションを作成します。
   - コレクションに名前を付けます（例: "Azure AD Auth Collection"）。

#### コレクションの認証設定

1. コレクション名の右側にある **...** をクリックし、「Edit」を選択します。
2. **Authorization** タブをクリックします。
3. 以下の設定を行います：

- **Type** を「OAuth 2.0」に設定。
- **Add auth data to** を「Request Headers」に設定。
- **Token Name** に任意の名前を入力（例: "AzureADToken"）。
- **Grant Type** を「Authorization Code」に設定。
- **Callback URL** に `https://oauth.pstmn.io/v1/callback` を入力。
- **Auth URL** に以下を入力：
  ```
  https://login.microsoftonline.com/<テナント ID>/oauth2/v2.0/authorize
  ```
- **Access Token URL** に以下を入力：
  ```
  https://login.microsoftonline.com/<テナント ID>/oauth2/v2.0/token
  ```
- **Client ID** に Azure AD で取得したクライアント ID を入力。
- **Client Secret** に Azure AD で取得したクライアントシークレットを入力。
- **Scope** に以下を入力：
  ```
  api://<クライアント ID>/access_as_user
  ```
- **State** は空欄のままでOK。
- **Client Authentication** を「Send as Basic Auth header」に設定。

### 3. トークンの取得

1. 設定が完了したら、**Get New Access Token** をクリック。
2. ブラウザが開き、Azure AD のサインインページにリダイレクトされます。
3. 認証情報を入力してサインイン。
4. 認証が成功すると、Postman に戻り、アクセストークンが取得されます。
5. **Use Token** をクリックして、トークンをリクエストに使用。

### 4. API リクエストの作成

1. **Collections** タブで、先ほど作成したコレクションを選択。
2. **Add Request** をクリックして、新しいリクエストを作成。
3. リクエストに名前を付け、HTTP メソッドと URL を設定。
4. **Authorization** タブで、「Inherit auth from parent」が選択されていることを確認。これにより、コレクションで設定した認証情報がこのリクエストにも適用されます。

### 5. リクエストの送信

1. 必要なヘッダーやパラメータを設定したら、リクエストを送信。
2. API のレスポンスを確認。

### 6. Postman スクリプトでスコープを追加する

#### Pre-request Script

```javascript
pm.environment.set("tenantId", "<テナント ID>");
pm.environment.set("clientId", "<クライアント ID>");
pm.environment.set("clientSecret", "<クライアントシークレット>");
pm.environment.set("scope", "api://<クライアント ID>/access_as_user");
pm.environment.set("authUrl", `https://login.microsoftonline.com/${pm.environment.get("tenantId")}/oauth2/v2.0/token`);

const getTokenRequest = {
    url: pm.environment.get("authUrl"),
    method: 'POST',
    header: {
        'Content-Type': 'application/x-www-form-urlencoded'
    },
    body: {
        mode: 'urlencoded',
        urlencoded: [
            { key: 'grant_type', value: 'client_credentials' },
            { key: 'client_id', value: pm.environment.get("clientId") },
            { key: 'client_secret', value: pm.environment.get("clientSecret") },
            { key: 'scope', value: pm.environment.get("scope") }
        ]
    }
};

pm.sendRequest(getTokenRequest, (err, response) => {
    if (err) {
        console.log(err);
    } else {
        const jsonResponse = response.json();
        pm.environment.set("accessToken", jsonResponse.access_token);
    }
});
```

#### Authorization ヘッダーの設定

リクエストの「Headers」タブで以下のヘッダーを追加します。

```
Authorization: Bearer {{accessToken}}
```

これで、Postman を使用して Azure AD 認証を設定し、WebAPI のテストを実行できます。各リクエストは認証トークンを含めて送信されるため、セキュアな API エンドポイントのテストが可能です。

### user — 2024-08-06T03:16:14.302752+00:00

PostManで使用する
APIのアクセス許可はアプリケーションのclientIDに対して設定が必用か？

### assistant — 2024-08-06T03:16:43.693464+00:00

PostmanでAzure ADを使ってWeb APIをテストする際、APIのアクセス許可を適切に設定するためには、アプリケーションのクライアントIDに対してアクセス許可を設定する必要があります。以下の手順でその設定を行います。

### 1. Azure AD アプリの登録

まず、Azure ADにアプリケーションを登録し、必要なスコープとAPIパーミッションを設定します。

1. **Azure ポータルにサインイン**。
2. **Azure Active Directory** に移動し、「アプリの登録」を選択。
3. **新規登録**をクリックし、アプリケーションを登録します。アプリ名やリダイレクトURI（例: `https://oauth.pstmn.io/v1/callback`）を入力します。
4. アプリケーションが登録されたら、「クライアント ID」と「テナント ID」を記録します。
5. 「API のアクセス許可」に移動し、「API のアクセス許可を追加」をクリックします。
6. 「My APIs」を選択し、対象のAPIを選択します。
7. 「委任された許可（Delegated Permissions）」または「アプリケーションの許可（Application Permissions）」を選択し、適切なスコープを追加します（例: `api://<client-id>/access_as_user`）。

### 2. Postman の設定

PostmanでAzure AD認証を設定し、アクセストークンを取得します。

#### 認証設定

1. **Postmanを開く**。
2. 新しいコレクションを作成し、そのコレクションの「Authorization」を設定します。
   - **Collections**タブをクリック。
   - **New Collection**をクリックして、新しいコレクションを作成します。
   - コレクションに名前を付けます（例: "Azure AD Auth Collection"）。

#### コレクションの認証設定

1. コレクション名の右側にある **...** をクリックし、「Edit」を選択します。
2. **Authorization** タブをクリックします。
3. 以下の設定を行います：

- **Type** を「OAuth 2.0」に設定。
- **Add auth data to** を「Request Headers」に設定。
- **Token Name** に任意の名前を入力（例: "AzureADToken"）。
- **Grant Type** を「Authorization Code」に設定。
- **Callback URL** に `https://oauth.pstmn.io/v1/callback` を入力。
- **Auth URL** に以下を入力：
  ```
  https://login.microsoftonline.com/<テナントID>/oauth2/v2.0/authorize
  ```
- **Access Token URL** に以下を入力：
  ```
  https://login.microsoftonline.com/<テナントID>/oauth2/v2.0/token
  ```
- **Client ID** にAzure ADで取得したクライアントIDを入力。
- **Client Secret** にAzure ADで取得したクライアントシークレットを入力。
- **Scope** に以下を入力：
  ```
  api://<クライアントID>/access_as_user
  ```
- **State** は空欄のままでOKです。
- **Client Authentication** を「Send as Basic Auth header」に設定します。

### 3. トークンの取得

1. 設定が完了したら、**Get New Access Token** をクリックします。
2. ブラウザが開き、Azure ADのサインインページにリダイレクトされます。
3. 認証情報を入力してサインインします。
4. 認証が成功すると、Postmanに戻り、アクセストークンが取得されます。
5. **Use Token** をクリックして、トークンをリクエストに使用します。

### 4. API リクエストの作成

1. **Collections** タブで、先ほど作成したコレクションを選択。
2. **Add Request** をクリックして、新しいリクエストを作成します。
3. リクエストに名前を付け、HTTP メソッドとURLを設定します。
4. **Authorization** タブで、「Inherit auth from parent」が選択されていることを確認します。これにより、コレクションで設定した認証情報がこのリクエストにも適用されます。

### 5. リクエストの送信

1. 必要なヘッダーやパラメータを設定したら、リクエストを送信します。
2. APIのレスポンスを確認します。

### 6. Postman スクリプトでスコープを追加する

#### Pre-request Script

```javascript
pm.environment.set("tenantId", "<テナント ID>");
pm.environment.set("clientId", "<クライアント ID>");
pm.environment.set("clientSecret", "<クライアントシークレット>");
pm.environment.set("scope", "api://<クライアント ID>/access_as_user");
pm.environment.set("authUrl", `https://login.microsoftonline.com/${pm.environment.get("tenantId")}/oauth2/v2.0/token`);

const getTokenRequest = {
    url: pm.environment.get("authUrl"),
    method: 'POST',
    header: {
        'Content-Type': 'application/x-www-form-urlencoded'
    },
    body: {
        mode: 'urlencoded',
        urlencoded: [
            { key: 'grant_type', value: 'client_credentials' },
            { key: 'client_id', value: pm.environment.get("clientId") },
            { key: 'client_secret', value: pm.environment.get("clientSecret") },
            { key: 'scope', value: pm.environment.get("scope") }
        ]
    }
};

pm.sendRequest(getTokenRequest, (err, response) => {
    if (err) {
        console.log(err);
    } else {
        const jsonResponse = response.json();
        pm.environment.set("accessToken", jsonResponse.access_token);
    }
});
```

#### Authorization ヘッダーの設定

リクエストの「Headers」タブで以下のヘッダーを追加します。

```
Authorization: Bearer {{accessToken}}
```

### 結論

Postmanを使用してAzure AD認証を通じてWebAPIをテストするためには、アプリケーションのクライアントIDに対してAPIのアクセス許可を適切に設定する必要があります。これにより、認証済みのアクセストークンを使用してセキュアなAPIエンドポイントのテストが可能となります。

### user — 2024-08-06T04:12:30.348270+00:00

リダイレクトURIはシングルページアプリケーションとして登録するのか

### assistant — 2024-08-06T04:12:59.612029+00:00

Azure AD にアプリケーションを登録する際に、Postman のリダイレクト URI を「シングルページアプリケーション」として登録する手順を示します。

### 1. Azure AD アプリの登録

1. **Azure ポータルにサインイン**。
2. **Azure Active Directory** に移動し、「アプリの登録」を選択。
3. **新規登録**をクリックし、アプリケーションを登録します。
   - 名前: 任意の名前を入力します。
   - サポートされているアカウントの種類: 適切なオプションを選択します（通常は「この組織ディレクトリ内のアカウントのみ」）。
   - リダイレクト URI (オプション): リダイレクト URI の追加はここでは行いません。後で設定します。

4. 登録が完了したら、「クライアント ID」と「テナント ID」を記録します。

### 2. リダイレクト URI の設定

1. **アプリケーションの概要ページ** から「認証」を選択します。
2. **プラットフォームの構成** で「シングルページアプリケーション (SPA)」を選択します。
3. **リダイレクト URI** に `https://oauth.pstmn.io/v1/callback` を追加します。
   - **リダイレクト URI** は、Postman がアクセストークンを取得するために使用する URL です。

### 3. API のアクセス許可を追加

1. 「API のアクセス許可」に移動し、「API のアクセス許可を追加」をクリックします。
2. 「My APIs」を選択し、対象の API を選択します。
3. 「委任された許可（Delegated Permissions）」を選択し、適切なスコープを追加します（例：`api://<client-id>/access_as_user`）。

### 4. クライアントシークレットの作成

1. 「証明書とシークレット」タブで「新しいクライアントシークレット」を作成します。
2. シークレットの説明と有効期限を設定し、**追加** をクリックします。
3. 作成されたクライアントシークレットを記録します。このシークレットは一度しか表示されないので、必ずコピーして保存してください。

### 5. Postman の設定

Postman で Azure AD 認証を設定し、アクセストークンを取得します。

#### コレクションの認証設定

1. Postman を開き、新しいコレクションを作成します。
   - **Collections** タブをクリック。
   - **New Collection** をクリックして、新しいコレクションを作成します。
   - コレクションに名前を付けます（例: "Azure AD Auth Collection"）。

2. コレクション名の右側にある **...** をクリックし、「Edit」を選択します。
3. **Authorization** タブをクリックし、以下の設定を行います：
   - **Type** を「OAuth 2.0」に設定。
   - **Add auth data to** を「Request Headers」に設定。
   - **Token Name** に任意の名前を入力（例: "AzureADToken"）。
   - **Grant Type** を「Authorization Code」に設定。
   - **Callback URL** に `https://oauth.pstmn.io/v1/callback` を入力。
   - **Auth URL** に以下を入力：
     ```
     https://login.microsoftonline.com/<テナント ID>/oauth2/v2.0/authorize
     ```
   - **Access Token URL** に以下を入力：
     ```
     https://login.microsoftonline.com/<テナント ID>/oauth2/v2.0/token
     ```
   - **Client ID** に Azure AD で取得したクライアント ID を入力。
   - **Client Secret** に Azure AD で取得したクライアントシークレットを入力。
   - **Scope** に以下を入力：
     ```
     api://<クライアント ID>/access_as_user
     ```
   - **State** は空欄のままでOKです。
   - **Client Authentication** を「Send as Basic Auth header」に設定します。

### 6. トークンの取得

1. 設定が完了したら、**Get New Access Token** をクリックします。
2. ブラウザが開き、Azure AD のサインインページにリダイレクトされます。
3. 認証情報を入力してサインインします。
4. 認証が成功すると、Postman に戻り、アクセストークンが取得されます。
5. **Use Token** をクリックして、トークンをリクエストに使用します。

### 7. API リクエストの作成

1. **Collections** タブで、先ほど作成したコレクションを選択します。
2. **Add Request** をクリックして、新しいリクエストを作成します。
3. リクエストに名前を付け、HTTP メソッドと URL を設定します。
4. **Authorization** タブで、「Inherit auth from parent」が選択されていることを確認します。これにより、コレクションで設定した認証情報がこのリクエストにも適用されます。

### 8. リクエストの送信

1. 必要なヘッダーやパラメータを設定したら、リクエストを送信します。
2. API のレスポンスを確認します。

以上の手順により、Postman を使用して Azure AD 認証を設定し、WebAPI のテストを行うことができます。シングルページアプリケーションとしてリダイレクト URI を設定することで、Postman での認証プロセスが正常に機能するようになります。

### user — 2024-08-06T04:21:59.674819+00:00

Proof key for code exchange is required for cross-origin authorization code redemption

### assistant — 2024-08-06T04:22:28.112487+00:00

Proof Key for Code Exchange (PKCE) を使用して、Postman で Azure AD を通じて WebAPI をテストするための手順を示します。PKCE は OAuth 2.0 フローをより安全にするためのメカニズムです。

### 1. Azure AD アプリの登録

まず、Azure AD にアプリケーションを登録し、必要なスコープと API パーミッションを設定します。

1. **Azure ポータルにサインイン**。
2. **Azure Active Directory** に移動し、「アプリの登録」を選択。
3. **新規登録**をクリックし、アプリケーションを登録します。
   - 名前: 任意の名前を入力します。
   - サポートされているアカウントの種類: 適切なオプションを選択します（通常は「この組織ディレクトリ内のアカウントのみ」）。
   - リダイレクト URI (オプション): リダイレクト URI の追加はここでは行いません。後で設定します。

4. 登録が完了したら、「クライアント ID」と「テナント ID」を記録します。

### 2. リダイレクト URI の設定

1. **アプリケーションの概要ページ** から「認証」を選択します。
2. **プラットフォームの構成** で「シングルページアプリケーション (SPA)」を選択します。
3. **リダイレクト URI** に `https://oauth.pstmn.io/v1/callback` を追加します。

### 3. API のアクセス許可を追加

1. 「API のアクセス許可」に移動し、「API のアクセス許可を追加」をクリックします。
2. 「My APIs」を選択し、対象の API を選択します。
3. 「委任された許可（Delegated Permissions）」を選択し、適切なスコープを追加します（例：`api://<client-id>/access_as_user`）。

### 4. クライアントシークレットの作成

1. 「証明書とシークレット」タブで「新しいクライアントシークレット」を作成します。
2. シークレットの説明と有効期限を設定し、**追加** をクリックします。
3. 作成されたクライアントシークレットを記録します。このシークレットは一度しか表示されないので、必ずコピーして保存してください。

### 5. Postman の設定

Postman で PKCE を使用して Azure AD 認証を設定し、アクセストークンを取得します。

#### コレクションの認証設定

1. Postman を開き、新しいコレクションを作成します。
   - **Collections** タブをクリック。
   - **New Collection** をクリックして、新しいコレクションを作成します。
   - コレクションに名前を付けます（例: "Azure AD Auth Collection"）。

2. コレクション名の右側にある **...** をクリックし、「Edit」を選択します。
3. **Authorization** タブをクリックし、以下の設定を行います：
   - **Type** を「OAuth 2.0」に設定。
   - **Add auth data to** を「Request Headers」に設定。
   - **Token Name** に任意の名前を入力（例: "AzureADToken"）。
   - **Grant Type** を「Authorization Code (With PKCE)」に設定。
   - **Callback URL** に `https://oauth.pstmn.io/v1/callback` を入力。
   - **Auth URL** に以下を入力：
     ```
     https://login.microsoftonline.com/<テナント ID>/oauth2/v2.0/authorize
     ```
   - **Access Token URL** に以下を入力：
     ```
     https://login.microsoftonline.com/<テナント ID>/oauth2/v2.0/token
     ```
   - **Client ID** に Azure AD で取得したクライアント ID を入力。
   - **Scope** に以下を入力：
     ```
     api://<クライアント ID>/access_as_user
     ```
   - **State** は空欄のままでOKです。
   - **Client Authentication** を「Send client credentials in body」に設定します。

### 6. トークンの取得

1. 設定が完了したら、**Get New Access Token** をクリックします。
2. ブラウザが開き、Azure AD のサインインページにリダイレクトされます。
3. 認証情報を入力してサインインします。
4. 認証が成功すると、Postman に戻り、アクセストークンが取得されます。
5. **Use Token** をクリックして、トークンをリクエストに使用します。

### 7. API リクエストの作成

1. **Collections** タブで、先ほど作成したコレクションを選択します。
2. **Add Request** をクリックして、新しいリクエストを作成します。
3. リクエストに名前を付け、HTTP メソッドと URL を設定します。
4. **Authorization** タブで、「Inherit auth from parent」が選択されていることを確認します。これにより、コレクションで設定した認証情報がこのリクエストにも適用されます。

### 8. リクエストの送信

1. 必要なヘッダーやパラメータを設定したら、リクエストを送信します。
2. API のレスポンスを確認します。

これで、Postman を使用して PKCE を使用した Azure AD 認証を通じて WebAPI をテストする準備が整いました。PKCE は OAuth 2.0 フローのセキュリティを強化するために使用され、特にシングルページアプリケーションやネイティブアプリケーションで有効です。

### user — 2024-08-06T04:26:29.184017+00:00

invalid_client Description: AADSTS700025: Client is public so neither 'client_assertion' nor 'client_secret' should be presented.

### assistant — 2024-08-06T04:26:54.625735+00:00

Azure AD の設定において、「Client is public so neither 'client_assertion' nor 'client_secret' should be presented」というエラーが表示される場合、これはクライアントアプリケーションが「パブリッククライアント」として登録されており、クライアントシークレットを使用することが許可されていないことを示しています。パブリッククライアントでは、クライアントシークレットを使用せずに PKCE (Proof Key for Code Exchange) を使用する必要があります。

以下は、Postman を使用して PKCE を利用して Azure AD 認証を設定する正しい方法です。

### 1. Azure AD アプリの登録

1. **Azure ポータルにサインイン**。
2. **Azure Active Directory** に移動し、「アプリの登録」を選択。
3. **新規登録**をクリックし、アプリケーションを登録します。
   - 名前: 任意の名前を入力します。
   - サポートされているアカウントの種類: 適切なオプションを選択します（通常は「この組織ディレクトリ内のアカウントのみ」）。
   - リダイレクト URI (オプション): 後で設定します。

4. 登録が完了したら、「クライアント ID」と「テナント ID」を記録します。

### 2. リダイレクト URI の設定

1. **アプリケーションの概要ページ** から「認証」を選択します。
2. **プラットフォームの構成** で「シングルページアプリケーション (SPA)」を選択します。
3. **リダイレクト URI** に `https://oauth.pstmn.io/v1/callback` を追加します。

### 3. API のアクセス許可を追加

1. 「API のアクセス許可」に移動し、「API のアクセス許可を追加」をクリックします。
2. 「My APIs」を選択し、対象の API を選択します。
3. 「委任された許可（Delegated Permissions）」を選択し、適切なスコープを追加します（例：`api://<client-id>/access_as_user`）。

### 4. Postman の設定

Postman で PKCE を使用して Azure AD 認証を設定し、アクセストークンを取得します。

#### コレクションの認証設定

1. Postman を開き、新しいコレクションを作成します。
   - **Collections** タブをクリック。
   - **New Collection** をクリックして、新しいコレクションを作成します。
   - コレクションに名前を付けます（例: "Azure AD Auth Collection"）。

2. コレクション名の右側にある **...** をクリックし、「Edit」を選択します。
3. **Authorization** タブをクリックし、以下の設定を行います：
   - **Type** を「OAuth 2.0」に設定。
   - **Add auth data to** を「Request Headers」に設定。
   - **Token Name** に任意の名前を入力（例: "AzureADToken"）。
   - **Grant Type** を「Authorization Code (With PKCE)」に設定。
   - **Callback URL** に `https://oauth.pstmn.io/v1/callback` を入力。
   - **Auth URL** に以下を入力：
     ```
     https://login.microsoftonline.com/<テナント ID>/oauth2/v2.0/authorize
     ```
   - **Access Token URL** に以下を入力：
     ```
     https://login.microsoftonline.com/<テナント ID>/oauth2/v2.0/token
     ```
   - **Client ID** に Azure AD で取得したクライアント ID を入力。
   - **Scope** に以下を入力：
     ```
     api://<クライアント ID>/access_as_user
     ```
   - **State** は空欄のままでOKです。
   - **Client Authentication** を「Send client credentials in body」に設定します。

### 5. トークンの取得

1. 設定が完了したら、**Get New Access Token** をクリックします。
2. ブラウザが開き、Azure AD のサインインページにリダイレクトされます。
3. 認証情報を入力してサインインします。
4. 認証が成功すると、Postman に戻り、アクセストークンが取得されます。
5. **Use Token** をクリックして、トークンをリクエストに使用します。

### 6. API リクエストの作成

1. **Collections** タブで、先ほど作成したコレクションを選択します。
2. **Add Request** をクリックして、新しいリクエストを作成します。
3. リクエストに名前を付け、HTTP メソッドと URL を設定します。
4. **Authorization** タブで、「Inherit auth from parent」が選択されていることを確認します。これにより、コレクションで設定した認証情報がこのリクエストにも適用されます。

### 7. リクエストの送信

1. 必要なヘッダーやパラメータを設定したら、リクエストを送信します。
2. API のレスポンスを確認します。

この手順に従うことで、Postman で PKCE を使用した Azure AD 認証を正しく設定し、WebAPI をテストすることができます。パブリッククライアントではクライアントシークレットを使用せずに、PKCE を使用することで安全に認証フローを実行できます。

### user — 2024-08-06T04:28:02.957217+00:00

ブラウザを開かずに認証をおこなう設定

### assistant — 2024-08-06T04:28:24.207395+00:00

ブラウザを開かずに Postman で Azure AD 認証を行う場合、クライアント資格情報の許可フロー (Client Credentials Flow) を使用します。このフローは、バックエンド サービスやデーモン アプリケーションの認証に適しており、ユーザーの関与なしにアクセストークンを取得できます。

### 1. Azure AD アプリの登録

まず、Azure AD にアプリケーションを登録し、必要なスコープと API パーミッションを設定します。

1. **Azure ポータルにサインイン**。
2. **Azure Active Directory** に移動し、「アプリの登録」を選択。
3. **新規登録**をクリックし、アプリケーションを登録します。
   - 名前: 任意の名前を入力します。
   - サポートされているアカウントの種類: 適切なオプションを選択します（通常は「この組織ディレクトリ内のアカウントのみ」）。
   - リダイレクト URI は設定しません（このフローでは不要です）。

4. 登録が完了したら、「クライアント ID」と「テナント ID」を記録します。
5. 「API のアクセス許可」に移動し、「API のアクセス許可を追加」をクリックします。
6. 「My APIs」を選択し、対象の API を選択します。
7. 「アプリケーションの許可（Application Permissions）」を選択し、適切なスコープを追加します（例：`api://<client-id>/access_as_user`）。
8. 「管理者の同意を与える」をクリックして、これらの許可を承認します。
9. 「証明書とシークレット」タブで「新しいクライアントシークレット」を作成し、記録します。このシークレットは後で使用します。

### 2. Postman の設定

Postman でクライアント資格情報フローを使用して Azure AD 認証を設定し、アクセストークンを取得します。

#### コレクションの認証設定

1. Postman を開き、新しいコレクションを作成します。
   - **Collections** タブをクリック。
   - **New Collection** をクリックして、新しいコレクションを作成します。
   - コレクションに名前を付けます（例: "Azure AD Client Credentials Flow"）。

2. コレクション名の右側にある **...** をクリックし、「Edit」を選択します。
3. **Authorization** タブをクリックし、以下の設定を行います：
   - **Type** を「OAuth 2.0」に設定。
   - **Add auth data to** を「Request Headers」に設定。
   - **Token Name** に任意の名前を入力（例: "AzureADToken"）。
   - **Grant Type** を「Client Credentials」に設定。
   - **Access Token URL** に以下を入力：
     ```
     https://login.microsoftonline.com/<テナント ID>/oauth2/v2.0/token
     ```
   - **Client ID** に Azure AD で取得したクライアント ID を入力。
   - **Client Secret** に Azure AD で取得したクライアントシークレットを入力。
   - **Scope** に以下を入力：
     ```
     api://<クライアント ID>/access_as_user
     ```
   - **Client Authentication** を「Send as Basic Auth header」に設定します。

### 3. トークンの取得

1. 設定が完了したら、**Get New Access Token** をクリックします。
2. Postman が自動的にアクセストークンを取得します。
3. **Use Token** をクリックして、トークンをリクエストに使用します。

### 4. API リクエストの作成

1. **Collections** タブで、先ほど作成したコレクションを選択します。
2. **Add Request** をクリックして、新しいリクエストを作成します。
3. リクエストに名前を付け、HTTP メソッドと URL を設定します。
4. **Authorization** タブで、「Inherit auth from parent」が選択されていることを確認します。これにより、コレクションで設定した認証情報がこのリクエストにも適用されます。

### 5. リクエストの送信

1. 必要なヘッダーやパラメータを設定したら、リクエストを送信します。
2. API のレスポンスを確認します。

この手順に従うことで、ブラウザを開かずに Postman で Azure AD を通じて WebAPI を認証することができます。クライアント資格情報フローを使用することで、バックエンド サービスやデーモン アプリケーションがユーザーの介入なしに安全に認証され、API にアクセスできるようになります。
