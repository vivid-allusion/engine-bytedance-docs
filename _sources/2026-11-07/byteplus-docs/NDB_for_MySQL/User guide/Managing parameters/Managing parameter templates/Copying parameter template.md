---
title: "Copying parameter template"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Copying_parameter_template"
---

If you need to create a new parameter template, but most of the parameters and values in an existing parameter template match those of the new one, you can quickly create the new template by copying the existing one and then editing it as needed. This topic describes how to copy parameter template.

<span id="7NIuPkmI"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. Click **Parameter templates** in the left\-side navigation bar.

4. On the **Parameter templates** page, choose the appropriate steps depending on the type of parameter template you want to copy.

   * **Copy customized template**

      On the **Customized template** tab, in the template list, find the target template to copy, and in the **Actions** column, select  **...**  \> **Copy**.

   * **Copy system template**

      1. Click the **System templates** tab.

      2. In the system template list, find the target template to be copied, and click **Copy** in the **Actions** column on the right.

5. In the pop\-up dialog box, configure the following parameters.

   
   |**Name** |**Description** |
   |---|---|
   |Template name |Enter the name of the parameter template. The name needs to meet the following requirements simultaneously:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 8 to 64 characters. |
   |Template description |Enter the remarks for the parameter template whose length cannot exceed 200 characters. |
   

6. Click **OK**.


<span id="S12NtcMq"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[CopyParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CopyParameterTemplate) |Call the CopyParameterTemplate API to copy a specified parameter template to a new parameter template. |
