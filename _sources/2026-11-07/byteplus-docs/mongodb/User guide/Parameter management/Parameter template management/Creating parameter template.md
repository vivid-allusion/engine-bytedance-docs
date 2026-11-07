---
title: "Creating parameter template"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/create-parameter-template"
---

Document Database for MongoDB provides a parameter template function. When you need to configure one or more identical parameter values for MongoDB instances of the same database version, you can use the parameter template function to centrally manage parameters and quickly apply the parameters in the template to the target instance to improve the efficiency of parameter management and instance configuration. This topic describes how to create parameter template.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Each root account of BytePlus can create up to 100 customized parameter templates in each region by default.

* Currently, only MongoDB replica set instances support the parameter template function. Therefore, when creating a parameter template, only parameters supported by replica set instances can be added to the template.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. In the left navigation bar, choose **NoSQL Database\> MongoDB \> Parameter templates**.

4. Under the **Customized template** sub\-tab, click **Create parameter template**.

5. In **Create parameter template** panel, set the following parameters.

   
   |Parameter |Required |Description |
   |---|---|---|
   |Template name |Yes |Enter the name of the parameter template. The name needs to meet the following requirements simultaneously:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 2 to 64 characters. |
   |Database version |Yes |Select the MongoDB database version to which the parameter template is adapted from the drop\-down list. Valid values:<br><br><br>* MongoDB 4.2<br><br>* MongoDB 4.4<br><br>* MongoDB 5.0<br><br>* MongoDB 6.0<br><br>* MongoDB 8.0<br><br>* MongoDB 8.3 |
   |Template description |No |Enter the remarks for the parameter template whose length cannot exceed 200 characters. |
   |Template parameters |Yes |You can perform the following operations in the **Template parameters** area:<br><br><br>* Add parameter<br><br>   1. Select the parameter name to be set from the **Parameter name** drop\-down box.<br><br>   2. Set the parameter value in the input box under **Parameter value**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to add more parameters to the template, click <strong>Add parameters</strong> just below the list, and then repeat the above operation steps to complete the addition of a single parameter.   </div><br>   <br><br>* Delete added parameters<br><br>   Click **Delete** in the **Actions** column on the right side of the added parameter to remove the parameter from the parameter template.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, only MongoDB replica set instances support the parameter template function. Therefore, when creating a parameter template, only parameters supported by replica set instances can be added to the template.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Each parameter template must contain at least one parameter. For details of the parameters supported by each database version and the value range of the parameters, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/supported-parameter">Supported parameters</a>.</div><br> |
   

6. click **OK**.


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent operations

After the parameter template is created, you can apply the parameter template to the target instance. For specific procedures, refer to [Applying parameter template](https://docs.byteplus.com/en/docs/mongodb/apply-parameter-template).
