---
title: "Private network performance monitoring"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Private-network-performance-monitoring"
---

Cloud Network Performance lets you view the average delay between different regions of BytePlus and between availability zones or access points within the same region to help you choose the best region or zone to deploy services.

## Action description

* The performance data is for reference only. The BytePlus platform does not guarantee its accuracy; actual operating data prevails.

* The BytePlus platform builds a dedicated cluster for performance monitoring, which regularly sends and receives probes and aggregates data into the console. Probing resources are completely independent of your resources and do not consume any of your resources.

## View intra\-region private network performance

1. Log in to the [Private Network Performance Monitoring console](https://console.byteplus.com/netadvisor/performance/cloud?tab=inner&type=chart).

2. In the top menu bar, select the **Intra\-region private network performance** tab.

3. Select the target region you want to monitor, such as **China (Beijing)** . You can view the **Average private network latency between different Availability Zones within the same region**.

4. Click a cell in the chart to view the latency trend between the two Availability Zones.

## View inter\-region private network performance

1. Log in to the [Private Network Performance Monitoring console](https://console.byteplus.com/netadvisor/performance/cloud?tab=inner&type=chart).

2. At the top left, select the **Inter\-region private network performance** tab.

3. Check multiple regions. For example, **China (Beijing), China (Shanghai), China (Guangzhou)** .

   * **Chart view**:

      1. Select the **Chart view** tab to view the average delay between regions.

      2. Click a cell in the chart to view the latency trend between the two regions, as well as the average latency and latency trend between different Availability Zones across the two regions.

   * **Map view:**

      1. Select the **Map view** tab to view the average delay between regions.

      2. Hover the mouse over the connection line between two different regions, then click **View details** in the pop\-up window to see the latency trend between those two regions **.**
