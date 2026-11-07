---
title: "Getting variables"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_variables"
---

Supabase console functions can be configured and used on the console, and are also available via APIs. When using the API, the variables `SERVICE_ROLE_KEY`, `SUPABASE_BASE_URL`, and `SUPABASE_ANON_KEY` need to be configured. This topic introduces information on obtaining these three variables.

<span id="lztuyHw3"></span>
## Prerequisites


* A workspace using the Supabase engine is created, and its status is **Running**. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging in to the Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).


<span id="QjVeysZp"></span>
## Obtain `SERVICE_ROLE_KEY` and `SUPABASE_ANON_KEY`


1. In the Supabase console, click **Project Settings** on the left to enter the **Settings** page.

2. On the **Settings** page, click **Project Settings** \> **API Keys** to access the **API Keys** page. On the **API Keys** page, you can view the `SERVICE_ROLE_KEY` and `SUPABASE_ANON_KEY`.


<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82660d0d49e9ee50ae1d38c2847fc603.png" width="994px" /></div>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can also call <a href="https://docs.byteplus.com/en/docs/aidap/DescribeAPIKeys">DescribeAPIKeys</a> to obtain <code>SERVICE_ROLE_KEY</code> and <code>SUPABASE_ANON_KEY</code>.</div>


<span id="zRxFWI2X"></span>
## Get SUPABASE_BASE_URL


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

1. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

2. On the **Branch overview** page, under the **Supabase service** tab, click **Connect** on the **Supabase public network connection string** card. In the pop\-up **Supabase public network connection string information** page, click the copy button to get the address string.

3. Remove the port number at the end of the address string, then prepend `https://` to the address string to get the `SUPABASE_BASE_URL`. For example, if the obtained address string is `br-bloom-tern-4bad****.supabase2.aidap-global.cn-beijing.volces.com:443`, then the `SUPABASE_BASE_URL` is `https://br-bloom-tern-4bad****.supabase2.aidap-global.cn-beijing.volces.com`.


<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_963c7e530428d04ada1c681b496a6d08.png" width="840px" /></div>


&nbsp;

&nbsp;
