---
title: "Configuring workspace private network access"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_workspace_private_network_access"
---

In the AI Native Database Platform, the workspace using the Supabase engine supports private network access. This topic introduces the procedure for configuring private network access for a workspace.

<span id="JkKLKLOW"></span>
## Prerequisites

A workspace using the Supabase engine is created, and its status is **Running**.

<span id="4cdrM60f"></span>
## Precautions


* After creation, the workspace using the Supabase engine automatically uses the AI Native Database Platform’s shared public network to provide services. To disable the workspace public network access, you must first configure workspace private network access.

* Once enabled, the workspace private network access cannot be disabled or changed to another virtual private cloud or subnet.


<span id="7f2ySrZN"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page's **Supabase service** tab, click **Enable private network access** on the **Supabase private network connection string** card at the top of the page. In the pop\-up **Enable private network access** page, select the network protocol type, virtual private cloud, and subnet, then click **OK** to enable private network access for the workspace.
