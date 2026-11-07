---
title: "Growth Marketing(DataFinder) Service Level Agreement"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Growth_Marketing_DataFinder_Service_Level_Agreement"
---

**Effective Date:**  1 April 2026

This Service Level Agreement (the “SLA”) sets forth the service availability metrics and compensation scheme for the **DataFinder** service provided by BytePlus to customers.

<span id="dcca37f6"></span>
## Definitions


* **Service Cycle:**  A service cycle refers to one calendar month.

* **Error Rate:**  For a given period of time, the error rate is calculated as the number of erroneous requests divided by the number of valid requests to the advanced analysis query APIs during that period. Repeated identical requests are not counted towards the error rate.

* **Service Unavailability:**  Service unavailability is measured based on the server\-side error rate. If all advanced analysis query requests of **DataFinder** fail on the server side, the service is deemed unavailable.

* **Period of Service Unavailability:**  Statistics are calculated in units of one minute. If **all** advanced analysis queries fail within a given minute, that minute is deemed a period of service unavailability.

* **Monthly Service Fees:**  On a per–BytePlus account basis, the total service fees incurred by the customer for the use of DataFinder during a service cycle (that is, a calendar month), excluding any portions already purchased but not yet consumed. If the customer purchases a resource package and pays the service fees for multiple months in a lump sum, for any service cycle in which events are consumed from the resource package, the monthly service fees are calculated as: (actual number of events consumed × unit price per event in the resource package).

* **Server\-Side Error Rate:**  Excludes validation\-related errors, timeout errors for complex queries, and errors caused by throttling\-related downgrade measures (including but not limited to excessive concurrent queries and excessive system load), such as reducing concurrency or restricting specific complex queries.


<span id="ba7ef87d"></span>
## Service Availability

<span id="0f455f7d"></span>
### 2.1 Service Availability Calculation

On a per–BytePlus account basis, the service availability of **DataFinder** for each service cycle is calculated as follows:

> Service Availability = ((Total number of minutes in the service cycle − Number of minutes of service unavailability) / Total number of minutes in the service cycle) × 100%

> Note: The total number of one‑minute intervals in a service cycle = 24 × (number of days in the service cycle) × 60.


<span id="cbaa889f"></span>
### 2.2 Service Availability Commitment

The service availability of **DataFinder** shall be no less than 99.5%. If **DataFinder** fails to meet the foregoing service availability commitment, the customer may obtain compensation in accordance with Article 3 of this SLA. **The compensation scope does not include any periods of service unavailability caused by the following reasons:** 


1. System maintenance performed by BytePlus after prior notice to the customer, including but not limited to cutovers, repairs, upgrades, and simulated failure drills.

2. Network or equipment failures or configuration changes of any equipment that does not belong to BytePlus.

3. Hacker attacks against the customer’s applications.

4. Loss or leakage of data, credentials, or passwords caused by the customer’s improper maintenance or failure to keep such information confidential.

5. Negligence by the customer or actions performed under the authorization of the customer.

6. The customer’s failure to follow BytePlus’s product documentation or usage recommendations.

7. Force majeure events.

8. For the cloud‑hosted version, any causes of service unavailability other than those attributable to the DataFinder product itself.


<span id="4ddce4e8"></span>
## Compensation Scheme

<span id="2a9464f4"></span>
### 3.1 Compensation Standard

If the **DataFinder** service under a customer’s account fails to meet the service availability standard in a given month, the amount of compensation will be calculated based on the table below. Compensation is provided **only** in the form of vouchers. Vouchers cannot be redeemed for cash, transferred, or gifted, and invoices cannot be issued for them. Vouchers may only be used to purchase the **DataFinder** product on BytePlus, and the total amount of compensation shall not exceed the monthly service fees actually paid by the customer for the relevant **DataFinder** project in the month in which the service availability commitment was not met (excluding any amounts offset by vouchers, coupons, or service fee waivers).


|Service Availability |Voucher Compensation Amount |
|---|---|
|< 99.5% but ≥ 99.00% |15% of the monthly service fees |
|< 99.00% but ≥ 95.00% |30% of the monthly service fees |
|< 95.00% |100% of the monthly service fees |


<span id="a0c050e3"></span>
### 3.2 Time Limit for Submitting Compensation Claims

The customer may submit a compensation claim for any instance that failed to meet the service availability standard in the preceding month after the fifth (5th) business day of each month. **Compensation claims must be submitted within two (2) months after the end of the month in which the relevant DataFinder project failed to meet the service availability standard. Compensation claims submitted after this time limit will not be accepted.** 

<span id="21ee5eee"></span>
## Miscellaneous

BytePlus has the right to modify the terms of this SLA. If any modifications are made to this SLA, BytePlus will notify you at least 30 days in advance by means of website announcement or email. If you do not agree to the modifications to the SLA made by BytePlus, you have the right to stop using the **DataFinder** service. If you continue to use the **DataFinder** service, you will be deemed to have accepted the modified SLA.
