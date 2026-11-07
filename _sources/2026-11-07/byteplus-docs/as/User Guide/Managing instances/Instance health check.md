---
title: "Instance health check"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Health-checks"
---

The instance health check capability is jointly provided by Auto Scaling and Load Balancer.

<span id=".5by55oCn5Ly457yp5YGl5bq35qOA5p-l"></span>
## Auto Scaling health check

Once an instance joins a scaling group, the health check feature is enabled immediately by default. The instance status is monitored every 5 minutes. If an instance shows an **Error** status, it is marked as unhealthy, and the scaling group will automatically remove the unhealthy instance. This effectively prevents business disruptions resulting from delayed detection of such instances.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you do not need the health check feature, you can also <a href="https://docs.byteplus.com/en/docs/as/Modifying-the-health-check-policy-of-a-scaling-group">disable scaling group health check</a>. After instance health check is disabled, the scaling group will no longer process unhealthy instances.</div>


<span id=".6LSf6L295Z2H6KGh5YGl5bq35qOA5p-l"></span>
## Load Balancer health check

When a scaling group is associated with a load balancer and health check is enabled on the listener, the scaling group automatically removes or deletes unhealthy instances detected by the listener from both the scaling group and the backend server group. This helps prevent business disruptions caused by delayed detection of unhealthy instances.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The health check feature of Load Balancer mainly monitors instance availability. Unlike Auto Scaling, it can mitigate the impact of instance failures on overall availability to a certain extent. For more information, see <a href="https://docs.byteplus.com/en/docs/clb/Health-check-01">CLB health check</a> and <a href="https://docs.byteplus.com/en/docs/clb/ALB-Health-check">ALB health check</a>.</div>
