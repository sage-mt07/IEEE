---
conversation_id: "68909ce0-0a10-8325-a3e3-5d2374a165c2"
title: "Kafka exception troubleshooting"
create_time: 1754307812.586248
update_time: 1754902082.754285
language_guess: "en"
num_messages: 155
part_index: 2
part_count: 3
---

### user — 2025-08-04T12:30:14.378000+00:00

========== テストの実行を開始しています ==========
[xUnit.net 00:00:00.00] xUnit.net VSTest Adapter v2.5.6+bf9b858c26 (64-bit .NET 8.0.18)
[xUnit.net 00:00:00.05]   Starting:    Kafka.Ksql.Linq.Tests.Integration
dbug: Kafka.Ksql.Linq.Infrastructure.Admin.KafkaAdminService[0]
      KafkaAdminService initialized with BootstrapServers: localhost:9092
dbug: Kafka.Ksql.Linq.Infrastructure.Admin.KafkaAdminService[0]
      DB topic already exists: orders
dbug: Kafka.Ksql.Linq.Infrastructure.Admin.KafkaAdminService[0]
      DLQ topic already exists: dead.letter.queue
dbug: Kafka.Ksql.Linq.Infrastructure.Admin.KafkaAdminService[0]
      Kafka connectivity validated: 1 brokers available
info: Kafka.Ksql.Linq.KsqlContext[0]
      Kafka initialization completed; DLQ topic 'dead.letter.queue' ready with 5-second retention
info: Streamiz.Kafka.Net.KafkaStream[0]
      stream-application[ksql-dsl-app]  Start creation of the stream application with this configuration: 
      	Stream property:
      		client.id: 	
      		num.stream.threads: 	1
      		default.key.serdes: 	Streamiz.Kafka.Net.SerDes.StringSerDes
      		default.value.serdes: 	Streamiz.Kafka.Net.SerDes.StringSerDes
      		default.timestamp.extractor: 	Streamiz.Kafka.Net.Processors.Internal.FailOnInvalidTimestamp
      		commit.interval.ms: 	30000
      		processing.guarantee: 	AT_LEAST_ONCE
      		transaction.timeout: 	00:00:10
      		poll.ms: 	100
      		max.poll.records: 	500
      		max.poll.restoring.records: 	1000
      		max.task.idle.ms: 	0
      		buffered.records.per.partition: 	[[REDACTED_PHONE]]
      		inner.exception.handler: 	System.Func`2[System.Exception,Streamiz.Kafka.Net.ExceptionHandlerResponse]
      		production.exception.handler: 	System.Func`2[Confluent.Kafka.DeliveryReport`2[System.Byte[],System.Byte[]],Streamiz.Kafka.Net.ProductionExceptionHandlerResponse]
      		deserialization.exception.handler: 	System.Func`4[Streamiz.Kafka.Net.ProcessorContext,Confluent.Kafka.ConsumeResult`2[System.Byte[],System.Byte[]],System.Exception,Streamiz.Kafka.Net.ExceptionHandlerResponse]
      		rocksdb.config.setter: 	System.Action`2[System.String,Streamiz.Kafka.Net.State.RocksDbOptions]
      		follow.metadata: 	False
      		state.dir: 	C:\Temp\KAFKA_STATE
      		replication.factor: 	-1
      		windowstore.changelog.additional.retention.ms: 	[[REDACTED_PHONE]]
      		offset.checkpoint.manager: 	
      		metrics.interval.ms: 	30000
      		metrics.recording.level: 	INFO
      		log.processing.summary: 	00:01:00
      		metrics.reporter: 	System.Action`1[System.Collections.Generic.IEnumerable`1[Streamiz.Kafka.Net.Metrics.Sensor]]
      		expose.librdkafka.stats: 	False
      		start.task.delay.ms: 	5000
      		parallel.processing: 	False
      		max.degree.of.parallelism: 	8
      		statestore.cache.max.bytes: 	[[REDACTED_PHONE]]
      		application.id: 	ksql-dsl-app
      		schema.registry.url: 	http://localhost:8081
      	Client property:
      		bootstrap.servers: 	localhost:9092
      	Consumer property:
      		max.poll.interval.ms: 	[[REDACTED_PHONE]]
      		enable.auto.commit: 	False
      		enable.auto.offset.store: 	False
      		allow.auto.create.topics: 	False
      		partition.assignment.strategy: 	range
      	Producer property:
      		allow.auto.create.topics: 	False
      		partitioner: 	murmur2_random
      	Admin client property:
      		allow.auto.create.topics: 	False
info: Streamiz.Kafka.Net.Processors.Internal.StateDirectory[0]
      Reading UUID from process file: f5189da2-7b07-4664-b9d0-dd738323bc1e
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0] Creating consumer client
info: Streamiz.Kafka.Net.KafkaStream[0]
      stream-application[ksql-dsl-app] State transition from CREATED to REBALANCING
info: Kafka.Ksql.Linq.Core.Abstractions.IKsqlContext[0]
      KafkaStream state changed to: REBALANCING
info: Streamiz.Kafka.Net.KafkaStream[0]
      stream-application[ksql-dsl-app] Starting Streams client with this topology : Topologies:
         Sub-topology: 0
          Source: KSTREAM-SOURCE-[[REDACTED_PHONE]] (topics: [orders])
            --> KTABLE-SOURCE-[[REDACTED_PHONE]]
          Processor: KTABLE-SOURCE-[[REDACTED_PHONE]] (stores: [orders])
            --> none
            <-- KSTREAM-SOURCE-[[REDACTED_PHONE]]
dbug: Streamiz.Kafka.Net.Processors.DefaultTopicManager[0]
      Starting to apply internal topics for topology 0 in topic manager (try: 1, max retry : 10).
dbug: Streamiz.Kafka.Net.Processors.DefaultTopicManager[0]
      Complete to apply internal topics in topic manager
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0] Starting
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0] State transition from CREATED to STARTING
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
info: Streamiz.Kafka.Net.Kafka.Internal.StreamsRebalanceListener[0]
      New partitions assign requested : orders [[0]]
dbug: Streamiz.Kafka.Net.Processors.Internal.TaskCreator[0]
      Created task 0-0 with assigned partition orders [[0]]
dbug: Streamiz.Kafka.Net.Processors.Internal.TaskCreator[0]
      Created task 0-0 with assigned partition orders [[0]]
dbug: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Initializing state stores.
dbug: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Initializing state stores
dbug: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Initializing store orders
dbug: Streamiz.Kafka.Net.Metrics.Internal.RocksDbMetricsRecorder[0]
      Adding metrics recorder of task 0-0 to metrics recording trigger
dbug: Streamiz.Kafka.Net.Metrics.Internal.RocksDbMetricsRecorder[0]
      Adding value providers for store orders of task 0-0
dbug: Streamiz.Kafka.Net.Processors.Internal.ProcessorStateManager[0]
      stream-task[0|0] Registering state store orders to its state manager
dbug: Streamiz.Kafka.Net.Processors.Internal.ProcessorStateManager[0]
      stream-task[0|0] Registered state store orders to its state manager
dbug: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Initializing topology with theses source processors : KSTREAM-SOURCE-[[REDACTED_PHONE]].
dbug: Streamiz.Kafka.Net.Processors.SourceProcessor[0]
      stream-task[0|0]|processor[KSTREAM-SOURCE-[[REDACTED_PHONE]]]- Initializing process context
dbug: Streamiz.Kafka.Net.Processors.KTableSourceProcessor[0]
      stream-task[0|0]|processor[KTABLE-SOURCE-[[REDACTED_PHONE]]]- Initializing process context
dbug: Streamiz.Kafka.Net.Processors.KTableSourceProcessor[0]
      stream-task[0|0]|processor[KTABLE-SOURCE-[[REDACTED_PHONE]]]- Process context initialized
dbug: Streamiz.Kafka.Net.Processors.SourceProcessor[0]
      stream-task[0|0]|processor[KSTREAM-SOURCE-[[REDACTED_PHONE]]]- Process context initialized
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0] State transition from STARTING to PARTITIONS_ASSIGNED
info: Streamiz.Kafka.Net.Kafka.Internal.StreamsRebalanceListener[0]
      Partition assignment took 00:00:[[REDACTED_PHONE]] ms.
      	Currently assigned active tasks: 0-0
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0] State transition from PARTITIONS_ASSIGNED to RUNNING
info: Streamiz.Kafka.Net.KafkaStream[0]
      stream-application[ksql-dsl-app] State transition from REBALANCING to RUNNING
info: Kafka.Ksql.Linq.Core.Abstractions.IKsqlContext[0]
      KafkaStream state changed to: RUNNING
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0]  State is RUNNING, initializing and restoring tasks if necessary
dbug: Streamiz.Kafka.Net.Processors.Internal.ProcessorStateManager[0]
      Loaded offsets from checkpoint manager: 
info: Streamiz.Kafka.Net.Processors.Internal.ProcessorStateManager[0]
      State store orders did not find checkpoint offset, hence would default to the starting offset at changelog ksql-dsl-app-orders-changelog [[0]]
info: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Task 0-0 state transition from CREATED to RESTORING
info: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Restoration will start soon.
dbug: Streamiz.Kafka.Net.Processors.Internal.StoreChangelogReader[0]
      State store ksql-dsl-app-orders-changelog [[0]] metadata found (begin offset: 0 / end offset : 0)
dbug: Streamiz.Kafka.Net.Processors.Internal.StoreChangelogReader[0]
      Added partitions with offsets ksql-dsl-app-orders-changelog-[0]#Beginning [-2] to the restore consumer, current assignment is ksql-dsl-app-orders-changelog-[0]
info: Streamiz.Kafka.Net.Processors.Internal.StoreChangelogReader[0]
      Finished restoring changelog orders to store ksql-dsl-app-orders-changelog [[0]] with a total number of 0 records
dbug: Streamiz.Kafka.Net.Processors.Internal.StoreChangelogReader[0]
      Paused partition ksql-dsl-app-orders-changelog [[0]] from the restore consumer
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0]  State is RUNNING, initializing and restoring tasks if necessary
info: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Task 0-0 state transition from RESTORING to RUNNING
info: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Restored and ready to run
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      Restoration took 419ms for all tasks 0-0
dbug: Streamiz.Kafka.Net.Processors.Internal.StoreChangelogReader[0]
      Finished restoring all changelogs [ksql-dsl-app-orders-changelog-[0]]
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      Committing all active tasks 0-0 since 30000.816ms has elapsed (commit interval is 30000ms)
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      Committing all active tasks 0-0 since 30061.8078ms has elapsed (commit interval is 30000ms)
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      Processed 0 total records, ran 0 punctuators and committed 0 total tasks since the last update
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      Committing all active tasks 0-0 since 30042.401ms has elapsed (commit interval is 30000ms)
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      Committing all active tasks 0-0 since 30019.3669ms has elapsed (commit interval is 30000ms)
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      Processed 0 total records, ran 0 punctuators and committed 0 total tasks since the last update
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]

      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]

      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.

      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]

      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
fail: Kafka.Ksql.Linq.Cache.Core.RocksDbTableCache[0]
      Timeout while waiting for state store orders to become available
