---
title: "Disabling SSL encryption"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/disabling_ssl_encryption"
---

This topic describes how to disable SSL encryption for a MySQL instance.

<span id="prerequisites"></span>
## Prerequisites


* You have [created an instance](https://www.volcengine.com/docs/6313/75366), and the instance is in the **Running** status.

* SSL encryption has been enabled for the instance.

* An instance will be restarted after the SSL configuration of the instance is modified. Please proceed with caution.


<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>Account's all resource</strong> at this step.</div>



3. On the **Instance list** page, click the target instance.

4. On the Instance Details page, click the **Data security** tab.

5. Click **SSL** tab under the **Data security** tab.

6. Click the switch for enabling/disabling SSL on the right side of the **SSL** tab.
