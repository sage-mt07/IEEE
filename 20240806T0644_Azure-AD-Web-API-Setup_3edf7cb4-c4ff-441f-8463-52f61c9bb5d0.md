---
conversation_id: "3edf7cb4-c4ff-441f-8463-52f61c9bb5d0"
title: "Azure AD Web API Setup"
create_time: 1722926649.919168
update_time: 1722926958.512523
language_guess: "en"
num_messages: 11
part_index: 1
part_count: 1
---

### system — 2024-08-06T06:44:09.919168+00:00

_(empty)_

### user — 2024-08-06T06:44:09.926647+00:00

EntraIDの認証を利用するwebapiをazureでホストし、postmanでapiにアクセスする設定

### assistant — 2024-08-06T06:44:41.023493+00:00

_(empty)_

### assistant — 2024-08-06T06:44:41.023600+00:00

Azure Active Directory (Azure AD) を利用した認証を設定し、ASP.NET Core Web API を Azure にホストして、Postman から API にアクセスする手順は以下の通りです。

### 手順概要
1. **Azure AD アプリ登録**
2. **ASP.NET Core Web API の設定**
3. **Web API のデプロイ**
4. **Postman の設定**

### 1. Azure AD アプリ登録
#### Azure Portal での設定
1. **Azure Portal** にサインインします。
2. 左側のナビゲーションメニューから **Azure Active Directory** を選択します。
3. **アプリの登録** を選択し、**新規登録** をクリックします。
4. アプリケーション名を入力し、**リダイレクト URI** に `https://localhost:5001/signin-oidc` を入力します（開発環境の場合）。
5. **登録** をクリックします。
6. 登録が完了したら、**アプリケーション (クライアント) ID** と **ディレクトリ (テナント) ID** をメモしておきます。
7. **API のアクセス許可** セクションで **Microsoft Graph** から **User.Read** を追加します。
8. **証明書とシークレット** セクションで **新しいクライアント シークレット** を作成し、シークレットの値をメモしておきます。

### 2. ASP.NET Core Web API の設定
#### appsettings.json の設定
以下のように `appsettings.json` ファイルを設定します。

```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "Domain": "your_domain.onmicrosoft.com",
    "TenantId": "your_tenant_id",
    "ClientId": "your_client_id",
    "ClientSecret": "your_client_secret",
    "CallbackPath": "/signin-oidc",
    "Scopes": "user.read"
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

#### Startup.cs の設定
`Startup.cs` ファイルに以下のコードを追加します。

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
        services.AddAuthentication(AzureADDefaults.BearerAuthenticationScheme)
            .AddAzureADBearer(options => Configuration.Bind("AzureAd", options));

        services.AddControllers();
        services.AddAuthorization();
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
}
```

### 3. Web API のデプロイ
1. **Visual Studio** または **Visual Studio Code** を使用して、Web API プロジェクトを Azure にパブリッシュします。
2. Azure Portal で新しい **App Service** を作成し、デプロイを行います。

### 4. Postman の設定
#### 認証トークンの取得
1. **Postman** を開き、新しいリクエストを作成します。
2. **Authorization** タブで、**OAuth 2.0** を選択します。
3. **Get New Access Token** をクリックし、以下の情報を入力します。
   - Token Name: 任意の名前
   - Grant Type: Authorization Code
   - Callback URL: `https://localhost:5001/signin-oidc`
   - Auth URL: `https://login.microsoftonline.com/{your_tenant_id}/oauth2/v2.0/authorize`
   - Access Token URL: `https://login.microsoftonline.com/{your_tenant_id}/oauth2/v2.0/token`
   - Client ID: あなたのクライアント ID
   - Client Secret: あなたのクライアント シークレット
   - Scope: `https://graph.microsoft.com/.default`

4. **Request Token** をクリックし、認証フローを完了してアクセストークンを取得します。

#### API リクエストの送信
1. Postman で、新しいリクエストを作成し、URL に Azure にデプロイされた Web API のエンドポイントを入力します。
2. **Authorization** タブで、取得したアクセストークンを使用する設定にします。
3. **Send** をクリックして、API リクエストを送信します。

