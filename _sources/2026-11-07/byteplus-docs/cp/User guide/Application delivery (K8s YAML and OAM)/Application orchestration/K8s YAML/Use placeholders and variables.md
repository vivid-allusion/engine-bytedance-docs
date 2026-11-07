---
title: "Use placeholders and variables"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Use_placeholders_and_variables"
---

The system provides system image placeholders, preset placeholders, and custom placeholders to help you quickly orchestrate applications. This article introduces features related to placeholders and explains how to use placeholders and variables.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information


* **Image placeholder**

   Users can dynamically specify the target image address at runtime, making it easier to upgrade application images, perform differentiated deployment across multiple environments, and address other similar scenarios.

   
   |Name |Type |Description |Notes |
   |---|---|---|---|
   |image.[custom name] |String |Enter remarks such as the purpose of the image and other relevant information. This field can be left blank. |* Click **Add** to add a new image placeholder. Supports customizing the names and descriptions of image placeholders.<br><br>* Click `{{ .AppDeliver.image.[custom name] }}` in the YAML edit area to reference the current image placeholder.<br><br>* By default, the system provides a placeholder image named image.backend for the Deployment resource. Modification and deletion are supported. |
   

* **Preset placeholder**

   A preset placeholder is a system\-defined placeholder. The value of a preset placeholder cannot be modified.

   
   |Name |Type |Value source |Value |Notes |
   |---|---|---|---|---|
   |appName |String |Variable |AppName |* appName is a system\-defined placeholder for the Application ID, which helps you quickly distinguish applications. The parameter "AppName" is a preset parameter that represents the Application ID of the current application and cannot be modified.<br><br>* In the YAML edit area, click or tap `{{ .AppDeliver.appName }}`; you can then reference the current predefined placeholder. |
   |envName |String |Variable |EnvName |* envName is a system\-preset Environment ID placeholder that helps you quickly distinguish the environment in which an application is deployed. EnvName is a predefined parameter that represents the Environment ID of the current application and cannot be modified.<br><br>* In the YAML edit area, type `{{ .AppDeliver.envName }}` to reference the predefined placeholder. |
   

* **Custom placeholders**

   Custom placeholders are placeholders set by the user. A value source can be a variable (system preset parameter, custom parameter) or a constant. By using custom placeholders together with variables, you can achieve differentiated deployment of application orchestration across different environments.

   The system provides commonly used custom placeholders by default, such as namespace, port, and replicas, and has already preset recommended default values. You can add, modify, or delete custom placeholders as needed.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The environment has been created. This example creates development environment 1 and test environment 1.

* The variables have already been created in advance. This example creates the custom parameter Label.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

The following takes adding a custom placeholder label to enable different Deployment labels for development and test environments as an example:


1. Log in to the current application.

   1. Log in to [Code Pipeline console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the target workspace name to enter the selected workspace.

   4. Select **Application Delivery \> Application Management** in the left navigation bar.

   5. Click the target application card to open the selected application.

2. Click **Application Orchestration**. Switch to the Application Orchestration tab.

3. Click **edit** to enter the application orchestration page.

4. In the YAML editing area, enter `run: "{{ .Values.label }} "` below the metadata.labels.run parameter.

5. Click **Extract placeholder**, and the custom placeholder area on the right will display the newly added custom placeholder label.

6. Set the information for the custom placeholder label.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Name |Display the names of extracted custom placeholders. This example is a label.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you need to change the name, please be sure to also modify the custom placeholder name in the YAML edit area at the same time. This example selects a variable.</div><br> |
   |Type |Select the type of the current placeholder as needed; the default is string. Supports string, integer, floating\-point number, and Boolean value.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When selecting a variable as the value source, the type remains the default.</div><br> |
   |Value source |Supports constants and variables. Variables are used to enable differentiated deployment across different environments. This example selects variables. |
   |Value |Enter the value of the parameter. This example uses the custom configuration parameter Label that was created in advance.<br><br><br>* When the value source is set to constant, simply enter the value of the corresponding type.<br><br>* When the value source is set to variable, you can use either preset parameters or custom parameters that you create. |
   

7. Click **Confirm**, and set the active environment in the pop\-up dialog box. In this example, development environment 1 and test environment 1, which were created in advance, are selected.

8. After completing the settings, click **Create**.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

Enable the custom configuration parameter Label in development environment 1 and assign it the value aaa, and in test environment 1 and assign it the value bbb. In other words, this is a set of configurations, each arranged in a different environment with distinct Deployment labels. When deploying development environment 1, assign aaa to label; when deploying test environment 1, assign bbb to label.
