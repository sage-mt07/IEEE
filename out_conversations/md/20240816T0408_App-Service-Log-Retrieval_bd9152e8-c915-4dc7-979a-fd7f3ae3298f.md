---
conversation_id: "bd9152e8-c915-4dc7-979a-fd7f3ae3298f"
title: "App Service Log Retrieval"
create_time: 1723781327.903356
update_time: 1723781495.79681
language_guess: "en"
num_messages: 11
part_index: 1
part_count: 1
---

### system — 2024-08-16T04:08:47.903356+00:00

_(empty)_

### user — 2024-08-16T04:08:47.907069+00:00

App Serviceでホストするアプリケーションのログを取得する方法

### assistant — 2024-08-16T04:09:02.015606+00:00

_(empty)_

### assistant — 2024-08-16T04:09:02.015682+00:00

Azure App Serviceでホストしているアプリケーションのログを取得する方法はいくつかあります。以下に代表的な方法を紹介します。

### 1. **Application Insights を使用する**
Azure Application Insights を有効にすると、アプリケーションのログやパフォーマンスデータをリアルタイムで取得できます。

- **設定方法:**
  1. Azure Portal にログインし、App Service を選択します。
  2. 「Application Insights」メニューを選択し、「Turn on Application Insights」をクリックします。
  3. 必要に応じて設定を行い、「適用」をクリックします。

- **データの確認:**
  Application Insights の「ログ」タブから、クエリを実行してログデータを取得できます。

### 2. **App Service の診断ログ**
App Service には、Web サーバーの診断ログ（HTTP ログ）、アプリケーションログ、Kudu サイトからのログなどを有効にして収集できます。

- **設定方法:**
  1. Azure Portal で App Service を選択します。
  2. 「診断ログ」メニューを選択します。
  3. 「Application Logging (Filesystem)」や「Web Server Logging」を有効にし、ログの保存先を指定します。

- **ログの確認:**
  Kudu サイトにアクセスして、`LogFiles` ディレクトリ内のログを参照したり、Azure Portal から直接ダウンロードできます。

### 3. **ログストリーミング**
App Service のログをリアルタイムで確認したい場合は、ログストリーミング機能を使用します。

- **設定方法:**
  1. Azure Portal で App Service を選択します。
  2. 「診断ログ」メニューで「ログストリーミング」をクリックします。

- **ログの確認:**
  ログストリーミングウィンドウが表示され、リアルタイムでログを確認できます。

### 4. **カスタム ロギング**
アプリケーション内で `ILogger` インターフェースを使用してカスタムログを記録し、それを App Service の診断ログや Application Insights に送信することも可能です。

### 5. **Azure Storage アカウントにログを保存**
診断ログを Azure Storage アカウントに保存し、そこからログをダウンロードして確認することもできます。

- **設定方法:**
  1. 「診断ログ」メニューで「Application Logging (Blob)」や「Web Server Logging (Blob)」を有効にし、Storage アカウントを指定します。

- **ログの確認:**
  Azure Storage Explorer などを使用して、指定した Blob ストレージからログファイルを取得できます。

これらの方法を組み合わせることで、App Service でホストしているアプリケーションのログを効果的に管理・確認することができます。

### user — 2024-08-16T04:11:12.290210+00:00

添付ファイルはApp Serviceのテンプレートである。
アプリケーションから出力したログを参照するための追加設定を確認

### assistant — 2024-08-16T04:11:34.989074+00:00

import zipfile
import os

# Define the path to the uploaded zip file and extract it
zip_file_path = '/mnt/data/ExportedTemplate-nstag-rg (1).zip'
extracted_folder_path = '/mnt/data/ExportedTemplate_extracted/'

# Create a directory to extract the contents
os.makedirs(extracted_folder_path, exist_ok=True)

# Extract the zip file
with zipfile.ZipFile(zip_file_path, 'r') as zip_ref:
    zip_ref.extractall(extracted_folder_path)

