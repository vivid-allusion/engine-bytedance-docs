---
title: "Configure automatic capacity expansion and reduction for services"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Configure_automatic_capacity_expansion_and_reduction_for_services"
---

Machine Learning Platform supports automatic capacity expansion and reduction configuration of services, which can dynamically scale the number of instances according to the configuration policy, which is convenient for automatic capacity expansion and reduction according to the tidal characteristics of the service.

<span id="操作步骤"></span>
# Procedure


1. Log in to the Machine Learning Platform and click [Model Services] \- [Inference Services] in the left navigation bar to enter the list page.

2. Click [+ Create Service] at the top left of the list page to enter the creation page.

3. Turn on the [Automatic capacity expansion and reduction] switch in the [Resource Configuration] column of the creation page.

4. Perform [timing capacity expansion and reduction] or [index capacity expansion and reduction] policy configuration

   * Timing capacity expansion and reduction

      * Timing capacity expansion and reduction using Cron statement for time configuration, by minute, hour, date, month and week, a total of five parameters, you can set a specific execution time for the task. The specific parameter configuration is shown in the following table:

         
         |**Parameter** |**Parameter Description** |
         |---|---|
         |points |* Represents minutes in execution time.<br><br>* Supports entering numbers between 0\-59, and entering `*`means matching any value. **Optional.**  |
         |time |* Represents the hour in the execution time.<br><br>* Supports entering numbers between 0 and 23, and entering `*`means matching any value. **Optional.**  |
         |day |* Represents the date in the execution time.<br><br>* Supports entering numbers between 1 and 31, and entering `*`means matching any value. **Optional.**  |
         |month |* Represents the month in the execution time.<br><br>* Supports entering numbers between 1\-12, and entering `*`means matching any value. **Optional.**  |
         |week |* Represents the week in the execution time.<br><br>* Support for entering numbers between 0\-6, 0 represents Sunday, and entering `*`means matching any value. **Optional.**  |
         

         * Error Message

         
         |**Cron statement** |**execution time** |
         |---|---|
         |`0 * * * *` |Execute the strategy every hour. |
         |`0 0 * * *` |Execute the strategy at `00:00`every day. |
         |`0 0 * * 0` |Strategies are executed every Sunday at `00:00`. |
         |`0 0 1 * *` |Execute the strategy at `00:00`on the first day of each month. |
         |`0 12 * * *` |Execute the strategy every day `at 12:00`. |
         

      * Supports setting the number of instances to change. After completing the policy configuration, the policy will start at execution time, with automatic capacity expansion and reduction to the set number of instances.

   * Indicator capacity expansion and reduction

   * The indicator capacity expansion and reduction is configured according to the monitoring indicators. The strategy capacity expansion and reduction mechanism is: according to the formula `desiredReplicas = ceil [currentReplicas * (currentMetricValue/desiredMetricValue) ]`Calculate the number of expansion/contraction. When setting multiple monitoring indicators, the maximum number of capacity expansion and reduction calculated according to each indicator is taken as the number of capacity expansion and reduction instances. The specific parameter configuration is shown in the following table:

   ```Plain
     |**Parameter Name** |**Parameter Description** |
     |---|---|
     | CPU Utilization | * Calculated by dividing the total CPU usage of all instances by the total allocated CPU specifications of all instances.\
    ||* Supports input of numbers between 0 and 100. \
    ||* Substitute the set CPU utilization as the `desiredMetricValue` into the formula `desiredReplicas = ceil[currentReplicas * ( currentMetricValue / desiredMetricValue )]` to calculate the `desiredReplicas` as the number of instances for capacity expansion and reduction. \
    || * When the actual CPU utilization reaches the value set in the policy, execute the capacity expansion or reduction policy and change the number of instances to the calculated number. |
    | GPU Utilization | * Calculated by taking the average of the GPU utilization of all instances. GPU utilization metric: DCGM\_FI\_DEV\_GPU\_UTIL\
    || * Supports input of numbers between 0 and 100. \
    || * Substitute the set GPU utilization as the `desiredMetricValue` into the formula `desiredReplicas = ceil[currentReplicas * ( currentMetricValue / desiredMetricValue )]` to calculate the `desiredReplicas` as the number of instances for capacity expansion and reduction. \
    || * When the actual GPU utilization reaches the value set in the policy, execute the capacity expansion or reduction policy and change the number of instances to the calculated number. |
    | Memory Utilization | * Calculated by dividing the total memory usage of all instances by the total allocated memory specifications of all instances. \
    || * Supports input of numbers between 0 and 100. \
    || * Substitute the set memory utilization as the `desiredMetricValue` into the formula `desiredReplicas = ceil[currentReplicas * ( currentMetricValue / desiredMetricValue )]` to calculate the `desiredReplicas` as the number of instances for capacity expansion and reduction. \
    || * When the actual memory utilization reaches the value set in the policy, execute the capacity expansion and reduction policy and change the number of instances to the calculated number. |
     | Minimum Number of Instances | Limits the minimum number of instances for capacity expansion and reduction. **Required.** |
     | Maximum Number of Instances | Limits the maximum number of instances for capacity expansion and reduction. **Required.** |
     | Sampling Frequency | Actual indicators are sampled every 5 seconds. |
     | Capacity Expansion Observation Period | * The observation period is set to avoid frequent changes in the number of instances due to glitches caused by indicator fluctuations. \
     || * The value ranges from 0 to 3600. \
     || * If the observation period is set to 0, capacity expansion is carried out immediately. \
    || * If the observation period is set > 0, and the sampled value is higher than the preset monitoring indicator during the observation period, capacity expansion will be carried out after the observation period ends. |
     | Capacity Reduction Observation Period | * The value ranges from 0 to 3600. \
     || * If the observation period is set to 0, capacity reduction is carried out immediately. \
    || * If the observation period is set > 0, and the sampled value is lower than the preset monitoring indicator during the observation period, capacity reduction will be carried out after the observation period ends. \
     || * The longer the observation period, the longer it takes to trigger capacity reduction. The expected number of instances for elastic capacity expansion and reduction is ultimately determined by the expected number of instances during the observation period and the number of instances at the current moment. |
     | Capacity Expansion Step | The amount of resources to be expanded over a period of time. If the user wants to double the capacity every 15 seconds, they can configure a 100% capacity expansion every 15 seconds until the indicators stabilize or the maximum number of instances is reached. |
     | Capacity Reduction Step | The amount of resources to be reduced over a period of time. If the user wants to reduce 4 instances per minute, they can configure a reduction of 4 instances every 60 seconds until the indicators stabilize or the minimum number of instances is reached.  |
   ```
   

5. In the [upgrade] operation of the created service, the [automatic capacity expansion and reduction] configuration can also be performed, and the specific configuration method is the same as above.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the user manually sets the number of instances of the service through "capacity expansion and reduction", if the service is configured with automatic capacity expansion and reduction capabilities at the same time, the background will automatically reset the number of instances of the service according to the service load.</div>
