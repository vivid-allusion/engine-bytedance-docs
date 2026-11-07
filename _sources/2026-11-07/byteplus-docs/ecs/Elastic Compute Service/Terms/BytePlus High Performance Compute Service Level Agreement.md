---
title: "BytePlus High Performance Compute Service Level Agreement"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/High_Performance_Compute_GPU_Service_Level_Agreement"
---

**Last Update: ** September 15, 2025

During the term of the [BytePlus Customer Agreement](https://docs.byteplus.com/en/legal/docs/customer-agreement) pursuant to which Byteplus Pte. Ltd.(“**BytePlus**”) has agreed to provide the **BytePlus** **High Performance Compute** **Service** (the “**Service**”) to you (the “**Agreement**”), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this “**SLA**”).Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.


1. ## Service Levels <span id="6Z85WCYl"></span>


BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.9% during any monthly billing cycle (the “**Service Levels**”) as calculated and subject to the exclusions outlined below in Section 4.


2. ## Service Credits <span id="RuMmI6T6"></span>


Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|<div style="text-align: center"><br><strong>Monthly Uptime Percentage ("MUP")</strong></div><br> |**Monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills** |
|---|---|
|<div style="text-align: center"><br>99% <= MUP < 99.9%</div><br> |2 \* Service Credits |
|<div style="text-align: center"><br>95% <= MUP < 99%</div><br> |5 \* Service Credits |
|<div style="text-align: center"><br>MUP< 95%</div><br> |10 \* Service Credits |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange the Service Credits into Service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 100% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.


3. ## Service Credit Application and Payment Procedures <span id="wGtDaEIz"></span>


In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:


1. the words “SLA Credit Request” in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected Services;


If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus’s information.


4. ## Exclusions of SLA <span id="HOVaPxR9"></span>


If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:


1. any system maintenance with prior notice by BytePlus to you, including system cutover, maintenance, RDMA network upgrades, upgrade and failure simulation test; 

2. any features excluded from this SLA;

3. any matters that is out of BytePlus’s control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus;

4. any loss or leak of data, pin or password due to your improper maintenance or improper security measures;

5. any negligence in authorization or mal\-operation by you;

6. any of your failure to comply with documentation or suggestions made available by BytePlus;

7. any Service unavailability or failure of the Service not attributable to BytePlus, including without limitation, force majeure event, your application and/or a domain is blocked due to any reason, and any hacker attacks on your or any user's system and/or application.

8. For the Service instances with local volumes, when a local volume fails, the data on it will be erased, which may result in service unavailability as the local volume or the data stored on it works as a dependency for instance startups.

9. **If your instance of the Service experiences an irrecoverable hardware failure, BytePlus will send you a failure notification. Upon receiving it, you have the option to terminate or unsubscribe such an instance. However, if you choose to keep the faulty instance active after being notified, the relevant instance will continue being billed until you terminate it. This failure period will not be counted as service downtime or unavailability.** 

10. Services are suspended or terminated due to the customer's violations of the Agreement or rules of the Service or BytePlus ECS Service, including but not limited to cases where a spot instance is released because the Customer's bid is lower than the settlement price, or an instance is suspended or released due to overdue payments.

11. Circumstances where BytePlus may be exempt from liability or compensation, as specified in applicable laws and regulations, agreements, or rules, or in rules or descriptions separately issued by BytePlus.

5. ## Definitions <span id="pqyX84D6"></span>


The following definitions shall apply to this SLA:


*  **"Downtime"**  means the total number of minutes of Unavailability within a Service Cycle.

*  **"Monthly Service Fee"**  means the total amount of service fees paid by the customer for a single Service instance in a service period, excluding any part that has been purchased but not yet consumed. If the customer has paid for the service fees of several months in one lump sum, then the monthly service fees will be proportionally allocated according to the number of months purchased or the quantity of usage.

* "**Monthly Uptime Percentage**" or "**MUP**" =  **<ins>(the Total Minutes of a Service Cycle \- Downtime) / the Total Minutes of a Service Cycle \* 100%</ins>**  . MUP is calculated for a singleService instance. Monthly Uptime Percentage measurements exclude any Unavailability resulting directly or indirectly from any exclusion set forth below in Section 4."**Service Cycle**" each calendar month is a Service Cycle. The period from the day on which you start to use the Service to the very last day of such month will be counted as one Service Cycle. The availability of the Service is calculated independently for each Service Cycle.

*  **"Service Credits" = ** **<ins>Downtime \- the Total Minutes of a Service Cycle \* (1\- Service Level)</ins>**  **. ** Service Level herein shall be "99.9%". The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 100% of such monthly service fee or equivalent value in other items.

* "**Total Minutes of a Service Cycle**" is calculated by the total number of days in each Service Cycle \* 24 (hours) \* 60 (minutes).

*  **"Unavailability"**  means a Service instance that has inbound/outbound access rules configured, which is in a "running" state, cannot communicate with any IP address in both directions (inbound/outbound) via TCP or UDP protocol, with a Valid Request , and this state lasts for more than 5 consecutive minutes. For the avoidance of doubt, if the Unavailability period is less than 5 consecutive minutes, those minutes shall not be counted as the Unavailability. If you did not make any requests in an interval, that interval is assumed to be 100% available.

* "**Valid Requests**" are the Service requests received by our server that would normally result in a non\-error response. Valid Requests exclude: (i) any request that fails to pass authentication and/or parameter verification; (ii) any request initiated due to hacker attacks on your system/program or other security breaches.

6. ## Miscellaneous <span id="RyO2LIwv"></span>


BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
