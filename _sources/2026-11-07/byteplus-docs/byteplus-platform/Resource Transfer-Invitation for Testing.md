---
title: "Resource Transfer-Invitation for Testing"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
section: "Document"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/Resource_Transfer"
---

<span id="wV5vyXq4"></span>
# **Definition of Resource Transfer**

Resource transfer refers to the process of transferring resource instances (such as Elastic IP Address) purchased on BytePlus from one account to another. This feature is mainly used to transfer resource ownership between different accounts, ensuring business continuity and management flexibility.

<span id="Qu54hCzl"></span>
# **Resource transfer process**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260715054958-973648602495.png) </span>

<span id="bB75dbt5"></span>
# **Applicable Scenarios for Resource Transfer**


1. Applicable Account

   * Personally verified accounts do not support resource transfer.

   * An enterprise\-verified account can only be transferred to another enterprise\-verified account and cannot be transferred to a personal account. 



|**Transfer Initiation Account** |Transfer Receiving Account |**Transfer Rules** |
|---|---|---|
|Enterprise Account |Enterprise Account |The real\-name authentication subject must be the same.  |
|Personal Account |Personal Account |Transfer of ownership is not supported. |
|Personal Account |Enterprise Account |Transfer of ownership is not supported. |
|Enterprise Account |Personal Account |Transfer of ownership is not supported. |



2. Applicable Product

   * **Only some cloud products support the resource transfer function**. Currently supported transferable products: Elastic IP Address, RDS for MySQL.

   * The precautions and restrictions for transferring different products vary. For details, please refer to[ Transferring an EIP](https://docs.byteplus.com/en/docs/eip/Transferring_an_EIP?lang=en)<ins>,</ins> [RDS for MySQL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Transfering_instance). 


&nbsp;

<span id="qnCtE39S"></span>
# Rules of Resource Transfer 


1. Before transfer:

   1. Account Rules:

      * The account initiating the transfer and the account receiving the transfer cannot be the same. 

      * The account initiating the transfer and the account receiving the transfer must both have completed real\-name verification and be enterprise\-verified, and the real\-name verification entities must be the same. 

      * If the transfer initiating account or the transfer receiving account is in the process of cancellation or is blocked, the transfer is not supported. 

      * The account initiating the transfer or the account receiving the transfer is undergoing real\-name authentication change, and transfer is not supported. 

      * The account initiating the transfer or the account receiving the transfer is undergoing a financial cloud relationship change, and the transfer is not allowed. 

      * If either the transfer initiating account or the transfer receiving account is bound to a consignment sales/agency sales relationship, the transfer is not allowed. 

      * Partner accounts do not support transfer of ownership.

      * The account initiating the transfer or the account receiving the transfer has overdue payments, and the transfer is not supported. 

   2. Instance Rules: 

      * Only running instances are allowed for transfer.

      * Transfer is not allowed within 7 days of instance creation or within 72 hours before expiration.

      * Instances with instance binding relationships must be transferred together.

      * The instance is in the process of temporary upgrade, and transfer of ownership is not allowed. 

      * Instances with undelivered orders are not allowed to be transferred.

      * The pay\-as\-you\-go billing model does not support transfer of ownership for preemptible instances and elastic reserved instances. 

      * Resource packs, Reserved Instance Coupons, Reserved Block Storage Capacity Packs, and Savings Plan Instances do not support transfer of ownership. 

      * If there is a change in the consignment sales/agency sales relationship or a change in the signing entity between the currently effective order and the unexpired renewal order of the instance to be transferred, then the transfer is not allowed. 

      * All instances included in a single transfer must have the same region and Available Zone. 

      * If the promotional package discount rule is hit, all instances within the package are not allowed to be transferred. 

   3. Receiving Requirements:

      * After the transfer is initiated but before it is accepted, if the instance has undergone operations such as configuration change or cancellation, resulting in non\-compliance with the above instance transfer rules, acceptance will not be allowed. 

      * If the product configuration of the instance to be transferred is not publicly available for sale, the transfer receiving account must add the relevant purchase permissions before it can receive the instance. 

      * If the instances to be transferred include pay\-as\-you\-go or mixed billing instances, the available balance of the account of the transfer recipient must meet the pre\-order reserve verification for the corresponding product (for example, the available balance of the account must not be less than 100 yuan when opening a cloud server), otherwise the transfer will not be supported. 

2. Transfer in progress:

   1. During the transfer execution process, all instances are prohibited from any operations, including renewal, auto\-renewal, configuration change, cancellation, etc. 

   2. During the transfer execution process, due to the existence of incomplete transactions, changes to financial relationships, including financial custody, financial management, consignment sales, and agency sales, are not supported. 

   3. During the transfer execution process, pay\-as\-you\-go instances will be suspended from use and billing will be paused, and billing will resume after the transfer is completed. 

   4. The system takes approximately 30 to 60 minutes to complete the transfer. 

3. After transfer:

   1. Annual or monthly subscription: The expiration time of the instance remains unchanged, and it is transferred from the initiating account to the receiving account. 

      1. Regarding the account that initiated the transfer: For this transfer instance, orders generated before the transfer will not be refunded and must still be invoiced under the source account.

      2. Regarding the transfer receiving account: After the transfer, the expiration time of the instance remains unchanged, and a 0\-yuan resource transfer order is generated to take over the transferred instance. The transferred instance has no cash value and can only continue to be used. Subsequent new orders for renewal, configuration change, etc., will be paid for and invoiced by the receiving account.

   2. Pay\-as\-you\-go instances: Billing resumes after the transfer is completed. 

      1. Regarding the account that initiates the transfer: The fees before the transfer is completed shall be borne by the initiating account, billed under the initiating account, and invoices must be issued under the initiating account.

      2. Regarding the account receiving the transfer: After the transfer is completed, the expenses will be borne by the receiving account, billed under the receiving account, and invoices must be issued under the receiving account.

   3. After the instance transfer, subsequent billing will be based on the business discounts of the receiving account. 

   4. If the transferred instance supports 7\-day no\-questions\-asked unsubscribe, it will no longer be eligible for 7\-day no\-questions\-asked unsubscribe after the transfer. 

   5. Explanation of Unsubscription and Downgrading after Transfer: For unsubscription or downgrading of transferred instances, the remaining value of the instance is always 0. If the instance has been renewed and then unsubscribed, only the remaining value of the renewed portion can be refunded; if the instance has been upgraded and then downgraded, only the remaining value of the upgraded portion can be refunded.


<span id="gmhf0NUZ"></span>
# Notice on Risks of Resource Transfer


* The transfer operation only involves changing the information of the user to whom it belongs, while other information remains unchanged, such as expiration time, renewal type, etc. 

* After the transfer, the source account will no longer be able to use the resources. If there are dependencies between the transferred instance and non\-transferred resources,  ** please ensure that the relevant dependencies are removed before the transfer **  to avoid affecting other services under the original account after the transfer. 

* Before transferring resources, please ensure that you have carefully read the[ Transferring an EIP](https://docs.byteplus.com/en/docs/eip/Transferring_an_EIP?lang=en)<ins>,</ins> [RDS for MySQL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Transfering_instance). , and understand the precautions for instance transfer and the risks that may arise after the transfer.

* If you perform risk operations such as modification or change on instances or data, you must pay attention to the disaster recovery and fault tolerance capabilities of the instances to ensure data security. 

* If you plan to configure or modify data for instances, it is recommended to create a snapshot in advance. 


<span id="KJvCEMQG"></span>
# **Resource Transfer Operation Instructions**


1. Initiate transfer: The initiating account logs in to BytePlus, enters the  ** billing center **  \> [ resource transfer ](https://console.volcengine.com/finance/resource-transfer) page. Under the transferable page,  ** select the region **  and the transferable instances in that region (supports batch selection). Click Initiate Transfer or Batch Transfer to execute the transfer initiation process. 

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260710110230-718259331284.png) </span>

2. Fill in the transfer information: In the **transfer receiving account ** area, fill in the transfer recipient account information, sign the BytePlus transfer agreement, and click "Transfer". 

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7ba05c1a17e0ebeb504ff3ca25747885.png) </span>



&nbsp;

3. Security Verification: Perform MFA device verification, and after the verification passes, the transfer application form will be created successfully.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2088a3595bc38e6770e356c8e363fb30.png) </span>

