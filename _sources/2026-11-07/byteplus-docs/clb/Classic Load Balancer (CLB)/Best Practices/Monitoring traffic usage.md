---
title: "Monitoring traffic usage"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Monitoring-the-traffic-usage"
---

This section describes how to use the monitoring function to view the Internet traffic and Virtual Private Cloud (VPC) traffic of Classic Load Balancer (CLB), and how to configure alarm policies to timely learn the traffic information.

<span id=".5L2_55So5Zy65pmv"></span>
## Scenarios

When using a CLB instance to distribute traffic, you can check the traffic of the CLB instance in time, or configure the inbound and outbound bandwidth alarm policies for this CLB instance to avoid service failures caused by excessive traffic.

You can also learn the traffic of a public CLB instance or traffic of a private CLB instance bound to an Elastic IP Address (EIP) by checking the CLB traffic or EIP traffic during a certain period of time. If a private CLB instance is not bound to any EIP, you can learn its traffic by checking the CLB traffic during a certain period of time.

After configuring the inbound and outbound bandwidth alarm policies for CLB, you do not need to manually check the CLB traffic from time to time. When the inbound or outbound bandwidth reaches the threshold, the system triggers an alarm and sends an email or SMS to notify the corresponding contacts, so that they can make timely adjustments and avoid service failures caused by excessive traffic.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The alarm contact and the contact group (alarmgroup test) have been created. 

* If an instance is stopped or upgraded, CLB monitoring data may be unavailable. Therefore, ensure that CLB has been running normally for a period of time before viewing its traffic.


<span id=".5p-l55yL5L2_55So5rWB6YeP"></span>
## Viewing the traffic


<Tabs>
<Tab zoneid="Z3m2IoH3OY" title="Viewing the CLB traffic">
<TabTitle>Viewing the CLB traffic</TabTitle>

1. Log in to [the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target region and target project.

3. Click the target CLB instance name.

4. On the **Monitoring** tab, click the **Instance** or **Listener** tab, and select a time period, for example, 1 day.

5. View the inbound and outbound bandwidth statistics of an instance or a listener.


</Tab>
<Tab zoneid="N8m9ce0iNI" title="Viewing the EIP traffic">
<TabTitle>Viewing the EIP traffic</TabTitle>

1. Log in to [the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target region and target project.

3. Click the target CLB instance name.

4. Click the EIP address.

5. Click the **Data Monitoring** tab, and select a time period, for example, 1 day.

6. View the statistical data on metrics, such as the outbound and inbound traffic and outbound and inbound bandwidth.


</Tab>
</Tabs>


<span id=".6YWN572u5ZGK6K2m562W55Wl"></span>
## Configuring an alert policy

The following describes how to configure an alert policy for an instance. You can use a similar method to configure an alert policy for a listener.


1. Log in to [the Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left\-side navigation pane, select **Alert Center \> Alert policy**.

3. On the alert policy page, click the **Create alert policy** button.

4. Configure the basic alarm information, and set the policy name to policy\-clb.

5. Configure the alarm object according to the table below.

   
   |Name |Valid Value |
   |---|---|
   |Resource type |Load Balancer |
   |Region |China (Beijing) |
   |Dimension |Instance |
   |Resources |All<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you select <strong>All</strong>, the alarm policy takes effect on all instances in the current region. If you select <strong>Part</strong>, you need to further select the instances on which the alarm policy takes effect.</div><br> |
   

6. Configure the alarm rule according to the table below.

   
   |Name |Valid Value |
   |---|---|
   |Metric Type |Single indicator |
   |Trigger condition |Average inbound bandwidth in three consecutive cycles (1 cycle = 1 minute) \> 30 Mbit/s<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This triggering condition indicates that the CloudMonitor service detects the inbound bandwidth of the CLB instance every minute, and triggers an alarm if the average value exceeds 30 Mbit/s for three consecutive times.</div><br> |
   |Alarm level |Warning |
   |Effective Time |00:00\-23:59 |
   |Alert sending cycle |5 minutes |
   

7. Configure the notification method in the alarm policy.

   Set **Alarm channel** to Email and **Alarm contact group** to alarmgroup\-test.

8. Click **OK**.
