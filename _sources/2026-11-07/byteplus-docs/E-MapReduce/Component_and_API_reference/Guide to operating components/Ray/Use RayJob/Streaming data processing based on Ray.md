---
title: "Streaming data processing based on Ray"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Streaming_data_processing_based_on_Ray"
---

<span id="cf0bbfd0"></span>
## Background

In real\-time recommendation systems on e\-commerce platforms, it is necessary to consume users' real\-time browsing, add\-to\-cart, and other behavioral data, invoke personalized recommendation models to generate product recommendation lists, and push them to the frontend for display via Kafka, thereby achieving sub\-second response for the process of "behavior occurs \- model computation \- recommendation takes effect". In intelligent customer service scenarios, the system can process user input text or speech\-to\-text data in real time, invoke intent recognition and question\-answering models to generate reply content, and support instant interactive experiences. In credit approval scenarios, the system can process applicants' credit, asset, and other dynamic data in real time, output credit limit evaluation results, and provide support for real\-time loan decision\-making.

All of the above scenarios require streaming real\-time data processing, as well as heterogeneous scheduling of CPU/GPU resources to adapt to different business workloads. Ray's distributed task scheduling capability can dynamically allocate GPU/CPU resources, support model parallelism and data parallelism, and effectively address inference latency bottlenecks. Kafka provides high throughput (up to millions per second) and persistence, ensuring no data loss or blocking under peak traffic, and meeting the stability requirements of real\-time scenarios.

<span id="fb0e6a52"></span>
## Processing flow

<span id="e8ff6668"></span>
### Ray Actor flow

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/239dca1af75f40de9f3bc53591230ba2~tplv-goo7wpa0wc-image.image) </span>

<span id="ff24a5d0"></span>
### Ray Data flow

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c73edcba70cf41c8927f1cfd742cee1c~tplv-goo7wpa0wc-image.image) </span>

<span id="d5dd369c"></span>
## Sample code

<span id="7319aa49"></span>
### Implementation based on Ray Actor

