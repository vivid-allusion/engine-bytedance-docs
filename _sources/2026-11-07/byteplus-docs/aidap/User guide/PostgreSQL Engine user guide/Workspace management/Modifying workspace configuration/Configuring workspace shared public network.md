---
title: "Configuring workspace shared public network"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Configuring_workspace_shared_public_network"
---

This topic introduces the procedure for configuring the shared public network for workspaces using the PostgreSQL engine.

<span id="pbe6nyV2"></span>
## Background

When creating a workspace using the PostgreSQL engine, it does not support setting the network protocol type, Virtual Private Cloud, or subnet for the workspace. The created workspace will use the shared public network provided by the AI Native Database Platform by default. After configuring a Virtual Private Cloud or subnet for the workspace, you can disable the shared public network function, and it can be enabled again after being disabled.

<span id="VEYz4rvh"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* A Virtual Private Cloud and subnet have been configured for the Workspace. For more information, refer to [Modifying workspace network configuration](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Modifying_workspace_network_settings).


<span id="0H23VbFu"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click **Workspaces** to access the workspace list.

4. In the Workspace list, click  **...**  \> **Configure** in the target workspace row to enter the **Workspace settings** page.

5. In the **Workspace settings** page's **Shared public network** area, click the function switch to enable the shared public network, then click **Save**.


<span id="PIcsE5vI"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[ModifyWorkspacePublicConnectionPolicy](https://docs.byteplus.com/en/docs/aidap/ModifyWorkspacePublicConnectionPolicy) |Call the ModifyWorkspacePublicConnectionPolicy API to enable or disable the workspace's shared public network. |