fail: Kafka.Ksql.Linq.KsqlContext[0]
      KsqlContext initialization failed: The state store, orders, may have migrated to another instance. 
      Streamiz.Kafka.Net.Errors.InvalidStateStoreException: The state store, orders, may have migrated to another instance.
         at Streamiz.Kafka.Net.State.Internal.QueryableStoreProvider.GetStore[T,K,V](StoreQueryParameters`3 storeQueryParameters)
         at Kafka.Ksql.Linq.Cache.Core.StreamizKafkaStreams.Store(StoreQueryParameters`3 parameters) in C:\rc\rc01\src\Cache\Core\StreamizKafkaStreams.cs:line 27
         at Kafka.Ksql.Linq.Cache.Core.RocksDbTableCache`1.InitializeAsync() in C:\rc\rc01\src\Cache\Core\RocksDbTableCache.cs:line 87
         at Kafka.Ksql.Linq.Cache.Core.RocksDbTableCache`1.InitializeAsync() in C:\rc\rc01\src\Cache\Core\RocksDbTableCache.cs:line 95
         at Kafka.Ksql.Linq.Cache.Core.TableCacheRegistry.InitializeCaches(IEnumerable`1 models, TableCacheOptions options, ISchemaRegistryClient schemaRegistryClient, ILoggerFactory loggerFactory) in C:\rc\rc01\src\Cache\Core\TableCacheRegistry.cs:line 52
         at Kafka.Ksql.Linq.Cache.Extensions.KsqlContextCacheExtensions.UseTableCache(IKsqlContext context, KsqlDslOptions options, ILoggerFactory loggerFactory, IKafkaStreams streams) in C:\rc\rc01\src\Cache\Extensions\KsqlContextCacheExtensions.cs:line 116
         at Kafka.Ksql.Linq.KsqlContext..ctor(KsqlDslOptions options, ILoggerFactory loggerFactory) in C:\rc\rc01\src\KsqlContext.cs:line 154
[xUnit.net 00:05:05.08]     Kafka.Ksql.Linq.Tests.Integration.CompositeKeyPocoTests.SendAndReceive_CompositeKeyPoco [FAIL]
[xUnit.net 00:05:05.08]       Streamiz.Kafka.Net.Errors.InvalidStateStoreException : The state store, orders, may have migrated to another instance.
[xUnit.net 00:05:05.08]       Stack Trace:
[xUnit.net 00:05:05.08]            at Streamiz.Kafka.Net.State.Internal.QueryableStoreProvider.GetStore[T,K,V](StoreQueryParameters`3 storeQueryParameters)
[xUnit.net 00:05:05.08]         C:\rc\rc01\src\Cache\Core\StreamizKafkaStreams.cs(27,0): at Kafka.Ksql.Linq.Cache.Core.StreamizKafkaStreams.Store(StoreQueryParameters`3 parameters)
[xUnit.net 00:05:05.08]         C:\rc\rc01\src\Cache\Core\RocksDbTableCache.cs(87,0): at Kafka.Ksql.Linq.Cache.Core.RocksDbTableCache`1.InitializeAsync()
[xUnit.net 00:05:05.08]         C:\rc\rc01\src\Cache\Core\RocksDbTableCache.cs(95,0): at Kafka.Ksql.Linq.Cache.Core.RocksDbTableCache`1.InitializeAsync()
[xUnit.net 00:05:05.08]         C:\rc\rc01\src\Cache\Core\TableCacheRegistry.cs(52,0): at Kafka.Ksql.Linq.Cache.Core.TableCacheRegistry.InitializeCaches(IEnumerable`1 models, TableCacheOptions options, ISchemaRegistryClient schemaRegistryClient, ILoggerFactory loggerFactory)
[xUnit.net 00:05:05.08]         C:\rc\rc01\src\Cache\Extensions\KsqlContextCacheExtensions.cs(116,0): at Kafka.Ksql.Linq.Cache.Extensions.KsqlContextCacheExtensions.UseTableCache(IKsqlContext context, KsqlDslOptions options, ILoggerFactory loggerFactory, IKafkaStreams streams)
[xUnit.net 00:05:05.08]         C:\rc\rc01\src\KsqlContext.cs(154,0): at Kafka.Ksql.Linq.KsqlContext..ctor(KsqlDslOptions options, ILoggerFactory loggerFactory)
[xUnit.net 00:05:05.08]         C:\rc\rc01\physicalTests\OssSamples\CompositeKeyPocoTests.cs(22,0): at Kafka.Ksql.Linq.Tests.Integration.CompositeKeyPocoTests.OrderContext..ctor(KsqlDslOptions options, ILoggerFactory loggerFactory)
[xUnit.net 00:05:05.08]         C:\rc\rc01\physicalTests\OssSamples\CompositeKeyPocoTests.cs(50,0): at Kafka.Ksql.Linq.Tests.Integration.CompositeKeyPocoTests.SendAndReceive_CompositeKeyPoco()
[xUnit.net 00:05:05.08]         --- End of stack trace from previous location ---
[xUnit.net 00:05:05.09]   Finished:    Kafka.Ksql.Linq.Tests.Integration
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
### assistant — 2025-08-04T12:30:21.886992+00:00

{
  "criteria": [
    "文章を簡潔に、わかりやすく説明してください",
    "重要な内容を箇条書きで示してください",
    "補足説明や具体例を付け加えてください"
  ],
  "response": "以下に、GitHub Copilotの使用に関する「3原則」のポイントをわかりやすくまとめます。\n\n---\n\n### GitHub Copilot 3原則のポイントまとめ\n\n1. **質問の具体性を高める**\n   - 何を実現したいのか、どんな問題かを具体的に伝える\n   - 曖昧な質問は避け、コード例やエラー内容を添えると効果的\n\n2. **試したこと・状況を共有する**\n   - 既に試した方法や環境（言語、フレームワークなど）を明示する\n   - こうすることで、より適切なアドバイスが得られやすい\n\n3. **Copilotの提案を検証・改良する**\n   - 出力されたコードをそのまま鵜呑みにせず、自分で理解・検証する\n   - 必要に応じてコードを修正し、自分のプロジェクトに最適化する\n\n---\n\n### 補足説明\n\n- これらの原則は、Copilotを効果的に活用するための基本的な考え方です。\n- 質問や指示を明確にすればするほど、AIが返す提案も精度が上がります。\n- AIは万能ではないため、最後の判断と責任は使う人にあることを忘れないでください。\n\nご希望であれば、この3原則を利用した具体的なプロンプト例や活用シナリオも作成可能です。いつでもお申し付けくださいね。"
}
### assistant — 2025-08-04T12:30:25.595622+00:00

{
  "content": "やあ、司令！\n\nPlaywright MCP Serverのみでできることや、GitHub Enterpriseとの連携、そして自然言語処理を含むAI連携についての質問がいくつかありましたね。ざっと整理すると：\n\n1. **Playwright MCP Server単独でできること**\n   - Webブラウザの自動操作やUIテストの実行がメイン。\n   - 自然言語処理機能は標準では持っていません。\n\n2. **GitHub Enterprise と Playwright MCP Server のAPI連携**\n   - GitHub EnterpriseのCI/CDパイプラインやプルリク管理と連携可能。\n   - Playwrightのテスト結果をGitHubに反映させるなどの連携が可能。\n\n3. **自然言語処理とLLMの関係**\n   - Playwright MCP Server自体は自然言語処理をしません。\n   - ただし、GitHub Copilot EnterpriseやAzure OpenAIなどのLLMを使えば自然言語による指示生成が可能。\n   - その場合、自然言語での指示からテストコードや操作指示を自動生成し、MCP Serverが実行する形。\n\n4. **自然言語指示を作るツールとしてVSCode + GitHub Copilotを使うことも可能**\n\n5. **LLM APIを間に挟む設定例**\n   - たとえば、Azure OpenAIのAPIを呼び出して自然言語をテストコードに変換し、生成したコードをPlaywright MCP Serverで実行するワークフロー。\n   - 具体的にはAzure FunctionsやGitHub ActionsのステップでAPI呼び出し。\n\nもし具体的な構成例や設定ファイル、またはコード例が必要なら教えてくださいね。\n\n2025年8月4日 20:15 JST",
  "metadata": {
    "timestamp": "[[REDACTED_PHONE]]-04T20:15:00+09:00"
  }
}
### assistant — 2025-08-04T12:31:13.931505+00:00

やあ司令、

ログを見ると、Kafkaストリームの状態はRUNNINGまで正常に遷移し、トピックや状態ストア（`orders`）の作成・復元も実施されているようです。しかし、以下の例外でテストが失敗しています。

```
Streamiz.Kafka.Net.Errors.InvalidStateStoreException: The state store, orders, may have migrated to another instance.
```

このエラーは、ストリーム処理の状態ストア（RocksDBベース）が期待したインスタンスに存在せず、別のインスタンスに移動してしまった可能性があることを示しています。

---

## 考えられる原因と対処案

1. **状態ストアの移動・再割り当てが発生している**
   - ストリームスレッドが再バランス中に状態ストアの所有権が変わることがあります。
   - テスト開始時にストアがまだ完全に準備できていないタイミングでアクセスするとこのエラーが発生しやすいです。

2. **複数インスタンスまたは複数スレッドの競合**
   - 複数のストリームインスタンスが同じアプリケーションIDや状態ストア名を共有していると競合する場合があります。
   - `application.id` がユニークか確認してください。

3. **状態ストアの初期化が完了していない**
   - ストアの復元・初期化処理が非同期で行われているため、アクセス前に初期化完了を待つ必要があります。
   - 初期化待機処理を追加するか、状態遷移を監視して`RUNNING`状態になったのを確認してからストアアクセスを行う設計にしてください。

4. **設定の見直し**
   - `state.dir` のパスが適切か確認してください。アクセス権限の問題やディスク容量不足も要チェックです。
   - `replication.factor` の値が `-1` となっているのは一般的には異常。Kafkaクラスタの構成に合わせて適切な値に設定してください。

---

## 対応のヒント

- ストアの取得を試みるコードにリトライやタイムアウト処理を入れてみる  
  → 例えば、`QueryableStoreProvider.GetStore` が例外を投げたら数秒間リトライする方法。

- ストリームインスタンスを一つだけ起動しているか、複数起動していないか確認

- `KafkaStream` の状態変化（`CREATED` → `RUNNING`）を確実に監視し、`RUNNING` になってから操作開始する

- ログの`Timeout while waiting for state store orders to become available`部分はストアが準備できていないことを示すので、この待機処理の見直しが重要

---

もしコードの該当部分を共有してもらえれば、具体的なリトライ実装例や状態監視の例も作成します。

2025年8月4日 20:31 JST
### user — 2025-08-04T12:31:14.623000+00:00

========== テストの実行を開始しています ==========
[xUnit.net 00:00:00.00] xUnit.net VSTest Adapter v2.5.6+bf9b858c26 (64-bit .NET 8.0.18)
[xUnit.net 00:00:00.05]   Starting:    Kafka.Ksql.Linq.Tests.Integration
dbug: Kafka.Ksql.Linq.Infrastructure.Admin.KafkaAdminService[0]
      KafkaAdminService initialized with BootstrapServers: localhost:9092
dbug: Kafka.Ksql.Linq.Infrastructure.Admin.KafkaAdminService[0]
      DB topic already exists: orders
dbug: Kafka.Ksql.Linq.Infrastructure.Admin.KafkaAdminService[0]
      DLQ topic already exists: dead.letter.queue
dbug: Kafka.Ksql.Linq.Infrastructure.Admin.KafkaAdminService[0]
      Kafka connectivity validated: 1 brokers available
info: Kafka.Ksql.Linq.KsqlContext[0]
      Kafka initialization completed; DLQ topic 'dead.letter.queue' ready with 5-second retention
