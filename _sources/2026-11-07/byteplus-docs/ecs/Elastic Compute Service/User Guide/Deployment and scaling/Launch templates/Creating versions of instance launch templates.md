---
title: "Creating versions of instance launch templates"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating-launch-template-versions"
---

You can create multiple versions of an instance launch template, and each version can store completely different configuration information. By default, the first version of the template is the default version. You can also specify any version as the default version.

<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


* When you create a version, not all configuration information is validated. Therefore, if any configuration information is incorrect, you can modify it when you purchase an instance.

* Version numbers are assigned sequentially based on the order in which they are created. You cannot manually specify a version number. After you delete a version, the numbers of the remaining versions do not change or shift forward to fill the gap.


You can use one of the following methods to create a version of an instance launch template.

<span id=".6YCa6L-H5ZCR5a-85Yib5bu654mI5pys"></span>
## Create a version by following the wizard


1. Log in to the [Launch Templates console](https://console.byteplus.com/ecs/template).

2. In the top menu bar, select a region.

3. In the template list, click the "New Version" button in the "Actions" column of the target template to go to the "New Version" page.

4. The parameters required to create a version are generally the same as those required to purchase an ECS instance. The following table describes the parameters specific to version creation. The actual parameters displayed in the console prevail. For more information, see [Purchasing ECS instances via wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   
   |Differential parameterDifferential parameter |DescriptionDescription |
   |---|---|
   |Basic configuration, Network configuration, and Custom configuration |Except for "Instance Type", all other parameters are optional. You can leave the optional parameters empty and configure them when you purchase instances.<br><br><br>* The supported instance types displayed in the console prevail. |
   |Subnet and Secondary network interface |Only IP addresses automatically assigned by the platform are supported. |
   |Login credentialsLogin credentials |Only SSH key pairs can be stored as login credentials in the template. You can leave this parameter empty and configure it when you purchase instances.<br><br><br>* If you want to associate your template with a [scaling group](https://docs.byteplus.com/en/docs/ecs/Associating-launch-templates-with-Auto-Scaling), you need to select "Key Pair". Otherwise, you cannot associate your template with a scaling group.Only SSH key pairs can be stored as login credentials in the template. You can leave this parameter empty and configure it when you purchase instances.<br><br>* If you want to associate your template with a [scaling group](https://docs.byteplus.com/en/docs/ecs/Associating-launch-templates-with-Auto-Scaling), you need to select "Key Pair". Otherwise, you cannot associate your template with a scaling group. |
   |Instance template |Select the instance launch template for the version. |
   

5. Click the "Create Now" button to complete the operation.


<span id=".6YCa6L-H5a6e5L6L6LSt5Lmw6aG15Yib5bu654mI5pys"></span>
## Create a version on the instance purchase page


1. Log in to the [Launch Templates console](https://console.byteplus.com/ecs/template).

2. In the top menu bar, select a region.

2. When you [purchase an ECS instance via the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances), click the "Save as a launch template" button in the "Confirm" step.

3. Select the method for saving the template. In this example, "Version" is selected. Select the instance launch template to which the version belongs.

4. Click the "Save" button to complete the operation.

   * To continue instance creation, click "Return to Create Instances" to go back to the "Confirm" step.

   * To view new versions, click "View New Version" to go to the "Version" tab.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operation

[Purchasing an instance based on an instance launch template or version](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-a-launch-template-or-version)
