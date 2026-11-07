---
title: "SLA for BytePlus TOS Service"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Sla-for-byteplus-tos-service"
---

During the term of the **BytePlus Customer Agreement** pursuant to which BytePlus Pte. Ltd.(“**BytePlus**”) has agreed to provide the **BytePlus TOS Service** (the “**Service**”) to you (the “**Agreement**”), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this “**SLA**”).Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.

<span id="465f8618"></span>
## **1 Service Levels**

BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.99% during any monthly billing cycle (the “**Service Levels**”) as calculated and subject to the exclusions outlined below in Section 4.

Byteplus TOS counts the corresponding service availability according to different storage types. The calculation formula for service availability is as follows:

**Service availability = (1 \- error rate per 5 minutes in the service period / total number of 5 minutes in the service period) \* 100%** 

<span id="ca1a091a"></span>
## 2 Service Credits

Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|**Storage Type** |**Service Availability** |**Compensation Coupon** |
|---|---|---|
|Standard storage |Lower than 99.99% but equal to or higher than 99.90% |10% of the monthly service fee |
||Lower than 99.90% but equal to or higher than 95.00% |30% of the monthly service fee |
||Lower than 95.00% |50% of the monthly service fee |
|Infrequent access storage/Archive storage |Lower than 99.00% but equal to or higher than 95.00% |30% of the monthly service fee |
||Lower than 95.00% |50% of the monthly service fee |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange the Service Credits into Service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle exceeds US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 50% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.

<span id="3fad4a0a"></span>
## **3 Service Credit Application** and Payment Procedures

In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:


1. the words “SLA Credit Request” in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected Services;

   If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

   If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus’s information.


<span id="33de8f11"></span>
## **4 Exclusions of SLA**

If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:


1. any system maintenance with prior notice by BytePlus to you, including system cutover, maintenance, upgrade and failure simulation test;

2. any features excluded from this SLA;

3. any matters that is out of BytePlus’s control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus;

4. any loss or leak of data, pin or password due to your improper maintenance or improper security measures;

5. any negligence in authorization or mal\-operation by you;

6. any of your failure to comply with documentation or suggestions made available by BytePlus;

7. any Service unavailability or failure of the Service not attributable to BytePlus, including without limitation, force majeure event, your application and/or a domain is blocked due to any reason, and

8. any hacker attacks on your or any user's system and/or application.

9. unavailability caused by operating system upgrades initiated by the user.

10. unavailability caused by the applications or installation activities of the user.

11. unavailability caused by force majeure or unexpected events.

12. unavailability caused by other reasons that have nothing to do with BytePlus.


<span id="324211cd"></span>
## **5 DEFINITIONS**

The following definitions shall apply to this SLA:

**5.1 Service cycle**: A service cycle is one calendar month.

**5.2 Valid requests**: Valid requests are requests that are sent from users and received by Torch Object Storage (TOS), **excluding:** 


1. Requests that fail TOS identity verification or authentication and requests sent from users whose account is in arrears (with an HTTP status code of 403).

2. All requests from asynchronous backend processing after cross\-region replication, batch processing, asynchronous fetching, or lifecycle management is configured.

3. All requests to obtain the bucket list by calling the GetService API.

4. Requests from a user application that is hacked.


**5.3 Failed requests**: Failed requests are requests with an error code of 5XX returned by TOS, **excluding:** 


1. Requests with an HTTP status code of 429 or 503, indicating that the TOS request quota is exceeded as the user adopts an inappropriate access mode.

2. Failed requests from asynchronous backend processing after cross\-region replication, batch processing, asynchronous fetching, or lifecycle management is configured.

3. Failed requests to obtain the bucket list by calling the GetService API.

4. Slow requests in the following scenarios:

   1. Callback timeout

   2. Mirroring\-based back\-to\-origin timeout

5. Error requests or service unavailability caused by proper upgrades, changes, or downtime initiated by TOS.

6. Requests from a user application that is hacked.


**5.4 Error rate per 5 minutes**: It refers to the proportion of failed requests to valid requests per 5 minutes and is calculated as follows:

**Error rate per 5 minutes = Number of failed requests per 5 minutes/Number of valid requests per 5 minutes × 100%** 

**5.5 Monthly service fee**: TOS charges a BytePlus account by region and storage type respectively per calendar month.

<span id="ddcc2451"></span>
## **6 MISCELLANEOUS**

BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
