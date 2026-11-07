---
title: "BytePlus Cloud Search Service Level Agreement"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/SLA"
---

**Last Update: 16th December, 2024**

During the term of the [BytePlus Customer Agreement](https://docs.byteplus.com/en/docs/legal/docs-customer-agreement) pursuant to which BytePlus Pte. Ltd.(“**BytePlus**”) has agreed to provide the **BytePlus Cloud Search Service** (the “**Service**”) to you (the “**Agreement**”), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this “**SLA**”). Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.

<span id="8c2db943"></span>
# **Service Levels**

BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.90% during any monthly billing cycle (the “**Service Levels**”) as calculated and subject to the exclusions outlined below in Section 4.

Monthly Uptime Percentage is calculated with the following expression：

**Monthly Uptime Percentage = ((Total Service Cycle Minutes \- Service Unavailable Minutes) / Total Service Cycle Minutes) \* 100%** 

<span id="89ec6316"></span>
# **Service Credits**

Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|**Monthly Uptime Percentage ("MUP")**  |**Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills** |
|---|---|
|99.00% <= MUP < 99.90% |15% |
|95.00% <= MUP < 99.00% |30% |
|MUP < 95.00% |100% |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange the Service Credits into Service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 100% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.

<span id="50790e10"></span>
# **Service Credit Application and Payment Procedures**

In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:


1. the words “SLA Credit Request” in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected Services.


If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus’s information.

<span id="f430d30f"></span>
# **Exclusions of SLA**

If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:


1. any system maintenance with prior notice by BytePlus to you, including system cutover, maintenance, upgrade and failure simulation test;

2. any features excluded from this SLA;

3. any matters that is out of BytePlus’s control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus;

4. any loss or leak of data, pin or password due to your improper maintenance or improper security measures;

5. any negligence in authorization or mal\-operation by you;

6. any of your failure to comply with documentation or suggestions made available by BytePlus;

7. any Service unavailability or failure of the Service not attributable to BytePlus, including without limitation, force majeure event, your application and/or a domain is blocked due to any reason, and any hacker attacks on your or any user's system and/or application.

8. the unavailability caused by customers not following product usage documentation or usage recommendations, such as running a single\-node instance or using 0 replicas in the formal production environment; performing frequent data reading, writing, and changing operations when the instance is in an unhealthy state(not Green), CPU utilization is too high, memory load is too high, or disk occupancy is too full(For CPU utilization, memory load, and disk occupancy, Byteplus recommends keeping them all below 50%.).

9. time consumed during instance changes restart and forced restart operations.

10. any Service unavailability caused by human configuration operations.

11. data request failures and other faults caused by potential undisclosed bugs in open source software.

12. any problems caused by security or stability issues with custom plugins uploaded by customers themselves.


<span id="a9b6f9e3"></span>
# **DEFINITIONS**

The following definitions shall apply to this SLA:


* **Instance**: A Cloud Search instance consists of one or more nodes, all nodes in a instance work together to store data.

* **Service Cycle**: A service cycle lasts for one natural month. If a customer uses a Cloud Search instance for less than one month, the cumulative usage time of the instance in that month will be treated as one service cycle.

* **Total Service Cycle Minutes**: It is calculated by multiplying the total number of days in the service cycle by 24 (hours) and 60 (minutes).

* **Service Unavailable**: All continuous attempts by the customer to establish a connection (such as data writing, query operations) with the specified cloud search service instance failed and could not be connected, and this state lasted for more than one minute, which was considered the instance unavailable within that minute.

* **Minutes of Unavailability**: The sum of minutes of unavailability of an instance in a service cycle.

* **Monthly Service Fee**: The total amount of service fees that a customer should pay for a single Cloud Search instance in a natural month. It does not include the portion that has been purchased but not consumed. If a customer pays service fees for multiple months at one time, the monthly service fees will be calculated by apportioning according to the number of months purchased. (The monthly service fee here should exclude the amount deducted or exempted by using vouchers, coupons, discount offers, and service fee reductions, etc.)


<span id="7a97cc5a"></span>
# **MISCELLANEOUS**

BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
