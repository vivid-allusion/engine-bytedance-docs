---
title: "Set up mirrored queue for instance"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Set_up_mirrored_queue_for_instance"
---

The message queue for RabbitMQ supports the open\-source RabbitMQ mirrored queue mechanism, offering higher reliability and availability compared to regular queues. This section describes the steps to configure a regular queue as a mirrored queue through the RabbitMQ instance's Web UI page.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Generally, regular queues and their contents are stored on a single node. If that node fails, the associated queue becomes unavailable. The message queue for RabbitMQ supports the open\-source RabbitMQ mirrored queue mechanism. Mirrored queues allow the cluster to replicate queues to other broker nodes. If a broker node in the cluster fails, the queue automatically switches to another mirrored broker.

For detailed information about the RabbitMQ Web UI, refer to the [RabbitMQ official website](https://www.rabbitmq.com/).

<span id="19de34cc"></span>
## Notes

During node restart, RabbitMQ mirrored queues synchronize full data. This synchronization consumes significant memory and may trigger a high memory watermark. It prevents producers from writing messages. If the mirrored queue backlog exceeds 1GB, it will greatly affect cluster performance and stability. We recommend that you monitor usage trends.

<span id=".5pON5L2c5q2l6aqk"></span>
## Operation steps


1. Log in to the Message Queue for RabbitMQ Web UI.

2. Click **Admin** in the top menu bar.<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a291bc3cbb158b2faaffb00720be3ffb.png) </span>

3. (Optional) Create a vhost.

   If you need to specify a vhost, perform this step. If not, proceed to step 4.

   1. Click **Virtual Hosts** in the right navigation bar.

   2. Enter the **Name**.

   3. Click **Add virtual host**.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ca0db642b5ef7728c571872cc6c311de.png) </span>

4. Select **Policies** in the right navigation bar to set rules for the vhost.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f56f54b37e1a1b8eec9bc15c940a3625.png) </span>

   
   |**Parameter** ||**Description** |
   |---|---|---|
   |Name ||Name of the rule. |
   |Pattern ||The queue matching pattern is regular expression format. |
   |Priority ||Priority of the rules. Optional parameter. |
   |Definition |ha\-sync\-mode |Synchronization methods for messages in mirrored queues support the following settings:<br><br><br>* automatic: automatically synchronize data to the master.<br><br>* manually: manually synchronize data to the master. |
   ||ha\-mode |Specify the mirrored queue mode, supporting these settings:<br><br><br>* all: mirror on all brokers in the cluster.<br><br>* exactly: mirror on a specified number of brokers. The number is set by ha\-params.<br><br>* nodes: mirror on specified brokers. The names of brokers are set by ha\-params. |
   ||ha\-params |Parameters related to the ha\-mode. |
   

5. Click **Add / update policy**.


<span id=".5pON5L2c57uT5p6c"></span>
## Operation result

The result after adding the rule is shown in the figure below.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9b56a2860421f5898a006939af15158c.png) </span>
