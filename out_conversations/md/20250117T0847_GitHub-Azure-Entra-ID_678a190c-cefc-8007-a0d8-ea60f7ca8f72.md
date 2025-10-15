---
conversation_id: "678a190c-cefc-8007-a0d8-ea60f7ca8f72"
title: "GitHub Azure Entra ID連携"
create_time: 1737103629.435982
update_time: 1739412163.527541
language_guess: "en"
num_messages: 8
part_index: 1
part_count: 1
---

### system — 2025-01-17T08:47:09.435982+00:00

_(empty)_

### user — 2025-01-17T08:47:09.441466+00:00

GithubはAzure Entra IDを認証に使えるのか

### tool — 2025-01-17T08:47:37.922996+00:00

**Connecting authentication**

OK, let me see. The user is curious if Azure Entra ID can handle GitHub authentication. GitHub typically uses Azure AD for login, but it's worth confirming if Azure Entra ID is supported for single sign-on (SSO).

**Navigating GitHub and Azure AD**

Hmm, I’m thinking about how GitHub Enterprise Cloud integrates with Azure AD using SAML for SSO, which seems to be covered in their official documentation.

### assistant — 2025-01-17T08:47:37.923438+00:00

結論から申し上げると、**GitHubとAzure Entra ID（旧称：Azure Active Directory）を連携してシングルサインオン(SSO)を実現**することは可能です。ただし、以下のような前提や制限があります。

---

## 1. GitHubのプラン要件

GitHubでAzure Entra IDを使ったSAML認証によるSSOを利用するためには、

- **GitHub Enterprise Cloud** または **GitHub Enterprise Server** のライセンスが必要

いわゆる無料のGitHub（GitHub Free）やGitHub Proなどでは、組織単位でのSAML SSOを有効にできません。SSO機能はあくまで**Enterpriseレベル**でサポートされる機能となります。

---

## 2. 連携方式: SAMLベースのSSO

GitHub Enterpriseでは**SAML(Secure Assertion Markup Language)** を使ったSSOをサポートしています。Azure Entra IDはSAML IdP（Identity Provider）として機能することができるため、GitHub Enterprise組織でのログイン時にAzure Entra IDの認証基盤を利用可能です。

### ざっくりとした設定手順

1. **Azure Entra ID (Azure AD)側でGitHub用のエンタープライズアプリケーションを作成**  
   - Azure ポータル (portal.azure.com) の「エンタープライズ アプリケーション」から新規アプリケーションを追加します。
2. **SAMLシングルサインオンを構成**  
   - Azure Entra IDでGitHub Enterprise向けのSAML SSOを構成します。
   - SSO用のメタデータURLやエンドポイント（SAML メタデータ）を取得し、GitHub側で設定するために控えます。
3. **GitHub Enterpriseの設定画面でSAMLの設定を有効化**  
   - 組織 (Organization) またはエンタープライズ (Enterprise account) の「Security」→「SAML SSO」などの項目で、Azure Entra IDで取得したメタデータやサインイン/サインアウトURLを入力します。
4. **ユーザやグループの割り当て**  
   - Azure Entra IDポータル側で、GitHub Enterpriseアプリケーションにアクセスできるユーザ・グループを割り当てます。

これにより、GitHub Enterpriseの組織でのログイン時に「Azure Entra IDによる認証→GitHub Enterpriseへシングルトークンでログイン」というフローが可能になります。

---

## 3. 公式ドキュメント

