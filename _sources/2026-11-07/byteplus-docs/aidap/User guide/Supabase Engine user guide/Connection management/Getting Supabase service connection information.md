---
title: "Getting Supabase service connection information"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_Supabase_service_connection_information"
---

This topic describes the steps to get the Supabase service connection information for the workspace.

## Background

To connect to the project database, the workspace using the Supabase engine provides private network connection strings and public network connection strings. Private network connection strings include

various connection strings used under multiple app frameworks and mobile frameworks. The public network connection strings include various connection strings used under multiple app frameworks and mobile frameworks, as well as PostgreSQL connection strings for multiple coding languages.

## Prerequisites

* A workspace using the Supabase engine is created, and its status is **Running**.

* To get the private network connection information of the Supabase service, you need to first enable private network access for the workspace. To enable, refer to [Configuring workspace private network access](https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_workspace_private_network_access).

* To obtain the public network connection information of the Supabase service, enable public network access for the workspace first. To enable, refer to [Configuring workspace public network access](https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_workspace_public_network_access?lang=en).

## Precautions

Workspaces using the Supabase engine automatically provide services using the AI Native Database Platform’s shared public network after creation. You can view the current public network type (Independent public network or Shared public network) used by the workspace on the **Supabase public network connection string** page.

## Procedure

1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)**Branch management** in the center navigation bar of the page, then click the icon![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png) to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page, in the **Supabase service** tab, click **Connect** of **Supabase private network connection string** card or **Supabase public network connection string** card, then select framework as needed on the popped\-up **Supabase private network connection string** page or **Supabase public network connection string** page to obtain the private network or public network connection string.
