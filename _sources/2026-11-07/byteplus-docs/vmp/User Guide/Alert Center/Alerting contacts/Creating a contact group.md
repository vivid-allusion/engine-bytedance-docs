---
title: "Creating a contact group"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Creating-alerting-receiver-groups"
---

A contact group is a collection of multiple contacts. When the matching rule of an alert notification policy is triggered, notifications will be sent to all contacts in the specified contact group.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An alert contact is created. For more details, refer to [Creating a contact](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-receivers).

<span id="40a32336"></span>
## Limits

A root account and its IAM users can create up to 100 contact groups in total.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region.

3. On the left navigation bar, click **Alert center \> Alerting notification policy**. Click the **Notification contact** tab.

4. Click **Create notification contact** to configure the alert notification contact group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89f64bf58883db7da566fba16589aa20.png) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Object type |Select the type of alert notification object. For this example, select **Contact group**. |
   |Name |Specify the name of the alert notification contact group. |
   |Contact person |In the **All contacts** section, select the check boxes before the names of the target contacts to add them to the **Selected contacts** section. |
   

5. Click **OK** to complete the configuration.
