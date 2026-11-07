---
title: "Client side billing explanation"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Client_side_billing_instructions"
---

This document introduces the billing details of Application Performance Monitoring Full\-Stack Edition.

<span id="tXNsr0HZ"></span>
## Billing Advantages

The billing for Application Performance Monitoring Full\-Stack Edition is not limited by the number of devices or users, and charges are based solely on the volume of reported events. You don't need to worry about the number of monitored end users being insufficient as your business grows. At the same time, to save costs, you can flexibly adjust the monitoring modules and sampling rates you need to use on the platform according to version features.

<span id="FWlWsEQi"></span>
## Billing Methods


* Client\-side billing methods include prepaid packages and postpaid (pay\-as\-you\-go).


<span id="uY81OHaV"></span>
## App\-side Monitoring

<span id="z2iMXOfp"></span>
### Prepaid

App\-side monitoring prepaid pricing is based on event volume package tiers.


|Event Volume Limit (events/year) |Price(USD) |
|---|---|
|5 million |220 |
|10 million |440 |
|50 million |2200 |
|200 million |6600 |
|400 million |13200 |
|2 billion |52800 |
|10 billion |200000 |


<span id="fNZVeSec"></span>
### Postpaid

Postpaid billing items have fixed unit prices and are settled hourly.


|Billing Item |USD per 100 events |
|---|---|
|Event |0.0057 |


The billing cycle is 1 hour. APMPlus calculates the event consumption of the previous hour at the beginning of each hour and generates a bill. If your account balance is sufficient, the system will automatically deduct the billed amount from your account. You can view your resource consumption in the APMPlus console.

<span id="PO7zZRav"></span>
### Monitoring Data Storage Period

Analysis data storage period is 90 days, crash and error detail data storage period is 90 days, and performance detail data storage period is 30 days.

<span id="OrmjMaw2"></span>
### Event Volume Explanation


* Events are defined when exceptions occur or performance metrics and custom metrics are collected, with data reporting.

* **Special Scenarios and Event Volume Weights**



|Special Scenario |Event Volume Weight |
|---|---|
|* 1 exception crash, lag, custom error, crash protection<br><br>* 1 downgraded iOS Memory Graph file |1\*N (N=100) |
|1 app exit reason |1\*N (N=50) |
|1 log retrieval |x\*N (N=200)<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">x represents the number of files reported in 1 log retrieval, N represents the weight of a single log file. For example: when 1 log retrieval reports 3 log files, the consumed event volume is 3\*200=600.</div><br> |
|* Crash with custom logs (optional)<br><br>* Android crash with business files (optional)<br><br>* iOS MetricKit stability module 1 report<br><br>* Coredump file generated during iOS crash |1\*N (N=200)<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This refers to the weight of a single Coredump file.</div><br> |
|* 1 Android memory Hprof file<br><br>* 1 iOS Memory Graph file |1\*N (N=7,000) |
|1 disk detail data |1\*N (N=0.067)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Approximately 15 disk detail data consume 1 event volume.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Disk metric sampling rate and disk exception sampling rate jointly affect disk details.</div><br> |



* Reporting 100 PVs consumes 1 event volume (rounded up within the statistical period, statistics are collected every half hour).

* Other data reports count as 1 event per report.

* If your application reports more events than the purchased tier's event volume limit within a year, new events will not be successfully reported and consumed. You can choose to continue purchasing the corresponding tier's event volume. If your application reports fewer events than the purchased tier's event volume limit within a year, you will not be able to continue using the service after the contract period expires.


<span id="Njr0wUK9"></span>
## WebPro Monitoring

<span id="oCPAGTTk"></span>
### Prepaid

WebPro\-side monitoring prepaid pricing is based on event volume package tiers.


|Event Volume Limit (events/year) |Price(USD) |
|---|---|
|2 million |60 |
|5 million |150 |
|10 million |300 |
|20 million |600 |
|50 million |1500 |
|100 million |3000 |
|300 million |9000 |
|500 million |15000 |
|1 billion |30000 |
|3 billion |90000 |


<span id="VTWfSC4s"></span>
### Postpaid

Postpaid billing items have fixed unit prices and are settled hourly.


|Billing Item |USD per 100 events |
|---|---|
|Event |0.0043 |


The billing cycle is 1 hour. APMPlus calculates the event consumption of the previous hour at the beginning of each hour and generates a bill. If your account balance is sufficient, the system will automatically deduct the billed amount from your account. You can view your resource consumption in the APMPlus console.

<span id="JdKxUSaE"></span>
### Monitoring Data Storage Period

Analysis data storage period is 90 days, and detail data storage period is 30 days.