# List the extracted files
extracted_files = os.listdir(extracted_folder_path)
extracted_files

### tool — 2024-08-16T04:11:34.989143+00:00

['template.json', 'parameters.json']

### assistant — 2024-08-16T04:11:34.989191+00:00

import json

# Load the JSON content from the extracted template.json file
template_file_path = os.path.join(extracted_folder_path, 'template.json')

with open(template_file_path, 'r', encoding='utf-8') as file:
    template_json = json.load(file)

# Checking for relevant logging settings in the JSON content
template_json

### tool — 2024-08-16T04:11:34.989236+00:00

{'$schema': 'https://schema.management.azure.com/schemas/[[REDACTED_PHONE]]/deploymentTemplate.json#',
 'contentVersion': '1.0.0.0',
 'parameters': {'sites_app000002_name': {'defaultValue': 'app000002',
   'type': 'String'},
  'serverfarms_ASP_nstagrg_a213_externalid': {'defaultValue': '/subscriptions/a4089896-458b-4a9d-90dd-133583de75d2/resourceGroups/nstag-rg/providers/Microsoft.Web/serverfarms/ASP-nstagrg-a213',
   'type': 'String'}},
 'variables': {},
 'resources': [{'type': 'Microsoft.Web/sites',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[parameters('sites_app000002_name')]",
   'location': 'Japan East',
   'tags': {'hidden-link: /app-insights-resource-id': '/subscriptions/a4089896-458b-4a9d-90dd-133583de75d2/resourceGroups/nstag-rg/providers/microsoft.insights/components/app000002',
    'hidden-link: /app-insights-instrumentation-key': '[[REDACTED_PHONE]]-4e34-bb2c-26ea07f5cf71',
    'hidden-link: /app-insights-conn-string': 'InstrumentationKey=[[REDACTED_PHONE]]-4e34-bb2c-26ea07f5cf71;IngestionEndpoint=https://japaneast-1.in.applicationinsights.azure.com/;LiveEndpoint=https://japaneast.livediagnostics.monitor.azure.com/;ApplicationId=7532792b-a580-4f3d-be48-f4c767a3fb05'},
   'kind': 'app',
   'properties': {'enabled': True,
    'hostNameSslStates': [{'name': "[concat(parameters('sites_app000002_name'), '-gvgkgwcta9g6ecay.japaneast-01.azurewebsites.net')]",
      'sslState': 'Disabled',
      'hostType': 'Standard'},
     {'name': "[concat(parameters('sites_app000002_name'), '-gvgkgwcta9g6ecay.scm.japaneast-01.azurewebsites.net')]",
      'sslState': 'Disabled',
      'hostType': 'Repository'}],
    'serverFarmId': "[parameters('serverfarms_ASP_nstagrg_a213_externalid')]",
    'reserved': False,
    'isXenon': False,
    'hyperV': False,
    'dnsConfiguration': {},
    'vnetRouteAllEnabled': False,
    'vnetImagePullEnabled': False,
    'vnetContentShareEnabled': False,
    'siteConfig': {'numberOfWorkers': 1,
     'acrUseManagedIdentityCreds': False,
     'alwaysOn': True,
     'http20Enabled': True,
     'functionAppScaleLimit': 0,
     'minimumElasticInstanceCount': 1},
    'scmSiteAlsoStopped': False,
    'clientAffinityEnabled': True,
    'clientCertEnabled': False,
    'clientCertMode': 'Required',
    'hostNamesDisabled': False,
    'vnetBackupRestoreEnabled': False,
    'customDomainVerificationId': '2C04CCD1CEB3C4C9AE6CA8A6D3F8066A888D6A610869E8AB9D54FED87B781EE8',
    'containerSize': 0,
    'dailyMemoryTimeQuota': 0,
    'httpsOnly': True,
    'redundancyMode': 'None',
    'publicNetworkAccess': 'Enabled',
    'storageAccountRequired': False,
    'keyVaultReferenceIdentity': 'SystemAssigned'}},
  {'type': 'Microsoft.Web/sites/basicPublishingCredentialsPolicies',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/ftp')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'tags': {'hidden-link: /app-insights-resource-id': '/subscriptions/a4089896-458b-4a9d-90dd-133583de75d2/resourceGroups/nstag-rg/providers/microsoft.insights/components/app000002',
    'hidden-link: /app-insights-instrumentation-key': '[[REDACTED_PHONE]]-4e34-bb2c-26ea07f5cf71',
    'hidden-link: /app-insights-conn-string': 'InstrumentationKey=[[REDACTED_PHONE]]-4e34-bb2c-26ea07f5cf71;IngestionEndpoint=https://japaneast-1.in.applicationinsights.azure.com/;LiveEndpoint=https://japaneast.livediagnostics.monitor.azure.com/;ApplicationId=7532792b-a580-4f3d-be48-f4c767a3fb05'},
   'properties': {'allow': False}},
  {'type': 'Microsoft.Web/sites/basicPublishingCredentialsPolicies',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/scm')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'tags': {'hidden-link: /app-insights-resource-id': '/subscriptions/a4089896-458b-4a9d-90dd-133583de75d2/resourceGroups/nstag-rg/providers/microsoft.insights/components/app000002',
    'hidden-link: /app-insights-instrumentation-key': '[[REDACTED_PHONE]]-4e34-bb2c-26ea07f5cf71',
    'hidden-link: /app-insights-conn-string': 'InstrumentationKey=[[REDACTED_PHONE]]-4e34-bb2c-26ea07f5cf71;IngestionEndpoint=https://japaneast-1.in.applicationinsights.azure.com/;LiveEndpoint=https://japaneast.livediagnostics.monitor.azure.com/;ApplicationId=7532792b-a580-4f3d-be48-f4c767a3fb05'},
   'properties': {'allow': False}},
  {'type': 'Microsoft.Web/sites/config',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/web')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'tags': {'hidden-link: /app-insights-resource-id': '/subscriptions/a4089896-458b-4a9d-90dd-133583de75d2/resourceGroups/nstag-rg/providers/microsoft.insights/components/app000002',
    'hidden-link: /app-insights-instrumentation-key': '[[REDACTED_PHONE]]-4e34-bb2c-26ea07f5cf71',
    'hidden-link: /app-insights-conn-string': 'InstrumentationKey=[[REDACTED_PHONE]]-4e34-bb2c-26ea07f5cf71;IngestionEndpoint=https://japaneast-1.in.applicationinsights.azure.com/;LiveEndpoint=https://japaneast.livediagnostics.monitor.azure.com/;ApplicationId=7532792b-a580-4f3d-be48-f4c767a3fb05'},
   'properties': {'numberOfWorkers': 1,
    'defaultDocuments': ['Default.htm',
     'Default.html',
     'Default.asp',
     'index.htm',
     'index.html',
     'iisstart.htm',
     'default.aspx',
     'index.php',
     'hostingstart.html'],
    'netFrameworkVersion': 'v6.0',
    'requestTracingEnabled': True,
    'requestTracingExpirationTime': '[[REDACTED_PHONE]]-31T23:59:00Z',
    'remoteDebuggingEnabled': False,
    'remoteDebuggingVersion': 'VS2022',
    'httpLoggingEnabled': True,
    'acrUseManagedIdentityCreds': False,
    'logsDirectorySizeLimit': 35,
    'detailedErrorLoggingEnabled': True,
    'publishingUsername': 'REDACTED',
    'scmType': 'VSTSRM',
    'use32BitWorkerProcess': True,
    'webSocketsEnabled': False,
    'alwaysOn': True,
    'managedPipelineMode': 'Integrated',
    'virtualApplications': [{'virtualPath': '/',
      'physicalPath': 'site\\wwwroot',
      'preloadEnabled': True}],
    'loadBalancing': 'LeastRequests',
    'experiments': {'rampUpRules': []},
    'autoHealEnabled': False,
    'vnetRouteAllEnabled': False,
    'vnetPrivatePortsCount': 0,
    'publicNetworkAccess': 'Enabled',
    'localMySqlEnabled': False,
    'ipSecurityRestrictions': [{'ipAddress': 'Any',
      'action': 'Allow',
      'priority': [[REDACTED_PHONE]],
      'name': 'Allow all',
      'description': 'Allow all access'}],
    'scmIpSecurityRestrictions': [{'ipAddress': 'Any',
      'action': 'Allow',
      'priority': [[REDACTED_PHONE]],
      'name': 'Allow all',
      'description': 'Allow all access'}],
    'scmIpSecurityRestrictionsUseMain': False,
    'http20Enabled': True,
    'minTlsVersion': '1.2',
    'scmMinTlsVersion': '1.2',
    'ftpsState': 'FtpsOnly',
    'preWarmedInstanceCount': 0,
    'elasticWebAppScaleLimit': 0,
    'functionsRuntimeScaleMonitoringEnabled': False,
    'minimumElasticInstanceCount': 1,
    'azureStorageAccounts': {}}},
  {'type': 'Microsoft.Web/sites/deployments',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/0ac51ae67d154cf8a33d4bde0ad1299f')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'properties': {'status': 4,
    'author_email': 'N/A',
    'author': 'N/A',
    'deployer': 'VSTS',
    'message': '{"type":"deployment","commitId":"5f65fd79d8b2d4354688aa6bfc8b21c88556c9af","buildId":"28","releaseId":"18","buildNumber":"[[REDACTED_PHONE]].2","releaseName":"Release-18","repoProvider":"TfsGit","repoName":"AzureTest01","collectionUrl":"https://dev.azure.com/seijim0pattern01/","teamProject":"297eadeb-0c37-4ddc-8690-a58baefa96dd","buildProjectUrl":"https://dev.azure.com/seijim0pattern01/297eadeb-0c37-4ddc-8690-a58baefa96dd","repositoryUrl":"","branch":"main","teamProjectName":"AzureTest01","slotName":"production"}',
    'start_time': '[[REDACTED_PHONE]]-16T03:24:21.9245133Z',
    'end_time': '[[REDACTED_PHONE]]-16T03:24:27.3639635Z',
    'active': False}},
  {'type': 'Microsoft.Web/sites/deployments',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/0dc56543d2e1454cb858f749215c6cca')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'properties': {'status': 4,
    'author_email': 'N/A',
    'author': 'N/A',
    'deployer': 'VSTS',
    'message': '{"type":"deployment","commitId":"1fb7cdfd45a6a15dfd9e8968ca0f746e422481be","buildId":"22","releaseId":"12","buildNumber":"[[REDACTED_PHONE]]","releaseName":"Release-12","repoProvider":"TfsGit","repoName":"AzureTest01","collectionUrl":"https://dev.azure.com/seijim0pattern01/","teamProject":"297eadeb-0c37-4ddc-8690-a58baefa96dd","buildProjectUrl":"https://dev.azure.com/seijim0pattern01/297eadeb-0c37-4ddc-8690-a58baefa96dd","repositoryUrl":"","branch":"main","teamProjectName":"AzureTest01","slotName":"production"}',
    'start_time': '[[REDACTED_PHONE]]-13T11:44:19.7346141Z',
    'end_time': '[[REDACTED_PHONE]]-13T11:44:20.3139222Z',
    'active': False}},
  {'type': 'Microsoft.Web/sites/deployments',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/4555e7f1efcf4b2e9bb784bfc4c1d0b0')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'properties': {'status': 4,
    'author_email': 'N/A',
    'author': 'N/A',
    'deployer': 'VSTS',
    'message': '{"type":"deployment","commitId":"d9b29401d0eec6e3dbfc02095e86ed48997888fe","buildId":"25","releaseId":"15","buildNumber":"[[REDACTED_PHONE]].1","releaseName":"Release-15","repoProvider":"TfsGit","repoName":"AzureTest01","collectionUrl":"https://dev.azure.com/seijim0pattern01/","teamProject":"297eadeb-0c37-4ddc-8690-a58baefa96dd","buildProjectUrl":"https://dev.azure.com/seijim0pattern01/297eadeb-0c37-4ddc-8690-a58baefa96dd","repositoryUrl":"","branch":"main","teamProjectName":"AzureTest01","slotName":"production"}',
    'start_time': '[[REDACTED_PHONE]]-15T01:55:00.7233308Z',
    'end_time': '[[REDACTED_PHONE]]-15T01:55:01.3014649Z',
    'active': False}},
  {'type': 'Microsoft.Web/sites/deployments',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/5c05a7e1e47c4435b816a7f55c05bc73')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'properties': {'status': 4,
    'author_email': 'N/A',
    'author': 'N/A',
    'deployer': 'VSTS',
    'message': '{"type":"deployment","commitId":"d11f3e420d680e98173e46524f66b5b7848360be","buildId":"29","releaseId":"19","buildNumber":"[[REDACTED_PHONE]].3","releaseName":"Release-19","repoProvider":"TfsGit","repoName":"AzureTest01","collectionUrl":"https://dev.azure.com/seijim0pattern01/","teamProject":"297eadeb-0c37-4ddc-8690-a58baefa96dd","buildProjectUrl":"https://dev.azure.com/seijim0pattern01/297eadeb-0c37-4ddc-8690-a58baefa96dd","repositoryUrl":"","branch":"main","teamProjectName":"AzureTest01","slotName":"production"}',
    'start_time': '[[REDACTED_PHONE]]-16T03:32:37.9806618Z',
    'end_time': '[[REDACTED_PHONE]]-16T03:32:38.5900505Z',
    'active': False}},
  {'type': 'Microsoft.Web/sites/deployments',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/6917a59e5b514ae89b34a2ce5b31787d')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'properties': {'status': 4,
    'author_email': 'N/A',
    'author': 'N/A',
    'deployer': 'VSTS',
    'message': '{"type":"deployment","commitId":"a06adc905f003861d01e68903080d2a9983cbeee","buildId":"30","releaseId":"20","buildNumber":"[[REDACTED_PHONE]].4","releaseName":"Release-20","repoProvider":"TfsGit","repoName":"AzureTest01","collectionUrl":"https://dev.azure.com/seijim0pattern01/","teamProject":"297eadeb-0c37-4ddc-8690-a58baefa96dd","buildProjectUrl":"https://dev.azure.com/seijim0pattern01/297eadeb-0c37-4ddc-8690-a58baefa96dd","repositoryUrl":"","branch":"main","teamProjectName":"AzureTest01","slotName":"production"}',
    'start_time': '[[REDACTED_PHONE]]-16T03:54:49.5525826Z',
    'end_time': '[[REDACTED_PHONE]]-16T03:54:50.115331Z',
    'active': False}},
  {'type': 'Microsoft.Web/sites/deployments',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/751acd40bf77408ca7e125e39fcb6c05')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'properties': {'status': 4,
    'author_email': 'N/A',
    'author': 'N/A',
    'deployer': 'VSTS',
    'message': '{"type":"deployment","commitId":"b870012e3e5ced769eb98811a4f49c26465770da","buildId":"23","releaseId":"13","buildNumber":"[[REDACTED_PHONE]]","releaseName":"Release-13","repoProvider":"TfsGit","repoName":"AzureTest01","collectionUrl":"https://dev.azure.com/seijim0pattern01/","teamProject":"297eadeb-0c37-4ddc-8690-a58baefa96dd","buildProjectUrl":"https://dev.azure.com/seijim0pattern01/297eadeb-0c37-4ddc-8690-a58baefa96dd","repositoryUrl":"","branch":"main","teamProjectName":"AzureTest01","slotName":"production"}',
    'start_time': '[[REDACTED_PHONE]]-13T11:55:49.7465494Z',
    'end_time': '[[REDACTED_PHONE]]-13T11:55:50.2934391Z',
    'active': False}},
  {'type': 'Microsoft.Web/sites/deployments',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/8fa1e7d210784779a991196051ebfc3d')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'properties': {'status': 4,
    'author_email': 'N/A',
    'author': 'N/A',
    'deployer': 'VSTS',
    'message': '{"type":"deployment","commitId":"c8ee45c67f19527a88175c9ae941a0f8ce7a19dd","buildId":"24","releaseId":"14","buildNumber":"[[REDACTED_PHONE]]","releaseName":"Release-14","repoProvider":"TfsGit","repoName":"AzureTest01","collectionUrl":"https://dev.azure.com/seijim0pattern01/","teamProject":"297eadeb-0c37-4ddc-8690-a58baefa96dd","buildProjectUrl":"https://dev.azure.com/seijim0pattern01/297eadeb-0c37-4ddc-8690-a58baefa96dd","repositoryUrl":"","branch":"main","teamProjectName":"AzureTest01","slotName":"production"}',
    'start_time': '[[REDACTED_PHONE]]-13T12:10:49.9627329Z',
    'end_time': '[[REDACTED_PHONE]]-13T12:10:50.5408685Z',
    'active': False}},
  {'type': 'Microsoft.Web/sites/deployments',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/c4adb703be57426dbc62f172bbf10f8c')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'properties': {'status': 4,
    'author_email': 'N/A',
    'author': 'N/A',
    'deployer': 'VSTS',
    'message': '{"type":"deployment","commitId":"bb68f6e70ed01181769e7587b81933fcc70ad513","buildId":"31","releaseId":"21","buildNumber":"[[REDACTED_PHONE]].5","releaseName":"Release-21","repoProvider":"TfsGit","repoName":"AzureTest01","collectionUrl":"https://dev.azure.com/seijim0pattern01/","teamProject":"297eadeb-0c37-4ddc-8690-a58baefa96dd","buildProjectUrl":"https://dev.azure.com/seijim0pattern01/297eadeb-0c37-4ddc-8690-a58baefa96dd","repositoryUrl":"","branch":"main","teamProjectName":"AzureTest01","slotName":"production"}',
    'start_time': '[[REDACTED_PHONE]]-16T04:04:43.2089465Z',
    'end_time': '[[REDACTED_PHONE]]-16T04:04:43.9295496Z',
    'active': True}},
  {'type': 'Microsoft.Web/sites/deployments',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/d9d8b6249b8148f8acc9f964c69c6e38')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'properties': {'status': 4,
    'author_email': 'N/A',
    'author': 'N/A',
    'deployer': 'VSTS',
    'message': '{"type":"deployment","commitId":"cccf54343efe8e20647fd4bdfcc442e3801fe426","buildId":"27","releaseId":"17","buildNumber":"[[REDACTED_PHONE]].1","releaseName":"Release-17","repoProvider":"TfsGit","repoName":"AzureTest01","collectionUrl":"https://dev.azure.com/seijim0pattern01/","teamProject":"297eadeb-0c37-4ddc-8690-a58baefa96dd","buildProjectUrl":"https://dev.azure.com/seijim0pattern01/297eadeb-0c37-4ddc-8690-a58baefa96dd","repositoryUrl":"","branch":"main","teamProjectName":"AzureTest01","slotName":"production"}',
    'start_time': '[[REDACTED_PHONE]]-16T02:01:01.9758861Z',
    'end_time': '[[REDACTED_PHONE]]-16T02:01:02.5540198Z',
    'active': False}},
  {'type': 'Microsoft.Web/sites/deployments',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/e7b62226464a4044b6eeecd977d5ef89')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'properties': {'status': 4,
    'author_email': 'N/A',
    'author': 'N/A',
    'deployer': 'VSTS',
    'message': '{"type":"deployment","commitId":"f2cec3b177263cd4808ab55cfc6256d70b9eacd0","buildId":"26","releaseId":"16","buildNumber":"[[REDACTED_PHONE]].2","releaseName":"Release-16","repoProvider":"TfsGit","repoName":"AzureTest01","collectionUrl":"https://dev.azure.com/seijim0pattern01/","teamProject":"297eadeb-0c37-4ddc-8690-a58baefa96dd","buildProjectUrl":"https://dev.azure.com/seijim0pattern01/297eadeb-0c37-4ddc-8690-a58baefa96dd","repositoryUrl":"","branch":"main","teamProjectName":"AzureTest01","slotName":"production"}',
    'start_time': '[[REDACTED_PHONE]]-15T02:52:46.7178914Z',
    'end_time': '[[REDACTED_PHONE]]-15T02:52:47.2491525Z',
    'active': False}},
  {'type': 'Microsoft.Web/sites/hostNameBindings',
   'apiVersion': '[[REDACTED_PHONE]]',
   'name': "[concat(parameters('sites_app000002_name'), '/', parameters('sites_app000002_name'), '-gvgkgwcta9g6ecay.japaneast-01.azurewebsites.net')]",
   'location': 'Japan East',
   'dependsOn': ["[resourceId('Microsoft.Web/sites', parameters('sites_app000002_name'))]"],
   'properties': {'siteName': 'app000002', 'hostNameType': 'Verified'}}]}

