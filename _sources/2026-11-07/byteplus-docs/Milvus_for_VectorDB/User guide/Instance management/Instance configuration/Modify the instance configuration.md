---
title: "Modify the instance configuration"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Modify_the_instance_configuration"
---

This topic describes how to modify the configuration of Milvus for VectorDB instances.

<span id="O06rC6PQ"></span>
## Background

Milvus for VectorDB supports adjusting instance settings by modifying instance parameters. For detailed information on supported modifiable parameters and configuration items, see the [parameter list](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Modifiable_parameter_list).

<span id="SJ1pJnQR"></span>
## Prerequisites

Created Dedicated instances with status **Running**. For more information about how to create an instance, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

<span id="VC5fdluG"></span>
## Precautions


* Modifying some instance configuration parameters requires a restart to take effect. Please note the restart scope's impact on business.

* On the **Instance configuration** page, if a parameter’s running value is `-`, the parameter has not been modified since instance creation, and the running value is the parameter’s default value.


<span id="VC5fdluG"></span>
## Procedure


1. Log in to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. On the top navigation bar, select the target project and region.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the instance is not configured with a project, select <strong>All resources</strong>.   </div>
   

3. Click **Instance list** in the left navigation pane.

4. In the **Instances** list, select the **Dedicated** tab, then click the target instance name.

5. On the **Instance details** page, click the **Instance configuration** tab.

6. On the **Instance configuration** page, click **Modify configuration**, then enter or select a new running value in the **Running value** column of the target parameter based on its value range.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can click <strong>Undo the previous step</strong> at the top left of the page to cancel the most recent modification. You can click it multiple times to undo several previous changes.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can modify multiple parameters and submit them together.   </div>
   

7. After completing modifications, click **Submit** at the top left of the page. In the pop\-up **Confirm parameter modifications** dialog box, verify the modifications and then click **OK**.
