---
title: "Scaling configuration source FAQ"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Scaling-configuration-source-FAQs"
---

<span id="Oc3uW6IG"></span>
## How many scaling configuration sources can be associated with a scaling group?

At any given time, a scaling group can only be associated with one scaling configuration source.

<span id=".5LiA5Liq5Ly457yp6YWN572u5p2l5rqQ5Y-v5Lul6YCJ5oup5aSa56eN6K6h566X6KeE5qC85ZCX77yf"></span>
## Can multiple instance types be selected for a scaling configuration source?

When the scaling configuration source is a scaling configuration, up to 10 instance types can be associated with the scaling configuration. When the scaling configuration source is an instance launch template, only one instance type can be selected. However, you can select multiple instance types when you associate the instance launch template with a scaling group. For more information, see [Scaling configuration source overview](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources).

<span id=".57uR5a6a5paw55qE5Ly457yp6YWN572u5p2l5rqQ77yM5Lya5b2x5ZON5Ly457yp57uE5Lit5bey5pyJ5a6e5L6L5ZCX77yf"></span>
## Does associating a new scaling configuration source affect existing instances in the scaling group?

No. After you associate a new scaling configuration source with a scaling group, the new scaling configuration source will be used to create instances only in subsequent adjustments. Existing instances in the scaling group are not affected.

<span id=".57uR5a6a5Ly457yp57uE5aSx6LSl77yM5aaC5L2V5o6S5p-l5Y6f5Zug77yf"></span>
## How do I troubleshoot the failure to associate a scaling group?

When you associate a scaling configuration source with a scaling group, confirm that the following requirements are met. Otherwise, the association will fail:


|Scaling policy |Scaling configuration sources requirements |
|---|---|
|Priority policy |The selected instance type and image must be available in the availability zones corresponding to the scaling group's highest\-priority subnet (that is, the first selected subnet). |
|Balanced policy |The selected instance type and image must be available in the availability zones corresponding to all subnets selected for the scaling group. |


<span id=".5L-u5pS55Ly457yp6YWN572u5p2l5rqQ5ZCO77yM5Lya5b2x5ZON5Ly457yp57uE5Lit5bey5pyJ5a6e5L6L5ZCX77yf"></span>
## Does modifying the scaling configuration source affect existing instances in the scaling group?

No. After you modify the scaling configuration source, the new scaling configuration source will be used to create instances only in subsequent adjustments. Existing instances in the scaling group are not affected.

<span id=".6YCa6L-H5Ly457yp6YWN572u5p2l5rqQ5Yib5bu65a6e5L6L5pe277yM5pSv5oyB5ZCM5pe257uR5a6a6L6F5Yqp572R5Y2h5ZCX77yf"></span>
## Can a secondary network interface be mounted to an instance when the instance is created by using a scaling configuration source?

No. Secondary network interfaces cannot be simultaneously created when the scaling group creates instances. After the instances are created, you can mount secondary network interfaces to the instances in the ECS console. For more information, see [Mounting network interfaces to instances](https://docs.byteplus.com/en/docs/ecs/Attaching-and-detaching-secondary-network-interfaces).

<span id=".5Li65LuA5LmI5peg5rOV5oiQ5Yqf6YCJ5oup5a6e5L6L5ZCv5Yqo5qih5p2_77yf"></span>
## Why do I fail to select an instance launch template?

When an instance launch template is used as the scaling configuration source for a scaling group, the template must comply with the scaling policy constraints of the scaling group. In addition, secondary parameter verification must be performed on the template. Failure to meet either requirement will prevent the template from being successfully associated with the scaling group. As described below:


1. Confirm that the template complies with the scaling policy constraints of the scaling group:

   
   |Scaling policy |Scaling configuration sources requirements |
   |---|---|
   |Priority policy |The selected instance type and image must be available in the availability zones corresponding to the scaling group's highest\-priority subnet (that is, the first selected subnet). |
   |Balanced policy |The selected instance type and image must be available in the availability zones corresponding to all subnets selected for the scaling group. |
   

2. Confirm that the template meets the following requirements:

   * The image, security group, and key parameters are configured in the template. The security group in the template belongs to the same VPC as the scaling group.

   * The availability zones selected in the template are the availability zones selected by the scaling group.

   * If a VPC is selected in the template, the VPC must be the same as the VPC of the scaling group. If a subnet is selected in the template but the subnet differs from the subnet of the scaling group, the subnet of the scaling group is used. If a VPC or subnet is not selected in the template, the VPC or subnet of the scaling group is automatically inherited.
