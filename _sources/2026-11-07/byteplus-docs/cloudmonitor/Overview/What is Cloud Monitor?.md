---
title: "What is Cloud Monitor?"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor"
---

The Cloud Monitor service offers an all\-in\-one cloud monitoring and alert solution.

Cloud Monitor collects and visualizes the status of your various cloud resources, helping you gain comprehensive insight into resource health conditions, such as resource utilization, key metric performance data, and running status. The service promptly detects exceptions and sends alert notifications to ensure smooth business operations and improve O&M efficiency.

<span id="1479668e"></span>
## Basic features


* Monitoring dashboard

   A clear and intuitive visual dashboard for monitoring, which allows you to view aggregated data of various metrics and alert trends across regions and cloud services.

* Cloud service monitoring

   You can view metric data for various cloud products, such as ECS, EBM, VKE, database products, and network products. The metric data is collected every 30 seconds or 1 minute, which helps you learn about resource running status in real time.

   In particular, Cloud Monitor allows you to install agent processes in ECS instances, which obtain operating system metrics from ECS with finer granularity and provide more accurate metric data.

* Alert policy

   You can specify custom thresholds for metrics of various cloud products based on your business requirements. When metric data reaches the threshold, an alert is triggered. Alert information is pushed at the earliest opportunity, which helps you promptly obtain information about failed resources and quickly handle exceptions.

* Alert notification

   You can specify multiple alert notification channels, such as SMS messages and phone calls. When an alert is triggered, information about the abnormal resource is pushed to you at the earliest opportunity. You can also set an alert callback address to push detailed alert information to this address by using a POST request. This helps you build intelligent programs to handle alerts.
