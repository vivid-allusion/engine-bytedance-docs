---
title: "Editing parameter template"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Editing_parameter_template"
---

After successfully creating a parameter template, you can edit it on the console to modify its name, description, or parameter details. This topic describes how to edit parameter template.

<span id="yIcyXs3n"></span>
## Limitations

Only **Customized templates** can be edited; **System templates** cannot be edited. For more information on creating customized parameter template, refer to [Creating parameter template](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_a_parameter_template).

<span id="HChR92Oo"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. Click **Parameter templates** in the left\-side navigation bar.

4. On the **Customized template ** tab, locate the target template to be edited, and in the **Actions** column on the right, click **Edit**.

5. In the **Modify parameter template** panel, set the following parameters.

   
   |**Name** |**Description** |
   |---|---|
   |Template name |Enter the name of the parameter template. The name needs to meet the following requirements simultaneously:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 8 to 64 characters. |
   |Database engine version |Modification not supported. |
   |Template description |Enter the remarks for the parameter template whose length cannot exceed 200 characters. |
   |Template parameter |You can perform the following modification operations in the **Template parameters** area:<br><br><br>* **Add single parameter**<br><br>   1. Click **Add parameter** at the bottom of the parameter list.<br><br>   2. Select the parameter name to be set from the **Parameter name** drop\-down box.<br><br>   3. Set the parameter value in the input box under **Parameter value**.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you need to add more parameters to the template, click <strong>Add parameters</strong> just below the list, and then repeat the above operation steps to complete the addition of a single parameter.   </div><br>   <br><br>* **Batch add parameters**<br><br>   1. Click **Add parameters in batches** at the lower left corner of the parameter list.<br><br>   2. In the pop\-up dialog box, enter the parameter names and parameter values to be added to the template.<br><br>      Enter in the format of ParameterName=value, and please break lines between multiple sets of data.<br><br>      Example is as follows.<br><br>      ```Plain Text```<br>```      auto_increment_increment=1```<br>```      auto_increment_offset=1```<br>```      ```<br>      <br><br>* **Edit the value of an existing parameter**<br><br>   Find the target parameter in the parameter list, and reset the parameter value in the input box under **Parameter value**.<br><br>* **Delete added parameters**<br><br>   Click **Delete** in the **Actions** column on the right side of the added parameter to remove the parameter from the parameter template.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Each parameter template must contain at least one parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For details on the parameters supported by each database engine version and their value ranges, refer to the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_modifiable_parameters">List of modifiable parameters</a>.</div><br> |
   

6. Click **OK**.


<span id="8A2pX7m5"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[ModifyParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyParameterTemplate) |Call the ModifyParameterTemplate API to modify a parameter template. |
