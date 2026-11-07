---
title: "Billing information for exclusive resource groups"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Billing_Instructions_for_Exclusive_Resource_Groups"
---

DataLeap currently offers four types of exclusive resource groups: **Exclusive Scheduling Resource Group**, **Exclusive Computing Resource Group**, and **DataSail Exclusive Integration Resource Group**. All Exclusive resource groups are billed on a yearly or monthly subscription basis.

This document provides billing information for each Exclusive resource group.

<span id="_2-独享资源组"></span>
## Overview of an exclusive resource group


* DataLeap provides Exclusive Scheduling Resource Group, Exclusive Computing Resource Group, and Exclusive Data Service Resource Group. The billing method is a pre\-paid model, available as annual or monthly subscriptions. The different types of resource groups are described as follows:

   
   |Resource group types |Note |
   |---|---|
   |Exclusive Scheduling Resource Group |Exclusive scheduling resource groups are applicable to all **offline tasks** in DataLeap, except for temporary query tasks.<br><br>When offline tasks experience high concurrency and cannot be scheduled at off\-peak times, the public scheduling resource group can no longer meet your business requirements. In this case, you need exclusive scheduling resources to ensure that tasks are dispatched and executed on schedule, and to avoid tasks failing to run on time due to resource constraints. |
   |Exclusive Computing Resource Group |When Notebook, Python, and Shell tasks under a project are running at high concurrency and cannot be scheduled to avoid peak times, enterprises need **Exclusive compute resource groups** to ensure continuous and rapid data computation and output. |
   |Exclusive Data Service Resource Group |This is used when calling the API of the data service module, and the Exclusive data service resource group is not subject to call limits. Different resource group specifications support different numbers of requests per second. You can select the appropriate specification based on the usage in your current production environment. |
   


<span id="cd194a5c"></span>
## Exclusive integrated resource groups

<span id="f95559b3"></span>
### Performance metrics for Exclusive integrated resource groups

An Exclusive integrated resource group with 1 CU (1 vCPU/4 GiB) supports 1 concurrent thread.

Offline data integration tasks:


* Users can customize the number of concurrent threads, with a minimum of 1 CU.

* A 1 CU resource can transfer approximately 24 GiB of data per hour.


Real\-time data integration tasks:


* Users can customize the number of concurrent threads in **Parameter Settings**, with a minimum allocation of 1 CU.

* With 1 CU resource, the amount of data that can be transferred in 1 hour is approximately 18 GiB.


<span id="cdda2fe5"></span>
### Billing cycles and pricing for Exclusive integration resource groups

The Exclusive integrated resource group with a 1 CU specification is priced at $31/month. The minimum specification available for sale is 4 CUs. If you need to purchase additional resources, you can increase the number of resource groups you purchase by multiples of four. For example, 8 CUs, 16 CUs, and so on.

Exclusive integrated resource group purchase. See: [Exclusive Integrated Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_integrated_resource_group).

<span id="7a430b0a"></span>
## Exclusive compute resource groups

The Exclusive computing resource group with a 1 CU specification is priced at $40/month. The minimum specification available for sale is 4C/16GiB. If you need to purchase additional resources, you can increase the number of resource groups with the same specifications or purchase resource groups with larger specifications.


|Region |Specifications |Unit price |
|---|---|---|
|* Johor |4 vCPU 16 GiB |$160/month |
||8 vCPU 32 GiB |$320/month |
||16 vCPU 64 GiB |$640/month |
||32 vCPU 128 GiB |$1,280/month |


Purchase an Exclusive compute resource group For details, see:[Exclusive Computing Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_computing_resource_group)

<span id="_2-4-独享调度资源组计费周期与定价"></span>
## Exclusive scheduling resource groups

Exclusive scheduling resource group **1 CU: 4 concurrent** specification. The price is $20/month. The minimum sales specification is **4 CU: 16 concurrent**. If you need to purchase additional resources, you can either purchase resource groups with larger specifications or purchase more resource groups with the same specification.


