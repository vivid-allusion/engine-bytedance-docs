---
title: "Expiration and overdue payments"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Expiration_and_overdue_payments"
---

To prevent business interruptions from service suspension or resource reclamation, it is crucial to understand the policies for instance expiration and overdue payments. This guide details the lifecycle and consequences for both subscription\-based and pay\-as\-you\-go instances, including grace periods and service status changes. You can use this information to ensure timely renewal or account recharge, maintaining continuous and stable business operations.

<span id="6ba97e5f"></span>
## Subscription\-based instance expiration

After your subscription\-based instance expires, we will retain the service for a period of time, after which the service will be automatically suspended and the resources will be reclaimed. The specific process is as follows:


|Time point |Service status |Impact |
|---|---|---|
|**Before expiration** |**Running** |All features are available for normal use. |
|**Within 12 hours after expiration** |**Running** |The service will continue to run, providing you with a buffer period. |
|**12 hours to 30 days after expiration** |**Expired and suspended** |Protection features will stop, but data forwarding capabilities will be retained. |
|**30 days after expiration** |**Expired and reclaimed** |The instance will be completely reclaimed, and all services (including data forwarding) will be stopped. |


<span id="b9f31b93"></span>
## Pay\-as\-you\-go instance overdue payments

If the available balance in your account is less than the outstanding bill, your account will be considered overdue. When your account becomes overdue, you will receive a notification via SMS or email. Please recharge and settle the bill within 2 hours of your account becoming overdue; otherwise, you will not be able to use the relevant features of the LLM Application Firewall.


* **Overdue for more than 15 days**: The service will be suspended, and the firewall will retain only data forwarding capabilities and will no longer provide protection.

* **Overdue for more than 30 days**: The instance will be reclaimed, and your business may be interrupted.


To ensure the stable operation of your business, please maintain a sufficient account balance.
