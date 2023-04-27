# utilities
utilities
Consumer group 'reactivekafka-perf-21' has no active members.

GROUP                 TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
reactivekafka-perf-21 neurontest4     0          55993           55993           0               -               -               -
reactivekafka-perf-21 neurontest4     1          55465           55465           0               -               -               -
reactivekafka-perf-21 neurontest4     2          55755           55755           0               -               -               -
reactivekafka-perf-21 neurontest4     3          55989           55989           0               -               -               -

===============================
** Consumer Performance Test **
===============================

1. Consumer worklaod - Random between 1 and 500 ms per message, 5000 messages
=========================================================================

a) Reactive test (Boundedelastic with threadcap of 1):
---------------------------------------------------

WARNING: payload=4999ofs=4990 Thread[#27,parallel-1,5,main] 1682562565249
Apr 26, 2023 7:29:25 PM com.niladri.demo.ConsumerPerformance$ReactiveConsumerPerformance lambda$consumeMessages$2
WARNING: payload=5000ofs=5058 Thread[#27,parallel-1,5,main] 1682562565249
Apr 26, 2023 7:29:25 PM com.niladri.demo.ConsumerPerformance$ReactiveConsumerPerformance lambda$consumeMessages$1
WARNING: time before=1682562565249ofs=5333
Apr 26, 2023 7:29:25 PM com.niladri.demo.ConsumerPerformance$ReactiveConsumerPerformance lambda$consumeMessages$2
WARNING: payload=5001ofs=4970 Thread[#27,parallel-1,5,main] 1682562565249
Apr 26, 2023 7:29:25 PM com.niladri.demo.ConsumerPerformance$ReactiveConsumerPerformance lambda$consumeMessages$1
WARNING: time before=1682562565249ofs=5334
Start-time               End-time               Total-MB  MB/sec Total-messages Messages/sec
2023-04-26 19:29:19:503, 2023-04-26 19:29:25:249, 0.4769, 0.0830, 5001, 870.3446

b) consumer poll (CompletableFuture with 12 thread executorservice):
----------------------------------------------------------------

19:33:38.235 [main] DEBUG org.apache.kafka.clients.consumer.KafkaConsumer - [Consumer clientId=consumer-nr-reactivekafka-non12-1, groupId=nr-reactivekafka-non12] Kafka consumer has been closed
Start-time               End-time               Total-MB  MB/sec Total-messages Messages/sec
2023-04-26 19:31:52:820, 2023-04-26 19:33:38:235, 0.4768, 0.0045, 5000, 47.4316


2. Consumer worklaod - Random between 1 and 50 ms per message, 5000 messages
========================================================================

a) Reactive test (Boundedelastic with threadcap of 1):
-----------------------------------------------------

Apr 26, 2023 7:36:15 PM com.niladri.demo.ConsumerPerformance$ReactiveConsumerPerformance lambda$consumeMessages$2
WARNING: payload=5000ofs=5298 Thread[#35,parallel-4,5,main] 1682562975417
Apr 26, 2023 7:36:15 PM com.niladri.demo.ConsumerPerformance$ReactiveConsumerPerformance lambda$consumeMessages$2
WARNING: payload=5001ofs=5196 Thread[#35,parallel-4,5,main] 1682562975417
Start-time               End-time               Total-MB  MB/sec Total-messages Messages/sec
2023-04-26 19:36:13:891, 2023-04-26 19:36:15:417, 0.4769, 0.3125, 5001, 3277.1953

b)consumer poll (CompletableFuture with 12 thread executorservice):
-----------------------------------------------------------------

Apr 26, 2023 7:37:58 PM com.niladri.demo.ConsumerPerformance$NonReactiveConsumerPerformance lambda$consume$0
WARNING: record=5070 Thread[#29,pool-1-thread-1,5,main]
Apr 26, 2023 7:37:58 PM com.niladri.demo.ConsumerPerformance$NonReactiveConsumerPerformance lambda$consume$0
WARNING: record=5076 Thread[#40,pool-1-thread-12,5,main]
.....
19:37:58.808 [main] INFO org.apache.kafka.common.utils.AppInfoParser - App info kafka.consumer for consumer-nr-reactivekafka-non12-1 unregistered
19:37:58.808 [main] DEBUG org.apache.kafka.clients.consumer.KafkaConsumer - [Consumer clientId=consumer-nr-reactivekafka-non12-1, groupId=nr-reactivekafka-non12] Kafka consumer has been closed
Start-time               End-time               Total-MB  MB/sec Total-messages Messages/sec
2023-04-26 19:37:46:504, 2023-04-26 19:37:58:808, 0.4768, 0.0388, 5000, 406.3719


======================================
** End to End delivery latency Test **
======================================

1. Semder receiver workload - 15000 messaged, sent, immediately consumed and checked for integrity
===================================================================================================

a) Reactive test:
------------------

Avg latency: 0.7709 ms

19:44:15.055 [reactive-kafka-reactivekafka-perf-24-1] DEBUG org.apache.kafka.clients.NetworkClient - [Consumer clientId=consumer-reactivekafka-perf-24-1, groupId=reactivekafka-perf-24] Received FETCH response from node 0 for request with header RequestHeader(apiKey=FETCH, apiVersion=13, clientId=consumer-reactivekafka-perf-24-1, correlationId=43602): FetchResponseData(throttleTimeMs=0, errorCode=0, sessionId=1834361329, responses=[])
Total latency: 11563.3521 ms


19:44:15.061 [reactive-kafka-reactivekafka-perf-24-1] DEBUG org.apache.kafka.clients.consumer.internals.Fetcher - [Consumer clientId=consumer-reactivekafka-perf-24-1, groupId=reactivekafka-perf-24] Sending READ_UNCOMMITTED IncrementalFetchRequest(toSend=(), toForget=(), toReplace=(), implied=(neurontest4-2, neurontest4-1, neurontest4-3, neurontest4-0), canUseTopicIds=True) to broker localhost:9092 (id: 0 rack: null)
19:44:15.061 [reactive-kafka-reactivekafka-perf-24-1] DEBUG org.apache.kafka.clients.NetworkClient - [Consumer clientId=consumer-reactivekafka-perf-24-1, groupId=reactivekafka-perf-24] Sending FETCH request with header RequestHeader(apiKey=FETCH, apiVersion=13, clientId=consumer-reactivekafka-perf-24-1, correlationId=43629) and timeout 30000 to node 0: FetchRequestData(clusterId=null, replicaId=-1, maxWaitMs=0, minBytes=1, maxBytes=20971520, isolationLevel=0, sessionId=1834361329, sessionEpoch=43617, topics=[], forgottenTopicsData=[], rackId='')
Percentiles: 50th = 0.3566, 75th = 0.5135, 90th = 0.8545, 99th = 5.0618, 99.9th = 17.4088

a) consumer poll test:
--------------------

19:49:02.603 [main] DEBUG org.apache.kafka.clients.NetworkClient - [Consumer clientId=consumer-reactivekafka-perf-27-1, groupId=reactivekafka-perf-27] Sending FETCH request with header RequestHeader(apiKey=FETCH, apiVersion=13, clientId=consumer-reactivekafka-perf-27-1, correlationId=29542) and timeout 30000 to node 0: FetchRequestData(clusterId=null, replicaId=-1, maxWaitMs=0, minBytes=1, maxBytes=20971520, isolationLevel=0, sessionId=1525115097, sessionEpoch=29527, topics=[FetchTopic(topic='neurontest4', topicId=VECPhSlaSaOAmH48OUoH4A, partitions=[FetchPartition(partition=2, currentLeaderEpoch=0, fetchOffset=63217, lastFetchedEpoch=-1, logStartOffset=-1, partitionMaxBytes=20971520)])], forgottenTopicsData=[], rackId='')
Avg latency: 0.8306 ms

Total latency: 12459.3136 ms

Percentiles: 50th = 0.2623, 75th = 0.4339, 90th = 1.3671, 99th = 7.2963, 99.9th = 21.4052



