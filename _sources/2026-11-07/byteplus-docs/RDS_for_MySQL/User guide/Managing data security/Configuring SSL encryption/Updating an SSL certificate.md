---
title: "Updating an SSL certificate"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/updating_an_ssl_cert"
---

An SSL certificate has an expiration date. You can update the SSL certificate before it expires to extend its validity period for one year. This topic describes how to update the validity period of the SSL certificate of MySQL instances.

<span id="precautions"></span>
## Precautions

An instance will be restarted after the validity period of the SSL certificate of the instance is updated. Please proceed with caution.

<span id="prerequisites"></span>
## Prerequisites


* You have [created an instance](https://www.volcengine.com/docs/6313/75366), and the instance is in the **Running** status.

* SSL encryption has been enabled for the instance. If SSL encryption is not enabled, refer to [Enabling SSL encryption](https://www.volcengine.com/docs/6313/126076).


<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>Account's all resource</strong> at this step.</div>



3. On the **Instance list** page, click the target instance.

4. On the Instance Details page, click the **Data security** tab.

5. Click **Renew certificate** on **SSL** tab, and click **OK** on the pop\-up dialog box.
