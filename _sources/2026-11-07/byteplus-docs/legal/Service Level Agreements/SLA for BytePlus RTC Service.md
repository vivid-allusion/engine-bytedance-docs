---
title: "SLA for BytePlus RTC Service"
product: "BytePlus Legal"
product_code: "legal"
source: "https://docs.byteplus.com/en/docs/legal/docs-sla-for-byteplus-rtc-service"
---

*Last Update: December 13, 2023*

During the term of the **BytePlus Customer Agreement** pursuant to which BytePlus Pte.Ltd. (“**BytePlus**”) has agreed to provide the BytePlus RTC Service (the “**Service**”) to you (the “**Agreement”** ), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this “**SLA**”). Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.

<span id="dae60c5a"></span>
# Service Levels

BytePlus will use commercially reasonable efforts to make the Service available, with a Monthly Uptime Percentage of no less than 99.9% during any monthly billing cycle (the “**Service Levels**”), subject to the exclusions outlined below in Section 4.

<span id="caaa7fac"></span>
# Service Credits

Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the Service Levels are not satisfied, you will be eligible to receive service credits (the “**Service Credits**”) as described below.


|**Monthly Uptime Percentage (or “MUP”)**  |**Percentage of monthly bill for the Service that will be credited to your next monthly bill** |
|---|---|
|99% ≤ MUP＜99.9% |10% |
|95% ≤ MUP＜99% |25% |
|MUP ＜ 95% |50% |



* We will apply any Service Credits only against future Service payments due from you. At our discretion, we may also convert the Service Credit into the equivalent Service hours (i.e., by extending the Service Term).

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 50% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary in this SLA and/or the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failures by us to provide the Service.

<span id="f75162ef"></span>
# Service Credit Application and Payment Procedures

In order to apply for the Service Credits, you must notify BytePlus within thirty (30) days after the end of the preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. The written notification must include:


1. the words “SLA Credit Request” in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming; and

3. the affected Service.


If we confirm that the MUP is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus's information.

<span id="f6f12e72"></span>
# Exclusion of SLA

If any failure to achieve the Service Levels is due to any of the following reasons, this will not contribute towards calculation of the Downtime:


1. any system maintenance with prior notice by BytePlus to you, including system cutover, maintenance, upgrade and failure simulation test;

2. any features excluded from this SLA;

3. any matter that is out of BytePlus’ control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus;

4. any loss or leak of data, pin or password due to your improper maintenance or improper security measures;

5. any negligence in authorization or mal\-operation by you;

6. any of your failure to comply with documentation or suggestions made available by BytePlus;

7. any high concurrency events (including upstream and downstream concurrency) on your end. You shall notify BytePlus in writing at least 3 business days prior to the event, otherwise BytePlus shall not assume any liability against downtime arising therefrom. The high concurrency events include the two scenarios as follows:

* The daily concurrency is less than 10,000 concurrent connections, but the maximum concurrency on a certain date exceeds 10,000 concurrent connections;

* The daily concurrency is over 10,000 concurrent connections, but the maximum concurrency on a certain date is increased by 30% compared to the daily average;

8. any Service unavailability of failure of the Service not attributable to BytePlus, including without limitation, Force Majeure Event, traffic limitation, or if your application and/or domain is blocked due to any reason, and

9. any hacker attacks on your or any user’s system and/or application;

10. unavailability caused by other reasons that have nothing to do with BytePlus;

11. any circumstance, under the relevant laws, regulations, codes, rules or agreements, where BytePlus could be exempted from any liability.


<span id="f99a656e"></span>
# Definitions

The following definitions shall apply to this SLA:


1. **Service Cycle**: Each calendar month is a Service Cycle.

2. **Total Time of a Service Cycle**: Calculated by the total number of days in each Service Cycle \* 24 (hours) \* 60 (minutes).

3. **Total Service Cycle Fee**: The total service fees paid by the customer for the service provided in one service cycle (a calendar month). For the upfront lump sum payment paid by the customer for the service, the monthly service fee equals the lump sum payment divided by the number of months of the service covered by such payment.

4. **Success Rate of Joining Room**: Users need to join the RTC room first in order to make audio and video calls successfully. A user successfully joins a room when the user triggers a call request in the SDK and joins the room successfully. The Success Rate of Joining Room = (the number of successful room joining per Unit Time / the total number of requests to join room per Unit Time) \* 100%.

5. **Unit Time**: Every 5 minutes is considered as Unit Time, e.g., 00:00:00 \- 00:04:59 shall be deemed as a Unit Time.

6. **Downtime**: If the total number of requests to join room per Unit Time is at least 500, and the Success Rate of Joining Room is less than 95.00% and lasts continuously for 5 minutes or longer, such a time period shall be counted as Downtime. Any such duration that is less than 5 minutes will not be considered as Downtime. Downtime does not include any unavailability resulting from any exclusion set forth in Section 4.

7. **Downtime Period**: The accumulated minutes of Downtime in that Service Cycle.

8. **Monthly Uptime Percentage** or **MUP** = (Total Time of a Service Cycle \- Downtime Period) / Total Time of a Service Cycle) × 100%. The Monthly Uptime Percentage will be calculated separately according to the different products in your account of BytePlus RTC.


<span id="9e1f895d"></span>
# Miscellaneous

BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. If so, BytePlus will provide reasonable notice in accordance with the terms of the Agreement. You may also review the most updated version of this SLA on our [website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service. By continuing to use the Service, you are deemed to have accepted the SLA as amended.
