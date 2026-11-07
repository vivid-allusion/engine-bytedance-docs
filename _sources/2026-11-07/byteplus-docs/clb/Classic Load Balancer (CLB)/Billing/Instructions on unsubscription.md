---
title: "Instructions on unsubscription"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Billing-10"
---

This section describes the unsubscribe feature of yearly/monthly subscription CLB instances.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the following description, <strong>CLB instances</strong> refer to yearly/monthly subscription CLB instances.</div>


<span id=".6YCA6K6i5LuL57uN"></span>
## Introduction to the unsubscribe feature

The unsubscribe operation is supported before a CLB instance is stopped. If the instance is no longer needed due to business changes, you can choose to unsubscribe from the instance, and the instance resources will be automatically deleted after unsubscribing.


* When you unsubscribe from a public CLB instance, its associated EIP is simultaneously unsubscribed. You cannot unsubscribe from the associated EIP separately.

* When you unsubscribe from a private CLB instance that is already bound to an EIP, the bound EIP is automatically unbound but not unsubscribed.

* When you unsubscribe from a private CLB instance that is not bound to an EIP, the operation does not involve any EIP.


After a CLB instance expires and is stopped, it cannot be unsubscribed. You can manually delete and release the instance. For more information about the operation, refer to [Deleting a CLB instance](https://docs.byteplus.com/en/docs/clb/CLB-instances-09).

CLB instances support both 7\-Day No Fault Return and Non 7\-Day No Fault Return.


|Unsubscription type |7\-Day No Fault Return |Non 7\-Day No Fault Return |
|---|---|---|
|Unsubscription Rules |Only one CLB instance can be unsubscribed from with 7\-Day No Fault Return within a calendar year.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The number of public CLB instances unsubscribed by 7\-Day No Fault Return is included in the number of EIP instances unsubscribed by 7\-Day No Fault Return. If an EIP instance has been unsubscribed within a calendar year, a public CLB instance cannot be unsubscribed by "7\-Day No Fault Return."</div><br> |* After a CLB instance is Suspended, it no longer supports Unsubscribe.<br><br>* CLB instances that support Non 7\-Day No Fault Return do not support 7\-Day No Fault Return. |
|Refund instructions |The actual amount paid (cash only) is refunded to the account balance, and cash coupons are not refunded. |The residual value of the actual amount paid of the order is refunded, and used cash coupons cannot be refunded. |
