---
title: "Creating custom templates"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating_custom_templates"
---

You can define JSON templates based on real\-world scenarios to preset standardized O&M processes. This allows for efficient handling of batch and customized O&M tasks across large\-scale instances.

<span id="MW3bj226"></span>
## Usage note

A single account supports up to 100 custom templates at the same time. If the number of custom templates in your account has reached this limit, you can [delete custom templates that are no longer required](https://docs.byteplus.com/en/docs/ecs/Deleting_custom_templates), and then create custom templates based on your business requirements.

<span id="PjmMhYyt"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select the "Maintenance & Monitoring \> Orchestration" menu.

3. In the top menu bar, select the project and region where your business is located.

4. On the CloudOps Orchestration page, click the "Custom template" tab.

5. Click the "Create custom templates" button and configure the parameters in the following table.

   
   |Parameter​ |Description |
   |---|---|
   |Name |The name of the custom template.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The template name must be unique within the current account or project. It cannot be the same as the name of the <a href="https://docs.byteplus.com/en/docs/ecs/Summary_of_orchestration_steps">public template</a>, nor can it be the same as the name of any other custom template.</div><br> |
   |JSON schema |Defines custom template files (O&M orchestration processes) in JSON format, including the data structure, field constraints, and validation rules for "Parameters", "Tasks", and "Outputs". [Learn more](https://docs.byteplus.com/en/docs/ecs/Overview_of_custom_template_syntax).<br><br>Default template structure:<br><br>```JSON```<br>```{```<br>```  "FormatVersion": "0.2",```<br>```  "Description": "",```<br>```  "Parameters": {},```<br>```  "Tasks": [],```<br>```  "Outputs": {}```<br>```}```<br><br><br><br>* **FormatVersion**: Optional. The engine version. The default value is 0.2.<br><br>* **Description**: Optional. The description that explains details such as the usage and purpose of the template.<br><br>* **Parameters**: Optional. Defines the list of parameters used during template execution. For more information, see [Parameters description](https://docs.byteplus.com/en/docs/ecs/Overview_of_custom_template_syntax#2kEHdh1B).<br><br>* **Tasks**: Required. The Tasks parameter is the most important component of a template. Each task defines a specific action to be executed. These actions are defined and implemented by the Orchestration service. For more information, see [Tasks description](https://docs.byteplus.com/en/docs/ecs/Overview_of_custom_template_syntax#iLk2JfAg).<br><br>* **Outputs**: Optional. The Outputs parameter defines information returned after template execution and can reference the output of a task (by specifying the task name). For more information, see [Outputs description](https://docs.byteplus.com/en/docs/ecs/Overview_of_custom_template_syntax#A39kFSTs). |
   |Project |Used to select the scope of instances the custom template applies to based on [projects](https://docs.byteplus.com/en/docs/ecs/Managing-projects).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">After you select a project, new instances that meet the conditions automatically match the custom template.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The project displayed here is the one you selected in Step 3. You can change the project in the top menu bar.</div><br> |
   |Tag |Optional. Used to select the scope of instances the custom template applies to based on tags. Click the "Add tag" button, and then select or enter the tag key and corresponding tag value.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Up to 20 tags can be added.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A tag is a key\-value pair used to identify cloud resources. Tags help you categorize resources based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your resources. <a href="https://docs.byteplus.com/en/docs/ecs/Tag-overview">Learn more</a>.</div><br> |
   

6. Click "Confirm" to complete the operation.


<span id="IhxrYHNK"></span>
## Subsequent steps

After the custom template is created, you can use this template to [create an orchestration plan](https://docs.byteplus.com/en/docs/ecs/Create_an_orchestration_plan) for automated O&M.
