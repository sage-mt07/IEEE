---
conversation_id: "68cb05f2-15ac-8325-9a1d-baa441a1e23a"
title: "Query stabilization issue"
create_time: 1758135796.289349
update_time: 1758135938.60658
language_guess: "en"
num_messages: 11
part_index: 1
part_count: 1
---

### user — 2025-09-17T19:03:14.863000+00:00

warn: Kafka.Ksql.Linq.KsqlContext[0]
      Derived query stabilization failed for Bar (attempt 2/3)
      System.TimeoutException: CTAS/CSAS query for bar_tbimp_1m_live did not reach RUNNING within 300s
         at Kafka.Ksql.Linq.KsqlContext.WaitForQueryRunningAsync(String targetEntityName, TimeSpan timeout)
         at Kafka.Ksql.Linq.KsqlContext.WaitForDerivedQueriesRunningAsync(TimeSpan timeout)
         at Kafka.Ksql.Linq.KsqlContext.&lt;&gt;c__DisplayClass95_0.&lt;&lt;EnsureQueryEntityDdlAsync&gt;g__EnsureDerivedQueryEntityDdlAsync|0&gt;d.MoveNext()
info: Kafka.Ksql.Linq.KsqlContext[0]
      KSQL DDL (derived bar_tbimp_1s_final): CREATE TABLE bar_tbimp_1s_final WITH (KAFKA_TOPIC='bar_tbimp_1s_final', KEY_FORMAT='AVRO', VALUE_FORMAT='AVRO') AS
      SELECT o.BROKER AS Broker, o.SYMBOL AS Symbol, WINDOWSTART AS BucketStart, EARLIEST_BY_OFFSET(Bid) AS Open, MAX(Bid) AS High, MIN(Bid) AS Low, LATEST_BY_OFFSET(Bid) AS Close
      FROM TICKS_TBIMP o WINDOW TUMBLING (SIZE 1 SECONDS)
      GROUP BY o.BROKER, o.SYMBOL
      EMIT FINAL;
info: Kafka.Ksql.Linq.KsqlContext[0]
      ksql execute: EXECUTE SQL=CREATE TABLE bar_tbimp_1s_final WITH (KAFKA_TOPIC='bar_tbimp_1s_final', KEY_FORMAT='AVRO', VALUE_FORMAT='AVRO') AS SELEC...
info: Kafka.Ksql.Linq.KsqlContext[0]
      KSQL DDL (derived bar_tbimp_1s_final_s): CREATE STREAM bar_tbimp_1s_final_s (BROKER VARCHAR KEY, SYMBOL VARCHAR KEY, BUCKETSTART TIMESTAMP KEY, OPEN DECIMAL(18, 2), HIGH DECIMAL(18, 2), LOW DECIMAL(18, 2), CLOSE DECIMAL(18, 2)) WITH (KAFKA_TOPIC='bar_tbimp_1s_final', KEY_FORMAT='AVRO', VALUE_FORMAT='AVRO', PARTITIONS=1, REPLICAS=1);
