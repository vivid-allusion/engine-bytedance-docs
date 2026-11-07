---
title: "Public resource group billing instructions"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Billing_Instructions_for_Public_Resource_Group"
---

DataLeap public resource groups currently provide three types of resource groups: **Public Scheduling Resource Group**, **Public Computing Resource Group**, and **Public Data Services Resource Group**. All public resource groups are billed on a Pay\-as\-you\-go (post\-paid) basis.

This article will introduce the billing instructions for each public resource group.

<span id="9dd056d0"></span>
## 1 Use limitations

When a single tenant uses a public resource group within a region, the following resource limits apply: **Public computing resource group**: the maximum per tenant per region is 100 CU; **Public scheduling resource group**: the maximum per tenant per region is 300 concurrent instances.

When the usage of the Public Resource Group approaches its limit, it is recommended to use an Exclusive Resource Group and migrate important tasks to the Exclusive Resource Group to run them, in order to ensure that task execution is not affected.

<span id="22f484d2"></span>
## 2 Public scheduling resource group

A public scheduling resource group is a type of public resource group provided by DataLeap. The billing method is Pay\-as\-you\-go. Users of BytePlus DataLeap will share and use the resources of the Public scheduling resource group. During peak usage periods, resource contention among different users may occur, and timely scheduling and execution of tasks cannot be guaranteed. We recommend using [Exclusive Scheduling Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_scheduling_resource_group). In a single\-tenant environment, you can assign scheduling resources yourself.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For the public scheduling resource group, the maximum number of concurrent instances per tenant per region is 300.</div>


<span id="a8a0b402"></span>
### 2.1 Description of billing items

The billing item for the Public scheduling resource group is the scheduling instance. All types of instances that are submitted to the scheduling system and run successfully will be included in the measurement range. Regardless of instance type, every instance that runs successfully is counted as one instance. The range of products involved includes Data Integration, Data Development, and Data Quality. Details include:


* Batch periodic scheduling instance, manual execution instance, and batch debug instance.

* Rerun instances for batch backfill.

* Batch data quality rule schedules, test instances, and rerun instances of quality rule results

* Profiling instances and rerun instances.

* Comparison instances and rerun instances.