以上で、Azure AD 認証を利用した ASP.NET Core Web API に Postman からアクセスできるようになります。

### user — 2024-08-06T06:45:31.363267+00:00

アプリはAzureのapp serviceにホストするものとする

### assistant — 2024-08-06T06:46:03.261259+00:00

AzureのApp ServiceにASP.NET Core Web APIをホストし、Azure AD認証を設定してPostmanからAPIにアクセスする方法について、具体的な手順を以下に示します。

### 手順概要
1. **Azure ADアプリ登録**
2. **ASP.NET Core Web APIの設定**
3. **Web APIのAzure App Serviceへのデプロイ**
4. **Postmanの設定**

### 1. Azure ADアプリ登録
#### Azure Portalでの設定
1. **Azure Portal**にサインインします。
2. 左側のナビゲーションメニューから**Azure Active Directory**を選択します。
3. **アプリの登録**を選択し、**新規登録**をクリックします。
4. アプリケーション名を入力し、**リダイレクトURI**に `https://{your-app-service-name}.azurewebsites.net/signin-oidc` を入力します（App Serviceにデプロイした場合のURL）。
5. **登録**をクリックします。
6. 登録が完了したら、**アプリケーション (クライアント) ID**と**ディレクトリ (テナント) ID**をメモしておきます。
7. **API のアクセス許可**セクションで**Microsoft Graph**から**User.Read**を追加します。
8. **証明書とシークレット**セクションで**新しいクライアント シークレット**を作成し、シークレットの値をメモしておきます。

### 2. ASP.NET Core Web APIの設定
#### appsettings.jsonの設定
以下のように `appsettings.json` ファイルを設定します。

```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "Domain": "your_domain.onmicrosoft.com",
    "TenantId": "your_tenant_id",
    "ClientId": "your_client_id",
    "ClientSecret": "your_client_secret",
    "CallbackPath": "/signin-oidc",
    "Scopes": "user.read"
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

#### Startup.csの設定
`Startup.cs` ファイルに以下のコードを追加します。

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
        services.AddAuthentication(AzureADDefaults.BearerAuthenticationScheme)
            .AddAzureADBearer(options => Configuration.Bind("AzureAd", options));

        services.AddControllers();
        services.AddAuthorization();
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
}
```

### 3. Web APIのAzure App Serviceへのデプロイ
1. **Visual Studio**または**Visual Studio Code**を使用して、Web APIプロジェクトをAzure App Serviceにパブリッシュします。
2. Azure Portalで新しい**App Service**を作成し、デプロイを行います。

### 4. Postmanの設定
#### 認証トークンの取得
1. **Postman**を開き、新しいリクエストを作成します。
2. **Authorization**タブで、**OAuth 2.0**を選択します。
3. **Get New Access Token**をクリックし、以下の情報を入力します。
   - Token Name: 任意の名前
   - Grant Type: Authorization Code
   - Callback URL: `https://{your-app-service-name}.azurewebsites.net/signin-oidc`
   - Auth URL: `https://login.microsoftonline.com/{your_tenant_id}/oauth2/v2.0/authorize`
   - Access Token URL: `https://login.microsoftonline.com/{your_tenant_id}/oauth2/v2.0/token`
   - Client ID: あなたのクライアントID
   - Client Secret: あなたのクライアントシークレット
   - Scope: `https://graph.microsoft.com/.default`

4. **Request Token**をクリックし、認証フローを完了してアクセストークンを取得します。

#### APIリクエストの送信
1. Postmanで、新しいリクエストを作成し、URLにAzureにデプロイされたWeb APIのエンドポイントを入力します。
2. **Authorization**タブで、取得したアクセストークンを使用する設定にします。
3. **Send**をクリックして、APIリクエストを送信します。

これで、Azure AD認証を利用したASP.NET Core Web APIにPostmanからアクセスできるようになります。

### user — 2024-08-06T06:47:00.916071+00:00

API のアクセス許可でアプリ固有のものを利用する方法

