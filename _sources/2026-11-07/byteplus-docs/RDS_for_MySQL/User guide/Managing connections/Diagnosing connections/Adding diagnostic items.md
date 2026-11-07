---
title: "Adding diagnostic items"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/adding_diagnostic_items"
---

This topic describes the procedure for adding connection diagnosis items to an RDS for MySQL instance.

<span id="background"></span>
## Background

Connection diagnosis is a diagnosis function provided by RDS for MySQL. Through connection diagnosis, possible connection access problems of the cloud database can be obtained, and solutions to the access problems can be acquired to ensure the normal access of your cloud database.

The connection diagnosis provided by RDS for MySQL offers the following diagnosis items under two connection methods: private network connection and public network connection.


|Connection method |Diagnosis items |
|---|---|
|Private network |MySQL instance status |
||ECS instance status |
||Whether ECS and MySQL are in the same VPC |
||ECS security group policy |
||Whether the network types of ECS and MySQL are consistent |
||MySQL allowlist policy |
|Public network |MySQL instance status |
||MySQL allowlist policy |


<span id="precautions"></span>
## Precautions

You can create diagnosis items for the connections between one MySQL instance and 500 cloud server ECSs, or between one MySQL instance and 500 public network servers.

<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL Console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region to which the instance belongs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs has not been set, for this operation, you should select the project as <strong>All Resources</strong>.   </div>
   

3. Click **Instances** on the left navigation bar.

4. On the **Instances** page, click the name of the target instance to enter the **Summary** tab.

5. On the **Summary** page, click the **Connectivity** tab to enter the **Connectivity** page.

6. In the **Endpoints** area of the **Connectivity** page, click **Connection diagnosis** to enter the **Connection diagnosis** page.

7. On the **Connection diagnosis** page, after selecting the **Connection method**, add corresponding diagnosis items for the connection diagnosis.

   * If you choose the **Via private network** method, continue with the following steps to add diagnosis items.

      1. Click **Add Elastic Computing Services (ECS)** .

      2. On the **Add Elastic Computing Services (ECS)**  page, after completing the following settings, click **OK**.

         
         |Configuration item |Description |
         |---|---|
         |Database endpoint |Specify the connection endpoint through which the connection to be diagnosed passes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only one connection endpoint can be specified for each diagnosis item.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can search by the name, ID, IP address, or domain name of the connection endpoint, or directly select it from the drop\-down list.</div><br> |
         |ECS |Specify the cloud server (ECS) of the connection to be diagnosed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The cloud server can be searched by its name, instance ID, and IPv4 address.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When searching by the name of a cloud server instance, fuzzy query is supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When searching by the instance ID of the cloud server, precise search by separating multiple IDs with commas or spaces is supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When searching by the IPv4 address of the cloud server instance, fuzzy query is supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">At most 10 IP addresses can be entered in one diagnosis item. Multiple IP addresses are separated by new lines or commas.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">At most 10 ECS servers can be added each time. At most, diagnosis items for the connections between one MySQL instance and 500 cloud server ECSs can be created.</div><br> |
         

   * If you choose the **Via public network** method, continue with the following steps to add diagnosis items.

      1. Click **Add public network server address**.

      2. On the **Add public network server address** page, after completing the following settings, click **OK**.

         
         |Configuration item |Description |
         |---|---|
         |Database endpoint |Specify the connection endpoint through which the connection to be diagnosed passes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the <strong>Via public network</strong> method is selected, the public network access function of the connection endpoint to be diagnosed must be in the enabled state.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only one connection endpoint can be specified for each diagnosis item.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can search by the name, ID, IP address, or domain name of the connection endpoint, or directly select it from the drop\-down list.</div><br> |
         |Public Network Server Address |Specify the IP address of the public network server of the connection to be diagnosed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">At most 10 IP addresses can be entered in one diagnosis item. Multiple IP addresses are separated by new lines or commas.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">At most 10 public network servers' IP addresses can be added each time. At most, diagnosis items for the connections between one MySQL instance and 500 public network servers can be created.</div><br> |
         


<span id="subsequent-steps"></span>
## Subsequent steps


* Performing diagnosis

   On the **Connection diagnosis** page, click **Diagnose** to perform diagnosis on all the added diagnosis items. The time of the last diagnosis is displayed at the top of the **Connection diagnosis** page, and you can initiate diagnosis again at any time.

* Viewing diagnosis results

   For detailed information on viewing diagnosis results, refer to [Viewing diagnosis results](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_diagnosis_results).

* Deleting diagnosis items

   For detailed information on deleting diagnosis items, refer to [Deleting diagnosis items](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_diagnosis_items).
