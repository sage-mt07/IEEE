---
conversation_id: "670ca57d-ec4c-8007-b086-666f55bf4ebe"
title: "ConcurrentQueue TryPeek 機能説明"
create_time: 1728882046.238703
update_time: 1728882053.587263
language_guess: "en"
num_messages: 5
part_index: 1
part_count: 1
---

### system — 2024-10-14T05:00:46.238703+00:00

_(empty)_

### user — 2024-10-14T05:00:46.246696+00:00

net8のConcurrentQueue<T>.TryPeek(T)はキューに１０こあるばあい、
１０回呼び出すとすべてのものを取り出せるのか

### assistant — 2024-10-14T05:00:52.299138+00:00

_(empty)_

### assistant — 2024-10-14T05:00:52.299367+00:00

`ConcurrentQueue<T>` の `TryPeek` メソッドは、キューから要素を「取り出す」わけではなく、「参照」するメソッドです。そのため、キュー内の要素は削除されません。

具体的には、`ConcurrentQueue<T>.TryPeek(T)` を 10 回呼び出しても、毎回先頭の要素を参照するだけで、キュー内の要素はそのまま残ります。つまり、10 回 `TryPeek` を呼び出しても最初の要素しか得られませんし、その要素はキューから消えないため、キュー内の他の要素を順に参照することはできません。

もし、キュー内の全ての要素を順に確認したい場合は、以下のように `TryDequeue` を使うとよいです。このメソッドは、キューから要素を取り出し、キューから削除します。

```csharp
ConcurrentQueue<int> queue = new ConcurrentQueue<int>();

// 10個の要素をキューに追加
for (int i = 0; i < 10; i++)
{
    queue.Enqueue(i);
}

// キュー内のすべての要素を取り出す
int item;
while (queue.TryDequeue(out item))
{
    Console.WriteLine(item);
}
```

このようにすれば、キュー内の全ての要素を順番に取り出すことができます。`TryPeek` は単に先頭の要素を参照するだけで、要素を取り出したり削除するためには使えないことを覚えておいてください。
