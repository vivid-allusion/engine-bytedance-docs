---
title: "Scaling configuration source overview"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources"
---

Scaling configuration sources define the compute, storage, network, and security capabilities of cloud resources such as ECS instances. These configurations are used to create cloud resource instances during elastic scaling.

<span id=".5Ly457yp6YWN572u5p2l5rqQ57G75Z6L"></span>
## Types of scaling configuration sources

Currently, two source types are supported: scaling configuration and instance launch template. You can refer to the table below to select the appropriate source:


|Difference |Scaling configuration |Launch template |
|---|---|---|
|Creation type |Created in the Auto Scaling console. For more information, see [Creating scaling configuration](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration). |This is a feature of ECS and can be created in the ECS console. For more information, see [Overview of instance launch templates](https://docs.byteplus.com/en/docs/ecs/Launch-template-overview). |
|Billing method |"Pay\-as\-you\-go" and "spot instance" instances can be created. |"Pay\-as\-you\-go" and "spot instance" instances can be created. |
|Sequentially ordered instance name/hostname |When a scaling group is associated with the same scaling configuration, the starting number of instance names for different scaling\-out activities will increment based on the maximum sequential number among existing names. All instance names within the scaling group are sequentially ordered and unique. |When a scaling group is associated with the same launch template, the instance names are sequentially ordered and unique only for a single scaling\-out activity. However, instance names may repeat across different scaling\-out activities. |
|Parameter validation |* Parameters are validated when you create a scaling configuration. If required parameters are missing, creation fails.<br><br>* When a scaling configuration is used as the scaling configuration source for a scaling group, the configuration must comply with the scaling policy constraints of the scaling group. Otherwise, the scaling configuration fails to be associated with the scaling group. For more information, see [Scaling configuration source restrictions](https://docs.byteplus.com/en/docs/as/Associating-a-scaling-configuration-source-with-a-scaling-group#.5rOo5oSP5LqL6aG5). |* When you create an instance launch template, parameters are not validated. Except for the instance type, all other parameters are optional.<br><br>* When an instance launch template is used as the scaling configuration source for a scaling group, the template must comply with the scaling policy constraints of the scaling group (For more information, see [Scaling configuration source restrictions](https://docs.byteplus.com/en/docs/as/Associating-a-scaling-configuration-source-with-a-scaling-group#.5rOo5oSP5LqL6aG5)). In addition, secondary parameter verification must be performed on the template (For more information, see [Instance launch template restrictions](https://docs.byteplus.com/en/docs/as/Associating-a-scaling-configuration-source-with-a-scaling-group?lang=en#.6YCJ5oup5ZCv5Yqo5qih5p2_)). Failure to meet either requirement will prevent the template from being successfully associated with the scaling group. |
|Multiple instance types |When you create a scaling configuration, you can select multiple instance types simultaneously. |When you create an instance launch template, only one instance type can be selected. However, when you associate the instance launch template with a scaling group, you can add more instance types. |
|Instance type weight |Not supported |Supported |
|Procedure |After you create a scaling group, you can create a scaling configuration and associate it with the scaling group. |After you create an instance launch template, you can select the template to create a scaling group, or create a scaling group first and then select the template. |
|Change method |* Modifying parameters of a single scaling configuration is supported, but version management is not supported.<br><br>* A single scaling group can contain multiple scaling configurations. |* Modifying parameters of a single template or version is not supported, but version management is supported. You can change parameters by creating a new template or version.<br><br>* A single scaling group can contain only one instance launch template. |


<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* After you associate a scaling configuration source with a scaling group, you can modify the scaling configuration source or associate a new scaling configuration source with the scaling group at any time. The new configuration source will be used only for the next instance creation. Existing instances in the scaling group will not be affected.

* You can select multiple instance types for a scaling configuration source. If scale\-out fails for a specific instance type due to insufficient stock or other reasons, the scaling group will automatically use other types to create instances. This increases fault tolerance and improves availability.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Up to 10 scaling configurations can be created for each scaling group.

* Up to 10 instance types can be selected for each scaling configuration source.

* Only one instance launch template can be selected for each scaling group.

* Only one scaling configuration source can be associated with a scaling group.
