---
title: "Viewing parameter template"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_parameter_template"
---

NDB for MySQL provides the parameter template function. When you need to configure one or more NDB for MySQL instances with the same parameter values for the same database engine version, you can use the parameter template feature to centralize the management of parameters and quickly apply the parameters in the template to the target instance to improve the efficiency of parameter management and instance configuration. This article describes how to view parameter template information.

<span id="MHRP3Lc5"></span>
## Type of parameter template


|**Type of parameter template** |**Customized template** |**System template** |
|---|---|---|
|Applicable scenarios |Place one or more parameter configurations in a parameter template according to your service requirements. Batch applies these configurations to instances of the same database engine version to improve the efficiency of parameter management and instance configuration. |NDB for MySQL provides a default parameter template for each database engine version, which includes all parameters and default parameter values supported by the version. You can use the system parameter template to quickly restore all parameters of the instance to their default values.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The parameters in the system template are a collection of parameters for all kernel versions.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When applying a parameter template, parameters unsupported by the instance's kernel version are automatically ignored.</div><br> |
|Quantitative limitation |Each root account of BytePlus can create up to 40 customized parameter templates in each region by default. |NDB for MySQL provide the following system parameter templates for different database engine versions:<br><br><br>* veDB_MySQL_8_0_Default parameter template<br><br>* veDB_MySQL_5_7_Default parameter template |
|Supported operations |* [Creating a parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_a_parameter_template)<br><br>* [Apply parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Apply_parameter_template)<br><br>* [Deleting a parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Deleting_a_parameter_template)<br><br>* [Edit parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Editing_parameter_template)<br><br>* [Copy parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Copying_parameter_template) |* [Apply parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Apply_parameter_template)<br><br>* [Copying parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Copying_parameter_template) |


<span id="6hLujdUe"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. Click **Parameter templates** in the left\-side navigation bar. On the parameter template list page, you can view the information of all parameter templates. This includes information such as parameter template name/ID, template classification, template description, database type, applicable version, creator, number of parameters included, whether it includes parameters that take effect after restart, creation and modification time, and supported operations.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can search for the target template in the upper right corner by <strong>Template name</strong> or <strong>Template ID</strong>. Among them, the <strong>Template name</strong> supports fuzzy match.   </div>
   

4. Click the target template name. On the **Parameter template details** page, you can view information such as the template name, description, applicable database engine version, and parameter list included in the template.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Click on the upper right corner<img src="https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg" width="14px" />icon to export the parameter list information contained in the parameter template.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeParameterTemplates](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeParameterTemplates) |Call the DescribeParameterTemplates to query the parameter template list. |
|[DescribeParameterTemplateDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeParameterTemplateDetail) |Call DescribeParameterTemplateDetail to query parameter template details. |
