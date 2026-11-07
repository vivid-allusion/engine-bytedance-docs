---
title: "Modifying workspace parameters"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Editing_workspace_specifications"
---

After a workspace is created, different parameters are provided by default, such as Active Time Series (1h), Metric Ingestion Rate, and Query QPS. You can also modify the values of these parameters based on your business requirements.

<span id="f3hMpERR"></span>
## Limits


* You can increase the values of the parameters for a workspace, but currently cannot decrease them.

* You can modify the parameters of a workspace within the following limits:

   * You can modify the parameters only once within 10 minutes.

   * You can modify the parameters cumulatively up to 10 times within 30 days.


<span id="JlPc8Ty5"></span>
## Prerequisites

A Standard Edition workspace has been created. For more details, refer to [Creating a common workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

<span id="B3ksifWS"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region.

3. Click **Workspace** on the left navigation bar to go to the workspace list page.

4. In the workspace list, find the target workspace and click the workspace name to go to the Overview page of the workspace.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2deb98cbb155ffbf4b757ed0e2e86328.png) </span>

5. On the Overview page, find the parameter that you need to modify and click the Edit icon next to the parameter.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c4c436e8ca7808f83313d0f7157bab46.png) </span>

6. Modify the value of the parameter based on your business requirements.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5537f5de8689d0fedca9a97b4547f4b6.png) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Quota Center determines the default quota of the workspace specifications. If the system default quota is exceeded, apply for a higher quota in the Quota Center first, and then modify the value of the corresponding parameter. For methods of increasing the quota, refer to <a href="https://docs.byteplus.com/en/docs/vmp/How_Do_I_Increase_the_Quota">How do I increase a quota?</a>   </div>
   

7. Click **Confirm** to complete the configuration.


<span id="3XKsTxuw"></span>
## Result validation

After the configuration is complete, you can view the modified parameters on the workspace Overview page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_647ec8ce6862cf0d37c90f9e49c5c3bf.png) </span>

&nbsp;