```Python
import ray
from ray.util.queue import Queue, Empty
import time
import logging
import json
from typing import List, Dict
import uuid

def setup_logger(name, level=logging.INFO):
    """配置并返回一个logger实例。"""
    logger = logging.getLogger(name)
    if not logger.handlers: # Prevent adding handler repeatedly
        logger.setLevel(level)
        handler = logging.StreamHandler()
        formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
        handler.setFormatter(formatter)
        logger.addHandler(handler)
    return logger

@ray.remote(num_cpus=0.5)
class KafkaReaderActor:
    def __init__(self, kafka_config: Dict, topic: str, partition: int, output_queue: Queue, flow_control_threshold: int, batch_size: int = 100, batch_timeout: float = 1.0):
        from confluent_kafka import Consumer, TopicPartition
        self.kafka_config = kafka_config
        self.topic = topic
        self.partition = partition
        self.output_queue = output_queue
        self.flow_control_threshold = flow_control_threshold
        self.consumer = Consumer(kafka_config)
        self.running = False
        # Assign specific partition instead of subscribing to the entire topic
        self.consumer.assign([TopicPartition(topic, partition)])
        self.logger = setup_logger(f"KafkaReaderActor-p{self.partition}")
        self.logger.info(f"KafkaReaderActor initialized for topic {topic}, partition {partition}")
        # Metrics
        self.messages_read = 0
        self.start_time = 0
        self.last_report_time = 0
        self.report_interval = 10  # seconds
        # Batch config
        self.batch_size = batch_size
        self.batch_timeout = batch_timeout

    def _report_metrics(self):
        current_time = time.time()
        if current_time - self.last_report_time > self.report_interval:
            total_time = current_time - self.start_time
            speed = self.messages_read / total_time if total_time > 0 else 0
            self.logger.info(
                f"Reader Partition-{self.partition} Metrics: "
                f"Total read: {self.messages_read}, "
                f"Avg speed: {speed:.2f} msg/s"
            )
            self.last_report_time = current_time

    def start(self):
        self.running = True
        self.start_time = time.time()
        self.last_report_time = self.start_time
        self.logger.info(f"KafkaReaderActor started for topic {self.topic}, partition {self.partition}")
        while self.running:
            # Flow control: check queue size before polling
            while self.running and self.output_queue.size() >= self.flow_control_threshold:
                self.logger.warning(
                    f"Reader for partition {self.partition} paused, output queue size "
                    f"({self.output_queue.size()}) reached threshold ({self.flow_control_threshold}). Waiting..."
                )
                time.sleep(1)

            if not self.running:
                break

            # Batch consume messages
            msgs = self.consumer.consume(num_messages=self.batch_size, timeout=self.batch_timeout)
            if not msgs:
                # Timeout but no messages consumed, continue loop
                continue

            for msg in msgs:
                if msg.error():
                    self.logger.error(f"Consumer error: {msg.error()}")
                    continue
                try:
                    # Put message into output queue
                    data = json.loads(msg.value().decode('utf-8'))
                    self.output_queue.put(data)
                    self.messages_read += 1
                    self.logger.debug(f"Successfully read and queued message: {data}")
                except json.JSONDecodeError:
                    self.logger.error(f"Failed to decode JSON message: {msg.value()}")

            self._report_metrics()

    def get_partition(self):
        return self.partition

    def stop(self):
        self.running = False
        self.consumer.close()
        self.logger.info(f"KafkaReaderActor stopped for topic {self.topic}, partition {self.partition}")

@ray.remote(num_cpus=1)
class DataProcessorActor:
    def __init__(self, input_queue: Queue, output_queue: Queue, process_function=None):
        self.input_queue = input_queue
        self.output_queue = output_queue
        self.process_function = process_function or self.default_process
        self.running = False
        self.actor_id = str(uuid.uuid4())[:8]
        self.logger = setup_logger(f"DataProcessorActor-{self.actor_id}")
        self.logger.info(f"DataProcessorActor {self.actor_id} initialized")
        # Metrics
        self.items_processed = 0
        self.start_time = 0
        self.last_report_time = 0
        self.report_interval = 10  # seconds

    def default_process(self, data: Dict) -> Dict:
        # Default handler function, can be overridden by subclass or custom function
        # This is a simple example: add processing timestamp
        data['processed_at'] = time.time()
        data['status'] = 'processed'
        return data

    def _report_metrics(self):
        current_time = time.time()
        if current_time - self.last_report_time > self.report_interval:
            total_time = current_time - self.start_time
            speed = self.items_processed / total_time if total_time > 0 else 0
            self.logger.info(
                f"Processor-{self.actor_id} Metrics: "
                f"Total processed: {self.items_processed}, "
                f"Avg speed: {speed:.2f} items/s"
            )
            self.last_report_time = current_time

    def start(self):
        self.running = True
        self.start_time = time.time()
        self.last_report_time = self.start_time
        self.logger.info(f"DataProcessorActor {self.actor_id} started")
        while self.running:
            try:
                data = self.input_queue.get(timeout=1.0)
                processed_data = self.process_function(data)
                self.output_queue.put(processed_data)
                self.items_processed += 1
                self.logger.debug(f"Processed data: {processed_data}")
            except Empty:
                # It is normal for the queue to be empty, continue waiting
                self._report_metrics()
                continue
            except Exception as e:
                if not self.running:
                    break
                self.logger.error(f"Error processing data: {str(e)}")
            
            self._report_metrics()

    def stop(self):
        self.running = False
        self.logger.info(f"DataProcessorActor {self.actor_id} stopped")

@ray.remote(num_cpus=0.5)
class KafkaWriterActor:
    def __init__(self, kafka_config: Dict, topic: str, input_queue: Queue):
        from confluent_kafka import Producer
        self.kafka_config = kafka_config
        self.topic = topic
        self.input_queue = input_queue
        self.producer = Producer(kafka_config)
        self.running = False
        self.actor_id = str(uuid.uuid4())[:8]
        self.logger = setup_logger(f"KafkaWriterActor-{self.actor_id}")
        self.logger.info(f"KafkaWriterActor {self.actor_id} initialized for topic {topic}")
        # Metrics
        self.messages_written = 0
        self.start_time = 0
        self.last_report_time = 0
        self.report_interval = 10  # seconds

    def delivery_report(self, err, msg):
        if err is not None:
            self.logger.error(f"Message delivery failed: {err}")
        else:
            self.logger.debug(f"Message delivered to {msg.topic()} [{msg.partition()}]")

    def _report_metrics(self):
        current_time = time.time()
        if current_time - self.last_report_time > self.report_interval:
            total_time = current_time - self.start_time
            speed = self.messages_written / total_time if total_time > 0 else 0
            self.logger.info(
                f"Writer-{self.actor_id} Metrics: "
                f"Total written: {self.messages_written}, "
                f"Avg speed: {speed:.2f} msg/s"
            )
            self.last_report_time = current_time

    def start(self):
        self.running = True
        self.start_time = time.time()
        self.last_report_time = self.start_time
        self.logger.info(f"KafkaWriterActor {self.actor_id} started for topic {self.topic}")
        while self.running:
            try:
                data = self.input_queue.get(timeout=1.0)
                self.producer.produce(
                    self.topic,
                    key=data.get('key'),
                    value=json.dumps(data).encode('utf-8'),
                    on_delivery=self.delivery_report
                )
                self.messages_written += 1
                self.producer.poll(0)
                self.logger.debug(f"Sent data to Kafka: {data}")
            except Empty:
                # It is normal for the queue to be empty, continue waiting
                self._report_metrics()
                continue
            except Exception as e:
                if not self.running:
                    break
                self.logger.error(f"Error writing to Kafka: {str(e)}", exc_info=True)
            
            self._report_metrics()
        # Ensure all remaining messages are sent
        self.producer.flush()

    def stop(self):
        self.running = False
        self.logger.info(f"KafkaWriterActor {self.actor_id} stopped for topic {self.topic}")

@ray.remote(num_cpus=0.5)
class ManagerActor:
    def __init__(
        self,
        reader_actors: List[ray.actor.ActorHandle],
        processor_actors: List[ray.actor.ActorHandle],
        writer_actors: List[ray.actor.ActorHandle],
        reader_queue: Queue,
        processor_queue: Queue,
        kafka_config: Dict,
        output_topic: str,
        scale_config: Dict = None
    ):
        self.reader_actors = reader_actors
        self.processor_actors = processor_actors
        self.writer_actors = writer_actors
        self.reader_queue = reader_queue
        self.processor_queue = processor_queue
        
        # KafkaReaderActor is no longer dynamically scaled by ManagerActor, so the related logic has been removed
        
        # Save the parameters required to create an Actor
        self.kafka_config = kafka_config
        self.output_topic = output_topic
        
        # Scaling configuration, including thresholds and maximum/minimum number of instances
        self.scale_config = scale_config or {
            'processor': {'min': 1, 'max': 10, 'high_threshold': 200, 'low_threshold': 20},
            'writer': {'min': 1, 'max': 5, 'high_threshold': 100, 'low_threshold': 10}
        }
        
        self.running = False
        self.check_interval = 5  # Check interval (seconds)
        self.logger = setup_logger("ManagerActor")
        self.logger.info("ManagerActor initialized")

    def get_queue_size(self, queue: Queue) -> int:
        try:
            return queue.size()
        except Exception as e:
            self.logger.error(f"Error getting queue size: {str(e)}")
            return 0

    def scale_actors(self, actor_type: str):
        if actor_type == 'processor':
            actors = self.processor_actors
            queue = self.reader_queue
            config = self.scale_config['processor']
        elif actor_type == 'writer':
            actors = self.writer_actors
            queue = self.processor_queue
            config = self.scale_config['writer']
        else:
            self.logger.error(f"Unknown actor type: {actor_type}")
            return

        queue_size = self.get_queue_size(queue)
        current_count = len(actors)

        # Scaling out required
        if queue_size > config['high_threshold'] and current_count < config['max']:
            new_count = min(current_count + 1, config['max'])
            self.logger.info(f"Scaling up {actor_type} actors from {current_count} to {new_count} (queue size: {queue_size})")
            # Create new Actor instances and add them to the list
            for _ in range(new_count - current_count):
                if actor_type == 'processor':
                    new_actor = DataProcessorActor.remote(self.reader_queue, self.processor_queue)
                    new_actor.start.remote()
                elif actor_type == 'writer':
                    new_actor = KafkaWriterActor.remote(self.kafka_config, self.output_topic, self.processor_queue)
                    new_actor.start.remote()
                actors.append(new_actor)

        # Scaling in required
        elif queue_size < config['low_threshold'] and current_count > config['min']:
            new_count = max(current_count - 1, config['min'])
            self.logger.info(f"Scaling down {actor_type} actors from {current_count} to {new_count} (queue size: {queue_size})")
            # Stop redundant Actors and remove them from the list
            actors_to_stop = actors[new_count:]
            for actor in actors_to_stop:
                try:
                    ray.get(actor.stop.remote())
                except Exception as e:
                    self.logger.error(f"Failed to stop {actor_type} actor: {str(e)}", exc_info=True)
            actors[:] = actors[:new_count]

    def start(self):
        self.running = True
        self.logger.info("ManagerActor started")
        while self.running:
            # Check and adjust each type of Actor
            self.scale_actors('processor')
            self.scale_actors('writer')
            
            # Record current concurrency and queue status
            reader_queue_size = self.get_queue_size(self.reader_queue)
            processor_queue_size = self.get_queue_size(self.processor_queue)
            self.logger.info(
                f"Status - Concurrency: [Readers: {len(self.reader_actors)}, Processors: {len(self.processor_actors)}, Writers: {len(self.writer_actors)}] | "
                f"Queue Sizes: [ReaderQ: {reader_queue_size}, ProcessorQ: {processor_queue_size}]"
            )
            
            time.sleep(self.check_interval)

    def stop(self):
        self.running = False
        self.logger.info("ManagerActor stopped")
        # Stop all Actors
        for actor in self.reader_actors + self.processor_actors + self.writer_actors:
            ray.get(actor.stop.remote())

def main():
    logger = setup_logger("main")
    try:
        # Initialize Ray
        ray.init(ignore_reinit_error=True)
        logger.info("Ray initialized")
    except Exception as e:
        logger.error(f"Failed to initialize Ray: {str(e)}", exc_info=True)
        return

    # Kafka configuration
    kafka_config = {
        'bootstrap.servers': 'kafka-xxx.kafka.volces.com:9592,kafka-xxx.kafka.volces.com:9593,kafka-xxx.kafka.volces.com:9594',
        'security.protocol': 'SASL_PLAINTEXT',
        'sasl.mechanisms': 'PLAIN',
        'sasl.username': 'xxxx',
        'sasl.password': 'xxxx',
        'group.id': 'ray-streaming-group',
        'auto.offset.reset': 'earliest',
    }
    input_topic = 'input_topic'
    output_topic = 'output_topic'

    # Create Ray queue
    reader_queue = Queue(maxsize=1000)
    processor_queue = Queue(maxsize=1000)

    # Obtain Kafka topic partition information
    from confluent_kafka.admin import AdminClient
    admin_client = AdminClient(kafka_config)
    metadata = admin_client.list_topics(topic=input_topic)
    total_partitions = len(metadata.topics[input_topic].partitions)
    logger.info(f"Discovered {total_partitions} partitions for topic {input_topic}")

    # Define flow control thresholds
    flow_control_threshold = 800
    # Define batch read configuration
    reader_batch_size = 100
    reader_batch_timeout = 12

    # Create initial ReaderActor for each partition
    readers = []
    for partition in range(total_partitions):
        reader = KafkaReaderActor.remote(
            kafka_config,
            input_topic,
            partition,
            reader_queue,
            flow_control_threshold,
            batch_size=reader_batch_size,
            batch_timeout=reader_batch_timeout
        )
        readers.append(reader)
        logger.info(f"Created initial KafkaReaderActor for partition {partition}")

    # Create other initial Actors
    processor = DataProcessorActor.remote(reader_queue, processor_queue)
    writer = KafkaWriterActor.remote(kafka_config, output_topic, processor_queue)

    # Create ManagerActor
    manager = ManagerActor.remote(
        readers, [processor], [writer],
        reader_queue, processor_queue, kafka_config, output_topic
    )

    # Start all Actors
    ray.get([
        *[r.start.remote() for r in readers],
        processor.start.remote(),
        writer.start.remote(),
        manager.start.remote()
    ])

    # Keep the main program running
    try:
        while True:
            time.sleep(1)
    except KeyboardInterrupt:
        logger.info("Received shutdown signal")
        # Ensure all Actors have stopped
        ray.get(manager.stop.remote())
        logger.info("All actors stopped successfully")
        ray.shutdown()

if __name__ == "__main__":
    main()
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ba2c52811cc4011b345d329d294bc43~tplv-goo7wpa0wc-image.image" width="3590px" /></div>


<span id="9fdc80f2"></span>
### Implementation based on Ray Data

```Java
import ray 

