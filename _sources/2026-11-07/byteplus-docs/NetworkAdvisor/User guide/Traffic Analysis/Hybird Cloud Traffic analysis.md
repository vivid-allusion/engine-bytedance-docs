---
title: "Hybird Cloud Traffic analysis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Hybird-Cloud-Traffic-Analysis"
---

## Action description

* **Enable**

   * You need to activate Hybrid Cloud Traffic Analysis before the Network Advisor (NA) can begin collecting and analyzing the log data from your **Direct Connect Gateway traffic**.

   * Hybrid Cloud Traffic Analysis does not consume your network bandwidth; you can use it with confidence.

   * Traffic analysis for the period before activation is not supported.

* **View**

   Different tabs display different types of hybrid cloud traffic information. You can select the tabs as needed to view corresponding trend charts, Top N traffic rankings, etc.

   * The available tabs are as follows:

      * Single tab: Displays the inbound and outbound cloud traffic of cloud\-based IPs.

      * Pair tab: Displays the traffic between cloud\-based IPs and on\-premises IPs.

   * Available Analysis Time Range: Traffic data from the current time back 7x24 hours.

   * The selected time must be after Hybrid Cloud Traffic Analysis is activated.

   * The maximum specified time range is 24 hours.

   * Hybrid Cloud Traffic Analysis and the CloudMonitor traffic collection for Direct Connect products may have different collection intervals, which might result in minor data discrepancies.

## Procedures

### Step 1: Enable hybrid cloud traffic analysis

1. Log in to the [Hybrid Cloud Traffic Analysis console](https://console.byteplus.com/netadvisor/trafficAnalysis/hybrid).

2. In the upper right corner of the page, click **Traffic activation management**.

3. Select the target region.

4. Click **Enable** to the right of the target Direct Connect Gateway.

### Step 2: View hybrid cloud traffic analysis results

**View Single**

1. Log in to the [Hybird Cloud Traffic console](https://console.byteplus.com/netadvisor/trafficAnalysis/hybrid).

2. Select **Inbound** or **Outbound**. This example uses Inbound.

3. Select the region, using **China (Beijing)**  as an example.

4. On the **Single** tab, select the specified time.

   * Overview: View the **Inbound total bandwidth** line chart.

   * View trend: Click **View trend** to the right of the target IP to display its traffic trend chart.

**View Pair**

1. Log in to the [hybrid cloud traffic analysis console](https://console.byteplus.com/netadvisor/trafficAnalysis/hybrid).

2. Select **Inbound** or **Outbound**. This example uses Inbound.

3. Select the region, using **China (Beijing)**  as an example.

4. Select the **Pair** tab.

   * Overview: View the **Top source\-destination IP traffic** bar chart​​.

   * View trend: Click **View trend** to the right of the target IP to display its traffic trend chart.

## Disable hybrid cloud traffic analysis

When you no longer need to analyze hybrid cloud traffic, you can disable Hybrid Cloud Traffic Analysis.

1. Log in to the [hybrid cloud traffic analysis console](https://console.byteplus.com/netadvisor/trafficAnalysis/hybrid).

2. In the upper right corner of the page, click **Traffic activation management**.

3. Select the target region.

4. Click **Disable** to the right of the target Direct Connect Gateway.
