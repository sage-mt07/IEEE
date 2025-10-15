---
conversation_id: "67a7922e-8e0c-8007-a7b2-2a762cbce50a"
title: "protobuf-net CompatibilityLevel 使い方"
create_time: 1739035182.778041
update_time: 1740113740.476707
language_guess: "en"
num_messages: 11
part_index: 1
part_count: 1
---

### system — 2025-02-08T17:19:42.778041+00:00

_(empty)_

### user — 2025-02-08T17:19:42.781370+00:00

protobuf-netのCompatibilityLevelの使い方

### tool — 2025-02-08T17:20:06.036229+00:00

**Explaining CompatibilityLevel usage**

ユーザーの質問は「protobuf-netのCompatibilityLevelの使い方」ですね。protobuf-netは、GoogleのProtocol Buffersシリアライズフォーマットを.NETで利用するためのライブラリです。この「CompatibilityLevel」オプションは、プロトコルバッファのバージョン間の互換性に関わる設定です。具体的には、例えば「CompatibilityLevel.Level200」や「CompatibilityLevel.Level240」など、異なる互換性レベルがあり、これを使用することで動作が調整されるようです。

**Recalling CompatibilityLevel usage**

protobuf-netでの「CompatibilityLevel」の使い方を思い出しています。これは、生成されるコードやシリアライズの動作を変更し、古いバージョンとの互換性に影響を与えることがある属性です。たとえば、「ProtoContract(CompatibilityLevel = CompatibilityLevel.Level240)」のように指定できます。これにより、必要なフィールドとオプションのフィールドの扱いや、デフォルト値、nullの扱いに影響を与えることができます。互換性を維持するため、プロトコルバッファのバージョンを指定するために使います。

**説明とコード例**

protobuf-netの「CompatibilityLevel」は、シリアライズ時の互換性レベルを指定するために使用されます。例えば、proto2とproto3の違いや、古いバージョンとの互換性を保つために利用できます。次のように属性を使用します：

```csharp
[ProtoContract(CompatibilityLevel = CompatibilityLevel.Level240)]
public class Sample
{
    [ProtoMember(1)]
    public int Id { get; set; }

    [ProtoMember(2)]
    public string Name { get; set; }
}
```

これにより、指定の互換性レベルでシリアライズが行われます。

### assistant — 2025-02-08T17:20:06.036327+00:00

`protobuf-net` の `CompatibilityLevel` は、シリアライズ／デシリアライズ時の既定動作や将来的なライブラリ更新時の挙動変化に対して、互換性を明示的に指定するためのオプションです。これを利用することで、たとえば新バージョンで既定動作が変わった場合でも、以前のシリアライズ形式との互換性を維持できるようになります。

以下、基本的な使い方と注意点を説明します。

---

## 基本的な使い方

1. **クラスに `[ProtoContract]` 属性を付与する際に指定する**

   `CompatibilityLevel` は、`[ProtoContract]` 属性のプロパティとして設定できます。たとえば、クラスがシリアライズされる際に特定の互換性レベルを利用するには、次のように記述します。

   ```csharp
   using ProtoBuf;

   [ProtoContract(CompatibilityLevel = CompatibilityLevel.Level240)]
   public class SampleData
   {
       [ProtoMember(1)]
       public int Id { get; set; }
       
       [ProtoMember(2)]
       public string Name { get; set; }
   }
   ```

   上記の例では、`SampleData` クラスが `CompatibilityLevel.Level240` を使ってシリアライズされるよう指定しています。  
   ※ `CompatibilityLevel` の enum には複数のレベルが定義されており、プロジェクトの要件や既存データとの互換性に応じて適切なレベルを選択してください。

2. **グローバル設定（必要に応じて）**

   プロジェクト全体で互換性レベルを統一したい場合、`RuntimeTypeModel` を利用してグローバル設定する方法もあります（バージョンや利用状況によって記述方法は異なる可能性があります）。

   ```csharp
   var model = RuntimeTypeModel.Default;
   model.CompatibilityLevel = CompatibilityLevel.Level240;
   ```

   このようにグローバル設定を行うと、明示的に個別の `[ProtoContract]` で指定しない型に対しても、指定した互換性レベルが適用されます。

---

## 注意点

- **ライブラリ更新時の影響：**  
  `CompatibilityLevel` を指定しない場合、protobuf-net の既定の互換性レベルが適用されます。しかし、将来的なバージョンアップに伴い既定値が変更される可能性があるため、以前と同じシリアライズ形式を維持したい場合は明示的に設定しておくことをおすすめします。

- **既存データとの互換性：**  
  すでにシリアライズされたデータが存在する場合、シリアライズフォーマットが変わるとデシリアライズ時に問題が発生する恐れがあります。特に、古いクライアントやサービス間のやり取りがある場合は、互換性を維持するために適切な `CompatibilityLevel` を選択することが重要です。

- **Enum の詳細：**  
  利用可能な `CompatibilityLevel` の具体的な値（例: `Level240`、`Level300` など）やそれぞれの動作の詳細は、protobuf-net の公式ドキュメントやソースコード（GitHub リポジトリ等）で確認してください。バージョンによっては新たな値が追加されている場合もあります。

---

## まとめ

