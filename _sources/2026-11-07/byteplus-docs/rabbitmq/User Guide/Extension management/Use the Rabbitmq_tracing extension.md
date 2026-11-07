---
title: "Use the Rabbitmq_tracing extension"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Use_the_Rabbitmq_tracing_Plugin"
---

The Message Queue for RabbitMQ supports the rabbitmq_tracing extension. It can track messages flowing in and out of RabbitMQ and save log files of these messages for troubleshooting and debugging purposes.

<span id="5ee1d2ea"></span>
## Background information

In message middleware scenarios, message loss sometimes occurs. For example, the message producer successfully sends a message but the consumer does not receive it. Message loss can result from various factors, such as logical errors caused by encoding or network connection issues. In these cases, a message tracing mechanism is needed to identify the specific cause of the message loss so as to facilitate debugging and troubleshooting.

The Message Queue for RabbitMQ provides message tracing through the rabbitmq_tracing extension. Once enabled and traced, the system automatically creates an Exchange in the backend. Each queue is automatically bound to this Exchange, and messages sent to these queues are logged in the Trace files. You can view the Trace files to check the tracking information of specific messages.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The message tracing function consumes some performance and storage space. The amount of storage consumed depends on the message volume. Ensure sufficient instance storage space before using rabbitmq_tracing. To prevent Trace logs from filling the disk, the message tracing feature continuously monitors disk usage and stops writing Trace logs when usage reaches 80%. You can delete unneeded Trace logs to free up disk space.</div>


* <div data-tips="true" data-tips-type="tip">We recommend that you disable the rabbitmq_tracing extension and clear related logs after troubleshooting. It helps to reduce performance impact and save storage space.</div>



<span id="472df978"></span>
## Prerequisites

An instance has been created, and the rabbitmq_tracing extension has been enabled for the instance. For detailed steps, refer to [Enable extension](https://docs.byteplus.com/en/docs/rabbitmq/Enable_extension).

<span id="32d909cd"></span>
## **Operation Steps**


1. Log in to the RabbitMQ Web UI page.

   For operation steps, refer to [Connect to the RabbitMQ management address](https://docs.byteplus.com/en/docs/rabbitmq/Connect_to_the_RabbitMQ_management_address).

2. Add a trace.

   1. Click **Admin** in the top navigation bar.

   2. Click **Tracing** in the right sidebar of the Admin tab.

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f9323aab80e4b68b16b1ef02d847d3b~tplv-goo7wpa0wc-image.image" />      </div>
      

   3. Enter the relevant parameters in the  **Add a new trace** section on the page of  **Tracing.**  

      Parameter descriptions are as follows:

      
      |**Parameter** |**Description** |
      |---|---|
      |Name |Name of the new trace. This name is used to distinguish different traces. |
      |Format |Output message log format. Supported formats:<br><br><br>* Text: (recommended) text format, information displayed plainly for easy reading in WebUI.<br><br>* JSON: JSON format encoded in Base64. It is convenient for parsing after export. |
      |Tracer connection username |Create username for the trace. This should be the username of the WebUI admin user. You can find it on the **Instance Information** page. For detailed instructions, see [View Instance Information](https://docs.byteplus.com/en/docs/rabbitmq/View_instance_information). |
      |Tracer connection password |User password for creating the trace. This should be set as the user password of WebUI administrator. If forgotten, you can reset it on the instance's **Instance Information** page. |
      |Max payload bytes |The maximum limit of the payload field in the trace file. Messages in the payload field will be truncated if exceeded. Unit: Byte. Optional.<br><br>For example, if Max payload bytes is set to 5, when the producer sends original message "Hello Worl!" to the RabbitMQ instance and it is delivered to the consumer, the backend service records it in the trace file truncated as “Hello”. |
      |Pattern |Message tracing mode. Supported settings are as follows:<br><br><br>* #: Trace all messages, including all messages flowing in or out of the RabbitMQ instance.<br><br>* publish.#: Trace only the records of the sender and log only all messages flowing into the RabbitMQ instance.<br><br>* publish.myExchage: Trace only messages entering the specified Exchange. Here, myExchage is the Exchange name; please modify it according to your actual situation.<br><br>* deliver.#: Trace only processing records of receivers and log all messages flowing out of the RabbitMQ instance.<br><br>* deliver.myQueue: Track messages leaving the specified queue. The myQueue is the queue name. Please change it according to your actual needs. |
      

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e4a621226824348814359d664571bad~tplv-goo7wpa0wc-image.image" />      </div>
      

   4. Click **Add trace**.

3. (Optional) Add traces for other nodes.

   Switch to another node in Node. Repeat step 2, and add traces for all other nodes.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the current RabbitMQ instance is a cluster version, you can create traces for all nodes.   </div>
   

4. View the created Trace list.

   After creating a trace, you can view the created trace list in the All traces section on Web UI page.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1168c22d041046b79516e7b8868bd714~tplv-goo7wpa0wc-image.image" />   </div>
   

5. View trace log files.

   When the trace log files store message logs, click the trace log file name in the **Trace log files** section to view the log content.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you no longer need these log details, click <strong>Delete</strong> to remove them.   </div>
   

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4137dec87b04f768932b0fe7ee09634~tplv-goo7wpa0wc-image.image" />   </div>
   

   * The log content of `text.log` is as follows.

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/646adb10b92e4049bf668921b6f580c8~tplv-goo7wpa0wc-image.image" />      </div>
      

   * The log content of `json.log` is as follows.

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb9d09d1fb554d40b84efc0dac14b648~tplv-goo7wpa0wc-image.image" />      </div>
