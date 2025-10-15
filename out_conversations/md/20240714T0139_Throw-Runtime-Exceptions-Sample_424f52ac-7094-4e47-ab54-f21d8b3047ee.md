---
conversation_id: "424f52ac-7094-4e47-ab54-f21d8b3047ee"
title: "Throw Runtime Exceptions Sample"
create_time: 1720921144.306359
update_time: 1720921182.31706
language_guess: "en"
num_messages: 7
part_index: 1
part_count: 1
---

### system — 2024-07-14T01:39:04.306359+00:00

_(empty)_

### user — 2024-07-14T01:39:04.314739+00:00

C#のtry-catchでruntime例外のみ上位にthrowするサンプル

### assistant — 2024-07-14T01:39:09.897421+00:00

_(empty)_

### assistant — 2024-07-14T01:39:09.897494+00:00

C#で`try-catch`ブロックを使用してランタイム例外のみを上位に再スローするサンプルコードを以下に示します。`Exception`クラスの`GetType`メソッドを使用して、キャッチした例外がランタイム例外かどうかをチェックし、ランタイム例外の場合のみ再スローします。

```csharp
using System;

namespace RuntimeExceptionHandling
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                PerformOperation();
            }
            catch (Exception ex)
            {
                if (ex.GetType().Namespace == "System")
                {
                    // 再スロー
                    throw;
                }
                else
                {
                    // ログ記録や他の処理
                    Console.WriteLine($"Caught exception: {ex.Message}");
                }
            }
        }

        static void PerformOperation()
        {
            try
            {
                // 例外が発生する可能性のある処理
                throw new InvalidOperationException("これはランタイム例外です。");
            }
            catch (Exception ex)
            {
                if (ex.GetType().Namespace == "System")
                {
                    // 再スロー
                    throw;
                }
                else
                {
                    // ログ記録や他の処理
                    Console.WriteLine($"Caught exception in PerformOperation: {ex.Message}");
                }
            }
        }
    }
}
```

このサンプルコードでは、`PerformOperation`メソッド内で例外を発生させ、それがランタイム例外であるかどうかをチェックします。ランタイム例外の場合は`throw`キーワードを使用して再スローし、そうでない場合はログに記録します。`Main`メソッドでも同様に例外を処理し、再スローします。

### user — 2024-07-14T01:39:32.824778+00:00

ex.GetType().Namespace == "System"となる例外を一覧化

### assistant — 2024-07-14T01:39:41.808673+00:00

`ex.GetType().Namespace == "System"`に一致する例外は、.NETの標準ランタイム例外です。主な例外の一覧は以下の通りです：

1. **System.ArgumentException**  
   無効な引数が渡された場合にスローされます。

2. **System.ArgumentNullException**  
   `null`の引数が渡された場合にスローされます。

3. **System.ArgumentOutOfRangeException**  
   引数が許容範囲外の場合にスローされます。

4. **System.ArithmeticException**  
   算術演算中にエラーが発生した場合にスローされます。
   
5. **System.ArrayTypeMismatchException**  
   配列型の不一致が発生した場合にスローされます。

6. **System.DivideByZeroException**  
   0で除算しようとした場合にスローされます。

7. **System.IndexOutOfRangeException**  
   配列やコレクションの範囲外のインデックスにアクセスしようとした場合にスローされます。

8. **System.InvalidCastException**  
   無効なキャストが行われた場合にスローされます。

9. **System.InvalidOperationException**  
   メソッドの呼び出しが無効な操作である場合にスローされます。

10. **System.NullReferenceException**  
    `null`オブジェクトを参照しようとした場合にスローされます。

11. **System.OutOfMemoryException**  
    メモリが不足した場合にスローされます。

12. **System.OverflowException**  
    算術演算のオーバーフローが発生した場合にスローされます。

13. **System.StackOverflowException**  
    スタックがオーバーフローした場合にスローされます。

14. **System.TypeInitializationException**  
    型の初期化子でエラーが発生した場合にスローされます。

15. **System.TypeLoadException**  
    型が読み込めない場合にスローされます。

16. **System.UnauthorizedAccessException**  
    I/Oエラーやアクセス許可のエラーが発生した場合にスローされます。

これらは主なランタイム例外であり、`System`名前空間に含まれています。これらの例外は、通常、アプリケーションの実行中に予期せず発生する可能性があり、適切に処理する必要があります。
