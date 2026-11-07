---
title: "Deleting tool instances"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Delete_a_tool_instance"
---

When a sandbox instance is no longer needed or you need to release resources early, manually delete the instance. Deleting a sandbox instance is irreversible. After you perform this operation, the system destroys all data in the instance. This topic describes how to delete a sandbox instance.

## Considerations

* **Deleting a sandbox instance destroys the instance, interrupts all tasks running in it, and permanently deletes its data**. Confirm that the instance does not contain unsaved data before you delete it.

* You can delete a sandbox instance in two ways: ** manual deletion** (covered in this topic) and **automatic deletion** upon lifecycle expiration. For details, see [Updating the lifecycle duration](https://docs.byteplus.com/en/docs/agentkit/Modify_the_lifecycle_duration_of_a_tool_instance).

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Sandbox Templates" and click the target tool name. On the "Instance management" tab, find the target instance and click "Delete" in the Actions column.

3. In the dialog box, click "Delete".

4. After deletion is complete, verify that the target instance no longer appears in the list on the **Instance management** tab. To use the sandbox environment again,[ create another sandbox instance](https://docs.byteplus.com/en/docs/agentkit/Creating_tool_instances).
