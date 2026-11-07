---
title: "Upgrade a Logstash instance"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Upgrade_a_Logstash_instance"
---

When your Logstash instance specifications can no longer meet your business requirements due to increased data volume and traffic, you can dynamically adjust its configuration, including node specifications, storage type, storage size, and the number of nodes. This topic describes how to upgrade a Logstash instance.

<span id="VKmhKEbc"></span>
## Prerequisites

A Logstash instance has been created and is in the **Running** state. For specific steps, refer to [Create a Logstash instance](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance).

<span id="gcMT4vdN"></span>
## Operation steps


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the upper\-left corner of the top menu bar, select the project and region to which the Logstash instance belongs.

3. In the left\-side navigation pane, select **Data Processing** \> **Logstash**.

4. On the Logstash Instances page, click **Upgrade** in the **Actions** column of the target Logstash instance.

5. On the **Upgrade** page, modify the specifications based on your requirements, and then click **Confirm order**.

   
   |**Upgrade item** |**Note** |
   |---|---|
   |Node specification |Upgrade the node specifications based on your business requirements. The number of CPU cores and memory size of the target specification cannot be lower than the current specification. |
   |Storage type |Changing the storage type is not supported during an upgrade. |
   |Storage specification |Upgrade the storage specifications based on your business requirements. The target specifications cannot be lower than the current specifications when upgrading. |
   |Number of nodes |Increase the number of nodes based on your business requirements. The number of nodes cannot be reduced during an upgrade. |
   

6. On the **Configuration information** page, confirm the upgrade details, read and select the relevant agreements, and then click **Buy now**.

   You can return to the Logstash Instances page. The status of the current Logstash instance is displayed as **Updating**. When the instance status is displayed as **Running**, the upgrade is successful.
