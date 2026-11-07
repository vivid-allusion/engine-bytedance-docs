---
title: "Overdue payments"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Overdue_payments"
---

When the user stops the EMR Serverless service due to system arrears and other reasons, the system will prompt you to renew the fee, which is described in detail in this paragraph.

Service shutdown in EMR Serverless is divided into two ways, namely **billing\-arrears shutdown** and **Subscription\-instance expiration shutdown** . The system will determine which shutdown method should be used based on the instances purchased by the user and the status of all instances.

<span id="16253bcb"></span>
## Life cycle

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/580d054a43b34d1ca60ab7cec51deab1~tplv-goo7wpa0wc-image.image) </span>

<span id="18cdd5d8"></span>
## **Pay\-As\-You\-Go**

The system **only exists Pay\-As\-You\-Go instances** (such as public queues, Pay\-As\-You\-Go instances, storage, postpaid parts of elastic exclusive queues).

**Pay\-As\-You\-Go instance is suspended due to arrears**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The service is shut down to the Min value of each resource, for example: in the billing mode, the actual delay is 2 hours, and the EMR Serverless service is not available.</div>



|resource type |Enter arrears |After n hours, the service is shut down |After n hours, the service is recycled |
|---|---|---|---|
|computing resources |—— |2 hours |7 \* 24 = 168 hours (no charge during the period) |



* If the arrears (account balance is negative) are not made up after 2 hours, the service will be shut down. During the service shutdown, storage resources are still billed and billed normally. After recharging or offline remittance, the service can be restored when the account balance is non\-negative.

* If all arrears are not made up 7 \* 24 hours after the arrears, they will enter the recovery state, release all resources of EMR Serverless, and the service will not be available. The released resources cannot be restored, and they can only be used normally after making up the arrears and reopening.


<span id="71914733"></span>
## **Subscription**

<span id="8b4e2491"></span>
### Fixed Resources

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The service is shut down to the Min value of each resource, for example, in Subscription mode, the resource expires for 12 hours, and the EMR Serverless service is unavailable.</div>



|Resource type |Shutdown due |Arrears recovery |Expiration shutdown |Recycling at maturity |
|---|---|---|---|---|
|computing resources |—— |—— |12 hours |15 \* 24 = 360 hours<br><br>(No charge during the period) |



* After the subscription instance expires, if the renewal is not completed within 12 hours, the service will be shut down. If the renewal is not completed 15 \* 24 hours after the shutdown, it will enter the recovery state, release all resources of EMR Serverless, and the service will not be available. The released resources cannot be restored, and they can only be used normally after making up the arrears and reopening.

* After the instance expires and before resource recovery, the instance can be restored and the instance valid period can be extended through automatic/manual renewal and additional purchase.

* The user's account is in arrears due to the use of storage resources billed by the amount (or other services of the Byteplus platform), and the Subscription computing resources that are still in the valid period cannot be used normally. You need to recharge to restore the normal use of the service.


<span id="bf5d6b16"></span>
### Elastic Resources \*\*\*\*

Attention

The service is shut down to the Min value of each resource, for example, in Elastic Subscription mode, the actual delay is 2 hours, and the EMR Serverless queue service is not available.


|Resource type |Shutdown due |Arrears recovery |Expiration shutdown |Recycling at maturity |
|---|---|---|---|---|
|Computing Resources \- Elastic Section |2 hours |7 \* 24 = 168 hours<br><br>(No charge during the period) |—— |—— |
|computing resources |—— |—— |12 hours |15 \* 24 = 360 hours<br><br>(No charge during the period) |



* Computing resources \- flexible part, if the arrears are not made up after 2 hours, the service will be shut down. If all arrears are not made up 7 \* 24 hours after the arrears, they will enter the recovery state, release the EMR Serverless queue, and all resources and services will be unavailable. The released resources cannot be restored, and they can only be used normally after making up the arrears and reopening.

* After the subscription instance expires, if the renewal is not completed within 12 hours, the service will be shut down. If the renewal is not completed 15 \* 24 hours after the shutdown, it will enter the recovery state, release the EMR Serverless queue, and all resources and services will be unavailable. The released resources cannot be restored, and they can only be used normally after making up the arrears and reopening.

* After the instance expires and before resource recovery, the instance can be restored and the instance valid period can be extended through automatic/manual renewal and additional purchase.

* The user's account is in arrears due to the use of storage resources billed by the amount (or other services of the Byteplus platform), and the Subscription computing resources that are still in the valid period cannot be used normally. You need to recharge to restore the normal use of the service.


<span id="ee8ce47b"></span>
## Recovery rules

If your service meets the conditions for **expiration discontinuation** , the EMR Serverless console will prompt you to renew the purchase.

At this time, you can click **Renew** to enter the exclusive queue to renew the purchase page. After the renewal and payment are completed, return to this page and click the **Refresh** button to restore the service. There may be a delay of a few seconds from the completion of payment to recovery.