### assistant — 2024-08-16T04:11:34.989280+00:00

テンプレートの内容を確認しましたが、ログ設定に関する直接的な記述（例えば、アプリケーションログや診断ログの設定）は見当たりません。App Serviceでアプリケーションのログを取得するための一般的な設定としては、以下の設定を追加する必要があります。

### ログの設定方法
1. **Application Logging（アプリケーション ログ）**: これにより、アプリケーションが出力するログをファイルに保存できます。

2. **Web Server Logging（Web サーバーログ）**: HTTP リクエストおよびレスポンスに関する詳細なログを取得できます。

3. **Application Insights**: 上記の方法に加えて、Application Insightsを使用して、詳細なアプリケーションパフォーマンスモニタリングやログを取得することも推奨されます。

### 設定追加例

以下は、テンプレートに診断ログを追加する例です。

```json
{
  "type": "Microsoft.Web/sites/config",
  "apiVersion": "[[REDACTED_PHONE]]",
  "name": "[concat(parameters('sites_app000002_name'), '/web')]",
  "location": "[resourceGroup().location]",
  "properties": {
    "applicationLogging": {
      "fileSystem": {
        "level": "Information",
        "retentionInMb": 100,
        "retentionInDays": 7
      }
    },
    "detailedErrorMessages": "true",
    "httpLoggingEnabled": "true",
    "requestTracingEnabled": "true",
    "requestTracingExpirationTime": "[utcNow('yyyy-MM-ddTHH:mm:ssZ')]",
    "failedRequestTracingEnabled": "true"
  }
}
```

この例では、以下の設定が含まれています：
- `applicationLogging.fileSystem.level`: ログの詳細レベル（`Error`、`Warning`、`Information`など）。
- `retentionInMb`: ログファイルの最大サイズ。
- `retentionInDays`: ログを保持する日数。
- `httpLoggingEnabled`: HTTP ログを有効にします。
- `detailedErrorMessages`: 詳細なエラーメッセージを有効にします。
- `failedRequestTracingEnabled`: 失敗したリクエストのトレースを有効にします。

これらの設定をテンプレートに追加することで、App Service上でのアプリケーションログの収集が可能となります。必要に応じて、この設定を修正してテンプレートに組み込んでください。
