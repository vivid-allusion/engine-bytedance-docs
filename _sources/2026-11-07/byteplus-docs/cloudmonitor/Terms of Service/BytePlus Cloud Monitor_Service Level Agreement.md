---
title: "BytePlus Cloud Monitor_Service Level Agreement"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/BytePlus-CloudMonitor_Service-Level-Agreement"
---

During the term of the [BytePlus Customer Agreement](https://docs.byteplus.com/en/legal/docs/customer-agreement) pursuant to which BytePlus Pte. Ltd.(“**BytePlus**”) has agreed to provide the **BytePlus CloudMonitor Service** (the “**Service**”) to you (the “**Agreement**”), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this “**SLA**”).Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.

<span id="_1-service-levels"></span>
## 1. Service Levels

BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.9% during any monthly billing cycle (the “**Service Levels**”) as calculated and subject to the exclusions outlined below in Section 4.

<span id="_2-service-credits"></span>
## 2. Service Credits

Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|<div style="text-align: center"><br>Monthly Uptime Percentage ("MUP")</div><br> |Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills |
|---|---|
|<div style="text-align: center"><br>99% <= MUP < 99.90%</div><br> |10% |
|<div style="text-align: center"><br>95% <= MUP < 99%</div><br> |25% |
|<div style="text-align: center"><br>MUP < 95%</div><br> |100% |



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


*  **"**  **Back\-off Requirements"**  means, when an error occurs, you are responsible for waiting for a period of time before issuing another request. This means that after the first error, there is a minimum back\-off interval of 1 second and for each consecutive error, the back\-off interval increases exponentially up to 32 seconds.

*  **"Downtime"**  means more than a 5% Error Rate. Downtime is measured based on server side Error Rate.

*  **"Downtime Period"**  means a period of one or more consecutive minutes of Downtime. Partial minutes or Intermittent Downtime for a period of less than one minute will not be counted towards any Downtime Periods.

*  **"Error Rate"**  means the number of Valid Requests that result in a response with HTTP Status 500 and Code "Internal Error" divided by the total number of Valid Requests during that period. Repeated identical requests do not count towards the Error Rate unless they conform to the Back\-off Requirements.

*  **"Monthly Uptime Percentage"**  means total number of minutes in a monthly billing cycle, minus the number of minutes of Downtime suffered from all Downtime Periods in a monthly billing cycle, divided by the total number of minutes in a monthly billing cycle. Monthly Uptime Percentage measurements exclude any lack of availability resulting directly or indirectly from any exclusion set forth below in Section 4.

*  **"Valid Requests**\*\*"\*\* are the Service requests received by our server, and that would normally result in a non\-error response. For the avoidance of any doubt, Valid Requests include the requests conform to the Back\-off Requirements, Valid Requests exclude: (i) any request that fails to pass authentication and/or parameter verification; (ii) any request initiated due to any hacker attacks on your system/program or any.


<span id="_6-miscellaneous"></span>
## 6. MISCELLANEOUS

BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
