---
title: "Apply parameter template"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Apply_parameter_template"
---

This article describes how to apply parameter templates.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* The instance currently has no **pending** parameter modification events. You can search and view them by instance ID in the **Planned event list**. For steps, see [Viewing event list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_event_list).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If the parameter template you choose contains parameters need to restart the instance to take affect, the instance will restart after applying the parameter template. Restart the instance The time\-consuming of restarting an instance depends on the load status of the instance. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database connection flashes on the business. During the restart process of a read\-only node, the corresponding nodes will be unavailable, and the load of the current read\-only node will be transferred to other nodes that meet the conditions. Proceed after accurately evaluating the impact of the restart.

* The underlying logic of MySQL will automatically adjust some parameters to preset limits or multiples of preset values, so the final effective value may differ from the value assigned by the user. For details, see [Parameter modification rules](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Parameter_modification_rules).

* A maximum of 20 instances of batch application parameter templates can be selected at a time, and all instances must have the same **database version**.


<span id=".5Li65Y2V5Liq5a6e5L6L5bqU55So5Y-C5pWw5qih5p2_"></span>
## Applying parameter templates to a single instance


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Parameters**.

5. In the **Parameter list** subtab, click **Apply parameter template**.

6. On the **Select parameter template** page, select the **parameter template** and **Execution method** to apply.

   * **Execute now** (default): Execute the parameter template operation immediately. If the selected parameter template contains parameters that require the instance to be restarted to take effect, the instance will enter the **restarting** state and other operations are not allowed on the instance.

   * **Execute during maintainable window**: Execute the application parameter template operation during the maintenance window. If the selected parameter template contains parameters that require the instance to be restarted to take effect, the instance will also be restarted during the maintenance window. For more information about maintainable time windows, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the parameter template is successfully applied, you can view the modification records of the parameters modified in this parameter template application in the <strong>Parameters</strong> \> <strong>Parameter modification history</strong> subtab of the target instance. For specific steps, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_parameter_modification_history">Viewing parameter modification history</a>.   </div>
   

<span id=".5om56YeP5bqU55So5Y-C5pWw5qih5p2_"></span>
## Batch apply parameter template

<span id=".5pa55byP5LiA77ya5Li65a6e5L6L5bqU55So5Y-C5pWw5qih5p2_"></span>
### Method 1: Apply parameter templates to the instance


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instance list** page, select multiple target instances.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A maximum of 20 instances can be selected simultaneously, and all instances must have the same database\-compatible version.   </div>
   

4. Select **Instance list** at the bottom of the page  **...**  \> **Apply parameter template**.

5. In the **Parameter templates** area of the **Batch apply parameter template** page, check the target template and click **Next step**.

6. In the **Confirm information** area, see how the template parameter values compare to the target instance parameter values. After confirming that it is correct, select the **Execution method** and click **OK**.

   * **Execute now** (default): Execute the parameter template operation immediately. If the selected parameter template contains parameters that require the instance to be restarted to take effect, the instance will enter the **restarting** state and other operations are not allowed on the instance.

   * **Execute during maintainable window**: Execute the application parameter template operation during the maintenance window. If the selected parameter template contains parameters that require the instance to be restarted to take effect, the instance will also be restarted during the maintenance window. For more information about maintainable time windows, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the parameter template is successfully applied, you can view the modification records of the parameters modified in this parameter template application in the <strong>Parameters</strong> \> <strong>Parameter modification history</strong> subtab of the target instance. For specific steps, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_parameter_modification_history">Viewing parameter modification history</a>.   </div>
   

<span id=".5pa55byP5LqM77ya5bqU55So5Y-C5pWw5qih5p2_5Yiw5a6e5L6L"></span>
### Method 2: Apply parameter templates to instances


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. Click **Parameter templates** in the left\-side navigation bar.

4. In the **Customized template** subtab, click **Apply to instance** for the target template **Actions** column.

5. On the **Apply parameter template to instance** page, in the **Select Instance** area, check the target instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Support for selecting up to 20 instances simultaneously.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the <strong>Selected</strong> area, click <strong>×</strong> after the instance name to unapply to the instance, or click <img src="https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_780fa292e1f1e020b9db018da34cb501.jpg" width="16px" /> icon to cancel all instances.   </div>
   

6. After the selection is complete, view the comparison between the template parameter value and the target instance parameter value in the **Parameter comparison** area. After confirming that it is correct, select the **Execution method** and click **OK**.

   * **Execute now** (default): Execute the parameter template operation immediately. If the selected parameter template contains parameters that require the instance to be restarted to take effect, the instance will enter the **restarting** state and other operations are not allowed on the instance.

   * **Execute during maintainable window**: Execute the application parameter template operation during the maintenance window. If the selected parameter template contains parameters that require the instance to be restarted to take effect, the instance will also be restarted during the maintenance window. For more information about maintainable time windows, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the parameter template is successfully applied, you can view the modification records of the parameters modified in this parameter template application in the <strong>Parameters</strong> \> <strong>Parameter modification history</strong> subtab of the target instance. For specific steps, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_parameter_modification_history">Viewing parameter modification history</a>.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
### Related APIs


|API |Description |
|---|---|
|[ApplyParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ApplyParameterTemplate) |Call the ApplyParameterTemplate to apply the parameter template. |