<span id="8aBps57O"></span>
### Event Volume Explanation


* Reporting 100 PVs consumes 1 event volume (rounded up within the statistical period).

* Events are defined when exceptions occur or performance metrics and custom metrics are collected, with data reporting. When data is reported, 1 report counts as 1 event.

* Exceptions include: JS errors, slow requests, request errors, slow static resource loading, static resource errors, white screen.

* Performance metrics include: FP, FCP, LCP, FMP, CLS, LOAD, TTI, TTFB, DomReady, Dom parsing, Processing, ResourceLoad, Redirect, DNS, TCP, SSL, Request, Response, longtask count, longtask duration.

* If your application reports more events than the purchased tier's event volume limit within a year, new events will not be successfully reported and consumed. You can choose to continue purchasing the corresponding tier's event volume. If your application reports fewer events than the purchased tier's event volume limit within a year, you will not be able to continue using the service after the contract period expires.


<span id="Dgu1Rp5d"></span>
## Mini Program Pro Monitoring

<span id="SyicwDS2"></span>
### Prepaid

Mini Program Pro monitoring prepaid pricing is based on event volume package tiers.


|Event Volume Limit (events/year) |Price(USD) |
|---|---|
|2 million |60 |
|5 million |150 |
|10 million |300 |
|20 million |600 |
|50 million |1500 |
|100 million |3000 |
|300 million |9000 |
|500 million |15000 |
|1 billion |30000 |
|3 billion |90000 |


<span id="bU2cdTuo"></span>
### Postpaid

Postpaid billing items have fixed unit prices and are settled hourly.


|Billing Item |USD per 100 events |
|---|---|
|Event |0.0043 |


The billing cycle is 1 hour. APMPlus calculates the event consumption of the previous hour at the beginning of each hour and generates a bill. If your account balance is sufficient, the system will automatically deduct the billed amount from your account. You can view your resource consumption in the APMPlus console.

<span id="5qLqMZ8Q"></span>
### Monitoring Data Storage Period

Analysis data storage period is 90 days, and detail data storage period is 30 days.

<span id="HLFVYC8a"></span>
### Event Volume Explanation


* Events are defined when exceptions occur or performance metrics and custom metrics are collected, with data reporting. When data is reported, 1 report counts as 1 event.

* If your application reports more events than the purchased tier's event volume limit within a year, new events will not be successfully reported and consumed. You can choose to continue purchasing the corresponding tier's event volume. If your application reports fewer events than the purchased tier's event volume limit within a year, you will not be able to continue using the service after the contract period expires.


<span id="ArJD1MyY"></span>
## Package Renewal

When client\-side monitoring services use package prepaid billing, you can renew in advance or renew after resources are exhausted or expired.

<span id="6t1Cgfqr"></span>
### Renewal When package is Available


