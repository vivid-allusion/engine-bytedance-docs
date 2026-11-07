---
title: "Network Load Balancer Service Level Agreement"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/BytePlus-NLB-Service-Level-Agreement"
---

During the term of the [BytePlus Customer Agreement](https://docs.byteplus.com/en/legal/docs/customer-agreement) pursuant to which BytePlus Pte. Ltd.(**BytePlus**) has agreed to provide the **BytePlus Network Load Balancer Service** (the **Service**) to you (the **Agreement**), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this **SLA**). Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.


1. ## **Service Levels** <span id="eMm4ByrK"></span>


BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.995% for multiple zones and no less than 99.95% for single zone during any monthly billing cycle (the **Service Levels**) as calculated and subject to the exclusions outlined below in Section 4.


2. ## Service Credits <span id="LGj0eIAf"></span>


Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the **Service Credits**) as described below.


|<div style="text-align: center"><br>Monthly Uptime Percentage ("MUP") for single zone</div><br> |<div style="text-align: center"><br>Monthly Uptime Percentage ("MUP") for multiple zones</div><br> |Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills |
|---|---|---|
|<div style="text-align: center"><br>99.00% <= MUP < 99.95%</div><br> |<div style="text-align: center"><br>99.90% <= MUP < 99.995%</div><br> |10% |
|<div style="text-align: center"><br>90.00% <= MUP < 99.00%</div><br> |<div style="text-align: center"><br>99.50% <= MUP < 99.90%</div><br> |25% |
|<div style="text-align: center"><br>MUP < 90.00%</div><br> |<div style="text-align: center"><br>MUP < 99.50%</div><br> |100% |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange the Service Credits into Service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 100% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.


3. ## **Service Credit Application** and Payment Procedures <span id="yfFOkA1H"></span>


In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:


1. the words **SLA Credit Request** in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected Services;


If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus's information.


4. ## **Exclusions of SLA** <span id="ZU8eFBkm"></span>


If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:


1. any system maintenance with prior notice by BytePlus to you, including system cutover, maintenance, upgrade and failure simulation test;

2. any features excluded from this SLA;

3. any matters that is out of BytePlus’s control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus;

4. any loss or leak of data, pin or password due to your improper maintenance or improper security measures;

5. any negligence in authorization or mal\-operation by you;

6. any of your failure to comply with documentation or suggestions made available by BytePlus;

7. any Service unavailability or failure of the Service not attributable to BytePlus, including without limitation, force majeure event, your application and/or a domain is blocked due to any reason, and

8. any hacker attacks on your or any user's system and/or application.

9. any events that result from your failure to configure servers or exceptions on servers;

10. any events that arise because of your business traffic exceeding the type of your purchased Network Load Balancer instance;

11. any events that arise because of your security policy forbids the availability detection network segment 100.64.0.0/10.

5. ## **DEFINITIONS** <span id="6a1tV6i6"></span>


The following definitions shall apply to this SLA:


*  **"Service Cycle"**  means a calendar month.

*  **"Service Cycle in Minutes"**  means the total number of minutes calculated by reference to the following formula: Total number of days in a Service Cycle x 24 (hours) x 60 (minutes).

*  **"Service Downtime"**  means when all continual attempts to connect to a particular listener service on a specified Network Load Balancer instance by the client have failed in any particular minute, the service is considered unavailable for the entire particular minute.

*  **"Instance Downtime in Minutes"**  means the total number of minutes of Service Downtime of all listener services on a single Network Load Balancer instance in a single Service Cycle.

*  **"Instance Service Cycle in Minutes"**  means the total number of Service Cycle in minutes of all listener services on a single Network Load Balancer instance in a single Service Cycle.

*  **"Monthly Service Fee"**  means the total charges paid by you for a single Network Load Balancer instance in one Service Cycle, excluding any part that has been purchased but not consumed. If the customer has paid for several months of service fees in one go, the Monthly Service Fee will be calculated based on the volume of months purchased or the proportion of use.

* **Monthly Uptime Percentage** = (**Instance Service Cycle in Minutes** \- **Instance Downtime in Minutes**) / **Instance Service Cycle in Minutes** × **100%.**  Monthly Uptime Percentage measurements exclude any lack of availability resulting directly or indirectly from any exclusion set forth in Section 4.

6. ## **MISCELLANEOUS** <span id="6b7V9ZGF"></span>


BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
