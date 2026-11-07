---
title: "Transferring an EIP"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Transferring_an_EIP"
---

When your organization structure changes or you plan to migrate your business, you can use the resource transfer feature to transfer Pay\-as\-you\-go Elastic IP Address (EIP) instances to another account.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">The EIP transfer feature is currently in invite\-only beta. To request access, please contact your account manager to apply.</div>


<span id="PBRjbJTE"></span>
## **Related terms**


|Term |Description |
|---|---|
|Resource transfer |Resource transfer refers to the process of transferring purchased cloud resource instances (such as Elastic Compute Service instances and EIPs) from one account to another. Through resource transfer, you can change resource ownership between accounts while ensuring business continuity and management flexibility. |
|Source account |Account applying for resource transfer. The instance is removed from the source account upon successful transfer. |
|Destination account |Account receiving the transferred resource. After a successful transfer, the destination account becomes the owner of the resource and is responsible for all subsequent charges. |
|Transferring |Refers to the status of an EIP instance that is currently in the transfer process. After the source account applies for a resource transfer, the relevant instance enters the **Transferring** status until the transfer is completed or terminated. |


<span id="BNykAfpd"></span>
## Limits

<span id="WRVLTj2j"></span>
### **Account limits**

Both source and destination accounts for resource transfer are subject to limits. For details, see [Resource transfer description](https://docs.byteplus.com/en/docs/byteplus-platform/Resource_Transfer).

<span id="5OhpvODa"></span>
### EIP instance limits


|EIP |Limit description |Related actions |
|---|---|---|
|Instance type |* IPv6 EIPs are not supported for transfer.<br><br>* EIPs belonging to the IP address pool are not supported for transfer.<br><br>* EIPs with enhanced protection are not supported for transfer. |[Create an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP) |
|Instance status |* The EIP must have been created for more than 7 days.<br><br>* The EIP cannot be **bound to an active cloud resource** or **added to a Bandwidth Package.** <br><br>* The EIP must not be in **arrears**, **banned**, **locked**, **frozen**, or **unavailable** status.<br><br>* No unpaid, incomplete, or unactivated orders (e.g., billing conversion, temporary upgrade) can exist for the EIP. Cancel any such orders before transferring. |* [Disassociate a cloud resource](https://docs.byteplus.com/en/docs/eip/Disassociating-Cloud-Resource-from-an-EIP)<br><br>* [Remove from a Bandwidth Package](https://docs.byteplus.com/en/docs/eip/Removing-an-EIP-address-from-a-bandwidth-package)<br><br>* [Renew](https://docs.byteplus.com/en/docs/eip/Renewal) |
|Metering method |Only Pay\-as\-you\-go EIPs are transferrable.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">To transfer a Subscription EIP, convert the EIP's metering method to Pay\-as\-you\-go before transferring.</div><br> |[Billing conversion](https://docs.byteplus.com/en/docs/eip/Billing-methods-change) |
|Quota limit |The total number of EIP instances under the destination account must not exceed the account's EIP quota. **If the quota is insufficient for transfer, apply for sufficient quota in advance**. |[Quota limits](https://docs.byteplus.com/en/docs/eip/Limits#.6YWN6aKd6ZmQ5Yi2) |
|Region |Only EIPs within the same region are transferable. |\- |
|Other limits |An EIP can be transferred only once within a 6\-month period. The instance ID remains the same before and after the transfer. |\- |


<span id="kQawBr3i"></span>
## Instructions


* EIP instances in the **transferring** state cannot be modified, deleted, or have actions such as associating/disassociating cloud resources, upgrading/downgrading, changing billing methods, or releasing performed on them.

* Once an EIP transfer is completed, it cannot be rolled back. Proceed with caution. After transfer:

   * The EIP instance remains its original basic configuration, including instance ID, ISP, metering method, maximum bandwidth, instance name, and other settings.

   * EIP beta capabilities already enabled in the source account do not migrate with the resource transfer. To enable more EIP features (such as EIP Direct) in the destination account, please [submit a ticket](https://console.byteplus.com/workorder/create) or contact customer service support.

   * The EIP instance will be removed from the source account's projects and tag groups. You must reconfigure the associations between the project, tags, and the instance in the destination account.


<span id="AxEHuuzH"></span>
## Procedure

For procedure, see [Resource transfer instructions](https://docs.byteplus.com/en/docs/byteplus-platform/Resource_Transfer).

&nbsp;

&nbsp;