info: Streamiz.Kafka.Net.KafkaStream[0]
      stream-application[ksql-dsl-app]  Start creation of the stream application with this configuration: 
      	Stream property:
      		client.id: 	
      		num.stream.threads: 	1
      		default.key.serdes: 	Streamiz.Kafka.Net.SerDes.StringSerDes
      		default.value.serdes: 	Streamiz.Kafka.Net.SerDes.StringSerDes
      		default.timestamp.extractor: 	Streamiz.Kafka.Net.Processors.Internal.FailOnInvalidTimestamp
      		commit.interval.ms: 	30000
      		processing.guarantee: 	AT_LEAST_ONCE
      		transaction.timeout: 	00:00:10
      		poll.ms: 	100
      		max.poll.records: 	500
      		max.poll.restoring.records: 	1000
      		max.task.idle.ms: 	0
      		buffered.records.per.partition: 	[[REDACTED_PHONE]]
      		inner.exception.handler: 	System.Func`2[System.Exception,Streamiz.Kafka.Net.ExceptionHandlerResponse]
      		production.exception.handler: 	System.Func`2[Confluent.Kafka.DeliveryReport`2[System.Byte[],System.Byte[]],Streamiz.Kafka.Net.ProductionExceptionHandlerResponse]
      		deserialization.exception.handler: 	System.Func`4[Streamiz.Kafka.Net.ProcessorContext,Confluent.Kafka.ConsumeResult`2[System.Byte[],System.Byte[]],System.Exception,Streamiz.Kafka.Net.ExceptionHandlerResponse]
      		rocksdb.config.setter: 	System.Action`2[System.String,Streamiz.Kafka.Net.State.RocksDbOptions]
      		follow.metadata: 	False
      		state.dir: 	C:\Temp\KAFKA_STATE
      		replication.factor: 	-1
      		windowstore.changelog.additional.retention.ms: 	[[REDACTED_PHONE]]
      		offset.checkpoint.manager: 	
      		metrics.interval.ms: 	30000
      		metrics.recording.level: 	INFO
      		log.processing.summary: 	00:01:00
      		metrics.reporter: 	System.Action`1[System.Collections.Generic.IEnumerable`1[Streamiz.Kafka.Net.Metrics.Sensor]]
      		expose.librdkafka.stats: 	False
      		start.task.delay.ms: 	5000
      		parallel.processing: 	False
      		max.degree.of.parallelism: 	8
      		statestore.cache.max.bytes: 	[[REDACTED_PHONE]]
      		application.id: 	ksql-dsl-app
      		schema.registry.url: 	http://localhost:8081
      	Client property:
      		bootstrap.servers: 	localhost:9092
      	Consumer property:
      		max.poll.interval.ms: 	[[REDACTED_PHONE]]
      		enable.auto.commit: 	False
      		enable.auto.offset.store: 	False
      		allow.auto.create.topics: 	False
      		partition.assignment.strategy: 	range
      	Producer property:
      		allow.auto.create.topics: 	False
      		partitioner: 	murmur2_random
      	Admin client property:
      		allow.auto.create.topics: 	False
info: Streamiz.Kafka.Net.Processors.Internal.StateDirectory[0]
      Reading UUID from process file: f5189da2-7b07-4664-b9d0-dd738323bc1e
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0] Creating consumer client
info: Streamiz.Kafka.Net.KafkaStream[0]
      stream-application[ksql-dsl-app] State transition from CREATED to REBALANCING
info: Kafka.Ksql.Linq.Core.Abstractions.IKsqlContext[0]
      KafkaStream state changed to: REBALANCING
info: Streamiz.Kafka.Net.KafkaStream[0]
      stream-application[ksql-dsl-app] Starting Streams client with this topology : Topologies:
         Sub-topology: 0
          Source: KSTREAM-SOURCE-[[REDACTED_PHONE]] (topics: [orders])
            --> KTABLE-SOURCE-[[REDACTED_PHONE]]
          Processor: KTABLE-SOURCE-[[REDACTED_PHONE]] (stores: [orders])
            --> none
            <-- KSTREAM-SOURCE-[[REDACTED_PHONE]]
dbug: Streamiz.Kafka.Net.Processors.DefaultTopicManager[0]
      Starting to apply internal topics for topology 0 in topic manager (try: 1, max retry : 10).
dbug: Streamiz.Kafka.Net.Processors.DefaultTopicManager[0]
      Complete to apply internal topics in topic manager
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0] Starting
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0] State transition from CREATED to STARTING
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
info: Streamiz.Kafka.Net.Kafka.Internal.StreamsRebalanceListener[0]
      New partitions assign requested : orders [[0]]
dbug: Streamiz.Kafka.Net.Processors.Internal.TaskCreator[0]
      Created task 0-0 with assigned partition orders [[0]]
dbug: Streamiz.Kafka.Net.Processors.Internal.TaskCreator[0]
      Created task 0-0 with assigned partition orders [[0]]
dbug: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Initializing state stores.
dbug: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Initializing state stores
dbug: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Initializing store orders
dbug: Streamiz.Kafka.Net.Metrics.Internal.RocksDbMetricsRecorder[0]
      Adding metrics recorder of task 0-0 to metrics recording trigger
dbug: Streamiz.Kafka.Net.Metrics.Internal.RocksDbMetricsRecorder[0]
      Adding value providers for store orders of task 0-0
dbug: Streamiz.Kafka.Net.Processors.Internal.ProcessorStateManager[0]
      stream-task[0|0] Registering state store orders to its state manager
dbug: Streamiz.Kafka.Net.Processors.Internal.ProcessorStateManager[0]
      stream-task[0|0] Registered state store orders to its state manager
dbug: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Initializing topology with theses source processors : KSTREAM-SOURCE-[[REDACTED_PHONE]].
dbug: Streamiz.Kafka.Net.Processors.SourceProcessor[0]
      stream-task[0|0]|processor[KSTREAM-SOURCE-[[REDACTED_PHONE]]]- Initializing process context
dbug: Streamiz.Kafka.Net.Processors.KTableSourceProcessor[0]
      stream-task[0|0]|processor[KTABLE-SOURCE-[[REDACTED_PHONE]]]- Initializing process context
dbug: Streamiz.Kafka.Net.Processors.KTableSourceProcessor[0]
      stream-task[0|0]|processor[KTABLE-SOURCE-[[REDACTED_PHONE]]]- Process context initialized
dbug: Streamiz.Kafka.Net.Processors.SourceProcessor[0]
      stream-task[0|0]|processor[KSTREAM-SOURCE-[[REDACTED_PHONE]]]- Process context initialized
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0] State transition from STARTING to PARTITIONS_ASSIGNED
info: Streamiz.Kafka.Net.Kafka.Internal.StreamsRebalanceListener[0]
      Partition assignment took 00:00:[[REDACTED_PHONE]] ms.
      	Currently assigned active tasks: 0-0
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0] State transition from PARTITIONS_ASSIGNED to RUNNING
info: Streamiz.Kafka.Net.KafkaStream[0]
      stream-application[ksql-dsl-app] State transition from REBALANCING to RUNNING
info: Kafka.Ksql.Linq.Core.Abstractions.IKsqlContext[0]
      KafkaStream state changed to: RUNNING
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0]  State is RUNNING, initializing and restoring tasks if necessary
dbug: Streamiz.Kafka.Net.Processors.Internal.ProcessorStateManager[0]
      Loaded offsets from checkpoint manager: 
info: Streamiz.Kafka.Net.Processors.Internal.ProcessorStateManager[0]
      State store orders did not find checkpoint offset, hence would default to the starting offset at changelog ksql-dsl-app-orders-changelog [[0]]
info: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Task 0-0 state transition from CREATED to RESTORING
info: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Restoration will start soon.
dbug: Streamiz.Kafka.Net.Processors.Internal.StoreChangelogReader[0]
      State store ksql-dsl-app-orders-changelog [[0]] metadata found (begin offset: 0 / end offset : 0)
dbug: Streamiz.Kafka.Net.Processors.Internal.StoreChangelogReader[0]
      Added partitions with offsets ksql-dsl-app-orders-changelog-[0]#Beginning [-2] to the restore consumer, current assignment is ksql-dsl-app-orders-changelog-[0]
info: Streamiz.Kafka.Net.Processors.Internal.StoreChangelogReader[0]
      Finished restoring changelog orders to store ksql-dsl-app-orders-changelog [[0]] with a total number of 0 records
dbug: Streamiz.Kafka.Net.Processors.Internal.StoreChangelogReader[0]
      Paused partition ksql-dsl-app-orders-changelog [[0]] from the restore consumer
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      stream-thread[ksql-dsl-app-f5189da2-7b07-4664-b9d0-dd738323bc1e-stream-thread-0]  State is RUNNING, initializing and restoring tasks if necessary
info: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Task 0-0 state transition from RESTORING to RUNNING
info: Streamiz.Kafka.Net.Processors.StreamTask[0]
      stream-task[0|0] Restored and ready to run
info: Streamiz.Kafka.Net.Processors.StreamThread[0]
      Restoration took 419ms for all tasks 0-0
dbug: Streamiz.Kafka.Net.Processors.Internal.StoreChangelogReader[0]
      Finished restoring all changelogs [ksql-dsl-app-orders-changelog-[0]]
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
      0 punctuators ran.
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]

      0 punctuators ran.

      0 punctuators ran.
fail: Kafka.Ksql.Linq.Cache.Core.RocksDbTableCache[0]
      Timeout while waiting for state store orders to become available
fail: Kafka.Ksql.Linq.KsqlContext[0]
      KsqlContext initialization failed: The state store, orders, may have migrated to another instance. 
      Streamiz.Kafka.Net.Errors.InvalidStateStoreException: The state store, orders, may have migrated to another instance.
         at Streamiz.Kafka.Net.State.Internal.QueryableStoreProvider.GetStore[T,K,V](StoreQueryParameters`3 storeQueryParameters)
         at Kafka.Ksql.Linq.Cache.Core.StreamizKafkaStreams.Store(StoreQueryParameters`3 parameters) in C:\rc\rc01\src\Cache\Core\StreamizKafkaStreams.cs:line 27
         at Kafka.Ksql.Linq.Cache.Core.RocksDbTableCache`1.InitializeAsync() in C:\rc\rc01\src\Cache\Core\RocksDbTableCache.cs:line 87
         at Kafka.Ksql.Linq.Cache.Core.RocksDbTableCache`1.InitializeAsync() in C:\rc\rc01\src\Cache\Core\RocksDbTableCache.cs:line 95
         at Kafka.Ksql.Linq.Cache.Core.TableCacheRegistry.InitializeCaches(IEnumerable`1 models, TableCacheOptions options, ISchemaRegistryClient schemaRegistryClient, ILoggerFactory loggerFactory) in C:\rc\rc01\src\Cache\Core\TableCacheRegistry.cs:line 52
         at Kafka.Ksql.Linq.Cache.Extensions.KsqlContextCacheExtensions.UseTableCache(IKsqlContext context, KsqlDslOptions options, ILoggerFactory loggerFactory, IKafkaStreams streams) in C:\rc\rc01\src\Cache\Extensions\KsqlContextCacheExtensions.cs:line 116
         at Kafka.Ksql.Linq.KsqlContext..ctor(KsqlDslOptions options, ILoggerFactory loggerFactory) in C:\rc\rc01\src\KsqlContext.cs:line 154
[xUnit.net 00:05:05.08]     Kafka.Ksql.Linq.Tests.Integration.CompositeKeyPocoTests.SendAndReceive_CompositeKeyPoco [FAIL]
[xUnit.net 00:05:05.08]       Streamiz.Kafka.Net.Errors.InvalidStateStoreException : The state store, orders, may have migrated to another instance.
[xUnit.net 00:05:05.08]       Stack Trace:
[xUnit.net 00:05:05.08]            at Streamiz.Kafka.Net.State.Internal.QueryableStoreProvider.GetStore[T,K,V](StoreQueryParameters`3 storeQueryParameters)
[xUnit.net 00:05:05.08]         C:\rc\rc01\src\Cache\Core\StreamizKafkaStreams.cs(27,0): at Kafka.Ksql.Linq.Cache.Core.StreamizKafkaStreams.Store(StoreQueryParameters`3 parameters)
[xUnit.net 00:05:05.08]         C:\rc\rc01\src\Cache\Core\RocksDbTableCache.cs(87,0): at Kafka.Ksql.Linq.Cache.Core.RocksDbTableCache`1.InitializeAsync()
[xUnit.net 00:05:05.08]         C:\rc\rc01\src\Cache\Core\RocksDbTableCache.cs(95,0): at Kafka.Ksql.Linq.Cache.Core.RocksDbTableCache`1.InitializeAsync()
[xUnit.net 00:05:05.08]         C:\rc\rc01\src\Cache\Core\TableCacheRegistry.cs(52,0): at Kafka.Ksql.Linq.Cache.Core.TableCacheRegistry.InitializeCaches(IEnumerable`1 models, TableCacheOptions options, ISchemaRegistryClient schemaRegistryClient, ILoggerFactory loggerFactory)
[xUnit.net 00:05:05.08]         C:\rc\rc01\src\Cache\Extensions\KsqlContextCacheExtensions.cs(116,0): at Kafka.Ksql.Linq.Cache.Extensions.KsqlContextCacheExtensions.UseTableCache(IKsqlContext context, KsqlDslOptions options, ILoggerFactory loggerFactory, IKafkaStreams streams)
[xUnit.net 00:05:05.08]         C:\rc\rc01\src\KsqlContext.cs(154,0): at Kafka.Ksql.Linq.KsqlContext..ctor(KsqlDslOptions options, ILoggerFactory loggerFactory)
[xUnit.net 00:05:05.08]         C:\rc\rc01\physicalTests\OssSamples\CompositeKeyPocoTests.cs(22,0): at Kafka.Ksql.Linq.Tests.Integration.CompositeKeyPocoTests.OrderContext..ctor(KsqlDslOptions options, ILoggerFactory loggerFactory)
[xUnit.net 00:05:05.08]         C:\rc\rc01\physicalTests\OssSamples\CompositeKeyPocoTests.cs(50,0): at Kafka.Ksql.Linq.Tests.Integration.CompositeKeyPocoTests.SendAndReceive_CompositeKeyPoco()
[xUnit.net 00:05:05.08]         --- End of stack trace from previous location ---
[xUnit.net 00:05:05.09]   Finished:    Kafka.Ksql.Linq.Tests.Integration
dbug: Streamiz.Kafka.Net.Processors.StreamThread[0]
### assistant — 2025-08-04T12:34:11.602375+00:00

