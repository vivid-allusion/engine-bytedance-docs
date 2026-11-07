---
title: "Setting alerts"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/set-alert"
---

Cloud Monitor allows you to set alert policies, so that you can monitor the performance and running information of MongoDB instances on Cloud Monitor. This topic describes how to create alert policies for MongoDB instances.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click **Monitoring** tab.

6. In the upper\-right corner of the **Monitoring** tab, click **Create alert policy**.

7. On the **Create alarm strategy** page, configure each parameter according to business needs. For detailed parameter configuration instructions, refer to [Creating alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When configuring <strong>Alarm object</strong> on the <strong>Create alarm strategy</strong> page, you need to select <strong>Resource type</strong> as <strong>Database \> Document Database for MongoDB \- Replica set</strong> or <strong>Database \> Document Database for MongoDB \- Sharding cluster</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Document Database for MongoDB supports using preset trigger conditions. When setting <strong>Alarm rules</strong>, you can click <strong>Application preset trigger conditions</strong>, and the system will use the pre\-configured trigger conditions based on alarm dimensions to help you quickly set up the alarm policy, including indicator types and trigger conditions. For more details, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Creating alarm strategy</a>.   </div>
