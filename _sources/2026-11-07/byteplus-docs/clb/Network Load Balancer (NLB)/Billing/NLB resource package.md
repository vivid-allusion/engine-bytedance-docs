---
title: "NLB resource package"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLBPackages"
---

<span id="oHsBdqbC"></span>
## Introduction​

The Network Load Balancer (NLB) resource package is a pre\-paid bundle of LCUs designed to deduct both the LCU fees and instance fees for Pay\-by\-CU NLB instances, enabling more cost management.

<span id="EUqX0uwn"></span>
## **Billing**


* **Specification and prices**

   
   |Specification |LCU quantity |Price (USD) |
   |---|---|---|
   |Small I |5000 LCU |24.5 |
   |Small II |10000 LCU |49 |
   |Medium |50000 LCU |240 |
   |Large |100000 LCU |475 |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can use the <a href="https://www.byteplus.com/en/pricing?product=NLB&tab=2">price calculator</a> to view the unit price of NLB resource packages. These prices are for reference only; actual fees are subject to the console.   </div>
   

* **Unsubscription**

   The NLB resource package only supports a 7\-day unconditional refund, with the following limits:

   * No deductions occurred.

   * Each account is eligible for a maximum of 10 unconditional NLB resource package refunds per calendar year.

   See Unsubscribing NLB resource package actions.

* **Time elapsed since expiration**

   1 year (non\-calendar year). For example, purchased on May 5, 2025, expires on May 4, 2026 at 23:59:59.


NLB resource packages will automatically reset to zero after expiration if not fully deducted, without affecting NLB service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For NLB resource packages that are not fully deducted, the platform will send expiration reminder messages 7 days, 3 days, 1 day, and on the day of expiration via SMS, email, or internal message based on the notification methodnotification method you set. Please pay attention.</div>


<span id="fYtxssC4"></span>
## Offsetting

All NLB instances under the same account and in the same zone use the same NLB resource package for deductions until it is depleted. Afterward, the next available NLB resource package will be used. If no NLB resource package is available, the undeducted portion will be charged Pay\-by\-CU.


* Zone and Region

   NLB resource packages from different zones can deduct fees for NLB instances in different regions, as shown in the table below:

   
   |Zone (NLB resource package) |Deductible region (NLB instance) |
   |---|---|
   |Mainland China |China (Beijing), China (Shanghai), China (Guangzhou) |
   |Regions outside Mainland China |China (Hong Kong), Asia Pacific (Johor) |
   

* **Effective period**

   When purchasing, you can configure it to take effect immediately or specify an effective time within six months.

* **Deduction rules**

   
   |Fee |Offsetting |
   |---|---|
   |Instance fee |The deduction ratio is 4:1, which means four LCUs offset the Instance Fee for one hour of one NLB instance. |
   |LCU Fee |The deduction ratio is 1:1, which means one LCU offsets one LCU that is actually consumed by an NLB instance. |
   |Internet fee |Not applicable for deduction. It is recommended to add Elastic IP (EIP) and IPv6 internet bandwidth to the Shared Bandwidth Package. |
   

* **Deduction order**

   In terms of billing items, instance fees and LCU fees have the same priority level.

   If there are multiple NLB resource packages, the deduction order rules are as follows:

   1. Expiration time first: Priority is given to deducting from NLB resource packages with an earlier expiration time.

   2. Effective time first: If multiple NLB resource packages have the same expiration time, priority is given to deducting from resource packages with an earlier effective time.


<span id="pV9LgRnq"></span>
## Actions

<span id="okRA6tad"></span>
### Purchase NLB resource package


1. Log in to the NLB resource package console.

2. Click Purchase package.

   
   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Regions |Select region for NLB instance fee deduction coverage:<br><br><br>* Mainland China<br><br>* Regions outside Mainland China |Mainland China |
   |Package specification |Select resource package specification. |10000 LCU |
   |Purchase quantity |Enter the quantity of resource packages to purchase. |1 |
   |Effective period |Select the effective time.<br><br><br>* Immediate activation<br><br>* Scheduled activation (within next 6 months) |Instant effect |
   |Validity period |Fixed duration is 1 year. |1 year |
   

3. Follow the console guidance to review and accept the Legal.

4. Click **Agree and Buy** to complete the action.


<span id="iuAeUzDu"></span>
### Unsubscribe NLB resource package


1. Log in to the NLB resource package console.

2. Click Unsubscribe to the right of the target NLB resource package.

3. Click **OK** to complete the action.


<span id="X9y7rsfL"></span>
### **View deduction details**


1. Log in to the NLB resource package console.

2. Click Detailed deduction on the right side of the target NLB resource package to complete the action.


<span id="yIVtCAVe"></span>
### Set the remaining balance alert

Please go to the Billing Center to configure threshold alerts. For actions, see Setting up the threshold alert.

<span id="3cI55ZsT"></span>
## FAQs

See FAQs for NLB resource packages.

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
