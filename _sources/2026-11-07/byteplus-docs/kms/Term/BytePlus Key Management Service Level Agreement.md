---
title: "BytePlus Key Management Service Level Agreement"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/BytePlus_Key_Management_Service_Level_Agreement"
---

During the term of the [BytePlus Customer Agreement](https://docs.byteplus.com/en/docs/legal/docs-customer-agreement) pursuant to which BytePlus Pte. Ltd.(“**BytePlus**”) has agreed to provide the **BytePlus** **Key** **Management** **Service** (the “**Service**”) to you (the “**Agreement**”), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this “**SLA**”).Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.


1. # **Service Levels** <span id="service-levels"></span>


BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.9% during any monthly billing cycle (the “**Service Levels**”) as calculated and subject to the exclusions outlined below in Section 4.

**Service availability calculation formula**


* Service Availability = (1 \- ( Service CycleΣ Error Rate per 5 Minutes / Total number of 5 minutes within the Service Cycle)) x 100%

* Total number of 5 minutes within the service cycle = （60 / 5） \* 24 \* Number of days in the Service Cycle

2. # Service Credits <span id="service-credits"></span>


Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|<div style="text-align: center"><br>Monthly Uptime Percentage ("MUP")</div><br> |Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills |
|---|---|
|<div style="text-align: center"><br>99.0% <= MUP < 99.90%</div><br> |10% |
|<div style="text-align: center"><br>95.0% <= MUP< 99.0%</div><br> |25% |
|<div style="text-align: center"><br>MUP< 95.0%</div><br> |50% |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange the Service Credits into Service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 50% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


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

6. any of your failure to comply with documentation or suggestions made available by BytePlus, you did not follow the instructions or recommendations in the product usage document, including but not limited to:

   1. Loss of data key in envelope encryption scenario or Volc account/password, resulting in inability to decrypt data

   2. Leakage of plaintext data key due to reasons other than this service in envelope encryption

   3. Accidentally deleting customer master key and secret

   4. Other non\-standard operations leading to data leakage or inability to decrypt data

7. any Service unavailability or failure of the Service not attributable to BytePlus, including without limitation, force majeure event, your application and/or a domain is blocked due to any reason, and any hacker attacks on your or any user's system and/or application.

8. # **DEFINITIONS** <span id="definitions"></span>


The following definitions shall apply to this SLA:


1. **Service Cycle:**  each calendar month is a Service Cycle. Any period less than one month shall be calculated as one full calendar month.

2. **The number of days in the Service Cycle: Total** number of days in each Service Cycle.

3. **Failed request:** 

   1. The service failure resulted in the request not being received normally

   2. Requests with HTTP status code 5XX

4. **Valid request:**  The server considers a request as valid when received, **but does not include the following types of requests:** 

   1. The request is made under an unopened or unpaid status.

   2. The request contains an incorrect signature.

   3. The request is initiated due to a hacker attack on your application.

5. **Error Rate** **per 5 Minutes:**  Calculate it on a per 5\-minute basis as follows:

   Error rate every 5 minutes = (Number of failed requests every 5 minutes / Total number of valid requests every 5 minutes) x100%

6. **Monthly Uptime Percentage** means total number of minutes in a monthly billing cycle, minus the number of minutes of Downtime suffered from all Downtime Periods in a monthly billing cycle, divided by the total number of minutes in a monthly billing cycle. Monthly Uptime Percentage measurements exclude any lack of Availability resulting directly or indirectly from any exclusion set forth below in Section 4.

7. **Monthly service fee:**  Refers to the accumulated billing charges for this service under your Byteplus account in a calendar month.

8. # **MISCELLANEOUS** <span id="miscellaneous"></span>


BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.

&nbsp;
