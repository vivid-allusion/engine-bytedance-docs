---
title: "Managing object groups"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Managing_object_groups"
---

This topic describes the operations that you can perform on Cloud Monitor object groups.

<span id="SVDd1peM"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration page.

3. In the alert configuration section on the left, select **Cloud Monitor** and click the **Object Grouping** tab.

4. Click a button in the "Actions" column that corresponds to the target object group to perform the corresponding operation. The currently supported management operations are as follows:

   
   |Actions |Description |
   |---|---|
   |Edit |Edit the information of the target object group. All information can be modified.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Changes to the object group are synchronized to the associated alert rules.</div><br> |
   |Copy |Copy the target object group and adjust its configuration to quickly create a new object group. |
   |Delete |Delete object groups that are no longer needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If an alert template is applied to the current object group, deleting the object group disassociates the template and deletes the related alert rules.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Deleted object groups cannot be recovered. Proceed with caution.</div><br> |
