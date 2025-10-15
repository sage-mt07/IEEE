---
conversation_id: "681ac3dc-d26c-8007-a174-e509a13c5b44"
title: "GitHub Enterprise ExpressRoute利用"
create_time: 1746584540.996678
update_time: 1746587962.949869
language_guess: "en"
num_messages: 19
part_index: 1
part_count: 1
---

### user — 2025-05-07T02:22:20.174000+00:00

Github enterprise はexpress route経由で使用できるか

### system — 2025-05-07T02:22:20.996678+00:00

_(empty)_

### assistant — 2025-05-07T02:22:21.245117+00:00

はい、**GitHub Enterprise Server** は ExpressRoute 経由で使用可能です。ただし、いくつかの前提条件と構成の注意点があります。

---

### 【前提】GitHub Enterpriseの種類

| 種類 | ExpressRoute 対応可否 | 備考 |
|------|-------------------------|------|
| GitHub.com (クラウド版) | **不可** | インターネット経由でのみアクセス可能。ExpressRoute は非対応。 |
| GitHub Enterprise Server（オンプレ／VM展開型） | **可** | 自社ネットワーク内または Azure 上の仮想マシンとして展開し、ExpressRoute 経由でアクセス可能。 |

---

### 【GitHub Enterprise ServerをExpressRouteで利用する構成例】

#### ケース：GitHub Enterprise Server を Azure VM 上に構築

1. **Hub & Spoke VNET 構成**を使用  
   - GitHub Enterprise Server を配置した Azure VNET（Spoke）
   - ExpressRoute Gateway と Azure Firewall を配置した Hub VNET

2. **オンプレミスと GitHub Server の間の通信経路**
   - ExpressRoute → Gateway → Azure Firewall → GitHub Enterprise Server（VM）

3. **セキュリティ管理**
   - Azure Firewall で IP/ServiceTag による制御
   - NSG によるポート制限
   - 必要に応じて TLS/SSL 証明書の管理

---

### 【注意点】

- **GitHub.com（クラウド版）との通信が必要な場合あり**（Actions、Packages など一部機能）  
  ⇒ ExpressRoute ではなく、Microsoft ピアリングやプロキシ経由の制御が必要になるケースもあります。
- **DNS 解決の調整が必要**（Private DNS Zone の活用）

---

必要であれば、Azure 構成図付きで例を提示できます。構成をご検討中でしょうか？

### assistant — 2025-05-07T02:22:29.036285+00:00

_(empty)_

### user — 2025-05-07T02:24:04.323000+00:00

Microsoft peeringに対応しているのか

### assistant — 2025-05-07T02:24:05.592776+00:00

GitHub Enterprise Server は **Microsoft Peering には対応していません**。  
理由は以下の通りです：

---

### 【Microsoft Peering とは】
Microsoft Peering は ExpressRoute を使って Microsoft 365 や Azure PaaS（Storage、SQL Database、Key Vaultなど）と **Microsoft のパブリック IP を経由して通信する手段**です。

---

### 【GitHub.com の通信先について】

GitHub（github.com や api.github.com）は **Microsoft の IP アドレス空間ではなく、独自の ASN（Autonomous System Number）** を使って運用されています。

- GitHub の ASN: `AS36459`（GitHub 自社運用）
- Microsoft Peering が対象とする IP 範囲には含まれない

つまり：

> **GitHub.com の通信は ExpressRoute の Microsoft Peering 経由では到達できません。**

---

### 【代替手段】

- GitHub Enterprise Server を Azure 上に構築し、ExpressRoute の **Private Peering** 経由でアクセス
- GitHub.com を使用する場合は **インターネット経由**または **プロキシ/ファイアウォール制御**でアクセス管理

---

必要であれば、GitHub.com 向けの IP アドレス制御や通信許可のベストプラクティスもお伝えできます。ご希望ですか？

### user — 2025-05-07T02:26:26.631000+00:00

Github enterprise はazure entraid を使用できるか

### assistant — 2025-05-07T02:26:27.814812+00:00

はい、**GitHub Enterprise は Azure Entra ID（旧称 Azure AD）と連携できます**。  
ただし、GitHubのどの製品を使うかによって対応状況が異なります。

---

### 【製品別の対応状況】

| GitHub 製品                     | Entra ID 連携        | 補足 |
|------------------------------|----------------------|------|
| **GitHub.com（クラウド版）Enterprise Cloud** | **可能**              | Entra ID を SAML IdP として設定可（SSO対応） |
| **GitHub Enterprise Server（オンプレ or Azure VM）** | **可能**              | Entra ID を SAML または OIDC IdP として連携 |

