---
title: "Creating a parameter template"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_a_parameter_template"
---

You can place one or more parameter configurations in a parameter template based on business needs, and apply these configurations in batches to instances of the same database version to improve the efficiency of parameter management and instance configuration. This article describes how to create a custom parameter template.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. Click **Parameter templates** in the left\-side navigation bar.

4. In the **Custom templates** subtab, click **Create parameter template** to configure the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Template name |Parameter template name. The rules are as follows:<br><br><br>* Can only contain Chinese, letters, digits, underscores(_) and hyphens(\-).<br><br>* The length is 8~64 characters.<br><br>* Cannot start with digits, hyphen (\-) or underscore (_). |
   |Database engine version |Support **MySQL 8.0** (default) or **MySQL 5.7**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Different database engine versions support different modifiable parameters, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_modifiable_parameters_in_mysql_8_0">List of modifiable parameters in MySQL 8.0</a> and <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_modifiable_parameters_in_mysql_5_7">List of modifiable parameters in MySQL 5.7</a>.</div><br> |
   |Template description |Enter the parameter template description information, and the description content length is 0 to 200 characters. |
   |Template parameter |Add parameters to templates, support single addition and batch addition.<br><br><br>* **Single add**<br><br>     Click **Add parameters**, select the target parameter in the drop\-down list of the **Parameter name** column, and set the **Parameter value** based on the **Parameter range**.<br><br>* **Batch Add**<br><br>     Click **Add parameters in batches**, enter the parameters and parameter values according to the prompts in the pop\-up dialogue. You need to connect the parameter names and parameter values with an equal sign (=), and only set one parameter per line.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only some parameters are supported as expressions. For more information about expressions, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Expression_parameter">Expression parameter</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The underlying logic of MySQL will automatically adjust some parameters to preset limits or multiples of preset values, so the final effective value may differ from the value assigned by the user. For details, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Parameter_modification_rules">Parameter modification rules</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Delete</strong> in the <strong>Actions</strong> column to delete the parameter from the list of parameters to be added to the parameter template.</div><br> |
   

5. After confirming that it is correct, click OK.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[CreateParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateParameterTemplate) |Call the CreateParameterTemplate to create a parameter template. |