4. Transfer Initiation Completed: After initiating the transfer, you can view the transfer application form in the [Resource transfers I initiated](https://console.byteplus.com/finance/resource-transfer?tab=2). Within 24 hours after initiation and before the receiving account confirms, you can cancel the transfer.


<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1ecf81d6810c7f43aad8304274b5f33e.png" width="3366px" /></div>



5. Receive transfer: Log in to BytePlus with the receiving account, enter the **billing center** \> [Resource Transfer](https://console.byteplus.com/finance/resource-transfer) page. Under the **Resource Transfers I Received** page, view the transfer application forms awaiting receipt. Click "Confirm Receipt of Transfer" to execute the transfer receipt process. Within 24 hours after initiation and before receipt confirmation, you can also **reject the transfer**.

   <div style="text-align: center">
   <img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_971c422dd5d580cc114123f298caa048.png" width="3394px" />   </div>
   

6. Fill in the acceptance information: Click to view details or confirm acceptance of the transfer, enter the transfer details page, fill in the acceptance information and sign the BytePlus Transfer Agreement, then click “**Accept**”.


<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_82aa3dacb7f23b79123af1633d731f15.png" width="3504px" /></div>



7. Security Verification: Perform MFA device verification. After the verification passes, you will enter the transfer execution phase, which is expected to take about 30 to 60 minutes to complete the transfer.

8. View transfer results: You can view the status of transfer application forms and learn about transfer results on the **Resource Transfers I Initiated / I Confirmed ** page.
