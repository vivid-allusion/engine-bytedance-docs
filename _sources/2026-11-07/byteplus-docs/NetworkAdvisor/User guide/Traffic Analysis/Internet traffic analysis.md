---
title: "Internet traffic analysis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Internet-Traffic-Analysis"
---

<span id="m9l2LOfk"></span>
## Action description


* **Enable**

   * You need to activate Internet Traffic Analysis before the Network Advisor (NA) can begin collecting and analyzing log data for internet traffic.

   * Internet Traffic Analysis does not consume your network bandwidth; you can use it with confidence.

   * Traffic analysis for the period before activation is not supported.

* **View**

   Different tabs display different types of internet traffic information. You can select the tabs as needed to view corresponding trend charts, Top N internet traffic rankings, etc.

   * The available tabs are as follows:

      * Single tab: Displays the internet traffic of cloud\-based IPs.

      * Pair tab: Displays the internet traffic between cloud\-based IPs and peer IPs.

      * Five\-tuple tab: Displays internet traffic data for specified Five\-tuple (Cloud IP, Cloud Port, Peer IP, Peer Port, Protocol).

   * Available analysis time ranges are as follows:

      * Single and Pair: Internet traffic data from the current time back 7x24 hours.

      * Five\-tuple: Internet traffic data from the current time back 24 hours.

   * The selected time must be after Internet Traffic Analysis is activated.

   * The maximum specified time range is 24 hours.

   * Internet Traffic Analysis and the CloudMonitor traffic collection for EIP products may have different collection intervals, which might result in minor data discrepancies.


<span id="XOZZUm3T"></span>
## Procedures

<span id=".5byA6YCa5YWs572R5rWB6YeP5YiG5p6Q"></span>
### Step 1: Enable Internet Traffic analysis


1. Log in to the [Internet Traffic console](https://console.byteplus.com/netadvisor/trafficAnalysis/internet).

2. In the upper right corner of the page, click **Traffic activation management**.

3. In the Target Region section, dropdown to select a **Region**.

4. Click **OK** to complete the action.


<span id="bWmQ9GeJ"></span>
### Step 2: View Internet Traffic analysis results


<Tabs>
<Tab zoneid="Zy2mjT3D" title="View Single">
<TabTitle>View Single</TabTitle>

1. Log in to the [Internet Traffic Analysis console](https://console.byteplus.com/netadvisor/trafficAnalysis/internet).

2. Select **Inbound** or **Outbound**. This example uses Inbound.

3. Select the region, using **China (Beijing)**  as an example.

4. On the **Single** tab, select the specified time.

   * Overview: View the **Total inbound bandwidth** line chart and line charts of **Inbound bandwidth by cloud product** (currently supporting ECS, NAT Gateway, CLB, Network Interface, and High\-Availability Virtual IP).

   * View trend: Click **View trend** to the right of the target EIP to display its traffic trend chart.





</Tab>
<Tab zoneid="vai5N9AI" title="View Pair">
<TabTitle>View Pair</TabTitle>

1. Log in[Internet Traffic Analysis console](https://console.byteplus.com/netadvisor/trafficAnalysis/internet).

2. Select **Inbound** or **Outbound**. This example uses Inbound.

3. Select the region, using **China (Beijing)**  as an example.

4. Select the **Pair** tab.

   * Overview: View the **Inbound traffic by city Top 10** bar chart, **Inbound traffic by Line Operator Top 10** bar chart and **On\-premises to cloud traffic Top 10** rankings.

   * View trend: Click **View trend** to the right of the target EIP to display its traffic trend chart.


</Tab>
<Tab zoneid="5CWZ3Icg" title="View Five-tuple">
<TabTitle>View Five-tuple</TabTitle>

1. Log in to the [Internet Traffic Analysis console](https://console.byteplus.com/netadvisor/trafficAnalysis/internet).

2. Select **Inbound** or **Outbound**. This example uses Inbound.

3. Select the region, using **China (Beijing)**  as an example.

4. Select the **Five\-tuple** tab.

   * Overview: View the Inbound traffic Top N bar chart by protocol, Inbound traffic by BytePlus port Top 10 bar chart and Top 10 rankings of on\-premises to cloud traffic.

   * View trend: Click **View trend** to the right of the target EIP to display its traffic trend chart.





</Tab>
</Tabs>


<span id="LIpNQ6fj"></span>
## Disable Internet Traffic analysis

When you no longer need to analyze internet traffic, you can disable Internet Traffic Analysis.


1. Log in to the [Internet Traffic console](https://console.byteplus.com/netadvisor/trafficAnalysis/internet).

2. In the upper right corner of the page, click **Traffic activation management**.

3. In the Target Region section, dropdown to select **Disable**.

4. Click **OK** to complete the action.


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