1. Log in to the [APMPlus Console](https://console.byteplus.com/observe/apmplus-client).

2. In the left sidebar, select **Client\-side Monitoring**, then find and click the target application name.

3. Under the service that needs renewal, click **Continue Purchase**.

4. Select the package specifications and quantity, then click **Purchase Now**.

5. On the order confirmation page, choose whether to use vouchers for payment, then click **Next**.


<span id="Er09c1YJ"></span>
### Renewal When the package is Exhausted


1. Log in to the [APMPlus Console](https://console.byteplus.com/observe/apmplus-client).

2. In the left sidebar, select **Client\-side Monitoring**, then find and click the target application name.

3. Under the service that needs renewal, click **Go to Renewal**.

4. Select the package specifications and quantity, then click **Purchase Now**.

5. On the order confirmation page, choose whether to use vouchers for payment, then click **Next**.


<span id="vMMy5iTR"></span>
### Renewal When Service Expires


1. Log in to the [APMPlus Console](https://console.byteplus.com/observe/apmplus-client) using the primary account.

2. In the left sidebar, select **Client\-side Monitoring**, then find and click the target application name.

3. Under the service that needs renewal, click **Service Expired**.

4. Select the package specifications and quantity, then click **Purchase Now**.

5. On the order confirmation page, choose whether to use vouchers for payment, then click **Next**.


<span id="1wcQNZGg"></span>
## Package to Postpaid Conversion

When client\-side monitoring services use package prepaid billing, you can set the package to automatically convert to postpaid billing after it is exhausted or expires.

<span id="qDTEBtn6"></span>
### Converting package to Postpaid


1. Log in to the Application Performance Monitoring Full\-Stack Edition Console.

2. In the top navigation bar, select the target region.

3. In the left sidebar, select Client\-side Monitoring, then find and click the target application name.

4. Under the service that needs to convert to Postpaid billing, check the option "Automatically convert to postpaid after package is exhausted or expires".

5. In the secondary confirmation dialog, click **Confirm**.


<span id="PK6sK9Qx"></span>
## Package Unsubscription Policy

This document introduces the unsubscription policy for Application Performance Monitoring Full\-Stack Edition (APMPlus) packages.

<span id="pTonOKqc"></span>
### Important Information Before Unsubscription


* Before applying for an unsubscription, please ensure you understand the relevant unsubscription rules and restrictions.

* Package unsubscription will not affect data already reported to APMPlus. After a package unsubscription, if there are no deductible packages under the current account and automatic conversion to postpaid billing is enabled, the system will adopt Postpaid billing mode. 

* If you decide to stop using APMPlus, you can turn off the data reporting switch to stop the service, after which no further charges will be incurred.


<span id="4EM7j2ep"></span>
### Unsubscription Management

APMPlus supports 7\-day unconditional unsubscription. For specific details, please refer to the [Unsubscription Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Each customer can only apply for one 7\-day unconditional unsubscription per year for APMPlus packages purchased.</div>


<span id="KJVUz6Bq"></span>
### Unsubscription Flow


* **Multiple Package**: When your account has multiple packages, after a unsubscription, the system will consume the remaining packages in order of their expiration time. When all packages are exhausted, if automatic conversion to postpaid billing is enabled, it will switch to Postpaid billing mode. If the account balance is sufficient, the service can operate normally; if the balance is insufficient, overdue charges will occur.

* **Single Package**: When your account has only one package, after an unsubscription, the billing mode will automatically convert to postpaid billing. If the account balance can cover the generated costs, the service can operate normally; if the balance is insufficient, it will result in overdue charges.


<span id="lcukknJl"></span>
### Postpaid Billing

Postpaid billing is a pay\-after\-use model. The system settles the costs incurred in the previous hour at fixed time points each hour and automatically deducts them from your account balance. Since no prepayment is involved, there are no refund issues. If the account balance is insufficient, overdue charges will occur.

<span id="jROw9RWW"></span>
## Arrears

If your account does not have sufficient balance to pay for a bill, your resources will enter the service suspension state due to arrears. This topic describes the service suspension state due to arrears and relevant instructions.

<span id="OlIUw23U"></span>
## Arrears cause

APMPlus client\-side monitoring performs settlement every hour and the expense is deducted in real time after a bill is generated. If the available quota of your account (including the account balance and cash coupons) is less than that in the settlement bill, you will enter the arrears state and receive an email notification for insufficient balance.

<span id="hHFXHwZt"></span>
## Arrears notification

After your account enters into arrears, the system sends an arrears notification through email, SMS, or internal message. Process the issue and recharge your account after receiving the notification.

<span id="BJvfQyRx"></span>
### Impact of Overdue Payment

After account overdue payment, billing stops, and service stops 24 hours after overdue payment. Data is retained for 90 days by default. After renewal, cleared data will not be restored, and service will not automatically resume. You need to manually enable the service in the console.

When using postpaid billing, if overdue payment exceeds 24 hours, you need to place a new order to resume billing.

<span id="0ZmHzk5w"></span>
## Project bill splitting

APMPlus client\-side monitoring supports using projects to manage workspace resources and perform bill splitting based on projects, solving the problem of financial cost sharing.

<span id="Qtx9YJpC"></span>
### Background information

Resource projects (Project) are a resource grouping management mechanism provided by BytePlus, helping users achieve logical resource isolation. You can perform operations including project\-based authorization and bills splitting through resource projects.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more project introductions, please refer to <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview">Project Overview</a>.</div>


<span id="5e45RCPq"></span>
### Prerequisites

The project has been created on the **Identity and Access Management** page. For details, please refer to [Project Management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management).

<span id="1kfl9yXm"></span>
### View results

<span id="C1h5ssaM"></span>
### View project resources


1. Log in to BytePlus [Identity and Access Management](https://console.byteplus.com/iam).

2. Select **Resource Management** \> **Project** on the left navigation bar. In the project list, select the target project and click **Manage** under the **Operation** column to view project details.

3. On the **Resources** tab, you can view the resource details of the project.


<span id="7H2fbzYH"></span>
### View splitting bills

After adding a project to the APMPlus client\-side monitoring workspace, it supports viewing splitting bills by project. The detailed operations are as follows:


1. Log in to the BytePlus [Cost Center](https://console.byteplus.com/finance).

2. Select **Bill Management** \> **Splitting Bills** in the left navigation bar.

3. On the **Splitting Bills** page, select a project from the **Project** dropdown menu to view the splitting bills for the specified project.
