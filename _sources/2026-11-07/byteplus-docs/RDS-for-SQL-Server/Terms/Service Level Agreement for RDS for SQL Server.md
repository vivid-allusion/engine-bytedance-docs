---
title: "Service Level Agreement for RDS for SQL Server"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/service-level-agreement-for-RDS-for-SQL-Server"
---

**Last Update: June 2, 2026**

During the term of the [BytePlus Customer Agreement](https://docs.byteplus.com/en/legal/docs/customer-agreement) pursuant to which BytePlus Pte. Ltd.("**BytePlus**") has agreed to provide the **BytePlus RDS for** **SQL** **Server Service** (the "**Service**") to you (the "**Agreement**"), the Service will be subject to the service level metrics set out below in this Service Level Agreement (the "**SLA**"). Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.

Special note: If you use the Microsoft license that you purchase on your own, please comply with Microsoft's applicable license terms. BytePlus shall not be responsible for Microsoft software or provide any availability guarantees herein.


1. ### **Service Levels** <span id="abuyym2Z"></span>


BytePlus will use all commercially reasonable efforts to make the SQL Server High Availability Edition Service available with a Monthly Uptime Percentage no less than 99.95% during any monthly billing cycle (the "**Service Levels**") as calculated and subject to the exclusions outlined below in Section 4. Monthly Uptime Percentage is calculated with the following expression： **Monthly Uptime Percentage = ((Total Service Cycle Minutes \- Service Unavailable Minutes) / Total Service Cycle Minutes) \* 100%** 


2. ### **Service Credits** <span id="DFXhwnE5"></span>


Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|**Monthly Uptime Percentage ("MUP")**  |**Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills** |
|---|---|
|99.00% <= MUP < 99.95% |15% |
|95.00% <= MUP < 99.00% |30% |
|MUP < 95.00% |100% |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange the Service Credit into Service hours.

* A Service Credit will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

* The aggregate maximum number of Service Credit you can claim in a single monthly billing cycle shall not exceed 100% of such monthly bill. Service Credit will not entitle you to any refund or other payment from BytePlus. Service Credit may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.


3. ### **Service Credit Application** **and Payment Procedures** <span id="jdborhnI"></span>


In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:

a. the words "SLA Credit Request" in the subject line;

b. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

c. the affected Services.

If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus' information.


4. ### **Exclusions of** **SLA** <span id="Ia34fXhr"></span>


If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:

a. any system maintenance with prior notice by BytePlus to you, including system cutover, maintenance, upgrade and failure simulation test;

b. any features excluded from this SLA;

c. any matters that are out of BytePlus' control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus;

d. any loss or leak of data, pin or password due to your improper maintenance or improper security measures;

e. any negligence in authorization or mal\-operation by you;

f. any of your failure to comply with documentation or suggestions made available by BytePlus;

g. any Service unavailability or failure of the Service not attributable to BytePlus, including without limitation, force majeure event, your application and/or a domain is blocked due to any reason;

h. any hacker attacks on your or any user's system, application, and/or website;

i. any circumstance, under the relevant laws, regulations, codes, rules or Agreements, where BytePlus could be exempted from any liability;

j. SQL Server instance errors caused by customer\-installed software or other third\-party software or configurations not directly operated by BytePlus;

k. any system performance degradation (e.g., slow response, system hang, replication delay or interruption) caused by excessive utilization of instance resources (including but not limited to CPU, memory and disk) where you fail to upgrade instance configurations promptly, and any service unavailability resulting from log replay operations;

l. any Downtime or failure after you enable SystemAdmin privileged accounts, service unavailability issues are not covered by this Service Level Agreement;

m. any business issues of RDS for SQL Server instances caused by bugs from Microsoft official releases;

n. any service unavailability arising from suspension or termination of RDS for SQL Server instance services due to your violation of service terms, including service suspension or release caused by overdue payments.


5. ### **Definitions** <span id="GicCHsLB"></span>


The following definitions shall apply to this SLA:


* "**Instance**", an instance is a virtualized, independently running database operating environment.

*  **"Service Cycle"**  , each calendar month is a Service Cycle. The period from the day on which a user starts to use the Service to the very last day of such month will be counted as one Service Cycle. The availability of the Service is calculated independently for each Service Cycle.

* "**Total Service Cycle Minutes"**  is calculated by the total number of days in each Service Cycle \* 24 (hours) \* 60 (minutes).

*  **"Downtime",**  when all of the customer's consecutive attempts to establish a connection with the specified SQL Server instance within a certain minute fail, the SQL Server instance service is deemed to be unavailable within that minute.

*  **"Downtime within a Service Cycle"**  , the accumulated minutes of Downtime in that Service Cycle.

* "**Monthly Service Fee**", the total service fee paid by the customer for a single SQL Server instance in a natural month. If the customer pays for multiple months of service at one time, the monthly service fee will be calculated based on the number of months purchased.

6. ### **MISCELLANEOUS** <span id="oYFNHwU4"></span>


BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
