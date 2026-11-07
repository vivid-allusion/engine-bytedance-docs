---
title: "Service Level Agreement for NDB for MySQL"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Service_Level_Agreement_for_NDB_for_MySQL"
---

**Last Update: June 2, 2026**

During the term of the [BytePlus Customer Agreement](https://docs.byteplus.com/en/legal/docs/customer-agreement) pursuant to which BytePlus Pte. Ltd.("**BytePlus**") has agreed to provide the **BytePlus NDB for MySQL Service** (the "**Service**") to you (the "**Agreement**"), the Service will be subject to the service level metrics set out below in this Service Level Agreement (the "**SLA**"). Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.

<span id="r4hMzSk2"></span>
## 1. Service Levels

BytePlus will use all commercially reasonable efforts to make the service available with a Monthly Uptime Percentage no less than 99.96% during any monthly billing cycle (the "**Service Levels**") as calculated and subject to the exclusions outlined below in Section 4.

Monthly Uptime Percentage is calculated with the following expression:

**Monthly Uptime Percentage =(Total Service Cycle Minutes \- Service Unavailable Minutes)/Total Service Cycle Minutes \* 100%** 

<span id="aexsdmwa"></span>
## 2. Service Credits

Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|**Monthly Uptime Percentage ("MUP")**  |**Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills** |
|---|---|
|99.00% <= MUP＜ 99.96% |15% |
|95.00% <= MUP ＜ 99.00% |30% |
|MUP ＜ 95.00% |100% |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange Service Credits into Service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 100% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.

<span id="GuMZE8mG"></span>
## 3. Service Credit Application and Payment Procedures

In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:


1. the words “SLA Credit Request” in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected Services.


If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus’s information.

<span id="J1QaeFVr"></span>
## 4. Exclusions of SLA

If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:


1. any system maintenance with prior notice by BytePlus to you, including system cutover, maintenance, upgrade and failure simulation test;

2. any features excluded from this SLA;

3. any matters that is out of BytePlus’s control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus;

4. any loss or leak of data, pin or password due to your improper maintenance or improper security measures;

5. any negligence in authorization or mal\-operation by you;

6. any of your failure to comply with documentation or suggestions made available by BytePlus;

7. any Service unavailability or failure of the Service not attributable to BytePlus, including without limitation, force majeure event, your application and/or a domain is blocked due to any reason;

8. any hacker attacks on your or any user's system, application, and/or website;

9. any circumstance, under the relevant laws, regulations, codes, rules or agreements, where BytePlus could be exempted from any liability;

10. The instance resources (including but not limited to CPU, memory, and hard disk) are overused and the instance configuration is not upgraded in time;

11. The situation where the high availability service capability is lost due to the customer adjusting the instance configuration. Including but not limited to:

   * Setting the instance as global read\-only leads to the rejection of write requests.

   * Irrational configuration of instance read weight leads to abnormal read\-only nodes, making it impossible to balance read traffic to other nodes.

   * When configuring a unique read\-only node for a read\-only connection endpoint, the unique read\-only node is abnormal, making the read\-only connection terminal unable to carry business.

12. any system performance degradation (e.g., slow response, system hang, replication delay or interruption) caused by excessive utilization of instance resources (including but not limited to CPU, memory and disk) where you fail to upgrade instance configurations promptly, and any service unavailability resulting from log replay operations;

13. any service unavailability arising from suspension or termination of NDB for MySQL instance services due to your violation of service terms, including service suspension or release caused by overdue payments;

14. any business issues of NDB for MySQL instances caused by bugs in open\-source communities.


<span id="Fn0K6U5a"></span>
## 5. Definitions

The following definitions shall apply to this SLA:


* "**Instance**", an instance is a virtualized, independently running database operating environment.

*  **"Service Cycle"** , each calendar month is a Service Cycle. Any period less than one month shall be calculated as one full calendar month. The period from the day on which a user starts to use the Service to the very last day of such month will be counted as one Service Cycle. The availability of the Service is calculated independently for each Service Cycle.

* "**Total Service Cycle Minutes"** , is calculated by the total number of days in each Service Cycle \* 24 (hours) \* 60 (minutes).

*  **"Downtime"** , When all of the customer's attempts to establish a connection with the specified NDB for MySQL instance fail for one consecutive minute, the NDB for MySQL instance service is deemed to be unavailable within that minute.

*  **"Downtime within a Service Cycle"** , the accumulated minutes of Downtime in that Service Cycle.

* "**Monthly Service Fee**", the total service fee paid by the customer for a single NDB for MySQL instance in a natural month. If the customer pays for multiple months of service at one time, the monthly service fee will be calculated based on the number of months purchased.


<span id="mE7GI7FK"></span>
## 6. Miscellaneous

BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
