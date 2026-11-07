---
title: "Cross-region traffic analysis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Cross-Region-Traffic-Analysis"
---

## Action description

* **Enable**

   * You need to activate Cross Region Traffic Analysis before the Network Advisor (NA) can begin collecting and analyzing log data for **outbound traffic between specified regions**.

   * Cross Region Traffic analysis does not consume your network bandwidth; you can use it with confidence.

   * Traffic analysis for the period before activation is not supported.

* **View**

   Different tabs display different types of cross region traffic information. You can select the tabs as needed to view corresponding trend charts, Top N cross region traffic rankings, etc.

   * The available tabs are as follows:

      * Single tab: Displays the **Outbound traffic** of the specified region.

      * Pair tab: Displays the traffic from the specified region to the peer region.

      * Five\-tuple tab: Displays the traffic from specified region resources to peer region resources.

   * Available Analysis Time Range: Cross\-region traffic data from the current time back 7x24 hours.

   * The selected time must be after Cross Region Traffic Analysis is activated.

   * The maximum specified time range is 24 hours.

   * Cross Region Traffic Analysis and the CloudMonitor traffic collection for Cloud Enterprise Network (CEN)/Transit Router (TR) products may have different collection intervals, which might result in minor data discrepancies.

## Procedures

### Step 1: Enable Cross Region Traffic analysis

1. Log in to the [Cross Region Traffic console](https://console.byteplus.com/netadvisor/trafficAnalysis/cross).

2. In the upper right corner of the page, click **Traffic activation management**.

3. Select the Resource Type, which supports **CEN** and **Transit Router**.

4. Turn on the switch on the right side of the target resource.

### Step 2: View cross region traffic analysis

* **View the cross region traffic analysis for CEN**

   **View Single**

1. Log in to the [Cross Region Traffic console](https://console.byteplus.com/netadvisor/trafficAnalysis/cross).

   2. Select the **CEN** tab.

   3. Select the region, using **China (Beijing)**  as an example.

   4. On the **Single** tab, select the specified time.

      * Overview: View the line chart of the **Total outbound bandwidth** from the region for CENs with cross\-region traffic analysis enabled.

      * View trend: Click **View trend** to the right of the target IP to display its traffic trend chart.

   **View Pair**

1. Log in to the [Cross Region Traffic console](https://console.byteplus.com/netadvisor/trafficAnalysis/cross).

   2. Select the **CEN** tab.

   3. Select the region, using **China (Beijing)**  as an example.

   4. Select the **Pair** tab.

      * Overview: View the **Cross region traffic Top** N bar chart and the Top N rankings of source/destination IP traffic.

      * View trend: Click **View trend** to the right of the target IP to display its traffic trend chart.

   **View Five-tuple**

1. Log in to the [Cross Region Traffic console](https://console.byteplus.com/netadvisor/trafficAnalysis/cross).

   2. Select the **CEN** tab.

   3. Select the region, using **China (Beijing)**  as an example.

   4. Select the **Five\-tuple** tab.

      * Overview: View the **TOP 10 outbound protocol traffic** and **TOP 10 outbound source port traffic**.

      * View trend: Click **View trend** to the right of the target IP to display its traffic trend chart.

* **View the cross region traffic analysis for Transit Router**

   **View Single**

1. Log in to the [Cross Region Traffic console](https://console.byteplus.com/netadvisor/trafficAnalysis/cross).

   2. Select the **Transit Router** tab.

   3. Select the region, using **China (Beijing)**  as an example.

   4. On the **Single** tab, select the specified time.

      * Overview: View the line chart of the **Total outbound bandwidth** from the region for Transit Routers with cross\-region traffic analysis enabled.

      * View trend: Click **View trend** to the right of the target IP to display its traffic trend chart.

   **View Pair**

1. Log in to the [Cross Region Traffic console](https://console.byteplus.com/netadvisor/trafficAnalysis/cross).

   2. Select the **Transit Router** tab.

   3. Select the region, using **China (Beijing)**  as an example.

   4. Select the **Pair** tab.

      * Overview: View the **Cross region traffic Top** N bar chart and the Top N rankings of source/destination IP traffic.

      * View trend: Click **View trend** to the right of the target IP to display its traffic trend chart.

   **View Five-tuple**

1. Log in to the [Cross Region Traffic console](https://console.byteplus.com/netadvisor/trafficAnalysis/cross).

   2. Select the **Transit Router** tab.

   3. Select the region, using **China (Beijing)**  as an example.

   4. Select the **Five\-tuple** tab.

      * Overview: View the **TOP 10 outbound protocol traffic** and **TOP 10 outbound source port traffic**.

      * View trend: Click **View trend** to the right of the target IP to display its traffic trend chart.

## Disable cross region traffic analysis

When you no longer need to analyze cross region traffic, you can disable Cross Region Traffic Analysis.

1. Log in to the [Cross Region Traffic console](https://console.byteplus.com/netadvisor/trafficAnalysis/cross).

2. In the upper right corner of the page, click **Traffic activation management**.

3. Select the Resource Type, which supports CEN and Transit Router.

4. Turn off the switch in the **Actions** column for the target resource.
