---
title: "Importing VMP notification configuration data"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Importing_VMP_notification_configuration_data"
---

The Unified Alerting Center supports one\-click import of notification configuration data from VMP, including alert notification policies, contacts, contact groups, notification templates, and alert silence policies. This topic describes how to import VMP notification configuration data.

<span id="FTtM4QN1"></span>
## Background

The correspondence relationships between the resource names in the VMP Alarm Center and the Unified Alert Center are as follows:


|VMP Alarm Center |Unified Alert Center |
|---|---|
|Alert notification policy |Notification policy |
|Contacts |Contacts |
|Contact group |Contact group |
|Notification template |Notification templates |
|Alerting silence policies |Silence policy |


<span id="vmNWuaP8"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select "**Alert Center \-\> Notification configuration**" to go to the "Notification configuration" page.

3. Select the **Notification Policy** tab and click **Import VMP notification configuration data**.

4. Select the import type as needed. Then, click **Confirm** to import VMP alert notification policy, contacts, contact groups, notification message template, notification template, and alert silence policy into the Unified Alert Center.

   
   |Parameter |Description |
   |---|---|
   |Import type |The type of resource to import. Select a type as needed.<br><br><br>* **Import only new**: Imports new resources only. Resources with duplicate names are not imported.<br><br>* **Overwrite import**: Imports all resources. If a resource has a duplicate name, the data in the Unified Alert Center is overwritten with the data from VMP. |