### assistant — 2024-08-06T06:47:37.493882+00:00

Azure ADでアプリ固有のAPIアクセス許可（スコープ）を利用するためには、以下の手順に従ってアプリ登録を設定し、APIおよびクライアントアプリケーションを構成します。

### 手順概要
1. **Azure ADアプリ登録**
2. **APIのスコープ定義**
3. **APIアクセス許可の構成**
4. **ASP.NET Core Web APIの設定**
5. **クライアントアプリケーションの構成**
6. **Postmanの設定**

### 1. Azure ADアプリ登録
#### Azure Portalでの設定
1. **Azure Portal**にサインインします。
2. 左側のナビゲーションメニューから**Azure Active Directory**を選択します。
3. **アプリの登録**を選択し、**新規登録**をクリックします。
4. アプリケーション名を入力し、**リダイレクトURI**に`https://{your-app-service-name}.azurewebsites.net/signin-oidc`を入力します。
5. **登録**をクリックします。
6. 登録が完了したら、**アプリケーション (クライアント) ID**と**ディレクトリ (テナント) ID**をメモしておきます。

### 2. APIのスコープ定義
1. 登録したアプリの設定ページで、左側のメニューから**Expose an API**を選択します。
2. **Add a scope**をクリックします。
3. **Application ID URI**を設定します（通常、自動生成されたものを使用します）。
4. **Add a scope**ダイアログで以下を設定します：
   - **Scope name**: 任意のスコープ名（例：`access_as_user`）
   - **Admin consent display name**: スコープの説明（例：`Access as a user`）
   - **Admin consent description**: スコープの詳細説明（例：`Allows the app to access API as a user`）
   - **State**: **Enabled**を選択
5. **Add scope**をクリックしてスコープを追加します。

### 3. APIアクセス許可の構成
1. **API permissions**タブを選択し、**Add a permission**をクリックします。
2. **My APIs**を選択し、先ほど登録したAPIアプリケーションを選択します。
3. **Delegated permissions**を選択し、先ほど定義したスコープ（例：`access_as_user`）にチェックを入れます。
4. **Add permissions**をクリックします。

### 4. ASP.NET Core Web APIの設定
#### appsettings.jsonの設定
以下のように `appsettings.json` ファイルを設定します。

```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "Domain": "your_domain.onmicrosoft.com",
    "TenantId": "your_tenant_id",
    "ClientId": "your_client_id",
    "ClientSecret": "your_client_secret",
    "CallbackPath": "/signin-oidc",
    "Scopes": "api://your_client_id/access_as_user"
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

#### Startup.csの設定
`Startup.cs` ファイルに以下のコードを追加します。

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
        services.AddAuthentication(AzureADDefaults.BearerAuthenticationScheme)
            .AddAzureADBearer(options => Configuration.Bind("AzureAd", options));

        services.AddControllers();
        services.AddAuthorization(options =>
        {
            options.AddPolicy("AccessAsUser", policy => policy.RequireClaim("scp", "access_as_user"));
        });
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
            endpoints.MapControllers()
                     .RequireAuthorization("AccessAsUser");
        });
    }
}
```

### 5. クライアントアプリケーションの構成
クライアントアプリケーション（ここではPostman）からAPIにアクセスするためには、アクセストークンを取得する必要があります。

### 6. Postmanの設定
#### 認証トークンの取得
1. **Postman**を開き、新しいリクエストを作成します。
2. **Authorization**タブで、**OAuth 2.0**を選択します。
3. **Get New Access Token**をクリックし、以下の情報を入力します。
   - Token Name: 任意の名前
   - Grant Type: Authorization Code
   - Callback URL: `https://{your-app-service-name}.azurewebsites.net/signin-oidc`
   - Auth URL: `https://login.microsoftonline.com/{your_tenant_id}/oauth2/v2.0/authorize`
   - Access Token URL: `https://login.microsoftonline.com/{your_tenant_id}/oauth2/v2.0/token`
   - Client ID: あなたのクライアントID
   - Client Secret: あなたのクライアントシークレット
   - Scope: `api://your_client_id/access_as_user`