- [Microsoft公式: Azure AD から GitHub への SAML SSO設定ガイド](https://learn.microsoft.com/ja-jp/azure/active-directory/saas-apps/github-tutorial)  
  （名前がAzure ADとなっていますが、Azure Entra IDとして同じ手順で設定できます。）

- [GitHub公式: About Enterprise Managed Users](https://docs.github.com/ja/enterprise-cloud@latest/admin/identity-and-access-management/managing-enterprise-accounts-with-managed-users/about-enterprise-managed-users)  
  エンタープライズ管理ユーザ機能についてのドキュメント（Azure ADとの連携例など）。

---

## 4. 注意点

1. **無料プランでは利用できない**  
   先述の通り、SSO機能はエンタープライズプランに限定されます。

2. **組織内のメンバー管理がAzure Entra ID側に依存する**  
   管理者がAzure Entra ID上でユーザやグループを付与・削除すると、その変更をGitHub Enterprise組織のアクセス権にも反映できます。

3. **GitHub.comへの個人利用アカウントへの通常ログインは対象外**  
   あくまで組織（Enterprise）でのログインフローに限られるので、個人アカウントのGitHubログインをAzure Entra IDで完全に置き換えるわけではありません。

---

### まとめ

- **GitHub Enterprise Cloud/Server + Azure Entra ID (旧Azure AD) + SAML SSO** という組み合わせで連携可能  
- 一般的にはAzureポータル側でSAMLアプリとしてGitHubを設定し、GitHub EnterpriseのSAML SSO設定でそれを読み込む形  
- 無料プランやProプランでは使えないため注意

以上の点を踏まえれば、**GitHubはAzure Entra IDを認証に使うことが可能**です。導入時はライセンス要件と設定手順をしっかりと確認してください。

### user — 2025-01-17T08:48:04.287278+00:00

AzureDevOpsServiceをGithubへ移行する方法はあるのか

### tool — 2025-01-17T08:48:34.820435+00:00

_(empty)_

### assistant — 2025-01-17T08:48:34.820546+00:00

Azure DevOps Services（以下、Azure DevOps）からGitHubへ移行する場合、主に以下の要素を検討・移行する必要があります。

1. **リポジトリ（コード）**  
2. **パイプライン（CI/CD）**  
3. **課題管理（Boards → Issues/Projects）**  
4. **WIKIやアーティファクト** など

本回答では、それぞれの要素別に移行方法や注意点をまとめます。

---

## 1. リポジトリ（コード）の移行

### 1.1 手動での移行
最もシンプルな方法は、**gitコマンドを使ってリモートリポジトリを複製（clone）し、GitHubリポジトリとしてプッシュし直す**手順です。以下は流れの一例です。

1. **Azure DevOpsリポジトリをローカルにclone**  
   ```bash
   git clone https://dev.azure.com/yourorganization/yourproject/_git/yourrepo
   ```
2. **GitHubに新規リポジトリを作成**  
   - 例: `github.com/youraccount/yourrepo.git`
3. **GitHubリポジトリをリモートリポジトリとして追加**  
   ```bash
   cd yourrepo
   git remote add github https://github.com/youraccount/yourrepo.git
   ```
4. **GitHubリポジトリへpush**  
   ```bash
   git push github main
   ```
   - 必要に応じて、ブランチやタグをすべて含めてpushしたい場合は  
     ```bash
     git push github --all
     git push github --tags
     ```

### 1.2 Azure DevOps Import Repository 機能
逆に「GitHub上にリポジトリを作成 → Azure DevOpsリポジトリをインポート」というやり方もあります。GitHubの「**Import a repository**」から、Azure DevOpsのリポジトリURLを指定して自動インポートする方法です。  
- ただし、プライベートリポジトリの場合はAzure DevOpsに対する認証情報（パーソナルアクセストークンなど）が必要になる場合があります。

#### 注意点
- **履歴（コミット履歴、ブランチ、タグ）はほぼそのまま移行可能**です。ただし、LFSやサブモジュールを使用している場合は追加作業が必要となる場合があります。  
- **Pull Requestの履歴やビルド結果などのメタデータは移行できません**。必要であれば、手動でIssue化したり記録を残す対応を検討してください。

---

## 2. パイプライン（CI/CD）の移行

Azure DevOpsのPipelines → **GitHub Actions** への移行が主なシナリオです。移行にあたって以下のポイントを押さえます。

1. **YAMLパイプラインの移行**  
   - Azure DevOpsのYAMLパイプラインに記述されているジョブやステップを**GitHub Actionsのワークフローファイル(`.github/workflows/*.yml`)**に書き換えます。  
   - タスク（Tasks）やプール（Pool）、変数などの定義方法が異なるため、手動での修正が必要になるケースが多いです。

2. **ビルドエージェント → GitHubホストランナー or 自ホストランナー**  
   - Azure PipelinesではMicrosoftホストエージェントを使っていた場合、GitHub Actionsでは「**GitHubホストランナー**（ubuntu-latestなど）」が相当します。  
   - 自社環境に合わせて**セルフホストランナー**を利用する場合は、インストール・設定が必要です。

3. **ライブラリや変数グループ → GitHubのシークレットや環境変数**  
   - Azure DevOpsのライブラリや変数グループに相当する機能として、GitHub Actionsの「**Secrets**」や「**Environment Variables**」があります。セキュアな情報（パスワードやトークンなど）は**リポジトリやOrganizationのSecrets**へ移行するとよいです。

4. **タスクテンプレートの差分**  
   - Azure DevOps特有のタスク（例: `VsTest` や `DotNetCoreCLI@2` など）と、GitHub Actionsの公式/コミュニティ製アクションは1対1対応にならないこともあります。  
   - MS製のアクションやMarketplaceから類似のアクションを探して置き換える必要があります。

#### 移行補助ツール
公式・非公式含めて完全自動変換ツールはあまり充実していません。以下のリポジトリなどが参考になる場合があります。  
- [Azure DevOps to GitHub Actions Code Migration Tools (GitHub公式サンプル)](https://github.com/github/azuredevops-actions-migration)

---

## 3. 課題管理（Boards → GitHub Issues / Projects） の移行

Azure Boardsで管理していた**Work Items, Epics, Features, Tasks**などをGitHubの**Issues**や**Projects**に移す方法は大きく2つです。

1. **手動（CSVエクスポート & インポート）**  
   - Azure DevOps BoardsでWork Itemsをエクスポート（CSVなど）し、GitHub Issuesへインポートする。  
   - GitHubのIssueインポートは、APIベースや一部ツールベースで行うことになります。
2. **サードパーティ製の移行ツール使用**  
   - ADOとGitHubを連携して、Work Items → Issuesへマッピングするツールを利用します。  
   - 例: [Azure DevOps Wiki to GitHub Wiki migration tool](https://github.com/bastienwirtz/azure-wiki-to-md) など（Wikiに特化）、もしくは[ado2gh](https://github.com/Microsoft/azure-devops-migration-tools) のようなツールで一部対応。  
   - 最新情報はGitHubのマーケットプレイスやMicrosoftドキュメントで確認するとよいでしょう。

#### 注意点
- **状態（ステータス）やラベル、コメント、リンク情報などは完全に1対1で移行できないことが多い**  
- **Azure Boards特有のプロセステンプレート (Scrum/Agile/CMMI) やクエリ、カスタムフィールド** などはGitHub IssuesやProjectsと概念が異なるため、部分的に移行不可となる場合あり

---

## 4. Wikiやアーティファクトの移行

### 4.1 Wikiの移行
Azure DevOpsのWikiは**Markdown**ベースなので、基本的にはMarkdownファイルを取得してGitHubリポジトリのWikiに配置することで移行可能です。  
- **Azure DevOps Wiki → GitHub Pages / GitHub Wiki / Docsサイト**などへ移行する場合は、Markdownをそのまま持っていけば最低限の対応はできます。  
- 相対パスや画像リンクなどは手動で修正が必要なケースがあります。

### 4.2 アーティファクト
NuGetパッケージなどのビルド成果物を**Azure Artifacts**で管理している場合、GitHubには**GitHub Packages**というパッケージ管理サービスがあります。  
- パッケージの種類（NuGet, npm, Mavenなど）によって移行方法が異なりますが、基本的には**パッケージを再発行**するのが手堅いアプローチです。  
- 既存のアーティファクトを丸ごと転送する機能は限定的なので、CI/CDパイプラインをGitHub Actionsに移行する際に**「ビルド → GitHub Packages へPush」**というフローを組むのが一般的です。

---

## まとめ

1. **リポジトリの移行**: 手動・インポート機能・gitコマンドいずれでも比較的容易に移行可能。ただしPull Requestやビルド履歴は移行されない。  
2. **パイプラインの移行**: Azure DevOps YAMLパイプライン → GitHub Actions YAML への書き換えが必要。ホストエージェントやタスクの置き換えを検討。  
3. **課題管理の移行**: Azure Boards → GitHub Issues/Projects への移行はツールやCSVの手動インポートを利用。プロセスやフィールドが1対1ではないため注意。  
4. **Wikiやアーティファクトの移行**: 基本的にMarkdownはコピーで移行可能。Azure Artifacts → GitHub Packagesへの移行はパッケージ再発行が多い。

Azure DevOpsからGitHubへの移行は、コードだけなら比較的スムーズですが、**パイプラインや課題管理の細かい要素を含めると完全自動化は難しく、ある程度手動作業やツールを組み合わせる必要があります**。移行範囲や粒度を明確化して、段階的に移行することをおすすめします。
