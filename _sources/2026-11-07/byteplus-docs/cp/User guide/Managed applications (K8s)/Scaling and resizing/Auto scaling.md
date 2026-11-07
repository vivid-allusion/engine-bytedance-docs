---
title: "Auto scaling"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Auto_scaling"
---

This article introduces how to configure automatic elastic scaling policies for managed applications.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

<span id=".5omp57yp5a655pa55byP"></span>
### Capacity scaling methods


* **Manual scaling**: When scaling an application is an urgent requirement, such as during a sudden spike in traffic, you can select manual scaling. For detailed instructions, see [Manual scaling](https://docs.byteplus.com/en/docs/cp/Manual_scaling).

* **Automatic scaling**: When scaling the application is not an urgent requirement, such as during periodic traffic peaks, you can select the automatic scaling method.


<span id=".6Ieq5Yqo5omp57yp562W55Wl"></span>
### An automatic scaling policy


* **Scheduled scaling policy**: Suitable for application scenarios with cyclical resource usage patterns, and is often used in the securities, healthcare, and education industries.

* **Metric scaling policy**: Suitable for application scenarios with sudden traffic spikes and typical periodic traffic, and is mainly used in the internet, gaming, and social platform industries.


<span id=".6Ieq5Yqo5omp57yp6KeE5YiZ"></span>
### Automatic scaling rules


1. **Expected number of replicas = ceiling [ current number of replicas × ( current metric / expected metric ) ]** . Here, 'ceil' means rounding up to the nearest integer.

2. If the calculated scaling ratio is close to 1.0, according to the Kubernetes HPA calculation method: `|scaling ratio - 1.0| <= Value`, the current scaling operation will be skipped. In the community version, the default tolerance Value is 0.1, which is the Value globally configured by the `--horizontal-pod-autoscaler-tolerance` parameter.

3. When both scheduled scaling policies and metric\-based scaling policies are used together, the effective policy relationship is **or**, meaning that if any enabled policy meets its condition, expand or shrink will be triggered.

   For example: With scheduled settings to maintain 1 replica of the instance starting at 20:00 each day, the number of instance replicas will be adjusted to 1 at 20:00. If at 20:05 the CPU utilization reaches 80 percent while the target Value is 40 percent, the number of instance replicas will increase to 1 × (80 / 40) = 2 replicas.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Managed application created. For detailed instructions, see [Create a managed application](https://docs.byteplus.com/en/docs/cp/Managed_applications_K8s).

* To configure scheduled scaling policies, you need to go to the container service console to install the Cronhpa component. For detailed steps, see [Install component](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* Only managed applications deployed to container service VKE clusters support configuring automatic elastic scaling policies.

* Up to 5 automatic scaling policies can be configured.

* You can enable at most one metric\-based scaling policy and one scheduled policy.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the current application.

   1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the target workspace name to enter that workspace.

   4. Select **Application Delivery \> Application Management** in the left navigation bar.

   5. On the application management page, select the target managed application, click the application card, and go to the basic information tab for the current application.

2. Click **Environment** to switch to the application's environment tab.

3. In the environment tab of the current application, click **Elastic Scaling** to switch to the Elastic Scaling tab.

4. On the Elastic Scaling tab, click **Configure Elastic Scaling**.

   * **Configure metric\-based scaling policy**

   
   |Configuration Item |Descriptions |
   |---|---|
   |Scaling policy |Select **the metric strategy**. |
   |Policy Name |Customize the policy name. |
   |Number of instances |Set the minimum and maximum number of instances. When the strategy is triggered, instances will scale within this range. |
   |Scaling metrics |Configuring scaling monitoring metrics allows the system to determine whether scaling is needed based on these metrics. Please configure at least one scaling metric. Scaling metrics support:<br><br><br>* **CPU utilization**: The percentage calculated as `total CPU usage of all Pod instances / total CPU requests of all Pod instances` is used as a monitoring metric. When CPU utilization reaches the target value, scaling is performed.<br><br>* **Memory utilization**: Calculated as `all Pod instance memory usage / all Pod instance memory requests` as a percentage, used as a monitoring metric. When memory utilization reaches the target Value, scaling is performed. |
   |Advanced settings |Optional configurations.<br><br><br>* **Adaptive step size**<br><br>   * **Expand:**  Set the maximum number of instances that can be expanded per minute.<br><br>   * **Scale\-in**: Set the maximum number of instances that can be scaled in per minute.<br><br>* **Stable window:**  During the stable window period, the system tends to enter a steady state. Primarily used to prevent frequent scaling up and down caused by traffic spikes.<br><br>   * **Expand**: Set the expansion stability window. For example, if the stabilization window for expansion is set to 5 seconds, this means that when the expansion condition is triggered, the system will wait for 5 seconds before proceeding. If the conditions for expansion are still met after 5 seconds, expand; otherwise, do not expand.<br><br>   * **Scaling in**: Scaling in stabilization window settings. For example, if the scale\-in stabilization window is set to 300 seconds, when the scale\-in condition is triggered, the system will wait for 300 seconds. If the scale\-down condition is still met after 300 seconds, scale down; otherwise, do not scale down.<br><br>* **Disable scaling in**: After you turn on this feature, the application's instances will never be scaled in, which can effectively prevent business risks caused by scaling in during traffic peaks. Disabled by default. |
   

   * **Configure a scheduled scaling policy**

   
   |Configuration Item |Descriptions |
   |---|---|
   |Scaling policy |In this scenario, select **scheduled policy**. |
   |Policy Name |The policy name. |
   |Scheduled repetition |Click **Add rule** to configure a scheduled rule. When configuring multiple scheduled rules, ensure that the rules do not conflict with each other.<br><br><br>* **Timed repetition**: Supports configuration of the timed repetition cycle by hour, day, week, or Cron expression.<br><br>* **Execution strategy**: When the scheduled time is reached, the number of instances is dynamically scaled to this value.<br><br><br>For example: The first scheduled policy adjusts the number of instances to 10 at 10:00 every day; the second scheduled policy adjusts the number of instances to 2 at 16:00 every day. Between 10:00 and 16:00, the number of application instances is kept at 10, and from 16:00 to 10:00 the following day, the number of application instances is kept at 2. |
   

5. (Optional) The policy status switch defaults to **disabled** and can be changed to **enabled**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Up to one metric scaling policy and one scheduled scaling policy are supported.   </div>
   

6. Click **Confirm** to complete the configuration.

   After configuring and enabling the auto scaling policy, you can verify whether the policy works as expected by observing the number of instances in the **environment \> instance list**.


<span id=".55u45YWz5pON5L2c"></span>
## Related Operations

Once you have configured the application's automatic scaling strategy, you can view the details of the configured strategy on the **environment \> elastic scaling** page. Enable, disable, edit, or delete auto scaling policies as needed.
