---
title: "Pipeline execution time"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Pipeline_run_duration"
---

This document provides an overview of the detailed billing rules for pipeline runtime duration.

<span id=".6K6h6LS56K-05piO"></span>
## Billing description


* Count the **cumulative execution time of all pipeline tasks that use compute resources provided by the public resource pool** under each BytePlus account. Resource\-intensive tasks mainly include testing tasks, compilation and build tasks, image build and push tasks, command execution tasks, and custom steps.

* Pipeline execution time is **billed on a pay\-as\-you\-go basis according to computing resource specifications**. You can flexibly adjust the resource specifications for pipeline tasks based on your actual business needs, significantly reducing resource usage costs.


<span id=".6K6h6LS55YWs5byP"></span>
## Billing formula

**Pipeline total cost = (unit price for task 1 resource specification × task 1 execution time) + (unit price for task 2 resource specification × task 2 execution time) + ...** 

<span id=".5oyJ6YeP5Y2V5Lu3"></span>
## Per\-unit price

The pipeline provides computing resource specifications with CPU\-to\-memory ratios of 1:2, 1:4, and 1:8. The unit price varies for each type of computing resource specification. For details, see the table below:


|Computing resource specifications |Unit price (USD/minute) |
|---|---|
|1C2G |0.0022 |
|1C4G |0.0029 |
|1C8G |0.0043 |


<span id=".57uT566X5ZGo5pyf"></span>
## Settlement cycles

Bills are issued on an **hourly** basis, with **USD** as the settlement unit. Billing charges are automatically deducted from your account, and you can view bill details in the [Cost Center](https://console.byteplus.com/finance/bill/detail).

<span id=".5qyg6LS56K-05piO"></span>
## Arrears

If the available credit in your account (including account balance and vouchers) is less than the amount due on the pending invoice, your account will be considered in arrears.


|**Overdue Payment Duration** |**Description** |
|---|---|
|≤ 360 hours |You can continue to use Code Pipeline normally, and a bill will be issued based on your actual usage. |
|360 hours＜ duration ≤ 720 hours |The platform will send you a notification and suspend your ability to run pipelines. You will not be able to run pipelines. Pipeline functionality will be restored only after the account is renewed and no longer in arrears. |
|＞ 720 hours |The platform will send you a notification and revoke your ability to run pipelines. Bring your account up to date so that it is not in arrears, log in to the Code Pipeline console, follow the on\-screen instructions, and click **Restore Service**. Only then can you restore pipeline functionality. |
