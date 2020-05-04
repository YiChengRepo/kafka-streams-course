I have scaleled  up consumer to have 3 threads.
Input topic using 6 partitions with sub node of 2, so 12 tasks, needed. with 3 threads per consumer.

If I run one consumer, each thread run 4 tasks:
```
INFO stream-thread [wordcount-application-96dc4281-67b7-4c76-a518-0b27faf58f42-StreamThread-1] partition assignment took 36 ms.
	current active tasks: [0_0, 1_0, 0_3, 1_3]
	current standby tasks: []
	previous active tasks: []
 (org.apache.kafka.streams.processor.internals.StreamThread:280) 
INFO stream-thread [wordcount-application-96dc4281-67b7-4c76-a518-0b27faf58f42-StreamThread-3] partition assignment took 36 ms.
	current active tasks: [0_1, 1_1, 0_4, 1_4]
	current standby tasks: []
	previous active tasks: []
 (org.apache.kafka.streams.processor.internals.StreamThread:280) 
INFO stream-thread [wordcount-application-96dc4281-67b7-4c76-a518-0b27faf58f42-StreamThread-2] partition assignment took 37 ms.
	current active tasks: [0_2, 1_2, 0_5, 1_5]
```

If I run two consumers, each thread would only run 2 tasks:
```
from c1:
INFO stream-thread [wordcount-application-96dc4281-67b7-4c76-a518-0b27faf58f42-StreamThread-2] partition assignment took 17 ms.
	current active tasks: [0_2, 1_1]
	current standby tasks: []
	previous active tasks: [0_2, 1_2, 0_5, 1_5]
 (org.apache.kafka.streams.processor.internals.StreamThread:280) 
INFO stream-thread [wordcount-application-96dc4281-67b7-4c76-a518-0b27faf58f42-StreamThread-3] partition assignment took 82 ms.
	current active tasks: [0_1, 1_0]
	current standby tasks: []
	previous active tasks: [0_1, 1_1, 0_4, 1_4]
 (org.apache.kafka.streams.processor.internals.StreamThread:280) 
INFO stream-thread [wordcount-application-96dc4281-67b7-4c76-a518-0b27faf58f42-StreamThread-1] partition assignment took 90 ms.
	current active tasks: [0_0, 0_3]
	current standby tasks: []
	previous active tasks: [0_0, 1_0, 0_3, 1_3]

from c2:
INFO stream-thread [wordcount-application-ffa92aac-8a4f-4ab1-904b-1faf081d8e28-StreamThread-1] partition assignment took 23 ms.
	current active tasks: [1_3, 0_4]
	current standby tasks: []
	previous active tasks: []
 (org.apache.kafka.streams.processor.internals.StreamThread:280) 
INFO stream-thread [wordcount-application-ffa92aac-8a4f-4ab1-904b-1faf081d8e28-StreamThread-3] partition assignment took 23 ms.
	current active tasks: [1_4, 0_5]
	current standby tasks: []
	previous active tasks: []
 (org.apache.kafka.streams.processor.internals.StreamThread:280) 
INFO [Consumer clientId=wordcount-application-ffa92aac-8a4f-4ab1-904b-1faf081d8e28-StreamThread-2-consumer, groupId=wordcount-application] Setting newly assigned partitions [wordcount-application-Counts-repartition-2, wordcount-application-Counts-repartition-5] (org.apache.kafka.clients.consumer.internals.ConsumerCoordinator:280) 
INFO stream-thread [wordcount-application-ffa92aac-8a4f-4ab1-904b-1faf081d8e28-StreamThread-2] State transition from PARTITIONS_REVOKED to PARTITIONS_ASSIGNED (org.apache.kafka.streams.processor.internals.StreamThread:209) 
INFO stream-thread [wordcount-application-ffa92aac-8a4f-4ab1-904b-1faf081d8e28-StreamThread-2] partition assignment took 3 ms.
	current active tasks: [1_2, 1_5]
	current standby tasks: []
	previous active tasks: []
```
