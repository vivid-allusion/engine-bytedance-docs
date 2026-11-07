---
title: "Cloning custom templates"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Cloning_custom_templates"
---

You can copy an existing custom template to create a new custom template that is identical except for its name. Additionally, you can modify the configuration based on the original template to quickly create custom templates.

<span id="S2RDgpqo"></span>
## Usage note


* You cannot clone custom templates across different projects. Custom templates can only be cloned within the same project and used exclusively within that project.

* A single account can have up to 100 custom templates at the same time. If the number of custom templates in your account has reached the upper limit, you can [delete any custom templates you no longer need](https://docs.byteplus.com/en/docs/ecs/Deleting_custom_templates) before cloning additional custom templates.


<span id="ELrBlADV"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

3. In the top menu bar, select the project and region where your business is located.

4. On the CloudOps Orchestration page, click the "Custom template" tab.

5. In the "Actions" column of the target template, click the "Clone" button.

6.  **(Optional)**  Modify the name, JSON schema, tag information, and other information based on your needs. For more information, see [Creating custom templates](https://docs.byteplus.com/en/docs/ecs/Creating_custom_templates).

7. Click the "Clone" button to complete the operation.
