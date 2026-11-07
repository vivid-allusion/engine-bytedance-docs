---
title: "Managing traffic for DataFlow"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Configuring_DataFlow_controls"
---

Enabled DataFlow policies or tasks concurrently consume FileNAS and TOS bucket resources, including read/write bandwidth and QPS, for their import and export rules. To prevent disruptions to FileNAS and TOS bucket IO access, you can adjust the bandwidth and QPS for DataFlow rules on FileNAS and TOS. This topic explains how to set up traffic management on FileNAS and TOS.

<span id="39034c73"></span>
## Background information

By default, DataFlow utilizes a maximum of 30% of the total FileNAS bandwidth. This DataFlow allocation is further divided between import and export operations, with import traffic limited to 30% of the total DataFlow bandwidth. TOS has no such limit.

For instance, if the bandwidth limit of a FileNAS file system is 20 GB/s, the total DataFlow allocation is 6 GB/s, with the import (write) bandwidth at 2 GB/s and the export (read) bandwidth at 6 GB/s.

<span id="305c823f"></span>
## Configuring throttling on FileNAS

When DataFlow and business access peak simultaneously and DataFlow usage leads to low bandwidth for business tasks, you can temporarily boost the provisioned bandwidth to support higher file system limits.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Provisioned bandwidth fees are based on the actual bandwidth used. For details, see <a href="https://docs.byteplus.com/en/docs/nas/Billing-overview">Billing overview</a>.</div>


<span id="894cb60d"></span>
### Steps


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File System** \> **File System list**.

4. On the **File System list** page, click **Change** in the **Actions** column of the target file system.

5. On the **Change** page, topple on the **Provisioned bandwidth** switch, specify the upper limit, and click **Confirm order**.

6. On the details page, read and check **The Terms of Storage Products and Services**, and click **Buy now**.


<span id="99b89696"></span>
## Configuring QoS policies on TOS

TOS has a default bandwidth limit of [10 Gbps](https://docs.byteplus.com/en/docs/tos/docs-restrictions#68a40616) per region. To ensure uninterrupted business operations on TOS, you can configure TOS QoS polices to define performance thresholds for data flows between FileNAS and TOS. For more information, see [QoS policy overview](https://docs.byteplus.com/en/docs/tos/Qos-policy-overview).

You can configure the write or read bandwidth in the TOS QoS policies to manage FileNAS DataFlow limits for export or import rules. You can also set the write QPS, read QPS, and List\-type QPS for DataFlow rules on TOS. Here are examples showing how to use QoS policies to limit bandwidth for FileNAS export and import rules.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The TOS QoS policy feature is currently in closed beta. Please contact your account manager for access.</div>


<span id="79021d6e"></span>
### **Steps**


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **QoS policy management**.

3. At the top left of the **QoS policy management** page, select the target region.

4. Choose the authorization method that fits your needs.

   
   <Tabs>
   <Tab zoneid="sLwZ0CCK" title="Visual view">
   <TabTitle>Visual view</TabTitle>
   
   Configure QoS policies by visual view:
   
   
   1. Click **Create policy**.
   
   2. On the **Create QoS policy** page, set the following parameters.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The policy name, QoS value, and resource settings shown here are for illustrative purposes. You need to set these parameters according to your actual situation.   </div>
      
   
      * **Policy configuration method**: Select **Visual view**.
   
      * **Policy name**: Enter the policy name qospolicy.
   
      * **QoS value**: Set **Category** to **WritesRate**, and **Value** to 1000. Click **Add row**, and set **Category** to **ReadsRate**, and **Value** to 2000.
   
      * **Authorized user**: Set **Authorized user** to **Specified account**, then select **Current main account**. In the **Role name** section, click **Add row** to apply FileNASAccessTOSRole.
   
      * **Resource**: Check the **Objects in bucket** check\-box. Set **Bucket** name to bucketevent, **Scope of application** to **Specified object(s)** , and **Resource path** to dir/\*.
   
      * **Condition**: No conditions are required for this scenario.
   
   3. After completing the settings, click **Next step**.
   
   4. After verifying the details, click **Confirm**.
   
   
   </Tab>
   <Tab zoneid="UOy2ykGc" title="JSON view">
   <TabTitle>JSON view</TabTitle>
   
   Click the **JSON view** tab, then click **Edit**. Next, copy the following content into the Statement parameter, modify the values of WritesRate and ReadsRate parameters, enter the account ID in Principal parameter, and specify the bucket name and resource path in Resource parameter. Finally, click **Save**.
   
   ```Plain Text
   {
         "Sid": "qospolicy",
         "Quota": {
           "WritesQps": "",
           "ReadsQps": "",
           "ListQps": "",
           "WritesRate": "1000",
           "ReadsRate": "2000"
         },
         "Principal": [
           "trn:iam::210015****:role/FileNASAccessTOSRole"
         ],
         "Resource": "trn:tos:::bucketevent/dir/*"
       }
   ```
   
   
   
   </Tab>
   </Tabs>
