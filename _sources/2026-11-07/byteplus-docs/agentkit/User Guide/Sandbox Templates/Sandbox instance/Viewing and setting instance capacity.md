---
title: "Viewing and setting instance capacity"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/view-and-set-instance-capacity"
---

Sandbox templates allow you to view the resource usage of business instances under the current template and set the maximum number of instances that can be created from the template. This topic describes the meaning of the resource statistics metrics and how to set instance capacity.

## Statistics description

On the "Instance management" tab of the sandbox template details page, you can view the following resource statistics:

* **Total instances**: The number of business instances that have been created under the current template.

* **Running instances**: The number of instances currently in the running state.

* **Instance capacity**: The number of created instances, the maximum number of instances, the current user quota, and the capacity usage rate of the current template. The capacity usage rate is calculated as "**Number of created instances/Maximum instance count**".

## Considerations

* The maximum instance count cannot exceed the current user quota. [View the quota](https://docs.byteplus.com/en/docs/agentkit/Limits?lang=en)

* After the configured maximum instance count is reached, you cannot create more instances. To continue, increase the limit in "Instance capacity" or delete unused instances to free up capacity.

## Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Sandbox Templates", and click the name of the target sandbox template in the list.

3. Go to the "Instance management" tab. On the "Instance capacity" card, click the "Settings" button.

4. Enter or use the increment/decrement buttons to set the maximum instance count. Valid values range from **1** to the current user quota.

5. Click the "Save" button to complete the operation. The modification takes effect immediately.