ray.init(logging_config=ray.LoggingConfig(log_level="INFO"))

consumer_config = {
    "bootstrap.servers": 'kafka-xxx.kafka.volces.com:9592,kafka-xxx.kafka.volces.com:9593,kafka-xxx.kafka.volces.com:9594',
    "security.protocol": "SASL_PLAINTEXT",  # 'SASL_SSL' or 'SASL_PLAINTEXT'
    "sasl.mechanism": "PLAIN",
    "sasl.username": "xxx",
    "sasl.password": "xxx",
    "auto.offset.reset": 'earliest',  // Start reading from the earliest message (optional: 'latest')
    "group.id": 'ray_consumer_group1',        // Consumer group ID (different groups consume independently)
}


ds = ray.data.read_kafka(bootstrap_servers="kafka-xxx.kafka.volces.com:9592,kafka-xxx.kafka.volces.com:9593,kafka-xxx.kafka.volces.com:9594", topic = 'dujl_test', consumer_config=consumer_config)



producer_config = {
    "bootstrap.servers": 'kafka-xxx.kafka.volces.com:9592,kafka-xxx.kafka.volces.com:9593,kafka-xxx.kafka.volces.com:9594',
    "security.protocol": "SASL_PLAINTEXT",  // 'SASL_SSL' or 'SASL_PLAINTEXT'
    "sasl.mechanism": "PLAIN",
    "sasl.username": "xxxx",
    "sasl.password": "xxxx",
}

def map_batches(record):
    // Example: Assume the original JSON contains 'name' and 'age' fields
    // Fields can be added or existing fields modified
    return record

ds.map_batches(map_batches, batch_size=200).write_kafka(bootstrap_servers="kafka-xxx.kafka.volces.com:9592,kafka-xxx.kafka.volces.com:9593,kafka-xxx.kafka.volces.com:9594", topic = 'dujl_test_ray_write', producer_config=producer_config)
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdbcc3032c944ab49dfd8d443f612280~tplv-goo7wpa0wc-image.image" width="3602px" /></div>


<span id="389fce48"></span>
### Serverless Ray Submit Job

Currently, both the visual method and the Python method are supported for Submit Job. For detailed instructions, please refer to: [Serverless Ray usage guide](https://docs.byteplus.com/docs/undefined/69d872d5b2b492054482fcae)。
