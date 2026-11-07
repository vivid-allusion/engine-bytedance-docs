---
title: "Viewing parameter modification history"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_parameter_modification_history"
---

By viewing the parameter modification history, you can quickly locate the recent modification of the target parameter. This article describes how to view the parameter modification history of an instance.

<span id="注意事项"></span>
## Precautions


* The parameter modification operations selected to be performed within the maintainable time period will be displayed in the parameter modification history list after the maintenance time period is completed.

* The underlying logic of MySQL will automatically adjust some parameters to preset limits or multiples of preset values, so the final effective value may differ from the value assigned by the user. For details, see [Parameter modification rules](https://www.byteplus.com/en/docs/NDB_for_MySQL/Parameter_modification_rules).


<span id="操作步骤"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Parameters**.

5. In the **Parameter modification history** subtab, you can view the parameter modification history.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Support searching target parameters by parameter name and start and end time. Parameter names support fuzzy matching.   </div>
