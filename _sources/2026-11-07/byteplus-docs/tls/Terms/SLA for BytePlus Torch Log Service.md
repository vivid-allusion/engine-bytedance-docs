---
title: "SLA for BytePlus Torch Log Service"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/sla-for-byteplus-torch-log-service"
---

**Last Update: 1st April,2024**

During the term of the [BytePlus Customer Agreement](https://docs.byteplus.com/en/legal/docs/customer-agreement) pursuant to which BytePlus Pte. Ltd.(“**BytePlus**”) has agreed to provide the **BytePlus Log Service** (the “**Service**”) to you (the “**Agreement**”), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this “**SLA**”).Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.

<span id="7fb92715"></span>
## **1 Service Levels**

BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.99% during any monthly billing cycle (the “**Service Levels**”) as calculated and subject to the exclusions outlined below in Section 4.

Byteplus TLS counts the corresponding service availability. The calculation formula for service availability is as follows:

**Service availability = (1 \- error rate per 5 minutes in the service period / total number of 5 minutes in the service period) \* 100%** 

<span id="9dfcdab1"></span>
## 2 Service Credits

Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|**Service Availability** |**Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills** |
|---|---|
|Lower than 99.90% but equal to or higher than 99.00% |15% of the monthly service fee |
|Lower than 99.00% but equal to or higher than 95.00% |30% of the monthly service fee |
|Lower than 95.00% |100% of the monthly service fee |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange the Service Credits into Service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle exceeds US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 100% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.

<span id="53870efe"></span>
## **3 Service Credit Application** and Payment Procedures

In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:


1. the words “SLA Credit Request” in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected Services;

   If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

   If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus’s information.

    &nbsp;


<span id="_4-exclusions-of-sla"></span>
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


<span id="293d8c8e"></span>
## **5 DEFINITIONS**

The following definitions shall apply to this SLA:

5.1 **Billing Cycle**

Each calendar month is a service cycle. Any period less than one month shall be calculated as one full calendar month.

5.2 **Valid Request**

A Valid Request is a request that is sent by the user and received by the server end of the Byteplus Log Service.

5.3 **Failed Request**

A Failed Request refers only to such request that is returned with an error code of internal error of the server (5xx errors). None of the following requests shall be deemed as a Failed Request or a Valid Request:

(1) any request that fails the authentication due to, including but not limited to, the mismatch of calculated signatures and lack of request authorization;

(2) any request that lacks required parameters or contains illegal parameters due to noncompliance with the documentations of Bytelus products.

In the event of a log service failure, when the number of failed requests cannot be obtained, the failure request count in this case will be calculated by multiplying the average number of user requests per minute in the previous 7 natural days by the failure time.

5.4 **Error Rate Per 5 Minutes**

The Error Rate Per 5 Minutes is the ratio of the count of Failed Requests returned by the BytePlus Log Service to the count of User Requests in the 5\-minute period, which shall be calculated as follows:

Error rate every 5 minutes = Count of failed requests per 5 minutes / The total number of Valid Requests per 5 minutes x 100%

**5.5 Monthly Service Fee**

The Monthly Service Fee is the aggregated amount of fees arising from the usage of the BytePlus Log Service in a Billing Cycle under the user’s BytePlus Account.

<span id="0c4c2dc5"></span>
## **6 MISCELLANEOUS**

BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
