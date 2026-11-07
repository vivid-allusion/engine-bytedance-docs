---
title: "BytePlus ECS_Service Level Agreement"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/BytePlus-ECS-Service-Level-Agreement"
---

**Last Update: 12th December,2024**

During the term of the [BytePlus Customer Agreement](https://docs.byteplus.com/en/legal/docs/customer-agreement) pursuant to which BytePlus Pte. Ltd.(“**BytePlus**”) has agreed to provide the **BytePlus** **ECS** **Service** (the “**Service**”) to you (the “**Agreement**”), the Service will be subject to the service level metrics set out below in this Service Level Agreement (this “**SLA**”).Capitalized terms used in this SLA, but not defined in this SLA, have the meaning stated in the Agreement.

This Service Level Agreement (SLA) specifies the service availability level indicators and compensation plans for the cloud server services (Elastic Compute Service, ECS) that BytePlus provides to customers. In this agreement, the cloud server services (ECS) include cloud servers, elastic block storage, GPU cloud servers, elastic bare metal servers, and high\-performance computing GPU cloud servers, among others. Please note that, unless otherwise agreed upon, this agreement does not apply to instances and specification families of ECS that are in public beta or by invitation testing.

<span id="_1-definitions"></span>
## 1. **DEFINITIONS**

The following definitions shall apply to this SLA:


*  **"Service Cycle"**  , each calendar month is a service cycle.

*  **"Total Minutes of a Single\-instance Service Cycle"**  is calculated by the total number of days in each Service Cycle \* 24 (hours) \* 60 (minutes).

*  **"Instance Unavailability"**  means when an ECS cannot communicate with any IP address in both directions (inbound/outbound) via TCP or UDP protocol, and this state lasts for more than one minute, it is deemed that the ECS instance within that minute is unavailable.

*  **"Number of Minutes of Single\-instance Service Unavailability"**  means sum of minutes of unavailability for a single ECS instance within a service cycle.

*  **"Single\-region Multi\-availability Zone Service Unavailability"**  means if a user's ECS instances are deployed in at least two availability zones in the same region (hereinafter referred to as 'single\-region multi\-AZ'), and if in any one of the availability zones within that region all of the user's ECS instances become unavailable, and the ECS instances in other availability zones within the same region also become unavailable at the same time (hereinafter referred to as 'ECS instances unavailable in other availability zones within the same region'), then these ECS instances unavailable in other availability zones within the same region are considered as a single\-region multi\-AZ service unavailability."

*  **"Minutes of Single\-instance Single\-region Multi\-AZ Service Unavailability"**  means the total number of minutes of service unavailability for a single ECS instance across multiple availability zones within the same region during a service period."

*  **"Monthly Service Fee"**  means the total amount of service fees paid by the customer for a single ECS instance in a service period, excluding any part that has been purchased but not yet consumed. If the customer has paid for the service fees of several months in one lump sum, then the monthly service fees will be proportionally allocated according to the number of months purchased or the quantity of usage."


<span id="_2-service-levels"></span>
## 2. **Service Levels**

<span id="_2-1-service-availability-calculation-method"></span>
### 2.1 Service Availability Calculation Method

The service availability of ECS will be calculated based on the service period, calculating the availability of each ECS instance in the following two dimensions separately:

(1) Single Instance Dimension:

Service Availability = (Total Minutes in Single Instance Service Period \- Minutes of Single Instance Service Unavailability) / Total Minutes in Single Instance Service Period × 100%

(2) Single Region Multi\-Availability Zone Dimension:

Service Availability = (Total Minutes in Single Instance Service Period \- Minutes of Unavailability for Single Instance Single Region Multi\-AZ Service) / Total Minutes in Single Instance Service Period × 100%

<span id="_2-2-service-availability-commitment"></span>
### 2.2 Service Availability Commitment

For the single instance dimension, BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.975% during any monthly billing cycle (the “**Service Levels**”) as calculated and subject to the exclusions outlined below in Section 4.

For the single region multi\-availability zone dimension, BytePlus will use all commercially reasonable efforts to make the Service available with a Monthly Uptime Percentage no less than 99.995% during any monthly billing cycle (the “**Service Levels**”) as calculated and subject to the exclusions outlined below in Section 5.

<span id="_3-service-credits"></span>
## 3. Service Credits

Subject to the terms and conditions of the Agreement, and your full compliance of the Agreement, in the event that the above Service Levels are not satisfied, you will be eligible to receive service credits (the "**Service Credits**") as described below.


|<div style="text-align: center"><br>Monthly Uptime Percentage ("MUP")</div><br><br><br><div style="text-align: center"><br>For the single instance dimension</div><br> |Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills |
|---|---|
|<div style="text-align: center"><br>99% <= MUP < 99.975%</div><br> |10% |
|<div style="text-align: center"><br>95% <= MUP < 99%</div><br> |25% |
|<div style="text-align: center"><br>MUP< 95%</div><br> |100% |
|<div style="text-align: center"><br><strong>Monthly Uptime Percentage ("MUP")</strong></div><br><br><br><div style="text-align: center"><br><strong>For the single region multi\-availability zone dimension</strong></div><br> |**Percentage of monthly bill for the Service which does not meet SLA that will be credited to your future monthly bills** |
|<div style="text-align: center"><br>99% <= MUP < 99.995%</div><br> |10% |
|<div style="text-align: center"><br>95% <= MUP < 99%</div><br> |25% |
|<div style="text-align: center"><br>MUP< 95%</div><br> |100% |



* We will apply any Service Credits only against future Service payments otherwise due from you. At our discretion, we may exchange the Service Credits into Service hours.

* Service Credits will be applicable and issued only if the credit amount for the applicable monthly billing cycle is greater than US one dollar (US$1).

* The aggregate maximum amount of Service Credits you can claim in a single monthly billing cycle shall not exceed 100% of such monthly service fee. Service Credits will not entitle you to any refund or other payment from BytePlus. Service Credits may not be transferred or applied to any other account.


Notwithstanding anything to the contrary hereunder and under the Agreement, you agree and acknowledge that the Service Credits (if eligible) are the sole and exclusive remedy for any unavailability, non\-performance, or other failure by us to provide the Service.

<span id="_4-service-credit-application-and-payment-procedures"></span>
## 4. **Service Credit Application** and Payment Procedures

In order to apply for the Service Credits, you must notify BytePlus within 30 days after the end of preceding calendar month where you become eligible to receive the Service Credits, and provide BytePlus with sufficient supporting information and materials evidencing the occurrence of the failure of Service Levels. Such written notification must include:

1. the words “SLA Credit Request” in the subject line;

2. the dates, times, and BytePlus regions of each lack of availability incident that you are claiming;

3. the affected Services;

If the MUP of such a request is confirmed by us and is less than the Service Levels, then we will issue the Service Credits to you within one billing cycle following the month in which your request is confirmed by us.

If you fail to meet the aforesaid requirements, your eligibility to receive the Service Credits may be forfeited. In case of any disputes regarding the Service Credits, BytePlus shall be entitled to make a determination in good faith based on BytePlus’s information.

<span id="_5-exclusions-of-sla"></span>
## 5. **Exclusions of SLA**

If any failure to achieve the Service Levels is due to any of the following reasons, you will not be eligible for the Service Credits:


1. any system maintenance with prior notice by BytePlus to you, including system cutover, maintenance, upgrade and failure simulation test;

2. any features excluded from this SLA;

3. any matters that is out of BytePlus’s control or resulting from the software, hardware, network, equipment or resources that are not provided by BytePlus;

4. any loss or leak of data, pin or password due to your improper maintenance or improper security measures;

5. any negligence in authorization or mal\-operation by you;

6. any of your failure to comply with documentation or suggestions made available by BytePlus;

7. any Service unavailability or failure of the Service not attributable to BytePlus, including without limitation, force majeure event, your application and/or a domain is blocked due to any reason, and

8. any hacker attacks on your or any user's system and/or application.

9. Caused by any force majeure.


<span id="_6-miscellaneous"></span>
## 6. **MISCELLANEOUS**

BytePlus has the right to amend this SLA as appropriate or necessary in light of changes in due course. You may review the most updated version of this SLA on our [Website](https://www.byteplus.com/en). If you disagree with such revisions to be made by BytePlus, you should cease using the Service; by continuing to use the Service, you are deemed to have accepted this SLA as amended.

&nbsp;
