---
title: "BytePlus EMR Serverless Service Level Agreement"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/BytePlus_EMR_Serverless_Service_Level_Agreement"
---

Last Update : April 30, 2025

During the term of the [BytePlus Customer Agreement](https://docs.byteplus.com/en/legal/docs/customer-agreement) pursuant to which BytePlus Pte. Ltd.("**BytePlus**") has agreed to provide the **EMR Serverless** **Service** (the "**Service**") to you (the "**Agreement**"), the Service will be subject to the service level metrics set out below in this Service Level Agreement (the "**SLA**"). Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.

<span id="097b592d"></span>
## **Service Levels**

BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.90% during any monthly billing cycle (the "**Service Levels**") as calculated and subject to the exclusions outlined below in Section 4.

Monthly Uptime Percentage is calculated with the following expression：

**Monthly Uptime Percentage = ((Total Service Cycle Minutes \- Service Unavailable Minutes) / Total Service Cycle Minutes) \* 100%** 

<span id="b7cc36c4"></span>
## **Service Credits**

Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|Monthly Uptime Percentage ("MUP") |Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills |
|---|---|
|99.00% <= MUP < 99.90% |10% |
|95.00% <= MUP < 99.00% |20% |
|MUP < 95.00% |30% |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange Service Credits into Service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 100% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.

<span id="a006e988"></span>
## **Service Credit Application** **and Payment Procedures**

In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:


1. the words "SLA Credit Request" in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected Services.


If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus' information.

<span id="04fb5e62"></span>
## **Exclusions of** **SLA**

If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:

(1) Caused by BytePlus's system maintenance after prior notice to the customer, including cutover, repair, upgrade, and simulated fault drills;

(2) Caused by the failure or configuration adjustment of any network or equipment other than BytePlus's own equipment;

(3) User\-mode failures caused by bugs within the scope of open\-source community components;

(4) Service unavailability caused by the customer configuring it in the "non\-high availability" mode or having a single data copy;

(5) Failures caused by user\-mode issues, including but not limited to: improper configuration parameters, unreasonable resource usage, business logic bugs, etc.;

(6) Caused by the loss or leakage of data, passwords, passcodes, etc. due to the customer's improper maintenance or improper confidentiality;

(7) Caused by the hacking of the customer's application programs or data information;

(8) Failures caused by the customer's or a third party's software, equipment, or other technologies;

(9) Caused by the customer's failure to follow BytePlus's product usage documentation or usage suggestions;

(10) Service unavailability caused by misoperations due to the customer's negligence or operations authorized by you;

(11) The slow response and system freeze of the service under ultra\-high performance pressure;

(12) Any force majeure events or accidents;

(13) Situations where BytePlus can be exempted from liability, compensation liability, etc. as described in relevant laws and regulations, relevant agreements, relevant rules, or relevant rules and instructions separately issued by BytePlus.

<span id="22ada2e6"></span>
## **Definitions**

The following definitions shall apply to this SLA:


*  **"Request"**  means an invocation of a Service function by directly calling the OpenAPI.

*  **"Time Interval"**  means 5 minutes.

* "**Downtime"**  means the total number of minutes in a billing month when the Service is unavailable. A Service is unavailable if all Requests processed by the Service within a Time Interval return a 500 or 503 error code. For the avoidance of doubt, if no Requests are made within a Time Interval (or a longer period of time), that Time Interval is assumed to be 100% available.

*  **"Service Cycle"**  , each calendar month is a Service Cycle. The period from the day on which a user starts to use the Service to the very last day of such month will be counted as one Service Cycle. The availability of the Service is calculated independently for each Service Cycle.

* "**Total Service Cycle Minutes"**  is calculated by the total number of days in each Service Cycle \* 24 (hours) \* 60 (minutes).

*  **"Downtime within a Service Cycle",**  the accumulated minutes of Downtime in that Service Cycle.

* "**Monthly Service Fee**", the total service fee paid by the customer for EMR Serverless Service in a natural month. If the customer pays for multiple months of service at one time, the monthly service fee will be calculated based on the number of months purchased.
