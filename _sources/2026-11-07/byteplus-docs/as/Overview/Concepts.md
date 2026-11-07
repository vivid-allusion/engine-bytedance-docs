---
title: "Concepts"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Feature-list"
---

When using the Auto Scaling (AS) service, you may encounter the following terms. This topic describes common terms.


|Term |Description |
|---|---|
|Scaling group |A scaling group is used to manage a group of instances for the same business scenario. The configuration of a scaling group is predefined, including the VPC to which the instances belong, and the maximum and minimum numbers of instances. |
|Scaling configuration source |Used to define the instance configurations for a scaling group, including those related to compute, memory, network, storage, and security. When the scaling group scales up, new instances are created based on the preset instance configuration. |
|Scaling rule |Defines the conditions for adjustment jobs: the timing and method for triggering scaling\-up or scaling\-down operations. |
|Adjustment type |Indicates the type of condition that triggers an adjustment, such as scheduled scaling, periodic scaling, or manual scaling. |
|Adjustment |Indicates the number of instances to be modified when the trigger conditions are met, for example, increasing the instance count, reducing it, or setting it to a fixed number. |
|Instance in a scaling group |An instance refers to an actually available cloud resource within a scaling group, such as an ECS instance. |
|Expected number of instances |Used to limit the number of instances actually running in the scaling group to a value between the minimum and maximum instance counts. |
|Instance protection |Protected instances are not deleted or moved out during adjustments and health checks. |
|Instance health check |Determines whether an instance is running normally and whether related business is available. This prevents an instance with exceptions from affecting normal business access, improving overall service availability. |
|Scaling log |Records the results after the scaling group executes adjustment jobs. |
|Lifecycle hook |After a scaling rule of the scaling group and the health check are triggered, the lifecycle hook takes effect and target instances enter the **Adding/removal suspended** state. For instances in waiting states, you can perform custom actions until the lifecycle hook times out or you manually call back to complete the wait. |
|Vertical scaling |Vertical scaling refers to adjusting the instance type configuration. This feature allows you to scale up or down the configurations (including vCPU and memory) of pay\-as\-you\-go instances in a scaling group. |
