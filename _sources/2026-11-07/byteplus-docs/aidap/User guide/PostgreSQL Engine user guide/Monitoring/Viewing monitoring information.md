---
title: "Viewing monitoring information"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Viewing_monitoring_information"
---

This topic describes the steps to view monitoring information of Workspace in the AI Native Database Platform.

<span id="8p4Lk7Rt"></span>
## Background

<span id="5e0WhYiH"></span>
### Monitoring information

The AI Native Database Platform homepage provides global monitoring metrics at the tenant level \- real\-time compute (CU) consumption. This metric aggregates compute consumption of all workspaces under the tenant account on a per\-tenant basis.

The Overview page and Branch overview page display monitoring information for all branches under the Workspace.

<span id="pCqzGyGB"></span>
### Notes on monitoring information

The AI Native Database Platform by default fetches data every 30 seconds. It aggregates the fetched data according to the selected time range and various cycles and methods, as detailed in the table below.


|Query time range |Monitor data aggregation interval |Decscription |
|---|---|---|
|(0~6] hours |30 seconds |Cloud Monitor retrieves data every 30 seconds and displays the collected data directly. |
|(6~24] hours |1 minute |Cloud Monitor retrieves data every 30 seconds and displays the data aggregated by a certain method (such as averaging two data points) after every two collections. |
|(1~7] days |5 minutes |Cloud Monitor acquires data every 30 seconds and displays the data collected every 10 times according to a certain aggregation method (such as finding the average of 10 times of data). |
|(7~15] days |60 minutes |Cloud Monitor retrieves data every 30 seconds and displays the data aggregated by a certain method (such as averaging 120 data points) after 120 collections. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The aggregation interval of monitoring data varies with different query time ranges. The values of the same monitoring item at the same time point slightly differ under different aggregation periods. To view accurate values, select a smaller time range.</div>


<span id="vULKQn5q"></span>
## Procedure


<Tabs>
<Tab zoneid="yiHwysLqH3" title="View global monitoring information">
<TabTitle>View global monitoring information</TabTitle>

1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6ef19c4b52af8df254e4ee815e1c4c14.png)<sub> </sub></span>**Homepage** displays global monitoring metrics \- real\-time compute (CU) consumption monitoring information.


</Tab>
<Tab zoneid="jg6QhlIhWL" title="View branch monitoring information">
<TabTitle>View branch monitoring information</TabTitle>

1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the target workspace's **Branch management** page. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * In the middle navigation bar, click<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** on the right of the branch section to enter the target workspace's **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page, click the **Monitoring** tab. In the **Monitoring** tab's **Resource monitoring** section, you can view the workspace's resource monitoring information.


</Tab>
</Tabs>
