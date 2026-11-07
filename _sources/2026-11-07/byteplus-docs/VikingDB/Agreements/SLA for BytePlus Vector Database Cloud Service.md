---
title: "SLA for BytePlus Vector Database Cloud Service "
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/SLA_for_BytePlus_Vector_Database_Cloud_Service"
---

This Service Level Agreement (SLA) for BytePlus Vector Database Cloud Service defines the service availability commitment from BytePlus. We guarantee a Monthly Uptime Percentage of at least 99.90%. Should we fail to meet this commitment, this document explains how you can become eligible for service credits as compensation.

<span id="18e349cf"></span>
# **Service Levels**

BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.90% during any monthly billing cycle (the “**Service Levels**”) as calculated and subject to the exclusions outlined below in Section 4.

<span id="17de4524"></span>
# Service Credits

Subject to the terms and conditions of the Agreement, and your full compliance with the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|**Monthly Uptime Percentage ("MUP")**  |**Credit as a percentage of the monthly bill for the non\-compliant Service** |
|---|---|
|95.00% <= MUP < 99.90% |10.00% |
|MUP< 95.00% |25.00% |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange the Service Credits for Service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than one U.S. dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 25% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.

<span id="d14be7f5"></span>
# **Service Credit Application** and Payment Procedures

In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of the calendar month in which you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:


1. the words “SLA Credit Request” in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected Services;

   If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

   If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus’s information.

    &nbsp;


<span id="exclusions-of-sla"></span>
# **Exclusions of SLA**

If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:


1. any system maintenance with prior notice by BytePlus to you, including system cutover, maintenance, upgrade and failure simulation test;

2. any features excluded from this SLA;

3. any matters that are out of BytePlus’s control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus;

4. any loss or leak of data, pin or password due to your improper maintenance or improper security measures;

5. any negligence in authorization or improper operation by you;

6. any of your failure to comply with documentation or suggestions made available by BytePlus;

7. any Service unavailability or failure of the Service not attributable to BytePlus, including without limitation, a force majeure event, your application and/or a domain being blocked for any reason, and

8. any hacker attacks on your or any user's system and/or application.


<span id="d37691e0"></span>
# **DEFINITIONS**

The following definitions shall apply to this SLA:


* **Service Cycle:**  A service cycle is one calendar month. If a customer uses the vector database for less than one calendar month, it will still be calculated as one calendar month.

* **Valid Requests:**  Requests sent by users and received by the server side of the vector database are regarded as valid requests. However, the following types of requests are not included:

   * Requests that fail the authentication and authorization of the vector database, and requests due to outstanding fees (requests with an HTTP status code of 403).

   * Requests initiated due to hacker attacks on the customer's application.

* **Failed Requests:**  Requests for which the vector database returns an error code in the 5XX range. However, the following types of requests are not included:

   * Error requests or situations of service unavailability caused by reasonable upgrades, changes, or downtimes initiated by the vector database service.

   * Requests restricted by the vector database due to hacker attacks on the customer's application.

* **Error Rate per 5 Minutes:**  The error rate per 5 minutes refers to the proportion of failed requests to the total number of valid requests. The calculation formula is as follows:

* **Error Rate per 5 Minutes** = (Number of Failed Requests per 5 Minutes / Total Number of Valid Requests per 5 Minutes) × 100%

* **Monthly Service Fee:**  The total service fee paid by the customer for the vector database within one service cycle (i.e., one calendar month).


<span id="ffd15af9"></span>
# **MISCELLANEOUS**

BytePlus has the right to amend this SLA from time to time. You may review the latest version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
