---
title: "Internet performance monitoring"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Internet-performance-monitoring"
---

Internet performance monitoring lets you view the average latency of access to BytePlus resources across different Regions. This helps you select the optimal Region for deploying your services.​​

## Action description

* The data provided by performance monitoring is for reference only. The BytePlus does not guarantee its accuracy. Please rely on actual operation data.

* The BytePlus builds a separate cluster for performance monitoring, periodically sending and receiving probe packets and aggregating the data to the console. Probe resources are completely independent of your resources and **do not consume any of your resources**.

## View Internet performance monitoring

1. Log in to the [Internet Network Performance console](https://console.byteplus.com/netadvisor/performance/internet?groupType=province&regionId=cn-beijing).

2. At the top left corner, select the **China** or **Global** tab as needed. This topic uses **China** as an example.

3. Select the target region you want to monitor, such as **China (Beijing)** .

4. Hover your mouse over an area on the map to view **The average latency for resources in that area accessing the specified target region over the internet**.

   * Red Dot: Indicates the specified target region.

   * Color: The color represents the latency for resources in that area to access the specified target region over the internet.

   * Table: Displays the latency from different areas and Line Operators to the specified target region.

5. Use the filters to narrow down the results by **Area**, **Line Operator**, **Latency**, and other criteria as needed.
