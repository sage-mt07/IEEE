---
conversation_id: "6710c82f-3190-8007-8cf1-f0f269492aa5"
title: "BlockingCollectionとCancellationToken"
create_time: 1729153071.348894
update_time: 1729153098.675136
language_guess: "en"
num_messages: 5
part_index: 1
part_count: 1
---

### system — 2024-10-17T08:17:51.348894+00:00

_(empty)_

### user — 2024-10-17T08:17:51.352944+00:00

net8ノblockingcollectionﾆCancelTokenをセッテイ
ジカンケイカデシュウリョウスルバアイ。レイガイガハッセイスルノカ

### assistant — 2024-10-17T08:18:07.150774+00:00

_(empty)_

### assistant — 2024-10-17T08:18:07.150863+00:00

`BlockingCollection` において、`CancellationToken` を使用して時間経過後に処理を終了させる場合、例外として `OperationCanceledException` が発生する可能性があります。具体的には、`TryAdd` や `TryTake` メソッドの呼び出し時に `CancellationToken` がキャンセルされると、この例外がスローされます。

以下のように `CancellationToken` を使ったコード例を示します。

```csharp
var blockingCollection = new BlockingCollection<int>();
var cts = new CancellationTokenSource();
cts.CancelAfter(TimeSpan.FromSeconds(10)); // 10秒後にキャンセル

try
{
    while (true)
    {
        int item = blockingCollection.Take(cts.Token);
        // 取り出したアイテムに対する処理
    }
}
catch (OperationCanceledException)
{
    Console.WriteLine("処理がキャンセルされました。");
}
finally
{
    blockingCollection.Dispose();
}
```

このコードでは、`CancellationToken` がキャンセルされた時点で `OperationCanceledException` がスローされ、`catch` ブロックでそれをキャッチして処理を停止します。
