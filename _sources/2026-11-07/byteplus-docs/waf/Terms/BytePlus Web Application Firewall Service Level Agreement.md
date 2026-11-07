---
title: "BytePlus Web Application Firewall Service Level Agreement"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/docs-byteplus-web-application-firewa-service-level-agreement"
---

***Last Update: Aug 2023***

During the term of the **BytePlus Customer Agreement** pursuant to which BytePlus Pte. Ltd.("**BytePlus**") has agreed to provide the **BytePlus Web Application Firewall （** "**WAF**" **）**  (the "**Service**") to you (the "**Agreement**"), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this "**SLA**"). Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.

<span id="bbb0e97a"></span>
## 1. Definitions

The following definitions shall apply to this SLA:


*  **"Service Cycle"** , each calendar month is a Service Cycle. Any period less than one month shall be calculated as one full calendar month. The period from the day on which a user starts to use the Service to the very last day of such month will be counted as one Service Cycle. The availability of the Service is calculated independently for each Service Cycle.

*  **"Service Cycle Time"**  is calculated by the total number of days in each Service Cycle \* 24 (hours) \* 60 (minutes).

*  **"Number of Failed Requests"**  The following requests shall be recognized as Failed Requests and included in the statistics of the number of Failed Requests: (i) requests with the response status code of 5XX due to the Service’s own issue; (ii) the normal requests that fail to reach the BytePlus WAF server due to its malfunction（calculated by the daily average number of requests for domains using WAF service seven days before the malfunction).

*  **"Valid Requests"**  are the Service requests forwarded to BytePlus WAF, and that would normally result in a non\-error response. For the avoidance of any doubt, Valid Requests include the requests that conform to the Back\-off Requirements. The following exception scenarios are not counted as Valid Requests: (i) any request that fails to pass authentication and/or parameter verification; (ii) any request sent due to any hacker attacks on your system/program or any; (iii) any request sent before you purchase the service; (ⅳ) any requests sent when your account has an overdue payment.

*  **"Total Number of Valid Requests"**  is the total number of requests for domains under BytePlus WAF protection of the customer's BytePlus account.

*  **"Error Rate"**  means the number of Failed Requests divided by the total number of Valid Requests during that period. Repeated identical requests do not count towards the Error Rate unless they conform to the exception scenarios.

*  **"Unit Time"**  Every 5 minutes shall be deemed as a Unit Time for the calculation of availability, such as 00:00:00 \- 00:04:59 shall be deemed as a Unit Time, and less than 5 minutes will not be counted.

*  **"Error Rate per Unit Time"**  = (Number of Failed Requests per Unit Time / Total Number of Valid Requests per Unit Time) \* 100%.

*  **"Downtime"**  If the Error Rate Per Unit Time exceeds 0.05% and lasts for 10 minutes or longer, such a time period shall be counted into Downtime. Any such duration that is less than 10 minutes will not be counted.

*  **"Downtime within a Service Cycle"**  The accumulated minutes of Downtime in that Service Cycle.


<span id="c83a2ca4"></span>
## **2. Service Levels**

BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.9% during any monthly billing cycle (the "**Service Levels**") as calculated and subject to the exclusions outlined below in Section 5.

*The Monthly Uptime Percentage = (1 \- Downtime within a Service Cycle/Service Cycle Time） 100%* \*

<span id="800b468e"></span>
## 3. Service Credits

Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|**Monthly Uptime Percentage ("MUP")**  |**Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills** |
|---|---|
|99.00% <= MUP < 99.90% |10% |
|MUP < 99.00% |25% |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange the Service Credits into Service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 50% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.

<span id="08a36157"></span>
## **4. Service Credit Application** **and Payment Procedures**

In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:


1. the words “SLA Credit Request” in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected Services.


If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus’s information.

<span id="641479df"></span>
## **5. Exclusions of SLA**

If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:


1. any system maintenance with prior notice by BytePlus to you, including system cutover, maintenance, upgrade and failure simulation test;

2. any features excluded from this SLA;

3. any matters that is out of BytePlus’s control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus;

4. any loss or leak of data, pin or password due to your improper maintenance or improper security measures;

5. any negligence in authorization or mal\-operation by you;

6. any of your failure to comply with documentation or suggestions made available by BytePlus;

7. any Service unavailability or failure of the Service not attributable to BytePlus, including without limitation, force majeure event, your application and/or a domain is blocked due to any reason, and

8. any hacker attacks on your or any user's system and/or application.

9. any service unavailability or failure of the Service not attributable to BytePlus, including without limitation, taking down of your application, or your websites' domain name blocking.

10. any circumstance, under the relevant laws, regulations, codes, rules or agreements, where BytePlus could be exempted from any liability.


<span id="2144c708"></span>
## **6. MISCELLANEOUS**

BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
