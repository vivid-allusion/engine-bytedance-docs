---
title: "Billing changes"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Billing-05"
---

Changing instance specifications or related configurations based on business needs will result in billing changes.

<span id=".5Y-Y5pu05a6e5L6L6KeE5qC8"></span>
## Change CLB instance

<span id="wSjXWNjs"></span>
### Change CLB instance specification


* Upgrading specifications does not affect business operations but increases costs.

* If the specification after a downgrade is insufficient for your running services, it will impact them. Please proceed with caution.



|Billing method |What changed |Fee description |
|---|---|---|
|Subscription |Effective immediately; billing starts at the new specification from the moment of change. For detailed steps, see [Changing the instance type](https://docs.byteplus.com/en/docs/clb/CLB-instances-03). |For detailed calculation rules for configuration change fees, see [Changing Annual or Monthly Subscription Resource Specifications](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change#.5LiA44CB5Y-Y5pu05YyF5bm05YyF5pyI6LWE5rqQ6KeE5qC8). |
|Pay\-as\-you\-go |Effective immediately; billing starts at the new specification from the moment of change. For detailed steps, see [Changing the instance type](https://docs.byteplus.com/en/docs/clb/CLB-instances-03). |Within the billing cycle, the fee is the sum of the fee before the change and the fee after the change. |


<span id="yPwqZXJv"></span>
### Change metering methods

Two billing conversion methods are supported. 

**Convert from Pay\-as\-you\-go to Subscription**


* The public CLB instance and its associated Elastic IP Address (EIP) are converted to Subscription. Subscription fees for both the CLB instance and its associated EIP need to be paid.

* When converting a private CLB instance to Subscription, the metering method of its associated EIP is not affected. Only the Subscription fee for the CLB instance needs to be paid.


**Convert to Subscription to Pay\-as\-you\-go**


* The public CLB instance and its associated EIP are both switched to Pay\-as\-you\-go billing. The CLB instance uses **Pay\-as\-you\-go\-(Pay by specification)** , and the EIP uses **Pay\-by\-bandwidth**.

* A private CLB instance is converted to Pay\-as\-you\-go\-(Pay by Specification), and the metering methods of its associated EIP remain unchanged.


The system will refund the remaining value of the actual amount paid for the subscription order. 

<span id="ob758DGx"></span>
## Edit EIP configuration

<span id="sJu7cufI"></span>
### **Public** ** CLB**


* Changing the public network configuration of a public CLB instance will cause changes to the CLB public network fees. Depending on the billing type and the information modified, the billing changes after modifying the public network configuration of a public CLB instance are shown in the table below.

   
   |Billing method |Limits |Add to Bandwidth Package |Billing description |Procedure reference |
   |---|---|---|---|---|
   |Subscription |Only supports modifying the bandwidth upper limit, including upgrades and downgrades. |Subscription does not support joining a Bandwidth Package |Takes effect immediately. From the moment of change, public network fees are charged according to the new bandwidth upper limit. |* [Modifying an internet bandwidth limit](https://docs.byteplus.com/en/docs/clb/CLB-instances-06)<br><br>* [Changing the billing method - Elastic IP Address](https://docs.byteplus.com/en/docs/6406/95294) |
   |Pay\-as\-you\-go |Supports modifying the bandwidth upper limit and billing method. Modifying the bandwidth upper limit supports upgrades and downgrades. |Yes |Not effective immediately. Public network fees will be charged according to the new bandwidth upper limit and billing method only after the EIP is removed from the Bandwidth Package. ||
   |||No |Takes effect immediately. From the moment of change, public network fees are charged according to the new bandwidth upper limit and billing method. ||
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the table above, upgrade means increasing the bandwidth upper limit, and downgrade means decreasing the bandwidth upper limit. Downgrades may involve a refund; the actual situation is subject to the console.   </div>
   

* Adding or removing the EIP of a public CLB instance from a Bandwidth Package will cause changes to CLB fees, as described below:

   * Add to Bandwidth Package: Takes effect immediately. From the moment of change, public network fees are no longer charged separately but are collected uniformly by the Bandwidth Package. For detailed billing instructions, see [Bandwidth Package Billing overview](https://docs.byteplus.com/en/docs/bandwidthpackage/Billing-overview).

   * Remove from Bandwidth Package: Takes effect immediately. From the moment of change, public network fees are charged separately again, and the billing information is based on the latest public network configuration before leaving the Bandwidth Package.


<span id="pCDmITIa"></span>
### Private CLB


|**Actions** |**CLB fee impact** |**Other fee changes** |**Documentation** |
|---|---|---|---|
|Change public network configuration  |No impact |EIP fee |[EIP Billing](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go#.5YWx5Lqr5bim5a695YyF6K6h6LS56K-05piO), [ElP Specification changes](https://docs.byteplus.com/en/docs/eip/Bandwidth-modifications) |
|Modify IPv6 internet bandwidth configuration |No impact |IPv6 gateway fee |[IPv6 gateway specification changes](https://docs.byteplus.com/en/docs/IPv6/Bandwidth_modifications) |
|Attach / Detach EIP |No impact |Internet fee |[EIP Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview) |


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
