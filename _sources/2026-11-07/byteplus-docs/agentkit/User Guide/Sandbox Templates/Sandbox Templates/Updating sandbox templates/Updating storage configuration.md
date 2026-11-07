---
title: "Updating storage configuration"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Update_storage_configuration"
---

The storage configuration of a sandbox template manages TOS mount points. By mounting a TOS bucket, sandbox instances can persist data or share files. You can update the storage configuration to add a mount point to expand storage or remove a mount point that is no longer needed. This topic describes how to update the storage configuration.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Sandbox Templates".

3. In the "Sandbox templates" list, click the target template name. On the "Configuration information" tab, click "Edit" in the "Storage" section **.**

4. In the "Edit storage" panel, enable TOS mounting or add or delete TOS mount points. For parameter details, see [Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools). Then, click "Confirm".

5. After a successful update, go to the "Configuration information" tab and confirm that the list of TOS mount points has been updated in the **Storage** section. After the storage configuration is updated, newly created instances will use the updated storage mount configuration. The storage mounts of existing instances are not automatically changed.