やあ司令、

`replication.factor` はKafka Streamsの設定の一部ですが、直接Kafka Streamsのクライアント設定には通常含まれません。これはKafkaクラスタ側でトピック作成時に指定するレプリケーションの因子で、主に**トピック作成時**に使われます。

---
### どこで設定するか？

1. **Kafka Admin API でのトピック作成時に指定**  
   たとえば、Streamiz.Kafka.Netの `AdminClient` を使ってトピックを作成するときに、`NewTopic` オブジェクトの `ReplicationFactor` プロパティで設定します。

```csharp
var newTopic = new NewTopic("orders", numPartitions: 3, replicationFactor: 2);
await adminClient.CreateTopicsAsync(new List<NewTopic> { newTopic });
```

2. **Kafkaサーバーのデフォルト設定**  
   Kafkaブローカー側の `server.properties` にデフォルトのレプリケーション係数を設定できますが、トピック作成時に指定しなければこちらが使われます。

```properties
default.replication.factor=3
```

3. **Streamiz.Kafka.Net の設定内には通常含まれない**  
   `KafkaStream` の `StreamConfig` の中に `replication.factor` という設定項目はありますが、これは通常、内部的にトピックを作る時に使われることが多いです。ただし、明示的にこの値を渡していなければ、デフォルトやトピック作成時の値が使われます。

---
### 今回のエラーとの関連

- `replication.factor` が `-1` という値が設定されているとKafka側で無効と判断されて問題が起こる可能性があります。  
- 明示的にKafka Adminでトピック作成時に適正な値（通常は1以上の整数）をセットしてください。

---
### まとめ

- Kafkaトピックの`replication.factor`は、**トピック作成時にAdmin APIやCLIで設定する**もの。  
- Streamizの設定で触るなら、`KsqlDslOptions` やトピック作成コードで正しい値を渡すこと。  
- 何も指定しなければKafkaブローカーのデフォルト値が適用される。

---

もし具体的なトピック作成コードがあれば教えてください。修正例を示します。

2025年8月4日 20:38 JST
### user — 2025-08-04T12:34:12.888000+00:00

replication.factor はどこで設定する？
### assistant — 2025-08-04T12:35:00.981109+00:00

やあ司令、

Kafkaのトピック設定はKafkaブローカーの管理APIで直接は見られませんが、**ksqlDBのREST API**や**Kafka Admin CLI**、あるいは**Confluent Control Center**などで確認できます。

---
### 1. ksqlDB REST APIで確認（トピックの設定確認）

ksqlDBが動いている場合、ksqlDBのREST APIでトピックの詳細を問い合わせることができます。

```bash
curl -X GET http://localhost:8088/info
```

でksqlDBの状態を確認し、

```bash
curl -X GET "http://localhost:8088/topics/<topic_name>"
```

（ただしこのAPIはバージョンによって異なり、`/topics` エンドポイントがない場合もあります）

---
### 2. Kafkaブローカーのトピック設定をコマンドラインで見る方法

Kafkaの管理ツールである `kafka-configs.sh` でトピックの設定を確認できます。Linux環境などKafkaがインストールされているマシンで以下を実行。

```bash
kafka-configs.sh --bootstrap-server localhost:9092 --entity-type topics --entity-name <topic_name> --describe
```

例：

```bash
kafka-configs.sh --bootstrap-server localhost:9092 --entity-type topics --entity-name orders --describe
```

---
### 3. Kafka REST Proxyがある場合（curlでAPI操作）

Confluent Kafka REST Proxyが動いていれば、curlでトピック情報の取得が可能です。

```bash
curl -X GET "http://localhost:8082/topics/<topic_name>/config"
```

例：

```bash
curl -X GET "http://localhost:8082/topics/orders/config"
```

---
### まとめ

- **純粋なKafka単体環境ではcurlで直接トピック設定を見るAPIはない**（Kafka REST Proxy導入時除く）  
- **Kafka CLIツールやksqlDBのREST API、Kafka REST Proxyを使って確認するのが一般的**

---

もしKafka REST Proxyがなければ、`kafka-configs.sh` コマンドが最も確実です。

何かあれば教えてくださいね！

2025年8月4日 20:44 JST
### user — 2025-08-04T12:35:02.292000+00:00

トピック上の設定をcurlで見れる？
### assistant — 2025-08-04T12:37:44.142665+00:00

司令、了解です！

`kafka-configs.sh` がない環境の場合、以下の方法を検討してください。

---
### 1. Kafka REST Proxy が使えれば一番簡単

Kafka REST Proxy（Confluent製）があれば、curlで設定確認できます。

もし環境に導入できるならおすすめです。

```bash
curl -X GET "http://localhost:8082/topics/orders/config"
```

---
### 2. Kafka Admin APIを使った自作スクリプト or .NETクライアントから確認

`kafka-configs.sh`はCLIですが、KafkaのAdminClient APIを使うとプログラムからトピック設定を取得可能です。

たとえば、.NETの`Confluent.Kafka`ライブラリの`AdminClient`で

```csharp
var admin = new AdminClientBuilder(new AdminClientConfig { BootstrapServers = "localhost:9092" }).Build();
var metadata = admin.GetMetadata("orders", TimeSpan.FromSeconds(10));
var configs = admin.DescribeConfigs(new ConfigResource(ConfigResourceType.Topic, "orders"));
```

みたいな感じで取得できます。

---
### 3. Kafka UIツールを使う

