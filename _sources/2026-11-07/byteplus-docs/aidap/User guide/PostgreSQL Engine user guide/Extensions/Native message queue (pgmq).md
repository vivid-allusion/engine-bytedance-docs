---
title: "Native message queue (pgmq)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pgmq"
---

<span id="RIPgTCPP"></span>
## Introduction

pgmq is a PostgreSQL\-based lightweight message queue extension. Its API design is similar to Amazon SQS and RSMQ, providing users with simple yet powerful message processing capabilities. It is fully implemented through SQL/PLpgSQL without any backend worker processes or external dependencies, greatly simplifying deployment and maintenance.

pgmq adopts a "queue as table" architecture, storing messages in regular tables in `JSONB` format. It supports visibility timeout, delayed delivery, long polling, batch operations (send/archive/delete), and rich monitoring metrics, making it an ideal choice for building event\-driven architectures, handling background tasks, and decoupling microservices.

<span id="Ga37vpKj"></span>
## Applicable scenarios


* **Asynchronous task processing:**  place time\-consuming operations such as sending emails, generating reports, and image processing into the queue for background consumers to handle asynchronously, improving system response speed.

* **Service decoupling:**  in microservice architectures, use message queues to transmit events, reducing direct dependencies between services.

* **Data pipeline:**  act as a lightweight data pipeline to reliably transfer data between different systems or processing stages.

* **Delayed tasks:**  use the delay delivery feature to implement timed reminders and timed task triggers.


<span id="SDwT1EnQ"></span>
## Create and delete extension

<span id="rTNAmzDd"></span>
### Create extension

Execute the following SQL command to enable the pgmq extension.

```SQL
CREATE EXTENSION pgmq;
```


<span id="gXArIPBJ"></span>
### Delete extension

If no longer needed, execute the following command to uninstall it. Uninstalling the extension removes all related queues, messages, and functions.

```SQL
DROP EXTENSION pgmq;
```


<span id="9GsmxeqR"></span>
## Basic usage

<span id="i4vIG5CU"></span>
### Queue management


1. Create queue (`pgmq.create`)

   Create a new message queue. Each queue physically corresponds to a data table.

   ```SQL
   -- create a regular queue named my_queue
   SELECT pgmq.create('my_queue');
   ```
   

2. Delete queue (`pgmq.drop_queue`)

   Delete a message queue and all its related data tables (including primary and archive queues).

   ```SQL
   -- delete my_queue message queue
   SELECT pgmq.drop_queue('my_queue');
   ```
   


<span id="r8Z7gaYD"></span>
### Message actions


1. Send message (`pgmq.send`)

   Send a message to the specified queue.

   * `queue_name` (text): required, the name of the target queue.

   * `msg` (jsonb): required, the message body to send, must be in `JSONB` format.

   * `delay` (integer): optional, message delay delivery time (seconds). Messages will only be visible to consumers after the specified delay.

      ```SQL
      -- send a message for immediate delivery
      SELECT * FROM pgmq.send(
          queue_name => 'my_queue',
          msg        => '{"task": "process_order", "order_id": 101}'
      );
      
      -- send a delayed message visible after 10 seconds
      SELECT * FROM pgmq.send(
          queue_name => 'my_queue',
          msg        => '{"task": "send_reminder", "user_id": 205}',
          delay      => 10
      );
      ```
      

2. Batch send messages (`pgmq.send_batch`)

   Send multiple messages to the queue at once to improve performance.

   * `msgs` (jsonb[]): required, a `JSONB` array containing multiple messages.

      ```SQL
      SELECT pgmq.send_batch(
          queue_name => 'my_queue',
          msgs       => ARRAY[
              '{"task": "batch_job", "job_id": 1}',
              '{"task": "batch_job", "job_id": 2}'
          ]::jsonb[]
      );
      ```
      

3. Read messages (`pgmq.read`)

   Read a batch of messages from the queue without deleting them immediately. After reading, messages enter an “invisible” state until the visibility timeout (`vt`) ends.

   * `vt` (integer): required, visibility timeout duration (seconds). During this period, other consumers cannot read these messages.

   * `qty` (integer): required, the maximum number of messages to read.

      ```SQL
      -- retrieve up to 5 messages from the queue and set a visibility timeout of 60 seconds
      SELECT * FROM pgmq.read(
          queue_name => 'my_queue',
          vt         => 60,
          qty        => 5
      );
      ```
      

   If successfully retrieved, the function returns a collection containing message details, including `msg_id`, and `message`. If no new messages arrive within the specified time, the long polling mode will wait. Otherwise, it returns an empty set.

4. Pop message (`pgmq.pop`)

   The `pop` action combines reading and deleting the message into an atomic step. It reads a message from the queue and deletes it immediately.

   ```SQL
   -- read and delete a message
   SELECT * FROM pgmq.pop('my_queue');
   ```
   

   This applies to simple scenarios without message acknowledgment mechanisms.

5. Archive message (`pgmq.archive`)

   After processing, the message moves from the primary queue to the archive queue. This is useful for auditing and issue tracing. Archive tables are prefixed with `a_`.

   * msg_id (bigint)/msg_ids (bigint[]): required, the single or multiple message IDs to archive.

      ```SQL
      -- archive a single message
      SELECT pgmq.archive('my_queue', 123);
      
      -- batch archive multiple messages
      SELECT pgmq.archive('my_queue', ARRAY[124, 125, 126]);
      ```
      

   After archiving, you can query the archive table pgmq.a_my_queue to view historical messages.

6. Delete message (pgmq.delete)

   Permanently delete one or more messages. These messages will not be archived.

   ```SQL
   -- delete a single message
   SELECT pgmq.delete('my_queue', 127);
   
   -- batch delete multiple messages
   SELECT pgmq.delete('my_queue', ARRAY[128, 129]);
   ```
   


<span id="kZR48AcC"></span>
## Monitor and measure

pgmq provides views and functions to monitor the queue state.


* `pgmq.metrics_all()` view: provides real\-time metrics for all queues, such as queue name, total message quantity, visible message quantity, and invisible message quantity.

   ```SQL
   SELECT * FROM pgmq.metrics_all();
   ```
   

* `pgmq.metrics(queue_name)` function: retrieves detailed metrics for a specified single queue.

   ```SQL
   SELECT * FROM pgmq.metrics('my_queue');
   ```
