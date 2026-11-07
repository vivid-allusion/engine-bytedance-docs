---
title: "SLA for BytePlus ALB Service"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/SLA-for-BytePlus-ALB-Service"
---

**Last Update: 1st April,**  **2024**

During the term of the [BytePlus Customer Agreement](https://docs.byteplus.com/en/legal/docs/customer-agreement) pursuant to which BytePlus Pte. Ltd.(“**BytePlus**”) has agreed to provide the **BytePlus ALB Service** (the “**Service**”) to you (the “**Agreement**”), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this “**SLA**”).Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.


1. # **Service Levels** <span id="service-levels"></span>


BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.97% for multi\-zone ALB instances and no less than 99.90% for single\-zone ALB instances during any monthly billing cycle (the “**Service Levels**”) as calculated and subject to the exclusions outlined below in Section 4.


2. # Service Credits <span id="service-credits"></span>


Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|<div style="text-align: center"><br>Single\-zone ALB Monthly Uptime Percentage ("MUP")</div><br> |<div style="text-align: center"><br>Multi\-zone ALB Monthly Uptime Percentage ("MUP")</div><br> |Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills |
|---|---|---|
|<div style="text-align: center"><br>90.00% <= MUP < 99.90%</div><br> |<div style="text-align: center"><br>99.00% <= MUP < 99.97%</div><br> |10% |
|<div style="text-align: center"><br>80.00% <= MUP < 90.00%</div><br> |<div style="text-align: center"><br>95.00% <= MUP < 99.00%</div><br> |25% |
|<div style="text-align: center"><br>MUP< 80.00%</div><br> |<div style="text-align: center"><br>MUP< 95.00%</div><br> |100% |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange the Service Credits into Service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 100% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.


3. # **Service Credit Application** and Payment Procedures <span id="service-credit-application-and-payment-procedures"></span>


In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:

1. the words “SLA Credit Request” in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected Services;

If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus’s information.


4. # **Exclusions of** **SLA** <span id="exclusions-of-sla"></span>


If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:


1. any system maintenance with prior notice by BytePlus to you, including system cutover, maintenance, upgrade and failure simulation test;

2. any features excluded from this SLA;

3. any matters that is out of BytePlus’s control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus;

4. any loss or leak of data, pin or password due to your improper maintenance or improper security measures;

5. any negligence in authorization or mal\-operation by you;

6. any of your failure to comply with documentation or suggestions made available by BytePlus;

7. any Service unavailability or failure of the Service not attributable to BytePlus, including without limitation, force majeure event, your application and/or a domain is blocked due to any reason, and

8. any hacker attacks on your or any user's system and/or application.

9. # **DEFINITIONS** <span id="definitions"></span>


The following definitions shall apply to this SLA:

**Service Period**: A service period is one (1) calendar month. **Total minutes in Service Period**: calculated as the total number of days in the service period × 24 (hours) × 60 (minutes). **The service of a single listener is unavailable**: Within a certain minute, if all of the customer's consecutive attempts to establish a connection with a listener in the specified ALB instance fail, the service of the listener is deemed to be unavailable within that minute. **Single instance unavailable minutes**: The sum of the service unavailability minutes of all listeners included in a single ALB instance within a service period. **Total service cycle minutes of a single instance**: The sum of the total service period minutes of all listeners included in a single ALB instance within a service cycle. **Monthly service fee**: The total service fee paid by the customer for a single ALB instance in a service cycle, excluding the portion that has been purchased but not consumed. If the customer pays for multiple months of service at one time, the monthly service fee will be calculated prorated based on the number of months purchased or usage.


* **Monthly Uptime Percentage:**  （**Total service cycle minutes of a single instance** \- **Single instance unavailable minutes**）/ **Total service cycle minutes of a single instance** × 100%

6. # **MISCELLANEOUS** <span id="miscellaneous"></span>


BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
