---
title: "Change the load network VPC of a prepaid resource group"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Change_the_load_network_VPC_of_a_prepaid_resource_group"
---

If you choose the wrong VPC when creating a prepaid resource group or need to replan your network, you can use this feature to replace the VPC of the resource group. This article describes how to replace a Private network VPC or subnet for Dev boxes.

<span id="使用场景"></span>
## Usage scenarios


* The early VPC planning was unreasonable. With the gradual expansion of the business, the original VPC could not meet the demand, and it was necessary to replace the load VPC operation for re\-planning.

* It is hoped that the VPC will connect with the IDC, but the cross\-VPC interconnection cannot be established due to address conflicts. At this point, you need to replace the resource group load VPC, and solve the address conflict problem before you can get through the VPC.


<span id="使用限制"></span>
## Usage Limitations


* The VPC instance that needs to be replaced has been authorized in the global configuration.

* The resource group is in the running state.


<span id="操作步骤"></span>
## Procedure


1. Log in to the Machine Learning Platform console.

2. In the left navigation bar, select Resource Group.

3. Select the resource group for which the load network needs to be replaced, and go to Operations \- \> Change Load Network and SecurityGroup.

4. Select the VPC/subnet/SecurityGroup that needs to be replaced.

5. Confirm the submission.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2ec6733ac604396a0afaf523f051f90~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0caf5ef2a2840ba9d22c1bfb9d314d0~tplv-goo7wpa0wc-image.image) </span>


<span id="执行结果"></span>
## Execution result


* Changing the VPC or subnet will affect the private IP of the existing Dev boxes. Please be careful to remind users in the group to pay attention to the change of the login link after the modification.

* After successfully changing the VPC or subnet,

   * The existing running Dev boxes need to be turned off and then turned on to upgrade to the new VPC network.

   * The existing Dev boxes that are shutting down need to be turned on before they can be upgraded to a new VPC network.

   * New Dev boxes and other loads will use the new VPC network.
