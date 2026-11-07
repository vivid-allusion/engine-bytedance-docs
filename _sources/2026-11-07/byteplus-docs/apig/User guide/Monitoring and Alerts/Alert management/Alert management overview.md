---
title: "Alert management overview"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Alert_Management_Overview"
---

The API Gateway and [Vital Managed Service for Prometheus (VMP)](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus) are naturally integrated, allowing you to configure alerting rules for instances or services of the API Gateway through the VMP to timely alert you to abnormal conditions. API Gateway currently supports configuring alerting rules in the following 3 ways:


* **Enable alerts with one click (recommended)** : Based on the **default template for APIG instance/service**, quickly enable default alerts at the instance or service level with one click, greatly simplifying the alert configuration process. For action details, please refer to [One-click alert activation](https://docs.byteplus.com/en/docs/apig/One-click_alert_activation).

* **Create using a template**: Based on the API Gateway's builtin alerting rule templates, quickly configure a set of alerting rules for target resources in batch. APIG alerting rule templates encapsulate commonly used alerting rules and corresponding PromQL statements, making it convenient for users to quickly configure alerts with low entry barriers. For action details, please refer to [Creating alert rules based on a template](https://docs.byteplus.com/en/docs/apig/Alert_Management_Overview).

* **Manually create**: Manually configure a single alert rule through a PromQL statement. While it is more complex to get started, it allows for more business\-specific alerting capabilities based on your business needs. For action details, please refer to [Creating an alerting rule manually.](https://docs.byteplus.com/en/docs/apig/Creating_an_alerting_rule_manually)
