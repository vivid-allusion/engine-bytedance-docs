---
title: "Editing parameter template"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/edit-parameter-template"
---

After successfully creating a parameter template, you can edit it on the console to modify its name, description, or parameter details. This topic describes how to edit parameter template.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Only **Customized templates** can be edited; **System templates** cannot be edited. For more information on creating customized parameter template, refer to [Creating parameter template](https://docs.byteplus.com/en/docs/mongodb/create-parameter-template).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, choose **NoSQL Database\> MongoDB \> Parameter templates**.

4. Under the **Customized template** sub\-tab, locate the target template to be edited and click **Edit** in the **Actions** column on the right.

5. In the **Modify parameter template** panel, set the following parameters.

   
   |Parameter |Editable? |Description |
   |---|---|---|
   |Template name |Yes |Enter the name of the parameter template modified. The name needs to meet the following requirements simultaneously:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 2 to 64 characters. |
   |Database version |No |No |
   |Template description |Yes |Enter the remarks for the parameter template whose length cannot exceed 200 characters. |
   |Template parameters |Yes |You can perform the following modification operations in the **Template parameters** area:<br><br><br>* Add individual parameters<br><br>   1. Select the parameter name to be set from the **Parameter name** drop\-down box.<br><br>   2. Set the parameter value in the input box under **Parameter value**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to add more parameters to the template, click <strong>Add parameters</strong> just below the list, and then repeat the above operation steps to complete the addition of a single parameter.   </div><br>   <br><br>* Delete added parameters<br><br>   Click **Delete** in the **Actions** column on the right side of the added parameter to remove the parameter from the parameter template.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, only MongoDB replica set instances support the parameter template function. Therefore, when creating a parameter template, only parameters supported by replica set instances can be added to the template.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Each parameter template must contain at least one parameter. For details of the parameters supported by each database version and the value range of the parameters, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/supported-parameter">Supported parameters</a>.</div><br> |
   

6. click **OK**.
