---
title: "Viewing parameter modification history"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_parameter_modification_history"
---

This topic describes the procedure for viewing the parameter modification history.

<span id="precautions"></span>
## Precautions

Due to the fact that the underlying MySQL logic automatically adjusts some parameters to preset limits or integer multiples of the preset values, the final values that take effect may differ from the values assigned by the user. In the parameter modification history, only the values that take effect in the instance are recorded, not the user\-assigned values that have been adjusted.

<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>All resources</strong> at this step.</div>



3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click the target instance name.

5. Click the **Parameters** tab at the top of the page.

6. Click the **MySQL parameter modification history** to view the parameter modification history.


<span id="related-apis"></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeDBInstanceParametersLog](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstanceparameterslog) |Call the DescribeDBInstanceParametersLog interface to query the modification history of instance parameters. |