|Regions |Specifications |Unit price |Maximum number of instances running concurrently |
|---|---|---|---|
|* Johor |4 CU: 16 concurrent |$80/month |16 |
||8CU: 32 concurrent |$160/month |32 |
||16 CU: 64 concurrent |$320/month |64 |
||32 CUs: 128 concurrent |$640/month |128 |


For information on purchasing an Exclusive scheduling resource group, see [Exclusive Scheduling Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_scheduling_resource_group).

<span id="0ce6ea71"></span>
## Resource group operation guide

<span id="373a4144"></span>
### Description of scaling up and down

After you purchase the specified resource group specifications and number of machines, you can scale the resource group up or down based on actual business requirements and scenarios. This allows you to meet varying resource demands during peak and off\-peak periods, so as to better improve resource group utilization.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Exclusive integration resource groups and Exclusive data service resource groups currently do not support changing resource group specifications; only expanding the number of resource groups is supported.</div>


<span id="_2-5-续费说明"></span>
### **Renewal instructions**

You can choose to renew your Exclusive resource group before it expires. If you do not renew before the expiration date, service features will be suspended after expiration. After the service is stopped, task instances that have not started will not be able to start, and those that are already running will be immediately marked as failed.

<span id="_2-6-到期关停说明"></span>
### **Instructions for shutdown upon expiration**

BytePlus will send expiration notifications to the phone number, email, or other contact methods bound to your BytePlus main account on the 7th, 3rd, and 1st day before the product or service you purchased expires, respectively. If you do not renew before the expiration date, all Exclusive resource group instances that have not been renewed will be immediately stopped at 12:00 noon on the day after the expiration shutdown date. After the service is stopped, task instances that have not started running cannot be started, and task instances that are already running will be immediately marked as failed.

<span id="_2-7-资源释放说明"></span>
### **Resource release instructions**

After a Exclusive resource group instance expires, it will be retained for you for 7 more days. If you do not complete the renewal within 7 days, the instance will be permanently released. If you successfully renew the Exclusive resource group instance through the official website's order center before it is completely released, the instance will resume running. No fees will be charged after the instance is shut down at expiration and before it is fully released.

<span id="_2-8-退订说明"></span>
### **Cancellation instructions**

The DataLeap Exclusive compute resource group supports no\-questions\-asked cancellation within seven days. In each calendar year (January 1 to December 31), an account can, by default, only unsubscribe from three DataLeap instances. For detailed unsubscription rules and procedures, see [unsubscription-management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).

The DataSail Exclusive integrated resource group supports no\-questions\-asked cancellation within seven days. By default, each account can unsubscribe from only one DataSail instance per calendar year (January 1 to December 31). For detailed unsubscription rules and procedures, see [unsubscription-management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).

<span id="_3-税费与发票"></span>
## Taxes, fees, and invoices

Unless otherwise specified, all product or service pricing on the BytePlus platform not includes value\-added tax(VAT). If, during the service provision process or the product usage period, there is an adjustment to national tax policy resulting in a change to the value\-added tax rate, the applicable value\-added tax rate shall be adjusted in accordance with the national tax policy. The price excluding tax will remain unchanged.

We support issuing value\-added tax (VAT) invoices to you for an amount equal to the amounts of orders that have been successfully purchased and/or billed amounts in your BytePlus account. Invoicing is not supported for unconsumed prepaid amounts. You can apply for a VAT invoice through the **BytePlus Console \> Billing Center \> Invoice Management**, or through other channels that BytePlus may designate from time to time and promptly notify you of. We will issue a VAT invoice to you promptly after receiving your application. If the service rules applicable to the service you use are inconsistent with this agreement, or if both parties have otherwise agreed, the specific service rules or the separately agreed terms and conditions shall apply. For scheduled settlement services and specific usage amounts, the company also reserves the right to require the user to provide proof of creditworthiness, prepayment, a deposit, or other conditions for activation and subscription that the company deems necessary.

For more details, see [Managing invoices](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-invoices).