---

### 【GitHub Enterprise Cloud + Entra ID】

- Entra ID を **SAML SSO** の IdP（Identity Provider）として使用可能
- SSO を有効にすると、ユーザーは GitHub へのログイン時に Entra ID 認証を通過する必要がある
- 条件付きアクセスや MFA（多要素認証）も Entra ID 側で適用可能

参考: [GitHub Docs - Enabling SAML SSO](https://docs.github.com/en/enterprise-cloud@latest/admin/authentication/managing-identity-and-access-management-for-your-enterprise/enabling-saml-single-sign-on-for-your-enterprise)

---

### 【GitHub Enterprise Server + Entra ID】

- **Entra ID を SAML または OIDC の IdP** として構成可能
- GitHub Enterprise Server の設定で IdP メタデータ URL を登録
- Azure 側ではエンタープライズアプリとして GitHub Enterprise Server を構成

参考: [GitHub Docs - SAML for Enterprise Server](https://docs.github.com/en/enterprise-server@latest/admin/authentication/using-saml)

---

必要であれば、Azure ポータルでの設定手順や GitHub 側の構成方法もご案内できます。構成をご検討中でしょうか？

### user — 2025-05-07T02:46:04.150000+00:00

Github enterprise へのアクセスをインターネットを経由しない方法

### assistant — 2025-05-07T02:46:04.956562+00:00

GitHub Enterprise へのアクセスを **インターネットを経由せずに実現する方法**は、オンプレミスまたは仮想ネットワーク内にデプロイ可能な **GitHub Enterprise Server（GHES）** を使用する構成です。

---

## 【方法】GitHub Enterprise Server を社内ネットワークに構築

### 1. **オンプレミス環境または Azure VNET に GHES を構築**
- 仮想アプライアンス（OVA/VHD）形式で GitHub Enterprise Server をデプロイ
- 通信は社内 LAN または ExpressRoute 経由のプライベート接続に限定

### 2. **ExpressRoute + Azure 上の構成（推奨例）**

| 構成要素 | 説明 |
|----------|------|
| **GitHub Enterprise Server** | Azure VM（VNET）上にデプロイ（またはオンプレ） |
| **ExpressRoute** | オンプレから Azure へのプライベート接続 |
| **Private Peering** | Azure 上の GHES へトラフィックを流す |
| **Azure Firewall / NSG** | インターネットからの不要なアクセスをブロック |
| **DNS（Private DNS Zone）** | GHES 用の内部名前解決を構成（例：`github.company.local`） |

---

## 【GitHub.com との通信を遮断する方法】

GHES はデフォルトで GitHub.com への通信（Actions, Container Registry 連携など）も使用可能ですが、**完全スタンドアロン構成**も可能です。

- **インターネット非依存構成オプション：**
  - GitHub Actions などの一部機能は利用不可
  - セキュリティ更新や Marketplace 連携なども限定される
  - 外部接続なしの環境構築は正式にサポートされています（Air-gapped 環境）

参考: [GitHub Docs - Air-gapped](https://docs.github.com/en/enterprise-server@latest/admin/installation/network-configuration-recommendations-for-github-enterprise-server)

---

## 【まとめ】

| 要件 | 対応方法 |
|------|----------|
| インターネットを経由しない | GHES を社内または Azure VNET に構築、ExpressRoute + Private Peering |
| Entra ID 認証連携 | SAML / OIDC 経由で社内認証基盤として利用可能 |
| 外部サービス連携不可にしたい | Air-gapped モードを使用し、GitHub.com との通信を遮断 |

---

構成図やサンプルネットワーク設計が必要であれば、作成しますか？

### user — 2025-05-07T02:58:57.324000+00:00

Express routeはazure devops serviceで利用できるのか

### assistant — 2025-05-07T02:58:59.271238+00:00

いいえ、**Azure DevOps Services（dev.azure.com）自体は ExpressRoute に対応していません**。  
つまり、**Azure DevOps へのアクセスはインターネット経由に限定**されます。

---

## 【詳細説明】

### Azure DevOps Services の通信特性：

| 項目 | 内容 |
|------|------|
| サービス提供場所 | Azure グローバルクラウド（dev.azure.com） |
| 通信方式 | **HTTPS over Internet（443番ポート）** |
| ExpressRoute 対応 | **非対応（Microsoft Peering でも不可）** |
| セキュリティ制御手段 | IPフィルタリング、プロキシ、Azure AD 条件付きアクセスなど |

---

## 【補足】なぜ ExpressRoute では使えないのか？

- **Azure DevOps Services は Microsoft Peering の対象外**  
  → Microsoft Peering で接続可能なサービス（例：Storage, SQL Database）に **dev.azure.com は含まれません**。

- `dev.azure.com` は [public Azure IP 範囲](https://www.microsoft.com/en-us/download/details.aspx?id=56519) にも含まれていません。

---

## 【代替策】

### 通信制御したい場合：

| 目的 | 方法 |
|------|------|
| 通信の出口制御 | **プロキシ経由で dev.azure.com への通信を制限** |
| クライアント制御 | Entra ID の **条件付きアクセス**で制限（MFA、デバイス制限など） |
| プライベート環境からのパイプライン実行 | Azure VM + Private Link + self-hosted agent を使用（詳細は下記） |

---

## 【補足】Azure DevOps を閉域から使う唯一の構成

- **自己ホスト型エージェント（Self-hosted agent）を ExpressRoute 内に設置**
  - → dev.azure.com はインターネット経由でアクセスするが、ビルド／デプロイ先は閉域（ExpressRoute内）に限定可能

---

## 【まとめ】

| 目的 | 対応可否 | 解説 |
|------|-----------|------|
| dev.azure.com へ ExpressRoute 経由で直接アクセス | **不可** | インターネット経由のみ |
| 閉域内システムへの DevOps 自動デプロイ | **可能** | self-hosted agent を ExpressRoute 内に設置 |

---

必要であれば、self-hosted agent を使った構成図も作成可能です。作成しますか？

### user — 2025-05-07T03:15:03.227000+00:00

Defender for cloud とAzure fire wallの違い

### assistant — 2025-05-07T03:15:04.310535+00:00

**Microsoft Defender for Cloud** と **Azure Firewall** は目的も機能も異なるセキュリティサービスです。それぞれの違いは以下の通りです。

---

## 【目的の違い】

| 項目                     | Defender for Cloud                        | Azure Firewall                         |
|--------------------------|--------------------------------------------|-----------------------------------------|
| 主な役割                 | **セキュリティの可視化・脅威検出・推奨** | **ネットワークレベルの通信制御**        |
| 保護対象                 | Azure リソース全体（VM、App Serviceなど） | Azure 上の VNET 間または外部との通信    |
| 機能カテゴリ             | セキュリティ管理 / 脆弱性検出 / XDR連携 | L3～L7 ファイアウォール（通信制御）     |

---

## 【機能の比較】

| 機能                     | Defender for Cloud                      | Azure Firewall                         |
|--------------------------|------------------------------------------|-----------------------------------------|
| セキュリティスコアの提供 | あり（Secure Score）                    | なし                                    |
| 脆弱性スキャン            | あり（VM, Containerなど）               | なし                                    |
| 通信の許可/拒否           | なし（制御はしない）                   | あり（NSGより詳細な制御が可能）         |
| ログの記録               | 活動の可視化（Log Analyticsと連携）    | あり（Traffic Log, Threat Intelligence）|
| 自動応答・修復提案       | あり（ポリシー、推奨アクション）        | なし（ルール手動設定）                  |
| IDS/IPS（侵入検知）      | Microsoft Defender for Endpointなどと連携 | Threat Intelligence による遮断あり     |

---

## 【よくある使い分け】

| シナリオ | 推奨サービス |
|----------|--------------|
| VM に脆弱性があるか確認したい | Defender for Cloud |
| ある URL へのアクセスを遮断したい | Azure Firewall |
| コンテナやSQLのセキュリティ状態を評価したい | Defender for Cloud |
| 特定の通信のみ通過させたい（IP制限） | Azure Firewall |
| Azure 環境の全体的なセキュリティスコアを見たい | Defender for Cloud |

---

## 【まとめ】

- **Defender for Cloud**：  
  セキュリティの「監視・検出・評価」機能（セキュリティセンターの役割）

- **Azure Firewall**：  
  ネットワークレベルの「アクセス制御」機能（実際に通信をブロック）

---

必要であれば、両方を組み合わせたセキュリティ構成例もご提案できます。ご希望ですか？

### user — 2025-05-07T03:17:35.570000+00:00

Express route にMicrosoft peering 経由で同じリージョンのサービスを接続した場合のネットワーク課金について

### assistant — 2025-05-07T03:17:36.625430+00:00

ExpressRoute の **Microsoft Peering 経由で同じ Azure リージョンのサービスに接続した場合でも、ネットワーク転送料金は発生します**。

---

## 【要点まとめ】

| 項目 | 内容 |
|------|------|
| 接続方式 | ExpressRoute Microsoft Peering |
| アクセス先 | Azure PaaS サービス（例：Storage, SQL, Key Vault など） |
| リージョン | 同一リージョン（例：東日本 → 東日本） |
| 通信経路 | **Microsoft のグローバルバックボーンネットワーク経由** |
| **転送料金** | **発生する（Egress課金あり）** |
| **Ingress（受信）** | 無料 |

---

## 【料金の特徴】

- **Egress（送信）データ**：ExpressRoute 経由で Azure サービスへデータを送信 → **課金対象**
- **Ingress（受信）データ**：Azure から戻ってくるデータ → **無料**

> ※ リージョンが同じであっても、**Microsoft Peering の対象は Azure の PaaS サービスの「Public IP」に対する通信**なので、**Private Peering（VNET接続）と異なり無料にはなりません**。

---

## 【参考資料】

- Microsoft公式: [ExpressRoute の課金と価格体系](https://azure.microsoft.com/ja-jp/pricing/details/expressroute/)
- 帯域幅料金は「Egress データ転送量（GB単位）」に応じて課金される
- データ転送料金は選択した帯域幅とリージョンによって異なる（例：5 TB/月で ¥xx,xxx など）

---

## 【補足】料金を抑えたい場合の選択肢

| 方法 | 概要 |
|------|------|
| **Private Peering（VNET）への接続** | 同一リージョン内なら、VNET 経由で Azure VM・Private Endpoint などに接続すればデータ転送料金がかからない構成にできる |
| **Private Link** + ExpressRoute Private Peering | PaaS を Private Endpoint 経由で使用（Microsoft Peering を使わない）ことで、課金を抑えつつ閉域アクセス可能 |

---

必要であれば、Private Link 経由で同一リージョン通信にした場合の課金比較もお示しできますか？

### user — 2025-05-07T03:19:09.900000+00:00

サービス間接続の課金は

### assistant — 2025-05-07T03:19:10.976102+00:00

Azure における「**サービス間接続（Service-to-Service 通信）**」の課金は、**接続方式・リージョン間関係・通信対象サービスの種別**によって変わります。以下に代表的なケースと課金有無を整理します。

---

## 【1. 仮想ネットワーク（VNet）間通信】

| 条件 | 通信内容 | 通信料（送信側） |
|------|----------|------------------|
| **同一リージョン・同一サブスクリプション内の VNet ピアリング** | VM → VM（VNet Peering） | **無料**（2021年以降） |
| **同一リージョン・異サブスクリプション VNet ピアリング** | VM → VM | **無料**（同上） |
| **異なるリージョン間の VNet ピアリング** | VM → VM | **課金あり（リージョン間データ転送）** |

---

## 【2. Private Link（Private Endpoint 経由）】

| 通信対象 | リージョン | 通信料 |
|----------|------------|--------|
| 同一リージョンの Private Endpoint へのアクセス | 同一リージョン | **無料（転送）＋ Private Link 利用料** |
| 異なるリージョンの Private Endpoint | 跨る | **転送料金が発生（リージョン間）＋ 利用料** |

> ※ Private Link は Azure PaaS サービス（Storage, SQLなど）を仮想ネットワークから**閉域接続**する方法です。

---

## 【3. Microsoft Peering 経由のサービス間通信】

| 例 | 通信料 |
|----|--------|
| オンプレ → Microsoft Peering 経由 → Azure SQL | **送信分課金（Egress）** |
| ExpressRoute で Azure PaaS にアクセス（同一リージョン） | **送信分課金** |

---

## 【4. 同一 Azure サービス間の通信（例：App Service → SQL Database）】

| 条件 | 通信方法 | 課金 |
|------|----------|------|
| 同一リージョン | インターネット経由 or 内部エンドポイント | **無料または内部接続扱いで安価** |
| 異なるリージョン | Azure バックボーン利用 | **リージョン間通信として課金あり** |

---

## 【5. コンテナ・Function・App Service など間の通信】

- 同一リージョンであれば基本 **課金なし**
- 異なるリージョン間であれば **課金あり（Egress）**

---

## 【まとめ表】

| 通信経路 | 同一リージョン | 異リージョン | 備考 |
|-----------|----------------|--------------|------|
| VNet Peering | 無料 | 課金あり | |
| Private Link | 利用料のみ | 転送料＋利用料 | |
| Microsoft Peering | 常に課金あり | 課金あり | |
| Azure サービス間 | 無料 or 安価 | 課金あり | サービスにより変動 |

---

ご利用中の具体的な構成があれば、それに応じた課金試算も可能です。構成を共有いただけますか？
