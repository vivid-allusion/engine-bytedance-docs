---
title: "Creating a parameter template"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Creating_a_parameter_template"
---

RDS for PostgreSQL supports the creation of parameter templates to achieve templated configuration of instance parameters. This topic describes how to create parameter templates.

<span id="tiKJpCtC"></span>
## Precautions


* Parameter templates have no project attributes and are not attributed to a project.

* An account can create up to 100 parameter templates in one region.


<span id="fBiECqMi"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper left corner of the top menu bar, select the project and region to which the parameter template belongs.

3. In the left navigation bar, click **Parameter templates ** to enter the **Custom templates** tab.

4. On the **Custom templates** tab, click **Create parameter template**.

5. On the **Create parameter template** page, after completing the following configuration, click **OK**.



|**Configuration item** |**Is it required?**  |**Note** |
|---|---|---|
|Template name<br><br> |Yes |Fill in the name of the parameter template. The template name should satisfy the following rules:<br><br><br>* Can only contain Chinese characters, letters, digits, underscores (_) and hyphens(\-).<br><br>* 2 to 64 characters in length.<br><br>* Cannot start with a digit or a hyphen (\-). |
|Database engine version |Yes |Select the database engine version of the parameter template.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Parameter templates can only be applied by instances with the same version of the database engine.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Modifying the database engine version after creating a parameter template is not supported. Please set it carefully.</div><br> |
|Template description |No |Add the description information of the template to facilitate the application and management of subsequent templates. Supports up to 200 characters. |
|Template parameters<br><br> |Yes |Add parameters to the parameter template. You can choose to add **One by one** or **In batches**.<br><br><br>* **One by one**<br><br>   1. In the **Template parameters** area, click **Add parameters** in the **Template parameters** area.<br><br>   2. In the **Parameter name** column, enter a parameter name or select the parameter you want to set in the drop\-down list and set the parameter value.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Repeat the above steps to add multiple parameters to the parameter template.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Click <strong>Delete</strong> in the <strong>Action</strong> column to remove the added parameter.   </div><br>   <br><br>* **In batches**<br><br>   1. In the **Template parameters** area, click **Add parameters in batches**.<br><br>   2. In the **Template parameters** text box in the **Add parameters in batches** window that pops up, after adding one or more parameters as parameterName=ParameterValue, click **OK**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If two addition methods are used simultaneously, the parameters under the two addition methods will be merged. If the same parameter is added by two addition methods, the parameter value is subject to the setting in the one\-by\-one addition method.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When adding parameters, the parameter value needs to be set within the modifiable range of the parameter, otherwise the creation task of the parameter template will not be submitted.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When adding parameters in batches, you need to connect the parameter name and parameter value with an equal sign (=), and set only one parameter per line.</div><br> |


<span id="Q4zrIsex"></span>
## Related APIs


|API |Note |
|---|---|
|[CreateParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateParameterTemplate) |Call CreateParameterTemplate API to create a parameter template. |
