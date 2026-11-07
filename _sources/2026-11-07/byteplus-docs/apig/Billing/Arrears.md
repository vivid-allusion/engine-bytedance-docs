---
title: "Arrears"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Arrears"
---

If your account does not have sufficient balance to pay for a bill, your resources will enter the service suspension state due to arrears. This topic describes the service suspension state due to arrears and relevant instructions.

<span id="arrears-cause"></span>
## Arrears cause

API gateway performs settlement every hour and the expense is deducted in real time after a bill is generated. If the available quota of your account (including the account balance and cash coupons) is less than that in the settlement bill, you will enter the arrears state and receive an SMS or email notification for insufficient balance.

<span id="arrears-notification"></span>
## Arrears notification

After your account enters into arrears, the system sends an arrears notification through email, SMS, or internal message. Process the issue and recharge your account after receiving the notification.

<span id="service-suspension-due-to-arrears"></span>
## Service suspension due to arrears

If your account is in arrears for **2 hours**, your resources will enter the **service suspension due to arrears** state, and resource usage will be limited. After the resource retention period is due, your resources will be reclaimed forcibly. Reclaimed resources cannot be recovered. To ensure normal use of the VMP service, recharge your account and settle your overdue payments within the specified period (before forced resource reclaim).

After overdue payments are settled, the instance in the service suspension state due to arrears is started automatically and enters the **running** state.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You have to pay for the billed fees regardless of whether your instance resources are frozen or released.</div>


The following figure shows the billing and arrears states of VMP.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_15d9d90aaa0482d140a352e5dfd62d57.png) </span>

<span id="reclamation-due-to-arrears"></span>
## Reclamation due to arrears

When your account remains in the arrears state for 15 days and 2 hours (362 hours), your resources will enter the **reclaimed due to arrears** state, and relevant instances and the data stored on them will be deleted.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">If you do not recharge your account after it is in arrears for 362 hours, the system will forcibly release instances and delete all the data of these instances. The deleted data cannot be recovered.</div>
