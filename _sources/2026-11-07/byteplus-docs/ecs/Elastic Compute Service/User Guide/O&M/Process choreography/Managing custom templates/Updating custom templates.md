---
title: "Updating custom templates"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Updating_custom_templates"
---

Updating custom templates allows you to adapt to evolving business requirements, address potential issues, and optimize user experience, ensuring they remain aligned with real\-world scenarios.

<span id="Q5Kisotp"></span>
## Usage notes


|Limits |Description |
|---|---|
|Number of templates |A single template supports up to 50 versions. If the version count of a template has reached this limit but you still need to update its information, you can [clone](https://docs.byteplus.com/en/docs/ecs/Cloning_custom_templates) the template and modify related information.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The initial version is "v1" by default. Each update increments the version number by 1. For example, if the current version is "v1", the next becomes "v2", and so forth.</div><br> |
|Update content |You cannot update the template name and associated project. |
|Historical version |After a custom template is updated, it cannot be restored to a previous version. You can only [view related information about previous versions](https://docs.byteplus.com/en/docs/ecs/Viewing_custom_templates). |


<span id="3Xhqp6cv"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select the "Maintenance & Monitoring \> Orchestration" menu.

3. In the top menu bar, select the project and region where your business is located.

4. On the CloudOps Orchestration page, click the "Custom template" tab.

5. In the "Actions" column of the target template, click the "Update" button.

6. For information about the parameters, see [Creating custom templates](https://docs.byteplus.com/en/docs/ecs/Creating_custom_templates).

7. Click the "Update" button to complete the operation.
