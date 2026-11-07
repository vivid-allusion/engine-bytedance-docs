---
title: "Creating instance launch templates"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating-launch-templates"
---

When you create an instance launch template, not all configuration information is validated. Therefore, if any configuration information is incorrect, you can modify it when you purchase an instance.

You can use one of the following methods to create an instance launch template.

<span id=".6YCa6L-H5ZCR5a-85Yib5bu65a6e5L6L5ZCv5Yqo5qih5p2_"></span>
## Create an instance launch template by following the wizard


1. Log in to the [Launch Templates console](https://console.byteplus.com/ecs/template).

2. In the top menu bar, select a region.

3. Click "Create Template" to go to the "Create Template" page.

4. The parameters required to create a launch template are generally the same as those required to purchase an ECS instance. The following table describes the parameters specific to template creation. The actual parameters displayed in the console prevail. For more information, see [Purchasing ECS instances by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   
   |Differential parameter |Description |
   |---|---|
   |Clone template |This parameter is used to create an instance launch template from an existing template. In this example, this parameter is not configured. For information about how to configure the parameter, see [Create an instance launch template by cloning a template](https://docs.byteplus.com/en/docs/ecs/Creating-launch-templates#.6YCa6L-H5qih5p2_5YWL6ZqG5Yib5bu65a6e5L6L5ZCv5Yqo5qih5p2_). |
   |Basic configuration, Network configuration, and Custom configuration |* Except for "Instance Type", all other parameters are optional. You can leave the optional parameters empty and configure them when you purchase instances.<br><br>* The supported instance types displayed in the console prevail. |
   |Subnet and Secondary network interface |Only IP addresses automatically assigned by the platform are supported. |
   |Login credentials |Only SSH key pairs can be stored as login credentials in the template. You can leave this parameter empty and configure it when you purchase instances.<br><br><br>* If you want to [associate your template with a scaling group](https://docs.byteplus.com/en/docs/ecs/Associating-launch-templates-with-Auto-Scaling), you need to select "Key Pair". Otherwise, you cannot associate your template with a scaling group. |
   |Name |The name of the instance launch template. |
   

5. Click Create Now to complete the actions.


<span id=".6YCa6L-H5qih5p2_5YWL6ZqG5Yib5bu65a6e5L6L5ZCv5Yqo5qih5p2_"></span>
## Create an instance launch template by cloning a template


1. Log in to the [Launch Templates console](https://console.byteplus.com/ecs/template).

2. In the top menu bar, select a region.

3. Click "Create Template" to go to the "Create Template" page.

4. The parameters required to create a launch template are generally the same as those required to purchase an ECS instance. The following table describes the parameters specific to template creation. The actual parameters displayed in the console prevail. For more information, see [Purchasing ECS instances by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   
   |Differential parameter |Description |
   |---|---|
   |Clone template |After you select the name of an existing template and its version, the configuration information from that version is quickly copied and filled in the corresponding fields. You only need to modify the parameters that do not meet your business requirements. |
   |Basic configuration, Network configuration, and Custom configuration |Except for "Instance Type", all other parameters are optional. You can leave the optional parameters empty and configure them when you purchase instances. |
   |Subnet and Secondary network interface |Only IP addresses automatically assigned by the platform are supported. |
   |Login credentials |Only SSH key pairs can be stored as login credentials in the template. You can leave this parameter empty and configure it when you purchase instances. |
   |Name |The name of the instance launch template. |
   

5. Click Create Now to complete the actions.


<span id=".6YCa6L-H5bey5pyJ5a6e5L6L5Yib5bu65a6e5L6L5ZCv5Yqo5qih5p2_"></span>
## Create an instance launch template by using an existing instance


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region of the target instance.

3. On the Instances page, click "... \> Instance settings \> Save as Template" in the "Actions" column of the instance.

4. Confirm the configuration information. If the configuration does not meet your business requirements, click the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_761d50efa63019e6e502a1316fa70e78.png) </span> icon to go to the corresponding configuration page.

5. After you confirm that the configuration information is correct, enter the name of the instance launch template.

6. Click Create Now to complete the actions.


<span id=".6YCa6L-H5a6e5L6L6LSt5Lmw6aG15Yib5bu65a6e5L6L5ZCv5Yqo5qih5p2_"></span>
## Create an instance launch template on the instance purchase page


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. When you [purchase an ECS instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances), click the "Save as a launch template" button in the "Confirm" step.

3. Select the method for saving the template. In this example, "Template" is selected. Enter the name of the instance launch template.

4. Click the "Save" button to complete the operation.

   * To continue instance creation, click "Return to Create Instances" to go back to the "Confirm" step.

   * To view the new template, click "View new Template" to go to the "Launch Templates" page.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operation

[Purchasing an instance based on an instance launch template or version](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-a-launch-template-or-version)
