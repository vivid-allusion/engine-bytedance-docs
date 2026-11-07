---
title: "Create Variables"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Create_Variables"
---

The BytePlus Flink platform provides variable functionality, supporting the direct referencing and effective use of variables in WITH parameters when creating default temporary tables or specifying tables in InMemoryCatalog in SQL tasks. Using variables can prevent the exposure of plaintext keys, addresses, resource names, etc., thus enhancing security.

<span id="4d70fd31"></span>
## Special Notes


* Variables are only supported in creating temporary tables in SQL tasks (i.e., CREATE TEMPORARY TABLE) or when referencing in WITH parameters during table creation specified in InMemoryCatalog.

* In SQL tasks, reference variables in the format `${secret_values.variable_name}`, where `secret_values.` is a fixed prefix, `variable_name` is the name of the variable you create.

* Global variables can be directly referenced and take effect, but referencing domain\-specific variables requires selecting the effective variable scope in the Flink parameter configuration. The system will first search for variables within the specified scope, and then look into global variables, where domain\-specific variables have a higher priority than global variables. If the variable does not exist, an error will occur during execution.


<span id="64c8702e"></span>
## Create Variables


1. Log in to the [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar.

3. In the left navigation bar, select **Project Management**, then click on the project block to enter the project.

4. In the left navigation bar of the project, select **Task Development \> Variables**.

5. On the **Variables** page, click the create variable button to create a variable.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d55662f342144159eaab30ec2b4745f~tplv-goo7wpa0wc-image.image) </span>


6. In the **Create Variable** dialog, choose to create a global variable or a domain\-specific variable, then set the variable name, variable value, and other parameters, and then click **Create**.

   * Create a global variable.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4be98b2de28a4758b8a60bf87ed73d7d~tplv-goo7wpa0wc-image.image) </span>

      
      |**Configuration** |**Description** |
      |---|---|
      |Scope |When creating a global variable, select **Global** for the scope. |
      |Target Folder |Set the folder to which the global variable belongs.<br><br><br>* Select Existing: Create a global variable in an already existing folder. There is a default folder in the system, which can be used directly.<br><br>* Create a new folder: Manually enter a new folder name and create global variables in the new folder. |
      |Variable Name |Set a custom variable name.<br><br><br>* Supports combinations of uppercase letters, lowercase letters, numbers, and hyphens (\-), and must start with a letter.<br><br>* The length must be 1 to 128 characters.<br><br>* The name must be unique in the global variables. |
      |Variable Value |Set the variable value based on actual business needs. |
      |Description |Description of the current variable. |
      

   * Create a domain\-specific variable.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40904f42fac74b3ea69b3a693482267c~tplv-goo7wpa0wc-image.image) </span>

      
      |**Configuration** |**Description** |
      |---|---|
      |Scope |When creating a specific domain variable, choose the **specified domain**. |
      |Target Domain |Set the domain to which the specific domain variable belongs, such as development, testing, production, etc.<br><br><br>* Select Existing: Create a variable within an already existing domain.<br><br>   The specified domain has no default domain. When creating a specified domain for the first time, you must choose to create a new domain.<br><br>* Create New: Manually enter a new domain name and create a global variable in the new domain. |
      |Variable Name |Customize variable names.<br><br><br>* Supports combinations of uppercase and lowercase letters, numbers, and hyphens (\-), and must start with a letter.<br><br>* Length must be between 1 to 128 characters.<br><br>* The name must be unique within its domain. |
      |Variable Value |Set variable value based on actual business requirements. |
      |Description |Description of the current variable. |
      


<span id="422ca1c1"></span>
## Other operations


* View variable details: Click on the variable name to view the variable details.

* Copy Variable: Click on the copy button next to the variable name to copy the variable to the clipboard for job development use.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b896fded2d5246c9b88597d8b420b268~tplv-goo7wpa0wc-image.image) </span>


* Delete Variable: Select **Delete** and confirm again.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/364ba6076c4d47a48906e2cd22bd9a26~tplv-goo7wpa0wc-image.image) </span>
