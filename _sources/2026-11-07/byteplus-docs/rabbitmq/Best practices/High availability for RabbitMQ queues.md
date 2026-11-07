---
title: "High availability for RabbitMQ queues"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/High_availability_for_RabbitMQ_queues"
---

If you have high requirements for data availability and reliability, you can choose to use the consistent hash extension or Quorum queues to ensure high service availability in the event of a single node failure. This document describes the configuration methods for various high availability solutions.

<span id="a58c5d7c"></span>
## Background information 

Classic queues are the most common basic queue type in RabbitMQ. Classic queues provide basic message delivery and processing functions, making them simple and efficient. Classic queues use a first\-in, first\-out (FIFO) message delivery mechanism to ensure that messages are processed in the order in which they are sent.

However, Classic queues in RabbitMQ are based on a single\-node storage architecture and do not provide data redundancy. If a node fails, messages in the queue may be lost.

If you still need to use Classic queues, you can also achieve high availability for Classic queues through the `rabbitmq_consistent_hash_exchange` extension. `rabbitmq_consistent_hash_exchange` is a consistent hash exchange provided by RabbitMQ, used to distribute messages to queues bound to the exchange using a consistent hash algorithm. This extension can split an existing queue into multiple queues and bind each of the new queues to different nodes, in order to address scenarios where a queue becomes unavailable due to a single node failure.

Quorum queues provide data redundancy and high availability, providing higher reliability assurance for messages. As Quorum queues are a newly introduced feature in RabbitMQ, there may be stability and consistency issues. **Please use Quorum queues with caution**.

<span id="27350162"></span>
## Implement high availability for Classic Queue through an extension

You can enable the `rabbitmq_consistent_hash_exchange` extension in the console, after which messages will be distributed to queues bound to the Exchange using the consistent hash algorithm. An Exchange of type `x-consistent-hash` routes messages by calculating a hash according to the method specified by the message. Queues with different weights are bound to the Exchange, and messages are distributed to the queues according to their respective weights.

<span id="06d134ef"></span>
### Operation steps


1. Enable the `rabbitmq_consistent_hash_exchange` extension in the Message Queue RabbitMQ console.

   Please refer to [Enable extension](https://docs.byteplus.com/en/docs/rabbitmq/Enable_extension) for operational steps.

2. Create a consistent hash Exchange in RabbitMQ Web UI.

   To log in to the RabbitMQ Web UI, please refer to [Connecting to the RabbitMQ management address](https://docs.byteplus.com/en/docs/rabbitmq/Connect_to_the_RabbitMQ_management_address).

   1. Click **Exchanges** in the top menu bar, then click **Add a new exchange**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d7da766c404422fac38be5be1165181~tplv-goo7wpa0wc-image.image) </span>

   2. Fill in the Exchange\-related configuration, and click **Add Exchange**.

      * Name: exchange name. Set the name for Exchange here.

      * Type: exchange. Select **x\-consistent\-hash** here.

      * Durability: Whether it is persisted.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc341d2c372048738dee8e395daa34c1~tplv-goo7wpa0wc-image.image) </span>

3. Create a Classic type queue in RabbitMQ WebUI.

   1. Click **Queues** in the top menu bar, then click **Add a new queue**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3328bf3b6b24eddbf1e8d13ec927265~tplv-goo7wpa0wc-image.image) </span>

   2. Fill in the Classic queue configuration, and click **Add queue**.

      * Type (queue type): Select **Classic** here.

      * Name: Queue name. Set the name of the Classic queue here.

      * Node: The node to which the queue is bound.

      * Arguments: Set the `x-queue-master-locator = client-local` parameter.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f71ce88e98642c0a93c8c291035343c~tplv-goo7wpa0wc-image.image) </span>

4. Bind Exchange and Queues in the RabbitMQ Web UI.

   1. In the **Exchanges** tab, locate and click the Exchange created in Step 2.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc13d6675c91464db073a53392fc2bdf~tplv-goo7wpa0wc-image.image) </span>

   2. Fill in the binding configuration between the Classic queue and Exchange.

      * To queue: Target queue. Here, select the Classic queue created in Step 2.

      * Routing key: The routing key. In a consistent hash exchange, the routing key is used to determine the weight ratio for routing messages to each queue. Based on these weight ratios, messages are proportionally distributed to the bound queues.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d1d70b44b66468f84d0bedc348a2501~tplv-goo7wpa0wc-image.image) </span>

   3. Bind all Classic queues to Exchange sequentially.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b12a82ff9d24779a0b168e9d81c1598~tplv-goo7wpa0wc-image.image) </span>


<span id="b5ee6a3f"></span>
### Production code example

The following is example code for message production.

