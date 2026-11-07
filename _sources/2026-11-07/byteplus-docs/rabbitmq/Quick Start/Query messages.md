---
title: "Query messages"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Query_messages"
---

If you are interested in or have questions about messages sent to the message queue for RabbitMQ, you can query messages on the management tool Web UI.

<span id="f861651f"></span>
## Obtain total/accumulated Queue messages


1. Log in to the RabbitMQ version instance Web UI.

   For steps, see [Connect to the RabbitMQ management address](https://docs.byteplus.com/en/docs/rabbitmq/Connect_to_the_RabbitMQ_management_address).

2. In the top menu bar, click **Queues**, then click the target queue name.

3. Set the time range in the **Overview** area of the target queue, then view the queue message data graph.

   * Ready: Number of messages waiting to be consumed in the queue, i.e. the message backlog.

   * Unacked: Number of messages received by consumers but not yet acknowledged. This metric usually appears only in manual acknowledgment consumption mode.

   * Total: Total number of messages currently in the queue.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00c5c009e57846ab92b2f5290443907f~tplv-goo7wpa0wc-image.image) </span>


<span id="2222815e"></span>
## Batch retrieve Queue messages

Query messages in the target Queue. Support for batch querying multiple messages.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">We recommend that you query messages in the Queue only in non\-production environments. If you set the Ack mode to <code>Automatic ack</code>, the messages will be acknowledged and deleted upon query.</div>



1. Log in to Message Queue for RabbitMQ instance Web UI.

   For steps, see [Connect to the RabbitMQ management address](https://docs.byteplus.com/en/docs/rabbitmq/Connect_to_the_RabbitMQ_management_address).

2. In the top menu bar, click **Queues**, then click the target queue name.

3. In the target queue's **Get messages** section, set the query message parameters, then click **Get message(s)** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9eae970749a04ce6b8c210b2182ba794~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameters** |**Description** |
   |---|---|
   |Ack Mode |Set Ack mode:<br><br><br>* Nack message requeue true: This mode receives the message without ack confirmation. The message reenters the queue.<br><br>* Automatic ack: This mode automatically confirms and deletes the message.<br><br>* Reject requeue true: This mode rejects the message. The message reenters the queue.<br><br>* Reject requeue false: This mode rejects the message. The message does not re\-enter the queue and will be deleted. |
   |Encoding |Specify the message encoding method. |
   |Messages |Define the number of messages queried from the queue at one time, with a default value of 1. |
   

4. View messages.

   Return to the message list to view message content, message ID, Exchange, Routing Key, and other information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/390a8a66a7b04dc381bcfc8b83e3c66e~tplv-goo7wpa0wc-image.image) </span>
