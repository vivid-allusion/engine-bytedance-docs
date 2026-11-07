---
title: "SLA for BytePlus SealSuite"
product: "BytePlus Legal"
product_code: "legal"
source: "https://docs.byteplus.com/en/docs/legal/docs-sla-for-byteplus-sealsuite"
---

*Last Update: 15/06/2023*

During the term of the BytePlus Customer Agreement pursuant to which BytePlus Pte. Ltd. ("**BytePlus**") has agreed to provide the BytePlus SealSuite Service (the "**Service**") to you (the "**Agreement**"), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this "**SLA**"). Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.

<span id="60b960d2"></span>
## 1. Service Levels

BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.9% during any monthly billing cycle (the "**Service Levels**") as calculated and subject to the exclusions outlined below in Section 4.

The Monthly Uptime Percentage shall be calculated per Billing Cycle, covering BytePlus SealSuite Services for all domains under a particular BytePlus SealSuite account of a Customer, calculated as follows:

**The Monthly Uptime Percentage = (1 – Downtime within a Billing Cycle / Total Time of a Billing Cycle) × 100%.** 

<span id="37a5a103"></span>
## 2. Service Credits

Subject to the terms and conditions of the Agreement, and your full compliance with the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|**Monthly Uptime Percentage ("MUP")**  |**Percentage of monthly bills for the Service which does not meet SLA that will be credited to your future monthly bills** |
|---|---|
|95% <= MUP < 99.90% |10% |
|MUP < 95% |25% |



* We will apply any Service Credits only against future Service payments otherwise due from you.


At our discretion, we may exchange the Service Credits into Service hours.


* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 25% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.

<span id="b43224bc"></span>
## 3. Service Credit Application and Payment Procedures

In order to apply for the Service Credits, you must notify BytePlus SealSuite within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus SealSuite with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:


1. the words "SLA Credit Request" in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected Services;


If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus SealSuite shall be entitled to make a determination in good faith based on BytePlus's information.

<span id="c3167d65"></span>
## 4. Exclusions of SLA

If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:


1. any system maintenance with prior notice by BytePlus SealSuite to you, including system cutover, maintenance, upgrade and failure simulation test;

2. any features excluded from this SLA;

3. any matters that are out of BytePlus's control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus;

4. any loss or leak of data, pin or password due to your improper maintenance or improper security measures;

5. any negligence in authorization or mal\-operation by you;®

6. any of your failure to comply with documentation or suggestions made available by BytePlus;

7. any Service unavailability or failure of the Service not attributable to BytePlus, including without limitation, force majeure event, your application and/or a domain is blocked due to any

8. any hacker attacks on your or any user's system and/or application


<span id="3e6f4deb"></span>
## 5. Definitions

The following definitions shall apply to this SLA:


* "**Service Period**" means one service period equal to one calendar month.

* "**Back\-off Requirements**" means, when an error occurs, you are responsible for waiting for a period of time before issuing another request. This means that after the first error, there is a minimum back\-off interval of 1 second and for each consecutive error, the back\-off interval increases exponentially up to 32 seconds.

* "**Unit Time**" refers to every 5 minutes shall be deemed as Unit Time for the calculation of availability, such as 00:00:00 \- 00:04:59 shall be deemed as Unit Time.

* "**Downtime**" means if the error rate per Unit Time exceeds 0.05% and lasts for 10 minutes or longer, such a time period shall be counted into Downtime. Any such duration that is less than 10 minutes will not be counted.

* "**Total Time of a billing Cycle**" is calculated by the actual number of days in that calendar month \* 24 (hours) \* 60 (minutes).

* "**Error Rate**" means the number of Valid Requests that result in a response with HTTP Status 500 and Code "Internal Error" divided by the total number of Valid Requests during that period.


Repeated identical requests do not count towards the Error Rate unless they conform to the Back\-off Requirements.


* "**Monthly Uptime Percentage**" means total number of minutes in a monthly billing cycle, minus the number of minutes of Downtime suffered from all Downtime Periods in a monthly billing cycle, divided by the total number of minutes in a monthly billing cycle. Monthly Uptime Percentage measurements exclude any lack of Availability resulting directly or indirectly from any exclusion set forth below in Section 4.

* "**Valid Requests**" means a call to the Service.

* "**Valid Requests**" are the Service requests received by our server, and that would normally result in a non\-error response. For the avoidance of any doubt, Valid Requests include the requests that conform to the Back\-off Requirements, Valid Requests exclude: (i) any request that fails to pass authentication and/or parameter verification; (ii) any request initiated due to any hacker attacks on your system/program or any.


<span id="cf8c8dfa"></span>
## 6. Miscellanous

BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
