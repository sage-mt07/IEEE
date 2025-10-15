---
conversation_id: "50a7b02f-4203-4b0a-abba-6a12b9128b3e"
title: "Azure DevOps Pipeline Artifacts"
create_time: 1706077041.391417
update_time: 1706078800.310295
language_guess: "en"
num_messages: 8
part_index: 1
part_count: 1
---

### system — 2024-01-24T06:17:21.391417+00:00

_(empty)_

### user — 2024-01-24T06:17:21.392470+00:00

Azure devopsのpipelineでprerelease版のパッケージをartifactsへ格納する方法

### assistant — 2024-01-24T06:18:05.770657+00:00

Azure DevOpsのPipelinesを使用してprerelease版のパッケージをArtifactsに格納する方法には、いくつかのステップが必要です。以下に、一般的な手順を説明します。

### 1. ビルドパイプラインの設定

まず、ソースコードに対してビルドパイプラインを設定します。これには、ソースコードの取得、パッケージのビルド、テストの実行などが含まれます。

#### YAMLでの例

```yaml
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

steps:
- script: echo Building...
  displayName: 'Build step'

- script: echo Running tests...
  displayName: 'Test step'

- script: dotnet pack --configuration Release --output $(Build.ArtifactStagingDirectory) /p:VersionSuffix=-prerelease.$(Build.BuildId)
  displayName: 'Pack step'
```

この例では、`.NET Core` プロジェクトをビルドし、prereleaseバージョンのパッケージを作成しています。`dotnet pack` コマンドの `VersionSuffix` オプションを使用して、ビルドIDを含むprereleaseバージョンを指定しています。

### 2. Artifactの公開

ビルドされたパッケージをAzure DevOpsのArtifactsに公開するためには、ビルドパイプラインの最後に公開ステップを追加します。

#### YAMLでの例

```yaml
- task: PublishBuildArtifacts@1
  inputs:
    PathtoPublish: '$(Build.ArtifactStagingDirectory)'
    ArtifactName: 'MyPackage'
    publishLocation: 'Container'
```

このタスクは、指定されたディレクトリ内のファイルをArtifactsとして公開します。`PathtoPublish` には、ビルドされたパッケージが格納されているディレクトリのパスを指定します。`ArtifactName` は、Artifacts内でのパッケージ名です。

### 3. パイプラインの実行

設定が完了したら、パイプラインを実行します。パイプラインが成功すれば、ビルドされたパッケージがAzure DevOpsのArtifactsに自動的に格納されます。

### 注意点

- パイプラインの設定はプロジェクトの種類や要件によって異なります。上記の例はあくまで一例です。
- バージョン番号やパッケージの命名規則は、プロジェクトの方針に合わせて適宜調整してください。
- Azure DevOpsのドキュメントやコミュニティフォーラムは、より詳細な情報や特定の問題に対するソリューションを提供する優れたリソースです。

### user — 2024-01-24T06:33:10.973738+00:00

Dotnetcorecl@2のtaskを利用する前提で示せ

### assistant — 2024-01-24T06:33:56.833052+00:00

Azure DevOpsのパイプラインで`.NET Core`プロジェクトのprerelease版パッケージをArtifactsに格納する場合、`DotNetCoreCLI@2`タスクを使用してパッケージをビルド、パック、そして公開することができます。以下は、`DotNetCoreCLI@2`タスクを使用したYAMLパイプラインのサンプルです。

### YAMLパイプラインの例

```yaml
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

variables:
  buildConfiguration: 'Release'

steps:
- task: DotNetCoreCLI@2
  inputs:
    command: 'restore'
    projects: '**/*.csproj'
  displayName: 'Restore NuGet packages'

- task: DotNetCoreCLI@2
  inputs:
    command: 'build'
    projects: '**/*.csproj'
    arguments: '--configuration $(buildConfiguration)'
  displayName: 'Build project'

- task: DotNetCoreCLI@2
  inputs:
    command: 'test'
    projects: '**/*Tests.csproj'
    arguments: '--configuration $(buildConfiguration)'
  displayName: 'Run tests'

- task: DotNetCoreCLI@2
  inputs:
    command: 'pack'
    projects: '**/*.csproj'
    arguments: '--configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory) /p:PackageVersion=1.0.0-prerelease.$(Build.BuildId)'
    packOptions: '--no-build'
  displayName: 'Pack NuGet package'

- task: PublishBuildArtifacts@1
  inputs:
    PathtoPublish: '$(Build.ArtifactStagingDirectory)'
    ArtifactName: 'MyPackage'
    publishLocation: 'Container'
  displayName: 'Publish Artifact'
```

このパイプラインは以下のステップで構成されています：

1. **Restore**: プロジェクトの依存関係を復元します。
2. **Build**: プロジェクトをビルドします。ビルド構成は変数を通じて指定されます。
3. **Test**: テストプロジェクトを実行します。
4. **Pack**: プロジェクトをパッケージ化します。`PackageVersion`プロパティを使用してprereleaseバージョンを指定します。ここでは、ビルドIDをバージョン番号の一部として使用しています。
5. **Publish Artifact**: ビルドされたパッケージをAzure DevOpsのArtifactsに公開します。

注意点：

- プロジェクトの種類や設定によって、パイプラインの詳細が異なる場合があります。
- `PackageVersion`の値はプロジェクトのバージョニング戦略に応じて調整してください。
- `publishLocation: 'Container'`は、ビルド成果物をAzure PipelinesのArtifactsとして公開することを意味します。

### user — 2024-01-24T06:46:02.651950+00:00

バージョンは環境変数を利用すること

### assistant — 2024-01-24T06:46:40.146019+00:00

環境変数を使用してパッケージのバージョンを指定する場合、Azure DevOps Pipelinesでは、ビルド変数やパイプライン変数を利用してバージョン情報を動的に設定することができます。以下は、環境変数を利用してパッケージのバージョンを設定するYAMLパイプラインのサンプルです。

### YAMLパイプラインの例

```yaml
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

variables:
  buildConfiguration: 'Release'
  packageVersion: '1.0.0-prerelease.$(Build.BuildId)'

steps:
- task: DotNetCoreCLI@2
  inputs:
    command: 'restore'
    projects: '**/*.csproj'
  displayName: 'Restore NuGet packages'

- task: DotNetCoreCLI@2
  inputs:
    command: 'build'
    projects: '**/*.csproj'
    arguments: '--configuration $(buildConfiguration)'
  displayName: 'Build project'

- task: DotNetCoreCLI@2
  inputs:
    command: 'test'
    projects: '**/*Tests.csproj'
    arguments: '--configuration $(buildConfiguration)'
  displayName: 'Run tests'

- task: DotNetCoreCLI@2
  inputs:
    command: 'pack'
    projects: '**/*.csproj'
    arguments: '--configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory) /p:PackageVersion=$(packageVersion)'
    packOptions: '--no-build'
  displayName: 'Pack NuGet package'

- task: PublishBuildArtifacts@1
  inputs:
    PathtoPublish: '$(Build.ArtifactStagingDirectory)'
    ArtifactName: 'MyPackage'
    publishLocation: 'Container'
  displayName: 'Publish Artifact'
```

このサンプルでは、`packageVersion`変数をパイプラインの変数として定義し、その値を`DotNetCoreCLI@2`タスクの`pack`コマンドでパッケージのバージョンとして使用しています。`$(Build.BuildId)`をバージョン番号に含めることで、ビルドごとに一意のバージョン番号が割り当てられます。

パッケージバージョンを環境変数またはパイプライン変数から動的に取得することで、ビルドプロセスをより柔軟に制御し、バージョン管理を自動化することができます。
