---
title: "How to confirm cluster messages have been fully consumed"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/How_to_confirm_cluster_messages_have_been_fully_consumed"
---

During the RabbitMQ business migration process, the old cluster can only be decommissioned after confirming that all messages in the old cluster have been consumed. When both the number of consumable messages and the number of unconsumed messages are zero, it indicates that the old consumer has consumed all messages. You can view these two values in the following two ways:


* Open source Web UI

* Open source API


<span id=".6YCa6L-H5byA5rqQIFdlYiBVSSDmn6XnnIs="></span>
## View through the open\-source Web UI


1. Log in to the open\-source RabbitMQ console via a browser.

2. On the **Overview** tab, expand **Totals**.

3. View relevant data in the **Queued messages** table. When the number of consumable messages (**Ready**), the number of unconsumed messages (**Unacked**), and the total number of messages (**Total**) are all zero, it indicates that all stored messages in the old cluster have been consumed.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ae757f798710163117b9c2825ef9ce9e.png) </span>


<span id=".6YCa6L-H5byA5rqQQVBJ5p-l55yL"></span>
## View using an open\-source API

You can also view relevant data by calling the open\-source API.

RabbitMQ API：

```plain
curl -s -u username:password -XGET http://ip:port/api/overview
```


Parameter description:


|Parameters |DescriptionDescription |
|---|---|
|username |The account for logging in to the Web UI of the old RabbitMQ cluster. |
|password |The password for logging into the Web UI of the old RabbitMQ cluster. |
|ip |Access point domain name for the old RabbitMQ Cluster Web UI. |
|port |Old RabbitMQ cluster Web UI port (default: 15672). |


An example of the response from this interface is as follows:

```plain
"queue_totals":{
    "messages":0,
    "messages_details":{
        "rate":0.0
     },
     "messages_ready":0,
     "messages_ready_details":{
         "rate":0.0
     },
     "messages_unacknowledged":0,
     "messages_unacknowledged_details":{
         "rate":0.0
     }
}
```


In the returned information, **queue_totals** represents data related to consumption. Specifically:


* **messages_ready**: Number of consumable messages.

* **messages_unacknowledged**: Number of unconsumed messages.


When all of the above parameters are zero, it means that the messages from the old cluster have been fully consumed.