info: Kafka.Ksql.Linq.KsqlContext[0]
      ksql execute: EXECUTE SQL=CREATE STREAM bar_tbimp_1s_final_s (BROKER VARCHAR KEY, SYMBOL VARCHAR KEY, BUCKETSTART TIMESTAMP KEY, OPEN DECIMAL(18, ...
info: Kafka.Ksql.Linq.KsqlContext[0]
      KSQL DDL (derived bar_tbimp_1m_live): CREATE TABLE bar_tbimp_1m_live WITH (KAFKA_TOPIC='bar_tbimp_1m_live', KEY_FORMAT='AVRO', VALUE_FORMAT='AVRO') AS
      SELECT o.BROKER AS Broker, o.SYMBOL AS Symbol, WINDOWSTART AS BucketStart, EARLIEST_BY_OFFSET(o.OPEN) AS Open, MAX(o.HIGH) AS High, MIN(o.LOW) AS Low, LATEST_BY_OFFSET(o.CLOSE) AS Close
      FROM bar_tbimp_1s_final_s o WINDOW TUMBLING (SIZE 1 MINUTES, GRACE PERIOD 2 SECONDS)
      GROUP BY o.BROKER, o.SYMBOL
      EMIT CHANGES;
info: Kafka.Ksql.Linq.KsqlContext[0]
      ksql execute: EXECUTE SQL=CREATE TABLE bar_tbimp_1m_live WITH (KAFKA_TOPIC='bar_tbimp_1m_live', KEY_FORMAT='AVRO', VALUE_FORMAT='AVRO') AS SELECT ...
info: Kafka.Ksql.Linq.KsqlContext[0]
      KSQL DDL (derived bar_tbimp_5m_live): CREATE TABLE bar_tbimp_5m_live WITH (KAFKA_TOPIC='bar_tbimp_5m_live', KEY_FORMAT='AVRO', VALUE_FORMAT='AVRO') AS
      SELECT o.BROKER AS Broker, o.SYMBOL AS Symbol, WINDOWSTART AS BucketStart, EARLIEST_BY_OFFSET(o.OPEN) AS Open, MAX(o.HIGH) AS High, MIN(o.LOW) AS Low, LATEST_BY_OFFSET(o.CLOSE) AS Close
      FROM bar_tbimp_1s_final_s o WINDOW TUMBLING (SIZE 5 MINUTES, GRACE PERIOD 3 SECONDS)
      GROUP BY o.BROKER, o.SYMBOL
      EMIT CHANGES;
info: Kafka.Ksql.Linq.KsqlContext[0]
      ksql execute: EXECUTE SQL=CREATE TABLE bar_tbimp_5m_live WITH (KAFKA_TOPIC='bar_tbimp_5m_live', KEY_FORMAT='AVRO', VALUE_FORMAT='AVRO') AS SELECT ...
warn: Kafka.Ksql.Linq.KsqlContext[0]
      Missing queryId in ksqlDB response for derived statement: CREATE TABLE bar_tbimp_1s_final WITH (KAFKA_TOPIC='bar_tbimp_1s_final', KEY_FORMAT='AVRO', VALUE_FORMAT='AVRO') AS
      SELECT o.BROKER AS Broker, o.SYMBOL AS Symbol, WINDOWSTART AS BucketStart, EARLIEST_BY_OFFSET(Bid) AS Open, MAX(Bid) AS High, MIN(Bid) AS Low, LATEST_BY_OFFSET(Bid) AS Close
      FROM TICKS_TBIMP o WINDOW TUMBLING (SIZE 1 SECONDS)
      GROUP BY o.BROKER, o.SYMBOL
      EMIT FINAL;
warn: Kafka.Ksql.Linq.KsqlContext[0]
      Missing queryId in ksqlDB response for derived statement: CREATE TABLE bar_tbimp_1m_live WITH (KAFKA_TOPIC='bar_tbimp_1m_live', KEY_FORMAT='AVRO', VALUE_FORMAT='AVRO') AS
      SELECT o.BROKER AS Broker, o.SYMBOL AS Symbol, WINDOWSTART AS BucketStart, EARLIEST_BY_OFFSET(o.OPEN) AS Open, MAX(o.HIGH) AS High, MIN(o.LOW) AS Low, LATEST_BY_OFFSET(o.CLOSE) AS Close
      FROM bar_tbimp_1s_final_s o WINDOW TUMBLING (SIZE 1 MINUTES, GRACE PERIOD 2 SECONDS)
      GROUP BY o.BROKER, o.SYMBOL
      EMIT CHANGES;
warn: Kafka.Ksql.Linq.KsqlContext[0]
      Missing queryId in ksqlDB response for derived statement: CREATE TABLE bar_tbimp_5m_live WITH (KAFKA_TOPIC='bar_tbimp_5m_live', KEY_FORMAT='AVRO', VALUE_FORMAT='AVRO') AS
      SELECT o.BROKER AS Broker, o.SYMBOL AS Symbol, WINDOWSTART AS BucketStart, EARLIEST_BY_OFFSET(o.OPEN) AS Open, MAX(o.HIGH) AS High, MIN(o.LOW) AS Low, LATEST_BY_OFFSET(o.CLOSE) AS Close
      FROM bar_tbimp_1s_final_s o WINDOW TUMBLING (SIZE 5 MINUTES, GRACE PERIOD 3 SECONDS)
      GROUP BY o.BROKER, o.SYMBOL
      EMIT CHANGES;

### system — 2025-09-17T19:03:16.289349+00:00

_(empty)_

### system — 2025-09-17T19:03:16.289349+00:00

_(empty)_

### assistant — 2025-09-17T19:03:17.395736+00:00

やあ司令、ログありがとう。状況と原因候補はだいたい特定できたよ。要点だけ手短に👇

# 症状
- `bar_tbimp_1m_live` が 300s 以内に `RUNNING` にならずリトライ。
- CTAS/CSAS 実行ログに対し `Missing queryId` が出ている。
- 1s→1m/5m の派生パイプラインで、`bar_tbimp_1s_final_s` を **既存トピック直読みの CREATE STREAM(スキーマ手書き)** で作っている。

# ほぼ核心の原因
1. **TABLE の変更ログトピックを「手書き CREATE STREAM」している点が不整合。**  
   `CREATE TABLE ... WINDOW TUMBLING` が作るトピックは **ウィンドウ付きキー（windowed key）** を持つ。  
   なのに `bar_tbimp_1s_final_s` では  
   ```sql
   (BROKER VARCHAR KEY, SYMBOL VARCHAR KEY, BUCKETSTART TIMESTAMP KEY, ...)
   WITH (KAFKA_TOPIC='bar_tbimp_1s_final', KEY_FORMAT='AVRO', VALUE_FORMAT='AVRO')
   ```
   と、**BUCKETSTART を “キー列” に置いてしまっている**。実体のキー符号化（window情報を含む）と宣言がズレるため、**内部リパーティションが永遠に安定せず RUNNING に到達しにくい**挙動になる。

2. **`Missing queryId` は「永続クエリになっていない扱い」に寄る**ケースが多い。  
   - 構文自体は受理されても、**キー/フォーマット不一致**や **依存の不整合**でコマンドキューに積まれた後にエラー遷移→`queryId` が付かない、というパターンが起こり得る。  
   - `CTAS/CSAS` では通常 `queryId` が返る（REST `/ksql` の `commandStatus` 内）が、**準備失敗/即時失敗**だと欠落する。

# 正しい作り方（1s TABLE → 1s STREAM）
**手書きの「同名トピック直読み CREATE STREAM」はやめて**、**CSAS で TABLE から STREAM を派生**させよう。ウィンドウは値側に `WINDOWSTART` を落として使う。

```sql
-- 1s の集計 TABLE（そのままでOK）
CREATE TABLE bar_tbimp_1s_final WITH (
  KAFKA_TOPIC='bar_tbimp_1s_final',
  KEY_FORMAT='AVRO',
  VALUE_FORMAT='AVRO'
) AS
SELECT
  o.BROKER        AS Broker,
  o.SYMBOL        AS Symbol,
  WINDOWSTART     AS BucketStart,
  EARLIEST_BY_OFFSET(Bid)  AS Open,
  MAX(Bid)        AS High,
  MIN(Bid)        AS Low,
  LATEST_BY_OFFSET(Bid)    AS Close
FROM TICKS_TBIMP o
WINDOW TUMBLING (SIZE 1 SECONDS)
GROUP BY o.BROKER, o.SYMBOL
EMIT FINAL;

-- ❌ 手書き CREATE STREAM … WITH (KAFKA_TOPIC='bar_tbimp_1s_final') はやめる
-- ✅ CSAS で TABLE からSTREAM化（キーは TABLE のまま、BucketStart は値列）
CREATE STREAM bar_tbimp_1s_final_s AS
SELECT
  Broker,
  Symbol,
  BucketStart,
  Open, High, Low, Close
FROM bar_tbimp_1s_final
EMIT CHANGES;
```

> ポイント  
> - こうすると **キーは windowed のまま**で正しい。`BucketStart` は **値**列として参照できる。  
> - 下流の 1m/5m は `WINDOW TUMBLING` と `GROUP BY Broker, Symbol`（キー列のみ）で OK。`BucketStart` を **GROUP BY に入れない**のは正しい（1m/5m の `BucketStart` は `WINDOWSTART` から再生成される）。

# 1m/5m 側の DDL 再掲（そのままで良いが、CSAS化に合わせて実行順を厳守）
```sql
CREATE TABLE bar_tbimp_1m_live WITH (
  KAFKA_TOPIC='bar_tbimp_1m_live',
  KEY_FORMAT='AVRO',
  VALUE_FORMAT='AVRO'
) AS
SELECT
  o.BROKER AS Broker,
  o.SYMBOL AS Symbol,
  WINDOWSTART AS BucketStart,
  EARLIEST_BY_OFFSET(o.OPEN)  AS Open,
  MAX(o.HIGH) AS High,
  MIN(o.LOW)  AS Low,
  LATEST_BY_OFFSET(o.CLOSE) AS Close
FROM bar_tbimp_1s_final_s o
WINDOW TUMBLING (SIZE 1 MINUTES, GRACE PERIOD 2 SECONDS)
GROUP BY o.BROKER, o.SYMBOL
EMIT CHANGES;

CREATE TABLE bar_tbimp_5m_live WITH (
  KAFKA_TOPIC='bar_tbimp_5m_live',
  KEY_FORMAT='AVRO',
  VALUE_FORMAT='AVRO'
) AS
SELECT
  o.BROKER AS Broker,
  o.SYMBOL AS Symbol,
  WINDOWSTART AS BucketStart,
  EARLLIEST_BY_OFFSET(o.OPEN) AS Open,
  MAX(o.HIGH) AS High,
  MIN(o.LOW)  AS Low,
  LATEST_BY_OFFSET(o.CLOSE) AS Close
FROM bar_tbimp_1s_final_s o
WINDOW TUMBLING (SIZE 5 MINUTES, GRACE PERIOD 3 SECONDS)
GROUP BY o.BROKER, o.SYMBOL
EMIT CHANGES;
```

# 実行順と安定化チェック
1. **既存の派生物を掃除**（衝突回避）  
   ```
   DROP TABLE IF EXISTS bar_tbimp_5m_live DELETE TOPIC;
   DROP TABLE IF EXISTS bar_tbimp_1m_live DELETE TOPIC;
   DROP STREAM IF EXISTS bar_tbimp_1s_final_s DELETE TOPIC;
   DROP TABLE  IF EXISTS bar_tbimp_1s_final DELETE TOPIC;
   ```
2. **1s TABLE → 1s CSAS STREAM → 1m → 5m** の順で DDL 作成。
3. それぞれで内部トピックができているか確認：  
   `SHOW TOPICS;` で
   - `...-Aggregate-GroupBy-repartition`
   - `...-changelog`  
   が **親トピックと同じパーティション数**になっているかを確認。
4. `SHOW QUERIES;` で各クエリに **queryId が付与**されているか確認。  
   付いていなければ直近の `ksqlDB server` ログで理由確認（キー/フォーマット不一致、サブジェクト不一致など）。

# ランタイム側の運用ヒント（今回の実装に合わせたもの）
- **`bar_tbimp_1s_final_s` は CSAS で作る**（これ前提で `WaitForDerivedQueriesRunningAsync` の安定化ロジックが効きやすくなる）。  
- **内部トピックの“事前作成”** は最後の手段。まずは **親のパーティション数に揃う**ことを確認（ズレていれば Admin で増減してもらう）。  
- **`EMIT CHANGES` を CTAS に付けても害はほぼないが、無くても良い**（文法上は SELECT 用）。気持ち悪ければ外してOK。  
- **`PARTITIONS=1` の指定は既存トピックには効かない**（既存なら無視される）。手書き STREAM をやめるので、ここも自然と解消。

---

必要なら、上の DDL を今の DSL 生成にあわせて **自動で CSAS に切り替えるパッチ**まで書くよ。まずは「手書き STREAM → CSAS」へ置換して再実行してみて。`queryId` がちゃんと付けば、`RUNNING` 到達まで滑らかになるはず。

送信日時（JST）: [[REDACTED_PHONE]]:34

### system — 2025-09-17T19:03:18.606764+00:00

_(empty)_

### system — 2025-09-17T19:03:18.613832+00:00

_(empty)_

### assistant — 2025-09-17T19:03:18.616075+00:00

_(empty)_

### assistant — 2025-09-17T19:03:18.835850+00:00

_(empty)_

### assistant — 2025-09-17T19:04:03.846585+00:00

_(empty)_

### user — 2025-09-17T19:05:38.572545+00:00

_(empty)_