* For EMR/ByteHouse job types, you will be charged both scheduling instance fees and compute fees for each corresponding engine.

   * For details on EMR fees, see [EMR Product Billing](https://docs.byteplus.com/en/docs/E-MapReduce/Billing).

   * For details on ByteHouse fees, see [ByteHouse Product Billing](https://docs.byteplus.com/en/docs/bytehouse/billing).


<span id="670cb07a"></span>
### 2.2 Billing cycle and pricing


|Region |Resource |Unit price |
|---|---|---|
|* Johor |Public scheduling resource group |$0.01/instance |


<span id="71f76a04"></span>
### 2.3 Fee deduction description

Bills are generated and charges are deducted on a daily basis. The billing system starts at 00:00 every day. It calculates charges for the instances that ran successfully during the previous calendar day and issues bills and performs deductions according to the above standard. Each time, only the daily fee for one interval is deducted; fees are not deducted cumulatively.

<span id="923df7b5"></span>
### 2.4 Description of arrears

If you recharge your account within 24 hours of your account entering arrears (that is, when your account balance becomes negative), your service will not be suspended. However, if the overdue payment is not settled within 24 hours, the service will be suspended. After Stop is executed, instances that have not started running cannot be started, while instances that have already started running can continue to run until "End".

<span id="6793bb83"></span>
## 3 Public Computing Resource Group

The Public Computing Resource Group is a type of Public Resource Group provided by DataLeap. The billing method is Pay\-as\-you\-go. Users of BytePlus DataLeap share resources in the Public Computing Resource Group. During peak usage periods, resource contention may occur between different users, and computing resources for tasks at runtime cannot be guaranteed. It is recommended to use [Exclusive Computing Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_computing_resource_group). In a single\-tenant environment, you can assign computing resources yourself.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For the Public Computing Resource Group, the maximum limit is 100 CU per tenant per region.</div>


<span id="4b8a837c"></span>
### 3.1 Description of billing items

The Public Computing Resource Group is suitable for development scenarios involving Notebook, Python, and Shell task types. The billing unit for the Public Computing Resource Group is **CU\*hour**, where the resource specification for 1 CU is 1C/4GiB.


* Notebook task: Billing starts immediately upon successful start of the Notebook Kernel. If startup fails, no usage is recorded and no charges are incurred. After the Notebook Kernel is closed, CU resources are released and metering stops immediately.

* Python, Shell: Costs are calculated based on the actual Running time of the task and the number of CUs occupied by the task, and do not include the time the task spends waiting for resources. Example: For a Shell job configured with 2 CU, the time spent waiting for resources is 0.5 hours, followed by an actual running time of 1 hour. The cost for this task is calculated as: $0.1 \* 2 \* 1 = $0.2.


<span id="3ea85b27"></span>
### 3.2 Billing cycle and pricing


|Region |Resource |Specifications |Unit price |
|---|---|---|---|
|* Southeast Asia Pacific (Johor) |Public Computing Resource Group |1CU(1CU/4GiB） |$0.1/CU/hour |


<span id="23e9a05c"></span>
### 3.3 Fee deduction description

Bills are issued and fees are deducted on an hourly basis. At the beginning of every hour, the billing system calculates the resource usage from the previous natural hour, issues a bill according to the above standard, and deducts the fee. Every time, only the fee for one interval will be deducted; no additional fees will be charged.

<span id="61a1cb92"></span>
### 3.4 Description of arrears

If you recharge your account within 2 hours after it enters arrears (that is, when the account balance is negative), your service will not be suspended. However, if the payment has been overdue for more than 2 hours and the outstanding amount remains unpaid, the service will be suspended. After Stop is performed, instances that have not started running cannot be started or debugged, and instances that are already running will be immediately set to Failed.

<span id="bffc22d4"></span>
## 4 Public Data Services Resource Group

The Public Data Services Resource Group is a type of Public Resource Group provided by DataLeap, and the billing method is Pay\-as\-you\-go. Users of BytePlus DataLeap share the Public Data Services Resource Group. During peak usage periods, there may be competition for resources among different users, and computing resources for API calls cannot be guaranteed.It is recommended to use [Exclusive Data Services Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_services_resource_group).

<span id="f1e43c99"></span>
### 4.1 Description of billing items

The billing item for the Public Data Services Resource Group is the number of API calls for the Data Service. All data service APIs invoked by the user will be included in the metering scope. Each application call is counted as one invocation. The product involved is Data Service.

<span id="4cc2e5b8"></span>
### 4.2 Billing cycle and pricing


|Region |Resource |Unit price |
|---|---|---|
|* Southeast Asia Pacific (Johor) |Public Data Service Resource Group |$0.007/10,000 requests |


<span id="01f905c9"></span>
### 4.3 Fee deduction descriptions

Generate a daily bill and deduct fees. Every day at 00:00, the billing system settles the number of Data Service API calls made during the previous calendar day, issues a bill according to the above standard, and performs the fee deduction. Every time, only the daily fee for one interval will be deducted; no cumulative deduction will occur.

<span id="9f369d5f"></span>
### 4.4 Description of arrears

If you recharge your account within 24 hours after your account enters arrears (that is, when your account balance is negative), your service will not be suspended. However, if the overdue payment remains unsettled for more than 24 hours, the service will be suspended. After being disabled, the Data Service API cannot be requested or invoked.

<span id="e10082b4"></span>
## 5 Taxes, fees, and invoices

Unless otherwise specified, all product or service pricing on the BytePlus platform not includes value\-added tax(VAT). If, during the service provision process or the product usage period, there is an adjustment to national tax policy resulting in a change to the value\-added tax rate, the applicable value\-added tax rate shall be adjusted in accordance with the national tax policy. The price excluding tax will remain unchanged.

We support issuing value\-added tax (VAT) invoices to you for an amount equal to the amounts of orders that have been successfully purchased and/or billed amounts in your BytePlus account. Invoicing is not supported for unconsumed prepaid amounts. You can apply for a VAT invoice through the **BytePlus Console \> Billing Center \> Invoice Management**, or through other channels that BytePlus may designate from time to time and promptly notify you of. We will issue a VAT invoice to you promptly after receiving your application. If the service rules applicable to the service you use are inconsistent with this agreement, or if both parties have otherwise agreed, the specific service rules or the separately agreed terms and conditions shall apply. For scheduled settlement services and specific usage amounts, the company also reserves the right to require the user to provide proof of creditworthiness, prepayment, a deposit, or other conditions for activation and subscription that the company deems necessary.

For more details, see [Managing invoices](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-invoices).
