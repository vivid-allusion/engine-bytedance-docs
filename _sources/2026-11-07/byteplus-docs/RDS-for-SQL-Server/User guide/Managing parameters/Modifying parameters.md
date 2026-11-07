---
title: "Modifying parameters"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifying-parameters"
---

This article describes the relevant operation steps for modifying parameters.

<span id="precautions"></span>
## **Precautions**


* In order to ensure the stability of the instance, the console only opens the modification of some parameters. If you can't find the parameters that need to be modified, please [submit a work order](https://console.byteplus.com/workorder/create) for processing.

* See the Modifiable Parameter Range column in the Console Parameters tab when modifying parameter values.

* Some parameters need to be restarted after modification, see **whether restart is required** in the Modifiable Parameters page on the console. It is recommended that you operate during peak business periods and ensure that the application has a reconnection mechanism.

* When modifying the parameters of the master instance, except that the configuration of the parameters `Default Full-text language` and `Default language` will be synchronized to all read\-only instances under the master instance by default, other parameter configuration changes will not be synchronized to read\-only instances.


<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name.

4. At the top of the page, click the **parameter configuration** tab.

5. In the **Parameters** tab, click the Modify button after the **Parameter Run Value** column of the target parameter, set the parameter, and click the checkmark icon.

6. After the modification is complete, click **Submit** at the top left of the page, and **determine Modify Instance Parameters?**  Dialog box Click **Confirm**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can change multiple parameters simultaneously and submit changes simultaneously.</div>


<span id="common-problem"></span>
## **common problem**

**Why can't I find the parameters that need to be modified?** 

For security and stability reasons, only some parameters are currently supported; if you cannot find the parameters that need to be modified, you can [submit a work order](https://console.volcengine.com/ticket/createTicketV2/) to contact technical support.

**Do I need to restart the instance after modifying the parameters?** 

Some parameter changes require restarting the instance. You can see if you need to [restart the instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/restart-instance) on the Modify Parameters page of the console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to operate in a business low peak and ensure that the application has a reconnection mechanism.</div>
