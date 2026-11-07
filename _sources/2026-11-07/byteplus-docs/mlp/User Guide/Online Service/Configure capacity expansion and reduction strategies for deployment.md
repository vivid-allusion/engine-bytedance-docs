---
title: "Configure capacity expansion and reduction strategies for deployment"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Configure_capacity_expansion_and_reduction_strategies_for_deployment"
---

<span id="操作步骤"></span>
# Procedure

Based on the multi\-deployment capability update, capacity expansion and reduction will be applied to each deployment. That is, the platform supports manual capacity expansion and reduction and automatic capacity expansion and reduction configuration for each deployment. The automatic capacity expansion and reduction can dynamically scale the number of replicas according to the configuration policy, which is convenient for automatic capacity expansion and reduction according to the tidal characteristics of the service.


1. Log in to the Machine Learning Platform and click "inference services" in the left navigation bar to go to the list page.

2. Click on the service you want to configure to go to the service details page.

3. The platform has two capacity expansion and reduction operations that support deployment. When you need to add a new deployment and configure capacity expansion and reduction, you can click "New Deployment". In the new page, select "Number of replicas" or turn on the "Automatic capacity expansion and reduction" switch.

4. If the "automatic capacity expansion and reduction" switch is turned on, the "timed capacity expansion and reduction" or "indicator capacity expansion and reduction" policy configuration is required

   1. Timing capacity expansion and reduction

      * Timing capacity expansion and reduction uses the `Cron`statement to configure the time, through minutes, hours, dates, months and weeks, a total of five parameters, you can set a specific execution time for the task. The specific parameter configuration is shown in the following table:

         
         |Parameter |Parameter Description |
         |---|---|
         |points |* Represents minutes in execution time.<br><br>* Supports entering numbers between `0-59`, and entering `*`means matching any value. **Optional.**  |
         |time |* Represents the hour in the execution time.<br><br>* Supports entering numbers between `0-23`, and entering `*`means matching any value. **Optional.**  |
         |day |* Represents the date in the execution time.<br><br>* Supports entering numbers between `1-31`, and entering `*`means matching any value. **Optional.**  |
         |month |* Represents the month in the execution time.<br><br>* Supports entering numbers between `1-12`, and entering `*`means matching any value. **Optional.**  |
         |week |* Represents the week in the execution time.<br><br>* Support for entering numbers between `0-6`, `0`represents Sunday, and entering `*`means matching any value. **Optional.**  |
         

      * Supports setting the number of replicas to change. After completing the policy configuration, the policy will start at execution time, with automatic capacity expansion and reduction to the set number of replicas.

         
         |Parameter |Parameter Description |
         |---|---|
         |`0 * * * *` |Execute the strategy every hour. |
         |`0 0 * * *` |Execute the strategy at `00:00`every day. |
         |`0 0 * * 0` |Strategies are executed every Sunday at `00:00`. |
         |`0 0 1 * *` |Execute the strategy at `00:00`on the first day of each month. |
         |`0 12 * * *` |Execute the strategy every day `at 12:00`. |
         

   2. Indicator capacity expansion and reduction

      * The indicator capacity expansion and reduction is configured according to the monitoring indicators. The strategy capacity expansion and reduction mechanism is: according to the formula `desiredReplicas = ceil [currentReplicas * (currentMetricValue/desiredMetricValue) ]`Calculate the number of expansion/contraction. When setting multiple monitoring indicators, the maximum value of the number of capacity expansion and reduction calculated according to each indicator is taken as the number of copies of capacity expansion and reduction. The specific parameter configuration is shown in the following table:

         
         |Parameter |Parameter Description |
         |---|---|
         |CPU utilization |* Calculated by CPU usage for all replicas/total CPU allocation for all replicas.<br><br>* Supports entering numbers between `0-100`.<br><br>* Substitute the set CPU utilization as `desiredMetricValue`into the formula `desiredReplicas = ceil [currentReplicas * (currentMetricValue/desiredMetricValue) ]`to calculate the `desiredReplicas`as the number of replicas to be capacity expansion and reduction. A calculation is made every `15`seconds.<br><br>* Execute the scaling/shrinking policy when the actual CPU utilization reaches the policy setting value, changing the number of replicas to the calculated number. |
         |GPU utilization |* Calculated by averaging all replica GPU utilization. GPU utilization metrics: `DCGM_FI_DEV_GPU_UTIL`<br><br>* Supports entering numbers between `0-100`.<br><br>* Substitute the set GPU utilization as `desiredMetricValue`into the formula `desiredReplicas = ceil [currentReplicas * (currentMetricValue/desiredMetricValue) ]`to calculate the `desiredReplicas`as the number of replicas to be capacity expansion and reduction. A calculation is made every `15`seconds.<br><br>* Execute the scaling/shrinking policy when the actual GPU utilization reaches the policy setting value, changing the number of replicas to the calculated number. |
         |Memory utilization |* Calculated by memory usage for all replicas/total memory allocation for all replicas.<br><br>* Supports entering numbers between `0-100`.<br><br>* Substitute the set memory utilization as `desiredMetricValue`into the formula `desiredReplicas = ceil [currentReplicas * (currentMetricValue/desiredMetricValue) ]`to calculate the `desiredReplicas`as the number of copies to be capacity expansion and reduction. A calculation is made every `15`seconds.<br><br>* When the actual memory utilization reaches the policy setting value, the capacity expansion and reduction policy is executed to change the number of replicas to the calculated number. |
         |minimum number of replicas |Limit the minimum number of replicas for capacity expansion and reduction, and set the value to be `≥ 1`. **Required.**  |
         |Maximum number of replicas |Limit the maximum number of replicas for capacity expansion and reduction to `≥ 1`. **Required.**  |
         |Extended observation period |* The observation period is set to avoid the phenomenon of frequent changes in the number of replicas caused by the fluctuation of the index.<br><br>* The range of values is `0-3600`.<br><br>* The observation period is set to `0`, and the expansion is carried out immediately.<br><br>* The observation period is set to `> 0`. During the observation period, if the sampling values are `all`higher than the preset monitoring indicators, the capacity will be expanded after the observation period ends. |
         |constriction observation period |* The range of values is `0-3600`.<br><br>* The observation period is set to `0`and scaling is performed immediately.<br><br>* The observation period is set to `> 0`. During the observation period, if the sampling values are `all`lower than the preset monitoring indicators, the shrinkage will be carried out after the observation period ends.<br><br>* The longer the observation period, the longer the time required to trigger scaling. The expected number of replicas for the final elastic capacity expansion and reduction will be determined based on the expected number of replicas during the observation period and the number of replicas at the current moment. |
         |expansion step size |The amount of resources to be expanded over time. If you want to double the capacity every 15 seconds, you can configure 100% expansion every 15 seconds `100% expansion every 15`seconds until the scale stabilizes or reaches the maximum number of replicas. |
         |scaling step |The amount of resources scaled down in each period of time. If you want to reduce `4`replicas per minute, you can configure to shrink 4 replicas every 60 seconds.`4 replicas every 60`seconds. Shrink until the index is stable or the minimum number of replicas is reached. |
         

5. In the "capacity expansion and reduction" operation of the created deployment, you can also specify the "number of replicas" and "automatic capacity expansion and reduction" configuration, the specific configuration method is as above.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Manually specifying the "number of replicas" and "automatic capacity expansion and reduction" will not take effect at the same time. When "automatic capacity expansion and reduction" is turned on, manually setting the "number of replicas" will turn off the configuration state, and the background will automatically reset the number of deployed replicas according to the deployment load.</div>


<span id="兼容说明"></span>
# Compatibility Instructions

Capacity expansion and reduction capabilities are not compatible with mGPU capabilities.
