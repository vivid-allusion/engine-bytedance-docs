---
title: "SLA for BytePlus CDN Service"
product: "BytePlus Legal"
product_code: "legal"
source: "https://docs.byteplus.com/en/docs/legal/docs-sla-for-byteplus-cdn-service"
---

*Last Update: June 02, 2022*

During the term of the BytePlus Customer Agreement pursuant to which BytePlus Pte.Ltd. (“BytePlus”) has agreed to provide the BytePlus CDN Service (the “Service”) to you (the “Agreement”), the Service will be subject to the service level metrics set out below in this Service Level Agreement ( this “SLA”). Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.

<span id="1. Service Level"></span>
# 1. Service Level

BytePlus will use all commercially reasonable efforts to make the Service Available with a Monthly Uptime Percentage no less than 99.9% during any monthly billing cycle (the “Service Levels”) as calculated and subject to the exclusions outlined below in Section 4.

The Monthly Uptime Percentage shall be calculated per Billing Cycle, covering CDN Services for all domains under a particular BytePlus account of a Customer (excluding domain whose monthly request volume less than 1 million), and calculated as follows:

**The Monthly Uptime Percentage = (1 – Downtime within a Billing Cycle / Total Time of a Billing Cycle) × 100%.** 

<span id="2. Service Credits"></span>
# 2. Service Credits

Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels were not satisfied, you will be eligible to receive a service credit (the “Service Credit”) as described below.


| | |
|---|---|
|**Monthly Uptime Percentage(“MUP”)**  |**Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills** |
|99% ≤ MUP＜99.90% |10% |
|MUP＜99% |25% |


We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange the Service Credit into Service hours.

A Service Credit will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

The aggregate maximum number of Service Credit you can claim in a single monthly billing cycle shall not exceed 25% of such monthly service fee. Service Credit will not entitle you to any refund or other payment from BytePlus. Service Credit may not be transferred or applied to any other account.

Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credit (if eligible) is the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.

<span id="3. Service Credit Application and Payment Procedures"></span>
# 3. Service Credit Application and Payment Procedures

In order to apply for the Service Credit, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credit, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of SLA. Such written notification also must include:


1. the words “SLA Credit Request” in the subject line.

2. the dates, times of each lack of availability incident that you are claiming.

3. the affected Service.


If the monthly Uptime Percentage of such request is confirmed by us and is less than the Service Levels, then we will issue the Service Credit to you within one billing cycle following the month in which your request is confirmed by us.

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credit may be forfeited. In case of any disputes regarding the Service Credit, BytePlus shall be entitled to make a determination in good faith based on BytePlus’s information.

<span id="4. Exclusion of SLA"></span>
# 4. Exclusion of SLA

If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credit:


1. any system maintenance with prior notice by BytePlus to you, including system cutover, maintenance, upgrade and failure simulation test.

2. any features excluded from this SLA.

3. any matters that is out of BytePlus’s control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus.

4. any lose or leak of data, pin or password due to your improper maintenance or improper security measures.

5. any negligence in authorization or mal\-operation by you.

6. any of your failure to comply with documentation or suggestions made available by BytePlus.

7. any Service unavailability of failure of the Service not attributable to BytePlus, including without limitation, force majeure event, your application and/or domain is blocked due to any reason, and

8. any hacker attacks on your or any user’s system and/or application.


<span id="5. Definitions"></span>
# 5. Definitions

The following definitions shall apply to this SLA:

a.Billing Cycle: Each calendar month is a service cycle. Any period less than one month shall be calculated as one full calendar month.

b.Total Time of a billing Cycle: Calculated by the actual number of days in that calendar month \* 24 (hours) \* 60 (minutes).

c.Number of Failed Requests: Requests with the response status code of “5XX” due to CDN’s own issue and the normal requests that fail to reach the CDN server due to the CDN server malfunction shall be recognized as a Failed Request and included in the statistics of the number of Failed Requests. Among others, the number of Failed Requests that fail to reach the CDN server = ∑ the average number of requests to the faulty server per unit in the preceding 7 days \* the time of malfunction.

d.Total Number of Valid Requests: the total number of requests for the CDN Service from the domain under a particular BytePlus account of the Customer.

e.Error Rate Per 5 Minutes: Error Rate Per 5 Minutes = (Failed Requests per 5 minutes / Total Number of Valid Requests per 5 minutes) \*100%

f.Unit Time: every 5 minutes shall be deemed as a Unit Time for the calculation of availability, such as 00:00:00 \- 00:04:59 shall be deemed as a Unit Time.

g.Downtime: If the error rate per Unit Time exceeds 0.05% and lasts for 10 minutes or longer, such a time period shall be counted into Downtime. Any such duration that is less than 10 minutes will not be counted.

h.Downtime within a billing Cycle: The accumulated minutes of Downtime in that Service Cycle.

i.Monthly Service Fee: The total charge incurred for CDN Services of a particular BytePlus account of a Customer in that calendar month.

<span id="6. Miscellaneous"></span>
# 6. Miscellaneous

BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our website. If you disagree with such revisions to be made by BytePlus, you should cease using the Service. By continuing to use the Service, you are deemed to have accepted this SLA as amended.
