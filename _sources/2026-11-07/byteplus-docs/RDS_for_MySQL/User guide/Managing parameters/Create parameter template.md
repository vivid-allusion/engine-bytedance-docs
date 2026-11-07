---
title: "Create parameter template"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_parameter_template"
---

You can create and manage customized parameter templates in the console. This topic describes how to create a customized parameter template.

<span id=".5Yib5bu65Y-C5pWw5qih5p2_"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the region for the parameter template.

3. In the left navigation bar, click **Parameter templates ** to enter the **Custom templates** tab.

4. On the **Custom templates** tab, click **Create parameter template**.

5. On the **Create parameter template** page, complete the following configurations and click **Next step**.



|Parameter |Description |
|---|---|
|Template name |Required. Enter the template name. The template name must be 2 to 64 characters long. |
|Database engine version |Required. Select **MySQL 5.7**, **MySQL 8.0, or MySQL 8.4**. |
|Engine type |Required. Select **InnoDB** or **RocksDB**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This option is supported only when the compatible version is set to MySQL 5.7. When the compatible version is set to MySQL 8.0 and MySQL 8.4, this option is not displayed and the InnoDB engine type is selected by default.</div><br> |
|Template description |Optional. Add the description information of the template to facilitate the application and management of subsequent templates. Supports up to 200 characters. |
|Affiliate project |Required. Select the affiliated project for the allowlists from the drop\-down list. By default, allowlists are assigned to the **default**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">A project is a virtual concept that includes a set of resources, users, and roles. A project allows you to view and manage a group of resources in a unified manner and control the permissions of users and roles to these resources. For more details, refer to <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Product_Overview">Resource management</a>.</div><br> |
|Template parameter |Required Add parameters to the parameter template. You can choose to add **One by one** or **In a batch**.<br><br><br>* **One by one**: In the **Parameter name** column of the **Template parameter** area, enter or select a parameter name, and set the parameter value or expression.<br><br>* **In a batch**: Add multiple parameters at once in the **Add parameters in a batch** text box.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If two addition methods are used simultaneously, the parameters under the two addition methods will be merged. If a duplicate parameter exists, the one added one by one takes precedence.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When adding a parameter, the parameter value must be within the specified range. Otherwise, the parameter template cannot be created.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When adding parameters in batches, you need to connect the parameter name and parameter value with an equal sign (=), and set only one parameter per line.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For the parameters that can be added to parameter templates, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_5_7">List of modifiable parameters in MySQL 5.7</a>, <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_8_0">List of modifiable parameters in MySQL 8.0</a>, and <a href="https://docs.byteplus.com/en/docs/6313/2481764?lang=en">List of modifiable parameters in MySQL 8.4</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Parameters not set in the parameter template use their default values. For details about default values, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_5_7">List of modifiable parameters in MySQL 5.7</a>, <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_8_0">List of modifiable parameters in MySQL 8.0</a>, and <a href="https://docs.byteplus.com/en/docs/6313/2481764?lang=en">List of modifiable parameters in MySQL 8.4</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Delete</strong> in the <strong>operation</strong> column to remove the parameter from the list of parameters to be added to the parameter template.</div><br> |



6. Confirm the parameter information to be added to the parameter template, including the total quantity of parameters to be added and the number of parameters that can be added. After confirmation, click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Click <strong>Previous step</strong> to modify the parameters to be added to the parameter template.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Click <strong>Set all to default values</strong> to set all parameters in the parameter template to their default values. After clicking, the button changes to <strong>Set all to import values</strong>. After you click this button, you can set all parameters in the parameter template to their default values.   </div>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[CreateParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createparametertemplate1) |Call the CreateParameterTemplate API to create a parameter template for a MySQL instance. |
|[DescribeParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeparametertemplate1) |Call the DescribeParameterTemplate API to obtain the information of a specified parameter template. |