4. **Request Token**をクリックし、認証フローを完了してアクセストークンを取得します。

#### APIリクエストの送信
1. Postmanで、新しいリクエストを作成し、URLにAzureにデプロイされたWeb APIのエンドポイントを入力します。
2. **Authorization**タブで、取得したアクセストークンを使用する設定にします。
3. **Send**をクリックして、APIリクエストを送信します。

これで、Azure AD認証を利用してアプリ固有のAPIアクセス許可を設定したASP.NET Core Web APIにPostmanからアクセスできるようになります。

### user — 2024-08-06T06:48:49.907528+00:00

invalid tokenとなる場合の解決策

### assistant — 2024-08-06T06:49:17.984242+00:00

アクセストークンが無効 ("invalid token") となる場合の解決策はいくつかあります。以下に、最も一般的な原因とその対処法をまとめます。

### 1. アプリケーション登録の設定確認
- **アプリケーションID (クライアントID)** と **クライアントシークレット** が正しいことを確認します。
- **ディレクトリ (テナント) ID** が正しいことを確認します。
- **APIのスコープ (scope)** が正しいことを確認します。`api://{client_id}/{scope_name}`の形式であることを確認してください。

### 2. トークンの取得設定の確認
Postmanの設定が正しいか確認します。
- **Authorization URL** と **Token URL** が正しいことを確認します。
- **Scope** が正しいことを確認します。スコープは `api://{client_id}/access_as_user` の形式であるべきです。
- **Client ID** と **Client Secret** が正しいことを確認します。

### 3. Web API の設定確認
- **appsettings.json** に正しい設定が含まれていることを確認します。
- **Startup.cs** で正しく認証と認可が設定されていることを確認します。

### 4. API エンドポイントの検証
APIエンドポイントに対してアクセストークンが適切に送信されていることを確認します。
- Postmanで**Authorization**タブの設定が正しいことを確認します。

### 5. トークンのデコードと確認
取得したトークンを [JWT.io](https://jwt.io/) などのツールを使用してデコードし、以下の項目を確認します。
- トークンの**audience (aud)** クレームが正しいこと (`api://{client_id}` と一致していること)。
- トークンの**scope** クレームに期待するスコープが含まれていること。

### 6. トークンの期限
- トークンの有効期限が切れていないことを確認します。

### 具体的な手順
#### 1. appsettings.jsonの設定
```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "Domain": "your_domain.onmicrosoft.com",
    "TenantId": "your_tenant_id",
    "ClientId": "your_client_id",
    "ClientSecret": "your_client_secret",
    "CallbackPath": "/signin-oidc",
    "Scopes": "api://your_client_id/access_as_user"
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

#### 2. Startup.csの設定
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
        services.AddAuthentication(AzureADDefaults.BearerAuthenticationScheme)
            .AddAzureADBearer(options => Configuration.Bind("AzureAd", options));

        services.AddControllers();
        services.AddAuthorization(options =>
        {
            options.AddPolicy("AccessAsUser", policy => policy.RequireClaim("scp", "access_as_user"));
        });
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
            endpoints.MapControllers()
                     .RequireAuthorization("AccessAsUser");
        });
    }
}
```

#### 3. Postmanの設定
- **Authorization** タブで **OAuth 2.0** を選択し、**Get New Access Token** をクリックします。
- 必要な情報を入力し、トークンを取得します。

#### 4. トークンのデコード
- 取得したトークンを [JWT.io](https://jwt.io/) でデコードし、内容を確認します。

#### 5. トラブルシューティングのためのログの確認
- APIのログを確認して、どの段階で問題が発生しているか特定します。

### 追加の検証
- Azure AD ポータルでアプリケーションの**APIのアクセス許可**が正しく設定されているか確認します。必要なアクセス許可に対する管理者の同意が与えられていることも確認します。
- Azure AD ポータルの**ダイアグノスティック設定**を有効にして、より詳細なログ情報を取得します。

これらの手順を踏むことで、アクセストークンが無効になる原因を特定し、解決することができます。