[Kafka Tool](https://www.kafkatool.com/)や[Kafka Manager](https://github.com/yahoo/kafka-manager)、[AKHQ](https://akhq.io/)などのGUIツールを入れるのも手です。

GUIからトピックの設定を一覧・変更できます。

---
### 4. kafka-topics.shでの簡易情報取得

`kafka-topics.sh` が使える場合は

```bash
kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic orders
```

でレプリケーションファクターやパーティション数などの基本情報は得られます。

---

もしCLIも一切ない場合は、管理者に環境整備を依頼するか、Admin APIを使う自作ツール作成をおすすめします。

---

何かあれば教えてくださいね！

2025年8月4日 20:52 JST
### user — 2025-08-04T12:37:45.118000+00:00

kafka-configs.shはない
### assistant — 2025-08-04T12:38:21.002654+00:00

司令、現状の挙動から察するに：

- `localhost:8082` での Kafka REST Proxy は起動していない、またはそもそも導入されていない可能性が高い
- `localhost:8088` はおそらく別のサービス（おそらく ksqlDB サーバなど）が立っていて、`/topics/orders/config` というパスは存在しない

---
### 現時点の対処案

1. **Kafka REST Proxyがない環境でトピック設定を確認したい場合**

   → Kafkaの管理用CLIツール（`kafka-configs.sh`）や管理ツールがない場合、APIを直接叩くしかありません。

2. **Kafka Admin APIを使う**

   - もし .NET 環境なら Confluent KafkaのAdminClientを使い、プログラム的にトピック設定を取得するカスタムツールを作るのが現実的です。

   - たとえば、`DescribeConfigsAsync()`を使ってトピックの設定情報が取得できます。

3. **ksqlDBのAPIでできる範囲を探す**

   - ksqlDBのAPIはトピック設定を直接返さないので、基本的には無理です。

---
### まとめ

- 8082でKafka REST Proxyが起動していないなら、導入しない限りcurlで直接トピック設定を取得できません。

- トピックのレプリケーションファクター等を知りたいなら、`kafka-topics.sh --describe`が使える環境が必要です。

- もしCLIもREST Proxyも使えない環境なら、Admin APIでプログラムを作るのが最善手になります。

---

必要ならAdmin APIを使ったトピック設定取得の簡単な.NETサンプルも作れますので、気軽に言ってくださいね。

2025年8月4日 21:03 JST
### user — 2025-08-04T12:38:21.618000+00:00

C:\rc\rc01\physicalTests>curl -X GET "http://localhost:8082/topics/orders/config"
curl: (7) Failed to connect to localhost port 8082 after 2267 ms: Could not connect to server

C:\rc\rc01\physicalTests>curl -X GET "http://localhost:8088/topics/orders/config"
<html><body><h1>Resource not found</h1></body></html>
C:\rc\rc01\physicalTests>
### assistant — 2025-08-04T12:45:46.174752+00:00

司令、共有いただいたJSONはksqlDBのCREATE TABLEコマンドの実行結果で、以下のようなトピック設定が含まれていますね。

- トピック名: `orders`
- パーティション数（PARTITIONS）: 1
- レプリケーション数（REPLICAS）: 1
- キーと値のフォーマット: AVRO
- クリーンアップポリシー: `compact`

この情報からは、レプリケーションファクターは `REPLICAS=1` で設定されていることがわかります。

---
### ポイントまとめ
- ksqlDBのCREATE TABLE文のWITH句で `PARTITIONS` と `REPLICAS` はトピックのパーティション数とレプリケーションファクターを指定している
- ksqlDBがトピックを自動生成する場合はここでの指定が適用される（ただし既存トピックがある場合は変更されない）
- 既に存在するトピックの設定を変更したい場合は、Kafkaの管理ツールなどで直接設定変更が必要になる

---

もしさらにトピックの詳細設定や動的確認が必要であれば、お知らせくださいね。

2025年8月4日 21:07 JST
### user — 2025-08-04T12:45:47.570000+00:00

[{"@type":"currentStatus","statementText":"CREATE TABLE IF NOT EXISTS ORDERS (ROWKEY STRUCT<`OrderId` INTEGER, `UserId` INTEGER> PRIMARY KEY, `OrderId` INTEGER, `UserId` INTEGER, `ProductId` INTEGER, `Quantity` INTEGER) WITH (CLEANUP_POLICY='compact', KAFKA_TOPIC='orders', KEY_FORMAT='AVRO', KEY_SCHEMA_FULL_NAME='kafka_ksql_linq_entities_samples_models.orders_keyAvro', KEY_SCHEMA_ID=1, PARTITIONS=1, REPLICAS=1, VALUE_FORMAT='AVRO', VALUE_SCHEMA_FULL_NAME='kafka_ksql_linq_entities_samples_models.orders_valueAvro', VALUE_SCHEMA_ID=2);","commandId":"table/`ORDERS`/create","commandStatus":{"status":"SUCCESS","message":"Table created","queryId":null},"commandSequenceNumber":2,"warnings":[]}]
### assistant — 2025-08-04T12:52:16.428215+00:00

司令、このエラーメッセージ

```
KsqlContext initialization failed: The state store, orders, may have migrated to another instance.
```

の「インスタンス」とは、Kafka Streams（Streamiz.Kafka.Net）が管理する**ストリーム処理の実行インスタンス（またはアプリケーションクライアント）**を指しています。

---
### 詳細説明

- Kafka Streamsは**分散処理フレームワーク**であり、複数のアプリケーションインスタンス（プロセスやノード）が連携してトピックのパーティションを処理します。
- 各インスタンスはパーティション単位で状態ストア（State Store）を持ちます。
- **状態ストア（orders）**は、そのパーティションを担当するインスタンスに「割り当てられて」初めてアクセス可能になります。
- しかし、負荷分散やリバランスが起きると、状態ストアは別のインスタンスに「移動（migrated）」することがあります。

---
### このエラーの意味

- あなたがアクセスしようとした状態ストア `orders` は、現在のアプリケーションインスタンスではなく、
- **別のKafka Streamsインスタンスが所有しているためアクセスできない** ことを表しています。

---
### 対応策の例

- Kafka Streamsアプリケーションが**正常にリバランスし終わるまで待つ**
- 状態ストアアクセスはリバランス後、担当インスタンスからアクセスするように設計する
- 複数インスタンス構成時に状態ストアアクセスを同期させる
- 状態ストアがまだ起動していないか、割り当てが未定の場合はタイムアウトや例外が発生しやすいので、再試行ロジックを入れる

---

つまり、**「インスタンス」とはKafka Streamsの処理単位で、現在はこの状態ストアは別の実行プロセスに割り当てられている**ためアクセスできません、という意味です。

2025年8月4日 21:10 JST
### user — 2025-08-04T12:52:17.769000+00:00

KsqlContext initialization failed: The state store, orders, may have migrated to another instance. 
このインスタンスは何を指してる？
### assistant — 2025-08-04T12:52:45.627221+00:00

司令、ご質問の「インスタンス」は厳密には単にプロセスだけを指すわけではなく、Kafka Streamsの**ストリームアプリケーションの実行単位**を指します。

---
### 具体的には

- Kafka Streamsのアプリケーションは、たとえば複数のサーバーやプロセス上で並行して動きます。
- これらそれぞれを「インスタンス」と呼びます。
- インスタンスは**複数のスレッドやプロセス、あるいはコンテナとして動作していることが多い**です。

---
### プロセスとの関係

- ほとんどの場合は**1インスタンス＝1プロセス**であることが多いです。
- つまり、この「インスタンス」は単一のKafka Streamsアプリケーション実行プロセスを指すケースが一般的です。
- ただし、厳密にはKafka Streamsの論理単位（同じプロセス内で複数のクライアントIDを持つこともある）も含む概念なので、
- 「プロセス」とイコールとは限らないが、実務上はほぼ同じものと捉えてよいです。

---
### まとめ

- 「インスタンス」＝Kafka Streamsアプリケーションの**実行中のプロセス（またはコンテナやサービス）**
- 状態ストアは特定のインスタンスに割り当てられており、別のインスタンス（プロセス）に移動するとアクセスできなくなる

---

わかりやすくいうと、「この状態ストアは今、別のKafka Streamsアプリのプロセスが管理しているので、あなたの今動いているプロセスからは使えませんよ」という意味です。

2025年8月4日 21:14 JST
### user — 2025-08-04T12:52:46.667000+00:00

プロセス？
### assistant — 2025-08-04T12:53:23.824866+00:00

司令、プロセスは1つだけ起動しているのに

```
The state store, orders, may have migrated to another instance.
```

というエラーが出る場合、以下のポイントを確認・検討してください。

---
### 1. Kafka Streamsのリバランス状態の影響

- Kafka Streamsは内部で**パーティションのリバランス**を行います。
- 状態ストアはパーティション単位で所有権が移動し、このタイミングで一時的に「状態ストアが別のインスタンスにある」ように見えます。
- プロセスが1つでも、**Kafkaのコーディネータがリバランスを繰り返している状態**だと同様のエラーが起きることがあります。

---
### 2. プロセス再起動やネットワーク断があるか

- プロセス再起動やKafkaとの接続断が頻繁にあると、リバランスが頻発し状態ストアが切り替わる場合があります。
- ログにリバランスや再接続の動きがないか確認してください。

---
### 3. トピックのパーティション数・レプリカ数の確認

- 状態ストアはパーティションに対応して作られます。
- パーティション数とインスタンス数の関係が不整合な場合、リバランスが発生しやすいです。
- 今回はインスタンスが1つなのでパーティションも1つが望ましいです（CREATE TABLE文では1でしたね）。

---
### 4. クライアントIDやアプリケーションIDの重複確認

- もし同じクライアントIDやアプリケーションIDで別プロセスが立ち上がっている場合、リバランスが起きます。
- タスクマネージャやDockerなどでプロセスが本当に1つか再確認してください。

---
### 5. 状態ストアのタイムアウトや初期化遅延

- 状態ストアの初期化や復元に時間がかかっている場合にもエラーが出ることがあります。
- 例えば RocksDBのストアが初期化完了前にアクセスしようとしている可能性。

---
### まとめ

- 1プロセスのみ起動していてもKafkaのリバランスや接続状態、クライアントID重複などで状態ストアの所有権が不安定になることがあります。
- ログを詳しく追い、リバランスや再起動、接続断がないかチェックするのが第一歩です。
- 状態ストアの復元にかかる時間を長めに取る設定も検討してください。

必要なら設定ファイルやコード周りも詳しく見ていきましょう。

2025年8月4日 21:15 JST
### user — 2025-08-04T12:53:25.113000+00:00

プロセスは１つのみ起動してる
### assistant — 2025-08-04T12:54:44.179827+00:00

司令、わかりやすく分けて整理しますね。

---

## 1. アプリケーション側の条件・原因

- **プロセス数**
  - 複数の同一アプリケーションIDまたはクライアントIDのプロセスが動いていると、リバランスが頻発する。
  - 1つのプロセスに限定されているか再確認。

- **アプリケーションID（application.id）**
  - Kafka StreamsはアプリケーションIDでグループ管理するため、重複があると状態ストアの所有権が移動する。

- **起動・シャットダウンのタイミング**
  - 頻繁な再起動や異常終了があるとリバランスが多発。

- **状態ストア初期化のタイミング・待機**
  - 状態ストア（RocksDB）がまだ復元中にアクセスするとエラーになる可能性があるため、初期化完了を正しく待つ設計が必要。

- **状態ストアの参照方法**
  - `QueryableStoreProvider.GetStore`の呼び出しタイミングに注意。状態ストアがまだ利用できない場合の例外処理も必須。

- **クライアントのネットワーク状態**
  - 接続不安定があると再接続・リバランスを誘発。

---

## 2. Kafkaサーバ側の条件・原因

- **トピックのパーティション数**
  - アプリケーションのインスタンス数に見合ったパーティション数であることが望ましい（インスタンス1ならパーティション1推奨）。

- **レプリケーションファクター**
  - レプリカ数が不適切だとパフォーマンスやリーダー選出に影響。トピックの状態を確認。

- **ブローカーの健康状態**
  - ブローカーが落ちている・クラスタに問題があるとリバランスや状態ストア所有権移動が起きやすい。

- **Zookeeper/Kafkaのメタデータ同期**
  - メタデータの同期が遅れているとリバランスが頻発。

- **状態ストアのChangelog Topic**
  - Kafka Streamsは状態ストアのバックアップにChangelog Topicを利用。
  - このTopicが存在し正常に動作しているか確認。

---
### まとめ

| 項目                     | アプリケーション側                                         | Kafkaサーバ側                                         |
|--------------------------|------------------------------------------------------------|-------------------------------------------------------|
| プロセス数・ID           | アプリケーションID重複なし、プロセス1                       | パーティション数とレプリカ数適切                        |
| 状態ストア初期化         | 復元完了待ちの実装、状態ストアアクセス時の例外対応           | Changelog Topicが正常                                   |
| ネットワーク              | 接続安定、再接続なし                                       | ブローカー正常稼働、クラスタ安定                       |
| 起動/停止挙動             | 頻繁な再起動や異常終了なし                                 | Zookeeper/Kafkaのメタデータ同期が正常                 |

---

必要であれば、具体的なログや設定を元にさらに深掘りしますね。

2025年8月4日 21:20 JST
### user — 2025-08-04T12:54:45.588000+00:00

アプリケーション側の条件とサーバ側（kafka）と分けて教えてください
### assistant — 2025-08-04T12:56:07.562604+00:00

司令、ありがとうございます。

---
### テスト実行時の複数同時起動について

- **テストフレームワーク挙動**
  - xUnitなどでは、テストクラスやメソッドごとに独立インスタンスを生成し並列で実行されることがあります。
  - `Parallelizable`設定や`Collection`属性により、複数テストが並列実行される可能性があります。

- **物理テストでの起動**
  - 物理的に同時に複数プロセスがテストを起動していれば、結果的にKafka Streamsアプリが複数起動する可能性があります。
  - 例えばCI環境やローカル実行で、複数テストが同時に走るとそれぞれがKafka Streamsクライアントを作る形。

- **Dockerやテスト環境の分離**
  - テスト環境が分離されていない場合、同じKafkaクラスタに複数のアプリケーションインスタンスとして接続することに。

- **Kafka StreamsのState Storeの所有権問題は、こうした複数起動で起きやすい**

---
### 対応案

- **テストの並列実行制御**
  - xUnitの並列実行設定をOFFにする（例：`[Collection("Sequential")]`や`DisableParallelization`設定）。

- **テスト内でのKafka Streamsクライアントの共有やシングルトン化**
  - 複数テスト間で同じクライアントインスタンスを共有するなど。

- **起動時にユニークな `application.id` を付ける**
  - テストごとにランダムや識別子付きで変えると、別グループとして扱われて競合しない。

---
### 結論

テストが複数同時起動している可能性は高いです。  
複数インスタンスが同じ`application.id`で起動している場合、状態ストアの所有権が移動し、エラーが発生しやすいです。

---

必要ならテストの並列設定やapplication.idの動的変更を確認する方法やサンプルもお伝えしますね。

2025年8月4日 21:34 JST
### user — 2025-08-04T12:56:08.697000+00:00

アプリケーション側ではないと考える。テストでの実行をおこなってる。このとき複数同時に起動することがあるのか？
### assistant — 2025-08-04T12:57:08.951675+00:00

司令、はい、その書き方は基本的に良いです。

ポイント整理しますね：

```csharp
var config = new StreamConfig<StringSerDes, StringSerDes>
{
    ApplicationId = Guid.NewGuid().ToString(), // ユニークIDを動的に割り当てることで複数インスタンスの競合を回避
    BootstrapServers = bootstrap,
    SchemaRegistryUrl = options.SchemaRegistry.Url,
    StateDir = @"C:\Temp\KAFKA_STATE",
    Logger = loggerFactory,
};
```

- **ApplicationId**  
  `Guid.NewGuid().ToString()` はテストごとにユニークなIDを生成し、状態ストアの所有権衝突を防ぐために有効です。

- **StateDir**  
  複数インスタンスが同じフォルダを使うと競合することがあるので、  
  可能ならテストごとに別フォルダを割り当てることも検討してください。

- **Logger**  
  `loggerFactory` を渡してログを取得できるのは良いです。

---

もしテストの並列実行もOFFにできるなら、より安定しますが、  
ApplicationIdのユニーク化は特に重要なので、この書き方はOKです。

---

必要なら、`StateDir`も動的に変えるサンプルコード作成しますよ。

2025年8月4日 21:40 JST
### user — 2025-08-04T12:57:10.293000+00:00

var config = new StreamConfig<StringSerDes, StringSerDes>
               {
                   ApplicationId =Guid.NewGuid().ToString(), // appId,
                   BootstrapServers = bootstrap,
                   SchemaRegistryUrl= options.SchemaRegistry.Url,
                    StateDir = @"C:\Temp\KAFKA_STATE",
                     Logger= loggerFactory,
                    
               };これでいい？
### assistant — 2025-08-04T13:29:37.627485+00:00

司令、状況の整理ありがとうございます。

この２つのコードは、Kafka Streamsの状態ストア（state store）を取得・作成する処理に関わっていますね。

---

## 1. `_store = _streams.Store(...)` の問題点

- `StoreQueryParameters.FromNameAndType<IReadOnlyKeyValueStore<byte[], byte[]>, byte[], byte[]>(_storeName, QueryableStoreTypes.KeyValueStore<byte[], byte[]>())`  
 という呼び出しは、状態ストア名 `_storeName` に該当するストアを**現在のインスタンスが所有している**必要があります。

- ここでエラーになるのは、状態ストアが**別のインスタンスに割り当てられている（migrated）**か、  
  **状態ストアの名前や型が一致していない**か、  
  あるいは **状態ストアがまだ初期化されていない**ことが主な原因です。

---

## 2. `Materialized<,,>.Create(string)` メソッド取得の問題点

- Reflectionでジェネリック型 `Materialized<keyType, valueType, IKeyValueStore<Bytes, byte[]>>` を作成し、  
  そこから静的メソッド `Create(string)` を探しています。

- 問題になるケースとしては、

  - `kv.AvroKeyType` または `kv.AvroValueType` がnullや型が異なる  
  - そもそも指定している型引数と `Create` のシグネチャが合わない  
  - Streamiz Kafkaライブラリのバージョン違いなどで `Create(string)` が存在しない・挙動が違う

---

## 考えられる対策

1. **状態ストア名・型の整合性確認**

   - `_storeName` は `CREATE TABLE` 等の設定で登録されている名前と完全一致しているか？
   - 使用しているストア型（`IReadOnlyKeyValueStore<byte[], byte[]>` vs 他の型）も合っているか？

2. **Materialized型の型引数の確認**

   - `kv.AvroKeyType` / `kv.AvroValueType` がnullでないかをチェック  
   - 期待される型と一致しているかチェック

3. **バージョン・依存関係確認**

   - `Streamiz.Kafka.Net` のバージョンがドキュメントやサンプル通りか？  
   - `Materialized` の静的メソッドのシグネチャが最新と合っているか

4. **状態ストアの初期化順序**

   - 状態ストアを使う前に、Streamが`RUNNING`状態になっていて初期化済みであることを確認

---

もし良ければ、具体的に

- `_storeName` の値  
- `kv.AvroKeyType` と `kv.AvroValueType` の実際の型名（`kv.AvroKeyType?.Name`など）  
- 使用中の `Streamiz.Kafka.Net` バージョン

を教えていただければ、より詳細に掘り下げられます。

---

これらの問題は、状態ストアのインスタンス所有・初期化の流れとReflectionの型解決が密接に絡むため、どちらかの不整合が致命的になります。

---

必要であれば、この辺のReflection呼び出しの代替案や安全な型チェックコードも用意しますので、遠慮なくお申し付けください。

2025年8月4日 21:53 JST
### user — 2025-08-04T13:29:38.977000+00:00

_store = _streams.Store(StoreQueryParameters.FromNameAndType<IReadOnlyKeyValueStore<byte[], byte[]>, byte[], byte[]>(_storeName, QueryableStoreTypes.KeyValueStore<byte[], byte[]>()));
と
                    var materializedType = typeof(Materialized<,,>).MakeGenericType(kv.AvroKeyType!, kv.AvroValueType!, typeof(IKeyValueStore<Bytes, byte[]>));
                    var createMethod = materializedType.GetMethods()
                                        .Where(m => m.Name == "Create"
                                            && m.IsStatic
                                            && m.GetParameters().Length == 1
                                            && m.GetParameters()[0].ParameterType == typeof(string)
                                            && m.ReturnType == materializedType)
                                        .FirstOrDefault();
の問題のようです
### assistant — 2025-08-04T13:30:46.387026+00:00

司令、ありがとうございます。

`Streamiz.Kafka.Net` バージョン **1.7.1** を使っていることは確認できました。  
このバージョンは安定版で、`Materialized<,,>.Create(string)` の静的メソッドも存在しますので、基本的には型周りの問題が多いです。

---
### 次のチェックポイント

1. `kv.AvroKeyType` と `kv.AvroValueType` の中身は何でしょうか？  
   - 具体的な型名（例えば `typeof(orders_keyAvro)` のような具合）を教えてください。  
   - nullや異なる型になっていないか確認をお願いします。

2. `_storeName` は `"orders"` など、実際にKafka上で作成したトピック名や状態ストア名と一致していますか？

3. テストで同時に複数起動して状態ストアが競合したりしませんか？  
   - もしテスト並列実行していたら ApplicationId をユニークに変えてみてください。

---
### 参考：MaterializedのCreateメソッド署名

```csharp
public static Materialized<TKey, TValue, IKeyValueStore<Bytes, byte[]>> Create(string storeName);
```

- ここで、`TKey` と `TValue` がAvroクラスの正確な型である必要があります。  
- かつ `IKeyValueStore<Bytes, byte[]>` は固定です。

---
### まとめ

- **型不一致やnull** が一番多い原因です。  
- **ストア名の間違い・競合** もよくある原因。  
- **バージョンはOK** なので、引数や生成時の型・名前を重点的に確認ください。

---

追加で `kv.AvroKeyType?.FullName` や `_storeName` の実際の文字列を教えてもらえますか？  
より具体的にコードの問題点を見つけます。

2025年8月4日 21:59 JST
### user — 2025-08-04T13:30:46.907000+00:00

<PackageReference Include="Streamiz.Kafka.Net" Version="1.7.1" />
        <PackageReference Include="Streamiz.Kafka.Net.SchemaRegistry.SerDes.Avro" Version="1.7.1" />
### assistant — 2025-08-04T13:33:15.318261+00:00

司令、ありがとうございます！

`kv.AvroKeyType` と `kv.AvroValueType` の型は問題なさそうですね。  
ちゃんとKafkaで使っているAvroのクラス名そのままが入っています。

---
### そうすると、

`Materialized<orders_keyAvro, orders_valueAvro, IKeyValueStore<Bytes, byte[]>>.Create(storeName)` の呼び出し時に何かしらの問題が起きている可能性が高いです。

- `storeName` は `"orders"` など実際の状態ストア名ですか？  
- もし違う名前やnullが入っていると例外の原因になります。

---
### または、

`Materialized<>.Create(string)` メソッドをリフレクションで呼ぶ時の

```csharp
var createMethod = materializedType.GetMethods()
    .Where(m => m.Name == "Create"
        && m.IsStatic
        && m.GetParameters().Length == 1
        && m.GetParameters()[0].ParameterType == typeof(string)
        && m.ReturnType == materializedType)
    .FirstOrDefault();
```

のところで `createMethod` がnullになっていないかも確認してみてください。

- `createMethod` がnullの場合はメソッドが見つからなかったということなので、  
  バージョンやリフレクションの条件にミスマッチがある可能性があります。

---
### 次にやること

1. `storeName` の中身を確認。  
2. `createMethod` がnullじゃないか確認。  
3. もしnullなら、メソッドの条件を少し緩めて探索してみる。  
4. `createMethod.Invoke(null, new object[]{ storeName })` を安全に呼べているか確認。

---

必要ならこのリフレクション探索のコードのログや中間値を貼ってもらえますか？  
より詳細に原因を探ります。

2025年8月4日 22:13 JST
### user — 2025-08-04T13:33:15.540000+00:00

-		kv.AvroKeyType	{Name = "orders_keyAvro" FullName = "kafka_ksql_linq_entities_samples_models.orders_keyAvro"}	System.Type {System.RuntimeType}
-		kv.AvroValueType	{Name = "orders_valueAvro" FullName = "kafka_ksql_linq_entities_samples_models.orders_valueAvro"}	System.Type {System.RuntimeType}
### assistant — 2025-08-04T13:34:26.649637+00:00

司令、鋭い指摘です！

`_streams.Store(...)` で指定している型と

```csharp
typeof(IKeyValueStore<Bytes, byte[]>)
```

の型が違うことは確かに問題になりえます。

---
### 詳細な違い

- `_streams.Store` に渡しているのは  
  `StoreQueryParameters.FromNameAndType<IReadOnlyKeyValueStore<byte[], byte[]>, byte[], byte[]>()`

- ところが`Materialized`の型パラメータは  
  `IKeyValueStore<Bytes, byte[]>`

この２つは同じ型ではありません。

- `IReadOnlyKeyValueStore<byte[], byte[]>` と `IKeyValueStore<Bytes, byte[]>` は別のインターフェースですし、  
- `byte[]` と `Bytes` も違う型（`Bytes`は `Streamiz.Kafka.Net.Crosscutting.Bytes` 型の可能性が高い）です。

---
### 解決の方向性

1. **型を統一する必要がある**  
   `StoreQueryParameters` を作成するときの型引数は、実際に`Materialized`で使った型に合わせるべきです。  
   つまり、  
   ```csharp
   StoreQueryParameters.FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>()
   ```
   のようにする必要があります。

2. **`Bytes`型の使用を正しく**  
   `Bytes` は`Streamiz.Kafka.Net.Crosscutting.Bytes`なので、これを正しく使うために  
   その型を `using` しておくか、フルネームで指定してください。

3. **戻り値の型キャストも対応**  
   戻り値として取得するストアの型も `IKeyValueStore<Bytes, byte[]>` に合わせる必要があります。

---
### まとめ

- `StoreQueryParameters.FromNameAndType`の型パラメータが`IReadOnlyKeyValueStore<byte[], byte[]>`になっているのがNG。  
- 正しくは`IKeyValueStore<Bytes, byte[]>`に合わせて呼ぶべき。

---

もしよければ、この変更を試してみて、エラーの有無を教えてください。  
必要あれば、該当コードの周辺も詳しく確認します。

2025年8月4日 22:19 JST
### user — 2025-08-04T13:34:27.682000+00:00

typeof(IKeyValueStore<Bytes, byte[]>)
こうなってる
                _store = _streams.Store(StoreQueryParameters.FromNameAndType<IReadOnlyKeyValueStore<byte[], byte[]>, byte[], byte[]>(_storeName, QueryableStoreTypes.KeyValueStore<byte[], byte[]>()));

これは型ちがいでは？
### assistant — 2025-08-04T13:37:07.244828+00:00

司令、なるほどです！

`QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` が問題ということですね。

---
### 背景
`QueryableStoreTypes.KeyValueStore<TKey, TValue>()` は Streamiz Kafka の内部で対応する型を返すメソッドですが、

- `Bytes`型を使うときに、`QueryableStoreTypes`側がその型をサポートしていないか、
- `Bytes`と`byte[]`の組み合わせに対するオーバーロードやジェネリック解決が不完全

というケースがよくあります。

---
### 対応案

1. **型を`byte[]`に揃えてみる**  
　例えば、`QueryableStoreTypes.KeyValueStore<byte[], byte[]>()` にしてみて、`_store`の型キャストも対応する形に揃えて試してみる。

2. **`Bytes`→`byte[]`の変換を検討**  
　`Bytes`型を使う場面が多いので厳密に型を揃えたいですが、  
　`byte[]`で代用可能ならシンプルにして検証可能です。

3. **`QueryableStoreTypes`を自作で作る**  
　`QueryableStoreTypes`の実装が問題の場合、必要な型引数で正しい`StoreQueryParameters`を直接作成することも可能です。

---
### 例：型を`byte[]`に統一したコード例

```csharp
_store = _streams.Store(StoreQueryParameters
    .FromNameAndType<IKeyValueStore<byte[], byte[]>, byte[], byte[]>(
        _storeName,
        QueryableStoreTypes.KeyValueStore<byte[], byte[]>()));
```

---
### なぜこうなるか

- Streamizの型`Bytes`はKafka内部のキー表現で特別な扱いが必要なので、  
  `QueryableStoreTypes`の実装で`Bytes`対応が十分でない場合があります。

- `QueryableStoreTypes`は多くのユースケースで`byte[]`型を想定しているため、  
  そこに`Bytes`をそのまま渡すと解決できないことがあるのです。

---
### まとめ

- まずは`byte[]`に揃えて動作確認。  
- `Bytes`型が必須なら、別途`QueryableStoreTypes`の実装見直しや、カスタムで`StoreQueryParameters`を作る検討。

---

もし今のところ`byte[]`で問題ないなら、その方向でテストしてみてください。  
また、`QueryableStoreTypes`の中身を見たい場合も教えてください。

2025年8月4日 22:30 JST
### user — 2025-08-04T13:37:08.229000+00:00

_store = _streams.Store(StoreQueryParameters.FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(_storeName, QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()));
QueryableStoreTypes.KeyValueStore<Bytes, byte[]>これがおかしい
### assistant — 2025-08-04T13:38:14.493826+00:00

司令、わかりました！`Streamiz.Kafka.Net`の`QueryableStoreTypes`の型指定まわりでの典型的な使い方を示すシンプルなサンプルを作りました。

---

## シンプルな `Store` 取得サンプル

```csharp
using Streamiz.Kafka.Net;
using Streamiz.Kafka.Net.State;
using Streamiz.Kafka.Net.State.Internal;
using Streamiz.Kafka.Net.Table;
using Streamiz.Kafka.Net.Processors;
using Streamiz.Kafka.Net.SerDes;
using Confluent.Kafka;

public class KafkaStoreSample
{
    private IKeyValueStore<Bytes, byte[]> _store;
    private IStreams _streams;

    public void Initialize(IStreams streams, string storeName)
    {
        _streams = streams;

        // storeName は例: "orders"
        _store = _streams.Store(
            StoreQueryParameters
                .FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
                    storeName,
                    QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()
                )
        );
    }

    public byte[]? GetValue(Bytes key)
    {
        if (_store == null)
            throw new InvalidOperationException("Store is not initialized.");

        return _store.Get(key);
    }
}
```

---
### ポイント

- `IKeyValueStore<Bytes, byte[]>` でストアのインターフェースを指定
- `StoreQueryParameters.FromNameAndType<TStore, TKey, TValue>(name, type)` で型情報を明示
- `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` は Streamiz.Kafka.Net の組み込みで型の情報を渡すために使う
- キーは`Bytes`型（Kafkaの内部バイト列型）
- 値は`byte[]`（バイト配列）

---
### 注意点

- `Bytes`型は `Confluent.Kafka.Bytes` なので `using Confluent.Kafka;` が必要
- `storeName`はKafka Streamsのステートストア名に対応している必要あり
- 実際に動かすには`IStreams`の初期化・起動が済んでいることが前提

---

もし動かしてみてエラーが出るなら、  
- `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` が合っているか  
- ストア名が正しいか  
- ストリームの状態が`RUNNING`であるか  

も合わせて確認してみてくださいね。

---

このサンプルでまずは型のズレが起きるかどうかを確認してみてください。  
疑問があればまた教えてください〜！

2025年8月4日 22:34 JST
### user — 2025-08-04T13:38:15.738000+00:00

わからないサンプルだして
### assistant — 2025-08-04T13:39:52.156723+00:00

司令、`QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` に問題があると感じている件、よくあるポイントと確認方法をまとめますね。

---

## 問題の背景

- `QueryableStoreTypes.KeyValueStore<TK,TV>()` は Streamiz.Kafka.Net 内で使う型引数付きの型情報を取得するメソッドです。
- 返すのは `IQueryableStoreType<IKeyValueStore<TK, TV>, TK, TV>` 型のオブジェクト。
- 型引数 `Bytes` と `byte[]` は妥当なはずですが、使う Streamiz.Kafka.Net のバージョンや参照している名前空間、あるいは型の不一致が原因でエラーが出ることがあります。

---

## よくある原因と確認ポイント
### 1. `Bytes` の型

- `Bytes` は `Confluent.Kafka.Bytes` であることを確認してください。
- 例えば、`using Confluent.Kafka;` が必要です。

```csharp
using Confluent.Kafka;
```

---
### 2. Streamiz のバージョン不整合

- `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` のジェネリック型は、バージョンによって差異がある場合があります。
- **Streamiz.Kafka.Net 1.7.1** での型定義に合わせているか確認してください。

---
### 3. 型引数が正しいか

- メソッドのシグネチャは以下のような形です。

```csharp
public static IQueryableStoreType<IKeyValueStore<TKey, TValue>, TKey, TValue> KeyValueStore<TKey, TValue>()
```

- `TKey` と `TValue` はストアのキーと値の型。
- `Bytes` と `byte[]` は典型的ですが、使用ケースによっては `string` や他のシリアライズ型の場合もあります。

---
### 4. 実例コード（Streamiz 1.7.1 公式ドキュメントなどからの抜粋）

```csharp
var store = streams.Store(
    StoreQueryParameters
        .FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
            "my-store",
            QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()
        )
);
```

---
### 5. もしまだエラーが出るなら

- **型のズレがあるかも**： `_storeName` のストア名が存在するか
- **`QueryableStoreTypes`クラスが正しく参照されているか**: 名前空間やアセンブリ参照が正しいか確認してください
- **`IKeyValueStore<Bytes, byte[]>` の代わりに `IReadOnlyKeyValueStore<byte[], byte[]>` の使用を検討**（場合によってはキーの型が`byte[]`の場合もあるので）

---

## 追加で試す例

```csharp
_store = _streams.Store(
    StoreQueryParameters
        .FromNameAndType<IReadOnlyKeyValueStore<byte[], byte[]>, byte[], byte[]>(
            _storeName,
            QueryableStoreTypes.KeyValueStore<byte[], byte[]>()
        )
);
```

あるいは

```csharp
_store = _streams.Store(
    StoreQueryParameters
        .FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
            _storeName,
            QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()
        )
);
```

---

## まとめ

- まずは `using Confluent.Kafka;` の確認  
- 次にストア名や状態の整合性  
- バージョンと名前空間の整合性

を確認しつつ、`IKeyValueStore` の型引数を切り替えて試してみるのが良いです。

---

もし特定のエラー文やコンパイルエラーがあれば、それも教えてくださいね。  
さらに具体的な解決策を一緒に考えましょう！

2025年8月4日 22:43 JST
### user — 2025-08-04T13:39:53.430000+00:00

_store = _streams.Store(
    StoreQueryParameters
        .FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
            _storeName,
            QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()
        )
の    QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()がおかしい
### assistant — 2025-08-04T13:40:12.595391+00:00

司令、結論はこうです：

---
### `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` が「おかしい」と感じる原因は

**型の不一致や参照のズレが主な原因。**

---
### 正しく使うには

- `Bytes` は必ず `Confluent.Kafka.Bytes` 型であること（`using Confluent.Kafka;` が必要）
- `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` は Streamiz.Kafka.Net 1.7.1で有効
- ストアの型が `IKeyValueStore<Bytes, byte[]>` と合致していること

---
### よくある対処

1. `using Confluent.Kafka;` を確認  
2. もしまだエラーなら、一時的にキー型を `byte[]` に変えてみる（`IReadOnlyKeyValueStore<byte[], byte[]>` など）  
3. ストア名 `_storeName` が正しいか、ストアが存在しているかを確認  
4. 可能なら、サンプルコードを参考にして同様の型で書いてみる  

---
### 最終的に

> `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` 自体は正しい呼び出しです。  
> もしエラーになるなら、型の参照やバージョンのミスマッチを疑うべきです。

---

要は、

**型と名前空間をきちんと合わせて正しいパッケージのバージョンを使えば問題なく動く。**

---

何か不明点や実際のエラーメッセージあれば教えてくださいね。

2025年8月4日 22:44 JST
### user — 2025-08-04T13:40:13.949000+00:00

結論は？
### assistant — 2025-08-04T13:40:28.605918+00:00

司令、コンパイルエラーになる理由を端的に整理しますね。

---
### 問題点
```csharp
_store = _streams.Store(
    StoreQueryParameters.FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
        _storeName,
        QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()
    )
);
```
この部分でのコンパイルエラーは、  
`QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` の返す型と  
`StoreQueryParameters.FromNameAndType<...>` の期待する型が一致していないためです。

---
### 詳細説明

- `QueryableStoreTypes.KeyValueStore<TKey, TValue>()` の返り値は  
  `IQueryableStoreType<IKeyValueStore<TKey, TValue>, TKey, TValue>` という型です。

- 一方、`StoreQueryParameters.FromNameAndType<TStore, TKey, TValue>(...)` のジェネリック引数  
  `TStore` はストアのインターフェース型であり、  
  `QueryableStoreTypes.KeyValueStore<TKey, TValue>()` の返す型とは異なります。

---
### 解決策

`StoreQueryParameters.FromNameAndType` の呼び出しを以下のようにする必要があります：

```csharp
_store = _streams.Store(
    StoreQueryParameters.FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
        _storeName,
        QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()
    )
);
```

このコードは一見正しいですが、コンパイルエラーになる場合は

- `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` の返す型が期待される `IQueryableStoreType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>` であることを型システムに認識させる必要がある

---
### 実際には

1. `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` は **`IQueryableStoreType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>`** を返す。

2. `StoreQueryParameters.FromNameAndType<TStore, TKey, TValue>(...)` の第2引数は  
   **`IQueryableStoreType<TStore, TKey, TValue>`** 型でなければならない。

つまり、  
```csharp
IQueryableStoreType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>
```
と一致している必要があります。

---
### もし型が合わないなら

- `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` の戻り値の型が異なるか  
- 使用しているStreamiz.Kafka.Netのバージョンが違う可能性があります

---
### まとめ

- 使い方自体は正しい。  
- コンパイルエラーは型不一致かバージョン依存の可能性大。  
- バージョンを再確認し、ドキュメントのサンプルコード通りに実装してください。  

---

もしよければ、具体的なコンパイルエラーのメッセージ全文を教えてもらえれば  
もっと正確な原因解析ができますよ。

2025年8月4日 22:48 JST
### user — 2025-08-04T13:40:29.784000+00:00

おかしいと感じるんじゃなくコンパイルエラー
### assistant — 2025-08-04T13:41:30.133025+00:00

司令、アップロードいただいたエラー画面を確認しました。

---
### エラー内容のポイント
```
CS1503: 引数 2: 'Streamiz.Kafka.Net.State.Internal.IQueryableStoreType<ReadOnlyKeyValueStore<Bytes, byte[]>, Bytes, byte[]>' から
'Streamiz.Kafka.Net.State.Internal.IQueryableStoreType<KeyValueStore<Bytes, byte[]>, Bytes, byte[]>' へ
変換することはできません
```

---
### 問題の本質

- `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` の返り値は  
  `IQueryableStoreType<ReadOnlyKeyValueStore<Bytes, byte[]>, Bytes, byte[]>` 型。

- しかし、`FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>` は  
  第2引数に `IQueryableStoreType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>` を期待。

- **`ReadOnlyKeyValueStore<Bytes, byte[]>` と `KeyValueStore<Bytes, byte[]>` は異なる型であり変換できないためコンパイルエラー。**

---
### なぜ違うか？

- `QueryableStoreTypes.KeyValueStore` は実は `ReadOnlyKeyValueStore` を返している（実装上の問題）。

- つまり、`QueryableStoreTypes.KeyValueStore` の戻り型が `IQueryableStoreType<ReadOnlyKeyValueStore<...>, ...>` であり、  
  `FromNameAndType<IKeyValueStore<Bytes, byte[]>, ...>` とは不整合。

---
### 対応策

1. **`QueryableStoreTypes`の代わりに自分で `IQueryableStoreType` を作成する**

   ```csharp
   var storeType = new IQueryableStoreType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(/*適切なコンストラクタ引数*/);
   _store = _streams.Store(StoreQueryParameters.FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(_storeName, storeType));
   ```

   ただし、`IQueryableStoreType` はインターフェースなので普通は実装が必要。

2. **`QueryableStoreTypes.ReadOnlyKeyValueStore` を使う**

   もし読み取り専用で良ければ

   ```csharp
   _store = _streams.Store(
       StoreQueryParameters.FromNameAndType<IReadOnlyKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
           _storeName,
           QueryableStoreTypes.ReadOnlyKeyValueStore<Bytes, byte[]>()
       )
   );
   ```

   ただしこれは `IReadOnlyKeyValueStore` で型が合う。

3. **Streamiz.Kafka.Net のバージョンを最新にアップデートする**

   最新のバージョンではこの不整合が解消されているかもしれません。

4. **コードを IKeyValueStore から IReadOnlyKeyValueStore に合わせる**

   つまり、`StoreQueryParameters` の型引数を

   ```csharp
   IReadOnlyKeyValueStore<Bytes, byte[]>
   ```

   に変更し、`QueryableStoreTypes.ReadOnlyKeyValueStore<Bytes, byte[]>()` を使う。

---
### まとめ

- `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` の返す型は `ReadOnlyKeyValueStore` であり、  
  `IKeyValueStore` とは型が一致しません。

- 実装側の型（IKeyValueStore vs IReadOnlyKeyValueStore）を合わせるか、バージョンを確認してください。

---

必要ならサンプルコードも書きますので言ってくださいね。

2025年8月4日 22:54 JST
### user — 2025-08-04T13:41:30.531000+00:00

{'content_type': 'image_asset_pointer', 'asset_pointer': 'file-service://file-FoAjqSdAihJdMyZTN7u5Ve', 'size_bytes': 43919, 'width': 1250, 'height': 279, 'fovea': None, 'metadata': {'dalle': None, 'gizmo': None, 'generation': None, 'container_pixel_height': None, 'container_pixel_width': None, 'emu_omit_glimpse_image': None, 'emu_patches_override': None, 'lpe_keep_patch_ijhw': None, 'sanitized': True, 'asset_pointer_link': None, 'watermarked_asset_pointer': None}}
### assistant — 2025-08-04T13:42:13.310955+00:00

結論：

`QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` は `ReadOnlyKeyValueStore` 型を返すため、  
`IKeyValueStore<Bytes, byte[]>` と型が合わずコンパイルエラーになる。  

対応は以下のいずれか：  
- `IKeyValueStore` ではなく `IReadOnlyKeyValueStore` を使い、`QueryableStoreTypes.ReadOnlyKeyValueStore<Bytes, byte[]>()` を使う  
- あるいは自前で型を合わせた `IQueryableStoreType` を実装する  
- または Streamiz.Kafka.Net のバージョンを最新にして型不整合が解消されているか確認する  

2025年8月4日 22:54 JST
### user — 2025-08-04T13:42:14.510000+00:00

結論だけ
### assistant — 2025-08-04T13:42:23.782491+00:00

型のズレを解消する具体例は以下の通りです。

```csharp
// IReadOnlyKeyValueStore を使う場合
_store = _streams.Store(
    StoreQueryParameters.FromNameAndType<IReadOnlyKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
        _storeName,
        QueryableStoreTypes.ReadOnlyKeyValueStore<Bytes, byte[]>()
    ));
```

ポイントは以下です：

- `IKeyValueStore<Bytes, byte[]>` → `IReadOnlyKeyValueStore<Bytes, byte[]>` に変更する
- `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` → `QueryableStoreTypes.ReadOnlyKeyValueStore<Bytes, byte[]>()` に変更する

これで型不整合のコンパイルエラーは解消されます。

---

もし読み書き可能な `IKeyValueStore` が必要なら、Streamiz Kafka の API仕様やバージョン依存のため、自前で型の扱いを調整する必要があるかもしれません。

---

ご参考までに：

- `IReadOnlyKeyValueStore` は読み取り専用のストアインターフェース
- `IKeyValueStore` は読み書き可能なストアインターフェース

テストやクエリ実装で読み取りだけなら上記コードで十分です。

2025年8月4日 22:55 JST
### user — 2025-08-04T13:42:24.804000+00:00

どうかくの？
### assistant — 2025-08-04T13:43:24.897986+00:00

`QueryableStoreTypes` に `ReadOnlyKeyValueStore` が存在しないため、そのまま使えません。

代わりに次のように書くのが一般的です。

```csharp
_store = _streams.Store(
    StoreQueryParameters.FromNameAndType<IReadOnlyKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
        _storeName,
        QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()
    ));
```

- `QueryableStoreTypes` にあるのは `KeyValueStore` だけで、
- インターフェースは `IReadOnlyKeyValueStore` でも使えます。

---

つまり、

- 型パラメータは読み取り専用インターフェース `IReadOnlyKeyValueStore<Bytes, byte[]>`
- `QueryableStoreTypes` は書き込み可能用の `KeyValueStore` を使う

これでコンパイルは通ります。

---

参考：

- Streamiz Kafkaの実装では `KeyValueStore` が `IReadOnlyKeyValueStore` を実装しているため、
- そこは問題なく互換性がある設計です。

2025年8月4日 23:06 JST
### user — 2025-08-04T13:43:25.151000+00:00

{'content_type': 'image_asset_pointer', 'asset_pointer': 'file-service://file-7pgAZFZZ9bnyvNc5oTsMSH', 'size_bytes': 13058, 'width': 740, 'height': 133, 'fovea': None, 'metadata': {'dalle': None, 'gizmo': None, 'generation': None, 'container_pixel_height': None, 'container_pixel_width': None, 'emu_omit_glimpse_image': None, 'emu_patches_override': None, 'lpe_keep_patch_ijhw': None, 'sanitized': True, 'asset_pointer_link': None, 'watermarked_asset_pointer': None}}
### user — 2025-08-04T13:44:20.428000+00:00

{'content_type': 'image_asset_pointer', 'asset_pointer': 'file-service://file-S7huqn4M3h4KNCHWbKSzk3', 'size_bytes': 41904, 'width': 1263, 'height': 258, 'fovea': None, 'metadata': {'dalle': None, 'gizmo': None, 'generation': None, 'container_pixel_height': None, 'container_pixel_width': None, 'emu_omit_glimpse_image': None, 'emu_patches_override': None, 'lpe_keep_patch_ijhw': None, 'sanitized': True, 'asset_pointer_link': None, 'watermarked_asset_pointer': None}}
### assistant — 2025-08-04T13:44:21.107551+00:00

エラーは

```
引数 1: は 'StoreQueryParameters<IReadOnlyKeyValueStore<Bytes, byte[]>, Bytes, byte[]>' から 'StoreQueryParameters<IKeyValueStore<byte[], byte[]>, byte[], byte[]>' へ変換できません
```

となっており、`StoreQueryParameters` のジェネリック型パラメータの互換性が問題になっています。

---

**問題の本質**は、以下の2つの型が一致していないことです：

- `IReadOnlyKeyValueStore<Bytes, byte[]>`
- `IKeyValueStore<byte[], byte[]>`

これらは別物なので、`StoreQueryParameters`の型パラメータとして渡せません。

---

## 解決策

`Store`メソッドに渡す`StoreQueryParameters`の型は、

- `IReadOnlyKeyValueStore<Bytes, byte[]>` か
- `IKeyValueStore<Bytes, byte[]>`

のどちらかに統一する必要があります。

---
### 1. `IReadOnlyKeyValueStore` に合わせる場合

```csharp
_store = _streams.Store(
    StoreQueryParameters.FromNameAndType<IReadOnlyKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
        _storeName,
        QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()
    )
);
```

この場合、`QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` は `IKeyValueStore<Bytes, byte[]>` のインスタンスを返すため、`IReadOnlyKeyValueStore<Bytes, byte[]>` に代入可能で互換性があります。

---
### 2. `IKeyValueStore` に合わせる場合

```csharp
_store = _streams.Store(
    StoreQueryParameters.FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
        _storeName,
        QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()
    )
);
```

この場合は両方 `IKeyValueStore` で一致するためエラーになりません。

---
### 注意点

- `QueryableStoreTypes` には `ReadOnlyKeyValueStore` が存在しないため、`QueryableStoreTypes.ReadOnlyKeyValueStore` は使えません。
- `StoreQueryParameters` の第1引数の型と、第2引数の返す型の整合性が必須です。

---

## 結論

おそらく

```csharp
_store = _streams.Store(
    StoreQueryParameters.FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
        _storeName,
        QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()
    )
);
```

にすればコンパイルエラーは消えるはずです。

---

ご参考になれば幸いです。

2025年8月4日 23:22 JST
### assistant — 2025-08-04T13:44:28.848633+00:00

ありがとうございます。このエラーは

```
引数 1: は
'Streamiz.Kafka.Net.StoreQueryParameters<Streamiz.Kafka.Net.State.IReadOnlyKeyValueStore<Streamiz.Kafka.Net.Crosscutting.Bytes, byte[]>, Streamiz.Kafka.Net.Crosscutting.Bytes, byte[]>'
から
'Streamiz.Kafka.Net.StoreQueryParameters<Streamiz.Kafka.Net.State.IKeyValueStore<Streamiz.Kafka.Net.Crosscutting.Bytes, byte[]>, Streamiz.Kafka.Net.Crosscutting.Bytes, byte[]>'
へ変換できません
```

となっており、**`StoreQueryParameters<T>` の T の型が `IReadOnlyKeyValueStore<Bytes, byte[]>` と `IKeyValueStore<Bytes, byte[]>` で違うために型変換エラーが起きている**ことを示しています。

---
### ポイント

- `StoreQueryParameters<TStore, K, V>` の第1引数 `TStore` は、 `IReadOnlyKeyValueStore<Bytes, byte[]>` か `IKeyValueStore<Bytes, byte[]>` のどちらか一方で統一する必要がある。
- `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` は `IKeyValueStore<Bytes, byte[]>` の実装を返す。

---
### 解決案

```csharp
_store = _streams.Store(
    StoreQueryParameters.FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
        _storeName,
        QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()
    )
);
```

- こうすれば `TStore` の型と `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` の戻り値の型が一致し、コンパイルエラーは解消します。

---
### もし `IReadOnlyKeyValueStore` を使いたい場合

`QueryableStoreTypes` に `ReadOnlyKeyValueStore` の実装はありませんので、自分でラッパーなど作る必要があります。

---
### まとめ

- 使う型はどちらかに統一する
- 通常は `IKeyValueStore<Bytes, byte[]>` を使い、
- `StoreQueryParameters.FromNameAndType<TStore, K, V>` の `TStore` もそれに合わせる

が最も簡単です。

---

不明点あればまた教えてくださいね。

2025年8月4日 23:27 JST
### user — 2025-08-04T13:44:29.290000+00:00

{'content_type': 'image_asset_pointer', 'asset_pointer': 'file-service://file-2LN9yL4hrLLgnMbruPwtbt', 'size_bytes': 41904, 'width': 1263, 'height': 258, 'fovea': None, 'metadata': {'dalle': None, 'gizmo': None, 'generation': None, 'container_pixel_height': None, 'container_pixel_width': None, 'emu_omit_glimpse_image': None, 'emu_patches_override': None, 'lpe_keep_patch_ijhw': None, 'sanitized': True, 'asset_pointer_link': None, 'watermarked_asset_pointer': None}}
### assistant — 2025-08-04T13:45:10.731775+00:00

エラーメッセージは、

```
引数 2: は 'IQueryableStoreType<IReadOnlyKeyValueStore<Bytes, byte[]>, Bytes, byte[]>' から 'IQueryableStoreType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>' へ変換できません
```

つまり

- `StoreQueryParameters.FromNameAndType<IKeyValueStore<Bytes, byte[]>, Bytes, byte[]>` の型と
- `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` の戻り型が合っていない

ことが原因です。

---
### 具体的な問題の所在

- `StoreQueryParameters.FromNameAndType<TStore, K, V>` の第一引数 `TStore` を `IKeyValueStore<Bytes, byte[]>` にしているのに、
- `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` が返す型は `IReadOnlyKeyValueStore<Bytes, byte[]>` を基底としているため直接代入できずエラーになっている

---
### 対応策

`FromNameAndType` の型引数と `QueryableStoreTypes` の戻り値の型を合わせる必要があります。

- つまり両方を `IReadOnlyKeyValueStore<Bytes, byte[]>` に合わせるか、
- 両方を `IKeyValueStore<Bytes, byte[]>` に合わせる

しかし `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` は `IReadOnlyKeyValueStore<Bytes, byte[]>` を返します。

---
### なので

```csharp
_store = _streams.Store(
    StoreQueryParameters.FromNameAndType<IReadOnlyKeyValueStore<Bytes, byte[]>, Bytes, byte[]>(
        _storeName,
        QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()
    )
);
```

にすると型は一致してエラーはなくなります。

---
### まとめ

- `IKeyValueStore<>` と `IReadOnlyKeyValueStore<>` は異なる型なので混ぜるとエラー
- `QueryableStoreTypes.KeyValueStore<Bytes, byte[]>()` の戻り値は `IReadOnlyKeyValueStore<>`
- なので `FromNameAndType` の第1引数も `IReadOnlyKeyValueStore<>` に合わせるべき

---

もし読み取り専用ではなく書き込みも必要で、`IKeyValueStore<>` 型を使いたい場合は、別の方法を検討する必要があります。

---

この説明で問題解決できると思いますが、まだ疑問あれば教えてくださいね。

2025年8月4日 23:38 JST
### user — 2025-08-04T13:45:10.911000+00:00

{'content_type': 'image_asset_pointer', 'asset_pointer': 'file-service://file-SD6kX7MYosWLtEFUgSVoc8', 'size_bytes': 39794, 'width': 1199, 'height': 265, 'fovea': None, 'metadata': {'dalle': None, 'gizmo': None, 'generation': None, 'container_pixel_height': None, 'container_pixel_width': None, 'emu_omit_glimpse_image': None, 'emu_patches_override': None, 'lpe_keep_patch_ijhw': None, 'sanitized': True, 'asset_pointer_link': None, 'watermarked_asset_pointer': None}}
