---
title: "Service Level Agreement for ContextSearch"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/ContextSearch_SLA"
---

<span id="mhMHjw8Z"></span>
## **Last Update: June 3, 2026**

During the term of the [BytePlus Customer Agreement](https://docs.byteplus.com/en/legal/docs/customer-agreement) pursuant to which BytePlus Pte. Ltd. ("**BytePlus**") has agreed to provide the **BytePlus ContextSearch Service** (the "**Service**") to you (the "**Agreement**"), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this "**SLA"** ). Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.


1. ## Service Levels <span id="4V5oXXqm"></span>


BytePlus will use all commercially reasonable efforts to make the service available with a Monthly Uptime Percentage no less than **99.90%**  during any monthly billing cycle (the "**Service Levels**") as calculated and subject to the exclusions outlined below in Section 4. Monthly Uptime Percentage is calculated with the following expression： **Monthly Uptime Percentage = ((Total Service Cycle Minutes \- Service Unavailable Minutes) / Total Service Cycle Minutes) \* 100%** 


2. ## Service Credits <span id="1bX0s4C2"></span>


Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below. 


|<div style="text-align: center"><br><strong>Monthly Uptime Percentage ("MUP")</strong></div><br> |**Percentage of monthly bill for the Service that does not meet SLA that will be credited to your future monthly bills **  |
|---|---|
|<div style="text-align: center"><br>99.00% <= MUP < 99.90%</div><br> |<div style="text-align: center"><br>15%</div><br> |
|<div style="text-align: center"><br>95.00% <= MUP < 99.00%</div><br> |<div style="text-align: center"><br>30%</div><br> |
|<div style="text-align: center"><br>MUP < 95.00%</div><br> |<div style="text-align: center"><br>100%</div><br> |



* We will apply any Service Credits only against future service payments otherwise due from you. At our discretion, we may exchange Service Credits into service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1). 

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 50% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account. 


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service. 


3. ## Service Credit Application and Payment Procedures <span id="Yrsigm0a"></span>


In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:


1. the words "SLA Credit Request" in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected services.


If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us. 

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus' information.


4. ## Exclusions of SLA  <span id="MDG1Mpp1"></span>


If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:


1. System maintenance following prior notice to the customer, including cutovers, repairs, upgrades, and simulated failure drills.

2. Failures or configuration adjustments of networks or equipment not owned by BytePlus.

3. Hacker attacks on the customer's applications.

4. Loss or leakage of data, passwords, or credentials caused by the customer's failure to use credentials, improper maintenance, or inadequate confidentiality.

5. Negligence of the customer or operations authorized by the customer.

6. Failure by the customer to follow BytePlus's product documentation or recommendations. For example: using a single\-node or 0\-replica instance in a formal production environment; or performing frequent data read/write/modification operations when the instance is in an unhealthy state (non\-Green), or experiencing high CPU utilization, high memory load, or full disk occupancy (BytePlus recommends maintaining these values below 50%).

7. Data erasure due to local disk downtime, or unavailability caused by reliance on local disks and the data therein as startup dependencies.

8. Time consumed during instance modification restarts or forced restarts.

9. Service unavailability caused by manual configuration errors.

10. Failures such as data request errors caused by undisclosed bugs in open\-source software.

11. Security or stability issues caused by custom plugins uploaded by the customer.

12. Force majeure events.

5. ## Definitions <span id="CIiVEAGg"></span>


The following definitions shall apply to this SLA:


*  **"Service Cycle":**  A service cycle refers to one natural month. If a customer uses the ContextSearch service for less than one month, the service cycle shall be the cumulative usage time of the instance within that month.

*  **"Total Service Cycle Minutes":**  Calculated as the total **number of days** in a single instance's service cycle x **24**(hours) x 60(minutes).

*  **"Service Unavailability":**  If all consecutive attempts by a customer to establish a connection with a specified ContextSearch service instance (e.g., data writing, querying) fail and cannot be connected, and this state persists for more than one minute, the instance is deemed unavailable for that minute.

*  **"Unavailability Minutes":**  The sum of minutes during which a single instance is unavailable within a service cycle.

*  **"Monthly Service Fee":**  The total service fee payable by the customer for a single ContextSearch instance within one service cycle.

6. ## Miscellaneous <span id="uSqMXpg3"></span>


BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.
