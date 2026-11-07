---
title: "Modifying parameters"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Modifying_parameters"
---

HBase allows you to customize some parameter values. This article describes how to modify instance parameters in the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance must be in the **Running** state. For more information about instance states, see [Instance status description](https://docs.byteplus.com/en/docs/HBase/Instance_status_description).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Modifying some parameters causes the instance to restart automatically. The new parameter values take effect after the instance restarts. For more information about parameters that require a restart to take effect, see [List of modifiable parameters](https://docs.byteplus.com/en/docs/HBase/List_of_modifiable_parameters).

* Instance restart will cause connection interruption. It is recommended to modify relevant parameters during off\-peak business hours and ensure that the business has a reconnection mechanism.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Parameters**.

5. On the **Current parameter** tab, click **Modify parameters**.

6. Find the target parameter, set a new value in the **Running value** column, and click **Submit** in the upper\-left corner.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can modify multiple parameters simultaneously.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Set the parameter value according to the value range shown in the <strong>Reference value</strong> column.   </div>
   

7. In the pop\-up dialog box, confirm the parameters to be modified and their corresponding values, then click **OK**.
