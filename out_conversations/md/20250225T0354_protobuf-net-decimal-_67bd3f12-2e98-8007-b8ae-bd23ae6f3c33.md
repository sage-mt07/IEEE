---
conversation_id: "67bd3f12-2e98-8007-b8ae-bd23ae6f3c33"
title: "protobuf-net decimal バイト数"
create_time: 1740455698.739708
update_time: 1740455716.041271
language_guess: "en"
num_messages: 5
part_index: 1
part_count: 1
---

### system — 2025-02-25T03:54:58.739708+00:00

_(empty)_

### user — 2025-02-25T03:54:58.748380+00:00

C# protobufnet decimalバイト数

### assistant — 2025-02-25T03:55:12.255388+00:00

_(empty)_

### assistant — 2025-02-25T03:55:12.255472+00:00

`protobuf-net` において `decimal` 型をシリアライズするときのバイト数は、エンコーディング方法によって異なります。

### `decimal` 型のエンコーディング方法
`protobuf-net` では `decimal` はネイティブの Protocol Buffers 型としてはサポートされておらず、カスタムの方法でシリアライズされます。通常、以下のようなフィールドに分割してエンコードされます。

- **`int lo`** (32ビット) - 下位の整数部分
- **`int mid`** (32ビット) - 中位の整数部分
- **`int hi`** (32ビット) - 上位の整数部分
- **`byte scale`** (8ビット) - スケール（小数点以下の桁数）
- **`bool sign`** (1ビット) - 符号（`true` なら負の値）

したがって、合計の最小バイト数は **13バイト（4+4+4+1+1=13）** です。

### `protobuf-net` における `decimal` のシリアライズ
デフォルトの設定では、`decimal` 型は `byte[]` に変換され、圧縮がかからないため、**13バイト固定** でシリアライズされます。

### 例: `decimal` を Protobuf メッセージとしてシリアライズ
```csharp
[ProtoContract]
public class Sample
{
    [ProtoMember(1)]
    public decimal Value { get; set; }
}

var obj = new Sample { Value = 123.45m };
using var ms = new MemoryStream();
Serializer.Serialize(ms, obj);
Console.WriteLine(ms.ToArray().Length);  // 15バイト (フィールドタグ含む)
```
この場合、実際の `decimal` のデータ部分が 13バイトで、それに **フィールドタグ（1バイト以上）** が加わるため、全体のバイト数は 15バイト程度になります。

### まとめ
- `decimal` のシリアライズデータは基本 **13バイト**
- `protobuf-net` の仕様で、タグ情報を含めると **15バイト前後**
- 圧縮や最適化オプションを指定しない限り、このサイズでエンコードされる

もし `decimal` のシリアライズサイズを小さくしたい場合、スケールと整数値を `int` や `long` で扱うカスタムシリアライザを作成する方法もあります。
