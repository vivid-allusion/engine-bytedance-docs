---
title: "Create quorum queue"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Create_quorum_queue"
---

The message queue for RabbitMQ supports the quorum queue mechanism from open\-source RabbitMQ. Compared to standard queues, it offers higher availability and data security. This section describes the steps for creating a quorum queue through the RabbitMQ instance Web UI.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information 

Quorum Queue is a new distributed message queue based on the Raft consensus protocol. It is designed for the RabbitMQ mirrored mode. Messages in a quorum queue are written only after being confirmed by a majority of nodes in the cluster. This queue provides high availability and data security and is available since version 3.8.0. For details, see the [RabbitMQ official website](https://www.rabbitmq.com/quorum-queues.html).

<span id=".5pON5L2c5q2l6aqk"></span>
## Operation steps


1. Log in to the Message Queue for RabbitMQ Web UI.

   For the operation steps, see [Connect to the RabbitMQ management address](https://docs.byteplus.com/en/docs/rabbitmq/Connect_to_the_RabbitMQ_management_address).

2. In the top menu bar, click **Queues**, then click **Add a new queue**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2404dd2d584a4a0cabd814948f3534be~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the arbitration queue configuration, then click **Add queue**.

   * Type: queue type, select **Quorum** here.

   * Name: queue name, custom set the arbitration queue name here.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87887540dfe14064a38a821566153a59~tplv-goo7wpa0wc-image.image) </span>


<span id="EJ5EEvNW"></span>
## Operation result

For operation results, you can view the successfully created quorum queue in **All queues**.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b903106fddb9d80395539e3aa08771e9.png) </span>
