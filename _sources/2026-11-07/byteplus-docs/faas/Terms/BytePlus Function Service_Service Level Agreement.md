---
title: "BytePlus Function Service_Service Level Agreement"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/BytePlus_Function_Service_Service_Level_Agreement"
---

**Last Update: March 31, 2025**

During the term of the **BytePlus Customer Agreement** pursuant to which BytePlus Pte. Ltd.(“**BytePlus**”) has agreed to provide the **BytePlus Function Service** (the “**Service**”) to you (the “**Agreement**”), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this “**SLA**”).Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.

<span id="_1-service-levels"></span>
## 1. Service Levels

BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.95% during any monthly billing cycle (the “**Service Levels**”) as calculated and subject to the exclusions outlined below in Section 4.

<span id="_2-service-credits"></span>
## 2. Service Credits

Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|<div style="text-align: center"><br>Monthly Uptime Percentage ("MUP")</div><br> |Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills |
|---|---|
|<div style="text-align: center"><br>99.00% <= MUP < 99.95%</div><br> |10% |
|<div style="text-align: center"><br>95% <= MUP < 99.00%</div><br> |25% |
|<div style="text-align: center"><br>MUP< 95%</div><br> |100% |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange the Service Credits into Service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 100% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.

<span id="_3-service-credit-application-and-payment-procedures"></span>
## 3. Service Credit Application and Payment Procedures

In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:


1. the words “SLA Credit Request” in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected Services;


If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus’s information.

<span id="_4-exclusions-of-sla"></span>
## 4. Exclusions of SLA

If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:


1. any system maintenance with prior notice by BytePlus to you, including system cutover, maintenance, upgrade and failure simulation test;

2. any features excluded from this SLA;

3. any matters that is out of BytePlus’s control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus;

4. any loss or leak of data, pin or password due to your improper maintenance or improper security measures;

5. any negligence in authorization or mal\-operation by you;

6. any of your failure to comply with documentation or suggestions made available by BytePlus;

7. any Service unavailability or failure of the Service not attributable to BytePlus, including without limitation, force majeure event, your application and/or a domain is blocked due to any reason, and

8. any hacker attacks on your or any user's system and/or application.


<span id="_5-definitions"></span>
## 5. DEFINITIONS

The following definitions shall apply to this SLA:


* **Unit time service unavailable**: 5 minutes

* **Failed request**: Function Service considers requests with HTTP status code 500 and requests that fail to reach the Function Service server due to Function Service failure as failed requests, but does not include the following types of requests:

   * Error requests that exceed the prescribed quota of Function Service due to improper access mode, resulting in requests being restricted by Function Service

   * Error requests or service unavailability caused by reasonable upgrades, changes, or downtime initiated by Function Service

   * Requests restricted by Function Service due to hacker attacks on customer applications

   * Requests that do not fall within the scope of valid requests

* **Valid requests**: Requests received by the Function Service server are considered valid requests, but do not include the following types of requests:

   * Requests that have failed Function Service identity verification and authentication, and requests in arrears (requests with HTTP status code 403)

   * All requests that are not function calls

   * Requests initiated by the customer's application being hacked

   * Requests that cannot reach the Function Service server due to customer network issues

*  **"Monthly Uptime Percentage"** :

   * Monthly Uptime Percentage =( 1\- Total error rate every 5 minutes during the service period / Total number of 5\-minute intervals ）x100%


<span id="_6-miscellaneous"></span>
## 6. MISCELLANEOUS

BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
