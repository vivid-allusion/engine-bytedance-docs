---
title: "Modifying parameters"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters"
---

This article describes the steps involved in modifying instance parameters.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* The instance currently has no **pending** parameter modification events. You can search and view them by instance ID in the **Planned event list**. For steps, see [Viewing event list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_event_list).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* To ensure the stability of the instance, the console only allows modification of some parameters. If you cannot find the parameters that need to be modified, please [submit a ticket](https://console.byteplus.com/workorder/create) order for processing.

* Some parameters require an instance restart after modification. For details, see the **Whether to restart** column on the modifiable parameters page on the console. We recommend you restart instances during off\-peak hours and ensure that applications have an automatic reconnection mechanism.

* If you need to modify the parameters that take effect after restart, please check whether the instance has an ongoing Online DDL task before modifying it. The restart operation will cause the task to be interrupted, so please proceed with caution. For more information, see [Viewing tickets](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_tickets#.5p-l55yL5bel5Y2V).

* The underlying logic of MySQL will automatically adjust some parameters to preset limits or multiples of preset values, so the final effective value may differ from the value assigned by the user. For details, see [Parameter modification rules](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Parameter_modification_rules).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Parameters**.

5. In the **Parameter list** subtab, click **Batch modification of parameters**, find the target parameter, and enter the modified parameter value or expression in the text box of the **Running value** column.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only some parameters are supported as expressions. For more information about expressions, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Expression_parameter">Expression parameter.</a>   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The values ​​of some parameters must follow certain rules when setting them. For details, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Parameter_modification_rules">Parameter modification rules</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Undo the previous step</strong>: Cancel the modification of the current parameter, undo the previous step, the current parameter has not been modified.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Cancel</strong>: Exit the edit state, all parameters have not been modified.   </div>
   

6. When your changes are complete, click **Submit** at the top left of the page.

7. In the pop\-up **Confirm parameter modifications** dialog box, after confirming that the parameters are modified correctly, select the execution method:

   * **Execution now** (default): Immediately perform the modification parameter operation. If the parameters that need to be restarted are modified, the instance will enter the **Restarting** state, and the instance is not allowed to perform other operations at this time.

   * **Execute during maintainable window**: Execute parameter modification operations during the maintenance window. If the modified parameters require an instance restart, the instance will also be restarted during the maintenance window. For more information about maintainable time windows, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window).


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQs

For common questions about parameter configuration, see [Parameter FAQ](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Parameter_faq).

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceParameters) |Call the DescribeDBInstanceParameters to query the instance parameter list. |
|[ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceParameters) |Call the ModifyDBInstanceParameters to modify instance parameters. |
