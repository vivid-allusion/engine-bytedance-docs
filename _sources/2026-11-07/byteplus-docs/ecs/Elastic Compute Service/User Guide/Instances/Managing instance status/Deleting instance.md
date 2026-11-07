---
title: "Deleting instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

  This topic describes how to delete ECS instances in the ECS console.

<span id=".5Yig6Zmk5ZCO5a6e5L6L55u45YWz6LWE5rqQ5oOF5Ya1"></span>
## Precautions


* After Pay\-as\-you\-go instances and their associated resources are deleted, billing stops. [Why is a deleted instance still being billed?](https://docs.byteplus.com/en/docs/ecs/Billing-FAQs#.5Li65LuA5LmI5a6e5L6L5bey57uP5Yig6Zmk77yM5L2G5LuN54S25Zyo6K6h6LS577yf)

* Subscription instances cannot be deleted before they [expire](https://docs.byteplus.com/en/docs/ecs/Expiration) or are [unsubscribed](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription#.6YCA6K6i6K-05piO). You can convert the instance to a Pay\-as\-you\-go instance and manually delete it, or manually delete it within the resource retention period after the instance expires or is unsubscribed. After an instance expires or is unsubscribed, it will also be automatically released if not renewed.

* ECS instances with deletion protection enabled can not be deleted manually through the console or API. You can refer to [Instance deletion protection](https://docs.byteplus.com/en/docs/ecs/Instance_delete_protection), disable this feature, and then proceed with the deletion action.

* Instance deletion is a sensitive operation. The root user or IAM users with the AdministratorAccess permission can configure deletion protection. After the setting, when deleting an instance, secondary verification is required. This involves using the security phone, security email, or MFA device associated with the login account according to the protection rules. The deletion operation will only be executed after the verification. Once the sensitive operation protection is enabled, it can not be disabled. [Learn more](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances?TagIDs=2,70,69,87#I2OF1kMx).


<span id="cw0s9mJQ"></span>
## Resource status after permanent deletion of the instance

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you delete an ESI, do not modify any associated resources. Otherwise, instance or resource deletion may fail.</div>



<Tabs>
<Tab zoneid="P0BOlev6ZL" title="Pay-as-you-go instance">
<TabTitle>Pay-as-you-go instance</TabTitle>


|Resources |Situation after you delete the ESI |
|---|---|
|System volume/local volume |When the instance is released, data is automatically cleared and can not be recovered. Please [back up your data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) at system volume/local volume in advance. |
|Image |The images used during instance purchase and the custom images created from the instance are still retained. |
|Data volume |Specify whether to delete the data volume with the ECS instance on demand:<br><br><br>* If you select this option, data volume is released with instance upon deletion and can not be recovered. Please [back up your data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) at data volume in advance.<br><br>* If you have not selected this option, the data volume is unmounted from instance but not released. By default, data in the volume is retained, and the **billing for the data volume continues**. You can still mount the data volume to another instance.<br><br><br>> If you set "Delete with instance" for the data volume when you create the instance, "Delete with instance" is checked for the data volume by default on the instance deletion page. You can uncheck the check\-box to not release the data volume with the instance, and vice versa. |
|Primary network interface |Automatically released with the ECS instance. |
|Secondary network interfaces |Whether the network interface is set to be deleted when the ECS instance is unsubscribed:<br><br><br>* If yes, the secondary network interface is deleted together with the ECS instance.<br><br>* If not, the secondary network interface is unmounted from the ECS instance. You can mount it to another ECS instance. |
|Elastic IP (EIP) |* Specify whether to delete the EIP of the primary network interface together with the ECS instance.<br><br>   * If you select this option, the EIP is released together with instance when you delete instance.<br><br>   * If not, it is disassociated from the instance, not automatically released, and the **billing continues**. You can still associate the EIP with another instance.<br><br>* The EIP associated with the secondary network interface is disassociated from the instance, not automatically released, and the **billing continues**. You can still associate the EIP with another instance. |





</Tab>
<Tab zoneid="gup2E2PdRk" title="Subscription-based instances">
<TabTitle>Subscription-based instances</TabTitle>


|Resources |Situation after you delete the ESI |
|---|---|
|System volume/local volume |When the instance is released, data is automatically cleared and can not be recovered. Please [back up your data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) at system volume/local volume in advance. |
|Image |The images used when purchasing instances and the custom images created through instances will still be retained. |
|Data volume |Specify whether to delete the data volume with the ECS instance on demand:<br><br><br>* If you select this option, data volume is released with instance upon deletion and can not be recovered. Please [back up your data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) at data volume in advance.<br><br>* If you have not selected this option, the data volume is unmounted from instance but not released. By default, data in the volume is retained, and the **billing continues**. You can still mount the data volume to another instance.<br><br><br>> If you set "Delete with instance" for the data volume when you create the instance, "Delete with instance" is checked for the data volume by default on the instance deletion page. You can uncheck the check\-box to not release the data volume with the instance, and vice versa. |
|Primary network interfaces |Automatically released with the ECS instance. |
|Secondary network interface |Whether the network interface is set to be deleted when the ECS instance is unsubscribed:<br><br><br>* If yes, it is automatically deleted along with the ECS instance.<br><br>* If not, the secondary network interface is unmounted from the ECS instance. You can mount it to another ECS instance. |
|EIP |* Specify whether to delete the EIP of the primary network interface together with the ECS instance.<br><br>   * If you select this option, the EIP is released together with instance when you delete instance.<br><br>   * If not, it is disassociated from the instance, not automatically released, and the **billing continues**. You can still associate the EIP with another instance.<br><br>* The EIP associated with the secondary network interface is disassociated from the instance, not automatically released, and the **billing continues**. You can still associate the EIP with another instance. |





</Tab>
</Tabs>


<span id="I2OF1kMx"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project where the target instance resides.

4. In the instance list, find the ECS instance that you want to delete and choose "··· \> Instance state \> Delete instance" in the "Actions" column.

5. In the pop\-up dialog box, confirm the instance name/ID, and select whether to delete the data volume or public network IP associated with the instance. Checking the box indicates the deletion of relevant resources.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The system volume will be deleted along with the ECS instance. It is checked by default and can not be changed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The EIP displayed on this page is the EIP bound to the primary network interface. The EIP bound to the secondary network interface will be unbound from the instance after the instance is deleted and will not be automatically released.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also check "Delete the volumes associated with all selected instances" or "Delete the EIPs associated with all selected instances". If you select them, the system will delete all the volumes or EIPs associated with all target instances. Please operate with caution.   </div>
   

6. After you confirm the operation, check the "I am aware of the Instances and related resources that are about to be deleted and understand the associated risks" check\-box.

7. Click the "Delete" button, perform secondary verification in the pop\-up dialog box, and then click the "Confirm" button to complete the deletion operation.

   * Support multiple verification methods (phone, email, MFA device). If you need to modify, please go to [Security settings - Sensitive Operations Protection](https://console.byteplus.com/user/security/) to make changes.

   * IAM users can modify the verification method and operation protection rules only after being granted the AdministratorAccess permission by the root user. 

   * If the verification method is unavailable (For example, phone number is invalid), you can click the "Submit Appeal" button at the bottom of the page, or directly modify the verification phone number or email. MFA devices require you to go to [Security settings - MFA device](https://console.byteplus.com/user/security/) for binding/disassociating.


<span id="7k1E2zZ3"></span>
## Result

After you delete an instance, it enters the Deleting status. Shortly afterward, it is deleted and removed from the list.

<span id=".5Yig6Zmk5ZCO5a6e5L6L55u45YWz6LWE5rqQ5oOF5Ya1"></span>
## Related document


* [DeleteInstance - Deletes an instance](https://docs.byteplus.com/en/docs/ecs/DeleteInstance)

* [DeleteInstances - Deletes one or multiple instances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances)


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQs


* [How to view information of deleted instances?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5aaC5L2V5p-l55yL5bey5Yig6Zmk5a6e5L6L55qE5L-h5oGv77yf)

* [Can I delete subscription instances?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5YyF5bm05YyF5pyI5a6e5L6L5pSv5oyB5Yig6Zmk5pON5L2c5ZCX77yf)

* [Can I recover deleted instances?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5a6e5L6L5Yig6Zmk5ZCO5Y-v5Lul5oGi5aSN5ZCX77yf)


&nbsp;
