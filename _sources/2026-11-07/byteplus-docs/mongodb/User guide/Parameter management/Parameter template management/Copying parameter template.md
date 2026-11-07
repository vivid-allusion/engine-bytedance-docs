---
title: "Copying parameter template"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/copy-parameter-template"
---

If you need to create a new parameter template, but most of the parameters and values in an existing parameter template match those of the new one, you can quickly create the new template by copying the existing one and then editing it as needed. This topic describes how to copy parameter template.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, choose **NoSQL Database\> MongoDB \> Parameter templates**.

4. On the **Parameter templates** page, choose the appropriate steps depending on the type of parameter template you want to copy.

   * Copy customized template

      On the **Customized template** sub\-tab, find the target template you want to copy in the template list, and click **Copy** in the **Actions** column on the right.

   * Copy system template

      1. Click on the **System template** sub\-tab.

      2. In the system template list, find the target template you want to copy, and click **Copy** in the **Actions** column on the right.

5. In the pop\-up dialog box, configure the following parameters.

   
   |Parameter |Required |Description |
   |---|---|---|
   |Template name |Yes |Enter the name of the parameter template. The name needs to meet the following requirements simultaneously:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 2 to 64 characters. |
   |Template description |No |Enter the remarks for the parameter template whose length cannot exceed 200 characters. |
   

6. click **OK**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After successfully copying the parameter template, you can edit and modify the settings in the new template and apply the modified template to instances. For specific procedures, refer to [Editing parameter template](https://docs.byteplus.com/en/docs/mongodb/edit-parameter-template) and [Applying parameter template](https://docs.byteplus.com/en/docs/mongodb/apply-parameter-template).
