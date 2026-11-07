---
title: "Deleting ESI"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Delete_Elastic_Scheduled_Instances"
---

Elastic Scheduled Instances (ESI) are not automatically released. After your business ends, you can follow the steps in this document to delete ESI in the console.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">ESI used for less than one hour is billed at a minimum of one hour. For specific billing details, refer to your invoice. <a href="https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances#.6K6h6LS5">What is the 1\-hour minimum charge?</a></div>


* <div data-tips="true" data-tips-type="warning">After ESIs and their associated resources are deleted, billing stops. <a href="https://docs.byteplus.com/en/docs/ecs/Billing-FAQs#.5Li65LuA5LmI5a6e5L6L5bey57uP5Yig6Zmk77yM5L2G5LuN54S25Zyo6K6h6LS577yf">Why is a deleted instance still being billed?</a></div>



<span id=".5pON5L2c5pa55byP"></span>
## Method

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you delete an ECS instance, do not modify any associated resources. Otherwise, instance or resource deletion may fail.</div>



<Tabs>
<Tab zoneid="N6hR4UGXSg" title="Delete ESI on the order list page">
<TabTitle>Delete ESI on the order list page</TabTitle>

<span id="VDzMQgL5"></span>
#### Considerations


* Only ESI orders in **Delivered** status or **Partial failed** status support batch deletion of all unreleased instances under the order.

* If you delete an instance on the ESI order list page, you can see the status of the instance's related resources in the following table for reference.

   
   |**Resources** |**Situation after you delete the ESI** |
   |---|---|
   |System volume/local volume |Automatically released along with instances. Once a system/local volume is released, the data is automatically cleared and cannot be recovered. Please[ back up your data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) in advance. |
   |Data volume |It depends on when you create an instance or mount a volume, whether you select the option to delete the data volume with the instance:<br><br><br>   * If you select this option, the data volume is released with the instance upon deletion and cannot be restored. Please [back up your data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) in advance.<br><br>   * If you have not selected this option, the data volume is unmounted from instance but not released. By default, data in the volume is retained, and the **billing for the data volume continues**. You can still mount the data volume to another instance. |
   |EIP |   * For EIP associated with the primary private IP of the instance's primary network interface, its situation depends on when you [create instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) or [associate instance with EIP](https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP), whether you select "Delete with instance".<br><br>      * If you select this option, the EIP is released together with instance when you delete instance.<br><br>      * If not, when the instance is deleted, EIP is automatically disassociated and not released. You **still need to pay for EIP**. You can still associate EIP with another instance.<br><br>   * For EIP associated with both the secondary private IP of the primary network interface and the secondary network interface, it is disassociated from the instance and not automatically released. You **still need to pay for EIP**. You can still associate the EIP with another instance. |
   


<span id="gWLEFKQC"></span>
#### Procedure


1. Log in to[ the Elastic Scheduled Instances console](https://console.byteplus.com/ecs/esi).

2. In the top menu bar, select the Region (where your business is located) and project.

3. Access the batch instance deletion page by any of the following methods:

   * On the order list page, click the "Batch delete" in the actions column of the target order.

   * On the order list page, click the target order name to enter the detail page. Click the "Batch delete" in the upper right corner.

4. In the pop\-up dialog box of batch deletion, confirm instance information.

6. Check "I acknowledge the instances and related resources to be deleted, and understand the associated risks and billing policy". Then, click the "Confirm" to complete the deletion.


</Tab>
<Tab zoneid="Qbf17IBsa0" title="Delete ESI on the instances page">
<TabTitle>Delete ESI on the instances page</TabTitle>

You can filter for all created but not released ESIs on the instances page by billing methods. To delete instance, refer to [Deleting instance](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances).


</Tab>
</Tabs>


<span id=".5pON5L2c57uT5p6c"></span>
## Operation results

After you delete an instance, it enters the **Deleting** status. Shortly afterward, it is deleted and removed from the list.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [DeleteInstance - Deletes an instance](https://docs.byteplus.com/en/docs/ecs/DeleteInstance)

* [DeleteInstances - Deletes one or multiple instances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances)