```Go
public class classicHashDemoProducer {
    public static void main(String[] args) throws IOException, TimeoutException, NoSuchAlgorithmException, KeyManagementException, InterruptedException {
        // Configure the following variables as appropriate.
        final String host = "xxxxxxx.rabbitmq.xxx.com";
        final int port = 5671;
        final String username = "xxxx";
        final String password = "xxxxxx";

        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost(host);
        factory.setPort(port);
        factory.setUsername(username);
        factory.setPassword(password);

        // Please configure connection-related parameters according to business characteristics and network conditions.
        factory.setAutomaticRecoveryEnabled(true);
        factory.setNetworkRecoveryInterval(5000);
        factory.setConnectionTimeout(30 * 1000);
        factory.setHandshakeTimeout(30 * 1000);
        factory.setShutdownTimeout(0);
        factory.useSslProtocol();

        // The following is the configuration for the AMQP-0-9-1 protocol object for message publishing.
        // Set the Vhost name and Exchange name. Please ensure they have already been created in the RabbitMQ Cluster web console.
        final String vhost = "/";
        final String EXCHANGE_NAME = "HashExchange";
        factory.setVirtualHost(vhost);
        // Create Connection and Channel
        Connection connection = factory.newConnection();
        Channel channel = connection.createChannel();

        for (int i = 0; i < 10000; i++) {
            String message = "Hello, RabbitMQ!";
            String messageId = UUID.randomUUID().toString();
            // Generate a random RoutingKey for each message for random hashing
            String RoutingKey = UUID.randomUUID().toString();
            channel.basicPublish(EXCHANGE_NAME, RoutingKey,
                    MessageProperties.PERSISTENT_TEXT_PLAIN.builder()
                            .messageId(messageId)
                            .build(), message.getBytes());
            System.out.println(" Sent message: '" + message + "' with id: " + messageId);
        }
        channel.close();
        connection.close();
    }
}
```


<span id="38c2c044"></span>
### Verify high availability scenarios

After achieving high availability for Classic queues using the consistency hash extension, you can refer to the following examples to verify the availability of Classic queues in scenarios involving single node failures.


* #### Node status is normal <span id="edae8fbd"></span>

   When all RabbitMQ instance nodes are operating normally, you can log in to the RabbitMQ Web UI and observe the production and consumption status of each queue under **Queues** in the top menu bar. The following example shows that messages are hashed to different queues on different nodes, reducing the load on a single node.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2199989d6f2b4c408cdd76102958ebae~tplv-goo7wpa0wc-image.image) </span>

* Single node failure

   When a single\-node failure occurs in a RabbitMQ instance, you can view the node status and message production and consumption activity in the RabbitMQ Web UI to verify whether message production and consumption are functioning normally.

   * View fault nodes

      View node status in the  ** Overview **  tab of the top menu bar. For example, the diagram below shows a single node failure.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64a885b3172d4b6595e55667033f36da~tplv-goo7wpa0wc-image.image) </span>

   * View the status of queue production and consumption

      In the **Queues **  tab in the top menu bar, observe the production and consumption status of each queue. In this scenario, the queue on the faulty node is unavailable, while normal nodes can continue to publish and consume messages, confirming the availability of the Classic queue.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a736d8e23f1040c59b25c9db89d3c587~tplv-goo7wpa0wc-image.image) </span>


<span id="bfb97e4a"></span>
## Achieve high availability through Quorum queues

RabbitMQ Quorum queue is a type of queue introduced in RabbitMQ version 3.8, featuring high availability and data redundancy. Compared with traditional Classic queues, Quorum queues provide better availability and data protection.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">As Quorum queue is a newly introduced feature in RabbitMQ, there may be stability and consistency issues. <strong>Please use Quorum queue with caution</strong>.</div>


Quorum queue features


* Replication and redundancy: Quorum queues use the Raft consensus protocol to replicate and synchronize messages in the queue across multiple nodes. Each message is replicated to multiple nodes to ensure redundant storage and availability of data.

* Automatic failover: When a node fails, the Quorum queue automatically performs failover, switching the role of the primary node to the backup node. This ensures the continued availability of the queue, even if some nodes fail.

* Data consistency: Quorum queue uses the Raft protocol to ensure data consistency. The Raft protocol ensures the atomicity, consistency, and durability of messages, and can maintain data consistency even in the event of node failures and network partitions.

* High availability: Since Quorum queues can be replicated across multiple nodes and have automatic failover capability, they provide higher availability and fault tolerance. Even if some nodes fail, the queue can continue to operate without losing data.


<span id="OlolpNSO"></span>
### Operation steps


1. Log in to the Message Queue for RabbitMQ Web UI.

   For the operating procedure, see [RabbitMQ management address](https://docs.byteplus.com/en/docs/rabbitmq/Connect_to_the_RabbitMQ_management_address).

2. Click **Queues** in the top menu bar, then click **Add a new queue**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2404dd2d584a4a0cabd814948f3534be~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the configuration related to the Quorum queue, then click **Add queue**.

   * Type: queue type, select **Quorum** here.

   * Name: queue name, custom set the arbitration queue name here.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87887540dfe14064a38a821566153a59~tplv-goo7wpa0wc-image.image) </span>
