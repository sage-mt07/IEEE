---
conversation_id: "67369d7b-de7c-8007-9ef9-8be6534a0d05"
title: "AzureDevOps Assignee Replacement Script"
create_time: 1731632508.123466
update_time: 1731632661.613924
language_guess: "en"
num_messages: 9
part_index: 1
part_count: 1
---

### system — 2024-11-15T01:01:48.123466+00:00

_(empty)_

### user — 2024-11-15T01:01:48.127158+00:00

AzureDevOpsのBoardsに割り当てた人を置換するスクリプト

### assistant — 2024-11-15T01:02:21.695419+00:00

_(empty)_

### assistant — 2024-11-15T01:02:21.695586+00:00

Azure DevOpsのBoardsで作業項目の割り当てを他の担当者に置換するためのスクリプトをPowerShellで作成します。以下の例では、特定のユーザーの割り当てを新しいユーザーに置き換えることを想定しています。

```powershell
# Azure DevOps情報
$organization = "YourOrganizationName"
$project = "YourProjectName"
$pat = "YourPAT"  # パーソナルアクセストークン (PAT)

# 置換対象とするユーザーと新しいユーザーのメールアドレス
$oldAssignee = "[[REDACTED_EMAIL]]"
$newAssignee = "[[REDACTED_EMAIL]]"

# REST APIのURLを設定
$apiUrl = "https://dev.azure.com/$organization/$project/_apis/wit/wiql?api-version=7.1-preview.1"

# Work Item Query Language (WIQL) クエリを作成
$query = @{
    query = "SELECT [System.Id] FROM WorkItems WHERE [System.AssignedTo] = '$oldAssignee'"
} | ConvertTo-Json

# 作業項目を取得
$response = Invoke-RestMethod -Uri $apiUrl -Method Post -Body $query -Headers @{Authorization = "Basic $([Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes(":$pat")))"}
$workItems = $response.workItems

# 作業項目ごとに割り当てを置換
foreach ($item in $workItems) {
    $workItemId = $item.id
    $workItemUrl = "https://dev.azure.com/$organization/$project/_apis/wit/workitems/$workItemId?api-version=7.1-preview.3"

    # 更新データを設定
    $body = @(
        @{
            "op" = "add"
            "path" = "/fields/System.AssignedTo"
            "value" = $newAssignee
        }
    ) | ConvertTo-Json

    # 作業項目の更新
    Invoke-RestMethod -Uri $workItemUrl -Method Patch -Body $body -ContentType "application/json-patch+json" -Headers @{Authorization = "Basic $([Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes(":$pat")))"}
    Write-Output "Work item $workItemId has been reassigned to $newAssignee."
}
```

### スクリプトの詳細
1. `oldAssignee`と`newAssignee`に置換前後の担当者のメールアドレスを設定します。
2. `WIQL`クエリで、古い担当者に割り当てられたすべての作業項目を検索します。
3. 各作業項目に対して、新しい担当者に割り当てを変更します。

PAT（Personal Access Token）を使用して認証しますが、組織でのセキュリティポリシーに応じて、適切な認証方法を設定してください。

### user — 2024-11-15T01:02:31.641371+00:00

必要な権限は

### assistant — 2024-11-15T01:02:44.549204+00:00

このスクリプトを実行するために必要なAzure DevOpsの権限は、以下の通りです：

1. **プロジェクトレベルの権限**: 
   - **Work Itemsの読み取り**（Read permissions for work items）：作業項目を取得するため。
   - **Work Itemsの編集**（Edit permissions for work items）：作業項目の割り当てフィールドを変更するため。

2. **スコープされたパーソナル アクセス トークン (PAT)**:
   - 作業項目に対する`Read`および`Write`のアクセス権限が必要です。
   - PATを発行する際には、`Work Items (read and write)`のスコープを指定する必要があります。

### PATのスコープ設定
PATを発行する際に、以下のスコープを設定してください：
   - `Work Items (read and write)`: 作業項目の読み取りと書き込みを許可します。

これらの権限が正しく設定されていれば、スクリプトを実行して、割り当てを他のユーザーに置き換えることができます。

### user — 2024-11-15T01:03:59.026393+00:00

回数制限はあるのか

### assistant — 2024-11-15T01:04:20.997420+00:00

Azure DevOpsのAPIには、**レート制限**が設定されています。具体的な制限はMicrosoftから公開されていませんが、以下のような点に注意が必要です：

1. **レート制限**:
   - Azure DevOpsのREST APIでは、特定の時間内に呼び出せる回数に制限があります。この制限に達すると、HTTPステータス`429 Too Many Requests`が返されます。
   - レート制限が適用されるかどうかは、APIの利用頻度やスコープ、Azure DevOpsのインスタンスの負荷などによって異なります。

2. **スロットリングの回避**:
   - レート制限に達した場合は、指定された待機時間（`Retry-After`ヘッダー）を確認し、その時間が経過してからリクエストを再試行してください。
   - スクリプト内で一定間隔ごとにAPI呼び出しを行うようにしたり、失敗時のリトライロジックを導入することで、スロットリングを回避できます。

3. **推奨対策**:
   - 大量の作業項目の更新が必要な場合は、**バッチ処理**や**一度にリクエストする項目の数を減らす**ことを検討すると、レート制限に達しにくくなります。
   - また、Microsoftによると、API呼び出しのパフォーマンスや可用性の影響を避けるために、重要な操作は業務時間外に行うことも推奨されています。

APIの実行に頻度が高い場合や大量のデータ更新を伴う場合には、これらの回数制限を考慮した設計が必要です。
