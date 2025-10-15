---
conversation_id: "07526c91-6533-4f85-8fb8-bd06e6848b5b"
title: "Redshift PowerBI Pipeline Switching"
create_time: 1675754117.915221
update_time: 1675754117.915221
language_guess: "en"
num_messages: 9
part_index: 1
part_count: 1
---

### system — 2023-02-07T07:15:17.915221+00:00

_(empty)_

### user — 2023-02-07T07:15:17.915872+00:00

redshiftへ接続するpowerbi上のレポートに関してパイプラインを利用し、オンプレミスデータゲートウェイの接続先を自動で切り替えるルールの設定方法

### assistant — 2023-02-07T07:16:42.851147+00:00

Power BI Desktop で Redshift に接続する場合、通常は Power BI Desktop 上で直接接続しますが、オンプレミスデータゲートウェイを使用することで、データを安全に保護しながら Redshift へ接続することもできます。オンプレミスデータゲートウェイを使用する場合、Power BI Desktop から Redshift への接続先を自動的に切り替えるには、次の手順を実行します。

1. Power BI Desktop 上で、「データ」タブを開き、「接続」を選択します。
2. 「SQL Server」を選択し、「オンプレミスデータゲートウェイ」を選択します。
3. 「新しいデータソース」を選択し、「Redshift」を選択します。
4. 「接続文字列」を指定します。
5.「接続先」を選択し、「データゲートウェイ」を選択します。
6.「データゲートウェイの管理」を選択し、「データゲートウェイのホスト」を選択します。
7.「データゲートウェイ」に接続します。
8.「データの読み込み」を実行します。

これで、Power BI Desktop から Redshift への接続先が自動的に切り替わります。

### user — 2023-02-07T07:17:57.808765+00:00

redshiftへ接続するpowerbi上のレポートに関してパイプラインを利用し、オンプレミスデータゲートウェイの接続先を自動で切り替えるルールの設定方法

### assistant — 2023-02-07T07:18:18.744671+00:00

Power BI Desktop 上で Redshift に接続する場合、オンプレミスデータゲートウェイを介して接続することができます。これにより、Redshift に接

### user — 2023-02-07T07:18:30.770817+00:00

redshiftへ接続するpowerbiサービス上のレポートに関してパイプラインを利用し、オンプレミスデータゲートウェイの接続先を自動で切り替えるルールの設定方法

### assistant — 2023-02-07T07:20:10.913368+00:00

Power BI Service で Redshift に接続する場合、オンプレミスデータゲートウェイを介して接続することができます。これにより、Redshift に接続する際にデータを保護することができます。次の手順に従って、Power BI Service 上でオンプレミスデータゲートウェイを使用して Redshift に接続する方法を説明します。

1. Power BI Service にサインインします。
2. [Workspace] を選択し、新しいワークスペースを作成または既存のワークスペースを選択します。
3. [Datasets] を選択し、[New Dataset] を選択します。
4. [Get Data] を選択します。
5. [SQL Server] を選択します。
6. [On-premises data gateway (recommended)] を選択します。
7. [Next] を選択します。
8. [Server name] に Redshift のサーバー名を入力します。
9. [Database name] に Redshift のデータベース名を入力します。
10. [Username] と [Password] を入力します。
11. [Sign In] を選択します。
12. [Load] を選択します。

これで、Power BI Service 上で Redshift に接続するためのオンプレミスデータゲートウェイが設定されました。以降、このデータセットを使用してレポートを作成することができます。

注意: オンプレミスデータゲートウェイが正常に設定されていることを確認するために、まずはローカルマシン上で同じ手順を試してみてください。

### assistant — 2023-02-07T07:27:03.656838+00:00

Power BI サービス上で Redshift に接続する場合、次の手順を実行することで、オンプレミスデータゲートウェイを介して接続することができます。

1. Power BI サービス上で、「Workspace」を選択します。
2.「Datasets」タブを選択します。
3.「New dataset」を選択します。
4.「SQL Server」を選択します。
5.「Redshift」を選択します。
6.「SQL Server」接続設定を完了します。
7.「Data source credentials」タブを選択します。
8.「Use a data gateway」を選択します。
9.「On-premises data gateway」を選択します。
10.「Publish」を選択します。

これにより、Power BI サービス上のレポートが Redshift に接続する際に、オンプレミスデータゲートウェイを介して接続することができます。また、このような接続設定を利用することで、Redshift への接続先を自動的に切り替えるルールを設定することができます。
