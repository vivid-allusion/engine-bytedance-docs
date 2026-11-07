---
title: "Enabling Cerebro"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Enabling-Cerebro"
---

Cerebro is an open source, visualized management tool for Elasticsearch (ES) clusters. It allows you to monitor cluster loads, node resources, index distribution, and other information in real time. When you create an ES or OpenSearch instance, Cerebro is disabled by default. Manually enable Cerebro as needed.

After Cerebro is enabled, it cannot be disabled. Before enabling it, evaluate whether it is required in your business scenario. This topic describes how to manually enable Cerebro.

<span id="注意事项"></span>
## Precautions


* Cerebro and Kibana/Dashboards share node resources. Cerebro exclusively occupies 1 core and 2 GiB of memory, and the remaining resources are allocated to Kibana/Dashboards. If you want to enable Cerebro, make sure that the specifications of your Kibana/Dashboards node are at least 2 cores and 4 GiB of memory.

* Cerebro and Kibana/Dashboards share the same domain name, but they use different port numbers.

* Cerebro cannot be enabled for single\-node instances.

* After Cerebro is enabled, it cannot be disabled.


<span id="开启-cerebro"></span>
## Procedure


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Region of the target instance

3. On the **Instances** page, click the name of the instance.

4. In **Instance management \>**  **Visulization configuration**, click **Enable** on the **Cerebro** card.

5. When enabling Cerebro, the system automatically identifies the specifications of your Kibana/Dashboards node. You can encounter the following two situations:

* **Minimum specifications of 1C2GiB**

1. Read the message. After confirming that the specifications are insufficient, click **Upgrade**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/424e676c43dc4588883acd42b1b9a949~tplv-goo7wpa0wc-image.image) </span>

2. On the **Upgrade** page, select **User\-defined specification** for the Kibana/Dashboards node, select the desired specifications, and click **Confirm order** on the lower\-right corner.

   After you upgrade specifications for the Kibana/Dashboards node, fees are charged based on the upgraded specifications. For more information, refer to [Billable items](https://docs.byteplus.com/en/docs/cloudsearch/billing-items).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff0dd926f9ac4a679ee4ab07cf744390~tplv-goo7wpa0wc-image.image) </span>

3. Verify the instance modifications, and click **Buy now**.

   At the beginning, the instance status is **Changing**. When the status changes to **Running**, it indicates that the specifications are successfully upgraded.

4. After the specifications of the Kibana/Dashboards node are upgraded, click **Enable** on the **Cerebro** card. Read the message and click **Immediately enable**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50c582619c0842a98fef0639220f5242~tplv-goo7wpa0wc-image.image) </span>

5. Wait until the Cerebro enabling process is complete.

   At the beginning, the instance status is **Updating**. When the status changes to **Running**, it indicates that Cerebro is successfully enabled.

* **2C4GiB or above**

1. Read the message. If the specifications of the node are sufficient, click **Immediately enable**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50c582619c0842a98fef0639220f5242~tplv-goo7wpa0wc-image.image) </span>

2. Wait until the Cerebro enabling process is complete.

   At the beginning, the instance status is **Updating**. When the status changes to **Running**, it indicates that Cerebro is successfully enabled.
