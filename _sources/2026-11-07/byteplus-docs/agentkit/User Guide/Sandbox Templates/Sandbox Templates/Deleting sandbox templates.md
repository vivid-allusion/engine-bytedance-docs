---
title: "Deleting sandbox templates"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Deleting_tools"
---

When a sandbox template is no longer in use, you can delete it to release resources. After deletion, the template cannot be recovered. Make sure your services no longer depend on the template before proceeding. This topic describes how to delete a sandbox template.

## Considerations

**Deleting a sandbox template is irreversible**. When a sandbox template is deleted, all associated sessions (session instances) are automatically reclaimed. If the sandbox tool is currently associated with an agent runtime, deleting it will affect the agent's functionality. Before deletion, ensure that no associated resources exist.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Sandbox Template".

3. In the sandbox template list, click the "Delete" button in the "Actions" column for the target template.

4. In the dialog box that appears, confirm that the deletion will not affect business operations, and then click the "Delete" button to complete the operation.

5. After deletion, confirm that the target template no longer appears in the sandbox template list. If this template has been associated with an agent runtime, update the associated tools on the **Associated components** tab.