`protobuf-net` の `CompatibilityLevel` は、将来的なライブラリの更新に伴うシリアライズ／デシリアライズ動作の変化を抑制し、既存のデータとの互換性を保つために利用します。  
- **個別の型で指定する場合：** `[ProtoContract(CompatibilityLevel = CompatibilityLevel.適切なレベル)]` として設定  
- **グローバルに設定する場合：** `RuntimeTypeModel.Default.CompatibilityLevel` を利用  

これらの設定により、システム全体で安定した動作を維持することが可能になります。

必要に応じて、プロジェクトの要件や既存シリアライズデータのフォーマットを考慮して、最適な `CompatibilityLevel` を選んでください。

### user — 2025-02-08T17:21:33.859376+00:00

RuntimeTypeModel.Default.CompatibilityLevelを使用するためのパッケージ

### tool — 2025-02-08T17:21:41.638686+00:00

**Considering the required package**

ユーザーは「RuntimeTypeModel.Default.CompatibilityLevelを使用するためのパッケージ」を尋ねているようですね。これは、protobuf-netパッケージに関連していると思います。具体的には、CompatibilityLevelプロパティはprotobuf-netライブラリから提供されていますので、この機能を使用するために必要なパッケージは「protobuf-net」だと思われます。質問が特定のパッケージバージョンを指しているかもしれませんが、基本的にはprotobuf-netのNuGetパッケージが必要です。

**Providing the correct package**

「RuntimeTypeModel.Default.CompatibilityLevel」を使用するには、「protobuf-net」パッケージが必要です。これをNuGetからインストールできます。インストールコマンドは以下の通りです：

```shell
Install-Package protobuf-net
```

また、.NET CLIを使ってインストールする場合は、次のコマンドを使用できます：

```shell
dotnet add package protobuf-net
```

「CompatibilityLevel」プロパティはprotobuf-netのバージョン2.4.0以降で導入されたので、古いバージョンでは使用できません。

### assistant — 2025-02-08T17:21:41.638772+00:00

`RuntimeTypeModel.Default.CompatibilityLevel` プロパティは、**protobuf-net** ライブラリに含まれています。  
したがって、この機能を利用するためには、NuGet から **protobuf-net** パッケージをプロジェクトにインストールする必要があります。

---

### インストール方法

- **.NET CLI を使用する場合:**

  ```bash
  dotnet add package protobuf-net
  ```

- **Package Manager Console を使用する場合:**

  ```powershell
  Install-Package protobuf-net
  ```

---

### 注意点

- **バージョン確認:**  
  `CompatibilityLevel` プロパティは、protobuf-net の特定のバージョン以降でサポートされています。使用しているバージョンがこのプロパティに対応しているか、[protobuf-net のリリースノート](https://github.com/protobuf-net/protobuf-net/releases)などで確認してください。

- **ドキュメントの参照:**  
  プロパティの詳細な使用方法や設定可能な互換性レベルの値については、[protobuf-net の公式ドキュメント](https://github.com/protobuf-net/protobuf-net)を参照することをおすすめします。

これで、`RuntimeTypeModel.Default.CompatibilityLevel` を利用するために必要なパッケージは **protobuf-net** となります。

### user — 2025-02-08T17:22:21.865054+00:00

protobuf-netの2.4.8を使用しているが、そのメソッドがない

### tool — 2025-02-08T17:22:27.860935+00:00

**確認中：protobuf-netの対応バージョン**

protobuf-net 2.4.8では、`RuntimeTypeModel.Default.CompatibilityLevel`プロパティは存在しません。このプロパティは、新しいバージョンで追加されたものです。もしこの機能を使いたいなら、バージョンアップを検討する必要があるかもしれません。ちなみに、古いバージョンでは一部のプロパティが欠けていることがありますので、その点も考慮するべきです。ドキュメントを確認しつつ、他の方法を検討しますね。

### assistant — 2025-02-08T17:22:27.861040+00:00

protobuf-net 2.4.8 では、`RuntimeTypeModel.Default.CompatibilityLevel` プロパティは実装されていません。  
このプロパティ（および関連する互換性レベルの機能）は、後続のバージョン（主に protobuf-net v3 以降）で追加されたため、2.4.8 では利用できません。

### 対応方法

1. **アップグレードの検討**  
   CompatibilityLevel の機能が必要な場合は、protobuf-net のバージョンアップをご検討ください。  
   - **メリット：** 新機能やバグ修正、互換性レベルの指定など、より柔軟な制御が可能になります。  
   - **注意点：** バージョンアップに伴い、既存のシリアライズデータやコードとの互換性に影響が出る可能性があるため、事前のテストやリファクタリングが必要となる場合があります。

2. **現状の利用方法の見直し**  
   もしバージョンアップが困難な場合、現在のバージョンの仕様に従った利用方法や、既存の設定で対応する方法を再検討する必要があります。ただし、v2.4.8 には `CompatibilityLevel` に相当する明示的な設定は用意されていないため、アップグレードが最も推奨される対応策となります。

### まとめ

- **protobuf-net 2.4.8** には `CompatibilityLevel` プロパティは存在しない。  
- **機能利用のためには**、protobuf-net を v3 以降にアップグレードする必要がある。  

アップグレード時には、リリースノートや移行ガイドを確認して、既存コードやシリアライズデータへの影響を十分に評価することをおすすめします。
