---
title: "Enable extension"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Enable_extension"
---

After creating an instance in the message queue for RabbitMQ console, the instance extension is disabled by default. You can manually enable extension for the instance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

The message queue for RabbitMQ supports enabling the following extensions in the console.


|**Extension name** |**Function description** |**Port number** |
|---|---|---|
|rabbitmq_mqtt |Indicates whether the instance supports the MQTT protocol (TCP mode). |8883 |
|rabbitmq_web_mqtt |Indicates whether the instance supports the MQTT protocol (WebSocket mode). |15676 |
|rabbitmq_delayed_message_exchange |Indicates whether the instance has enabled the message delay function.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The extension delay time has an error margin of about 1%. It may cause messages to be sent to consumers either earlier or later than expected. The error margin increases with larger message volumes.</div><br> |/ |
|rabbitmq_stomp |Indicates whether the instance supports the STOMP protocol. |61614 |
|rabbitmq_tracing |Tracks message flow in and out and logs them into a file.<br><br>Please ensure sufficient instance storage capacity. Open and access it through the WebUI console. For instructions on using the rabbitmq_tracing extension, please refer to [Using the rabbitmq_tracing extension](https://docs.byteplus.com/en/docs/rabbitmq/Use_the_Rabbitmq_tracing_Plugin). |/ |
|rabbitmq_consistent_hash_exchange |Consistent hash exchange routes messages to queues using a consistent hash algorithm.<br><br>Enable to achieve high availability for Classic queues with this extension. For instructions on using the rabbitmq_consistent_hash_exchange extension, refer to [high availability for Classic queues via extension](https://docs.byteplus.com/en/docs/rabbitmq/High_availability_for_RabbitMQ_queues#27350162) |/ |
|rabbitmq_shovel |Supports message replication between different RabbitMQ servers. |/ |
|rabbitmq_shovel_management |Supports managing and monitoring the configuration and status of Shovel.<br><br>Open and access it through the WebUI console. |/ |
|rabbitmq_federation |Supports transmitting messages between brokers or clusters. |/ |
|rabbitmq_federation_management |Provide a GUI for Federation function. |/ |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Modifying the extension port number is not supported.

* In cluster instances, enabling or disabling the rabbitmq_mqtt, rabbitmq_web_mqtt, or rabbitmq_stomp extensions triggers a rolling restart of the RabbitMQ cluster. It is recommended to perform this operation outside business hours. The rolling restart may cause loss of non\-persistent messages and brief connection instability, such as disconnections. Whether the client reconnects automatically depends on the client's configuration.

* In single\-node instances, enabling or disabling the rabbitmq_mqtt, rabbitmq_web_mqtt, or rabbitmq_stomp extensions causes a service interruption and requires the client to actively reconnect.

* Disabling the rabbitmq_delayed_message_exchange extension will cause undelivered delayed messages to be lost. Proceed with caution.


<span id=".5pON5L2c5q2l6aqk"></span>
## Enable extension


1. Log in to the [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq).

2. Select the region where the instance is located in the top menu bar.

3. Find the specified instance on the **Instances** page and click the instance name.

4. On the **Instance information** page, click **extension management**.

5. On the **extension management** tab, toggle the switch in the **Actions** column for the specified extension.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also select the extension to enable and click <strong>Open</strong> at the bottom of the list to enable extensions in bulk.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If enabling extension fails, you can retry after troubleshooting.   </div>
   

6. In the pop\-up dialog, click **OK**.
