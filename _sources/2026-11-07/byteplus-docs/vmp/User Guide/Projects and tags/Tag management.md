---
title: "Tag management"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/biaoqian"
---

Management difficulty rises as the number of VMP workspaces continues to increase. You can add different tags to categorize workspaces of different types and ownerships. This topic describes how to use tags.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, IAM users do not have permissions to use the tag feature. For IAM users who need to use the tag feature, contact the root user to add custom policies and <a href="https://docs.byteplus.com/en/docs/6257/94013">attach the policies to the IAM users</a>. For details, see <a href="https://docs.byteplus.com/en/docs/6257/1158323">Creating custom policies</a>.</div>


<span id="rQqUb00U"></span>
## Tag types


* **System tags**: Tags automatically added to resources by the system. They generally start with `volc:` or `sys:`. System tags are view‑only and cannot be edited.

* **User tags**: Tags manually added to resources. User tags cannot start with `volc:` or `sys:` (case\-insensitive).


<span id="zHrwZZ7o"></span>
## Limits

The resource types that support tag management in VMP include common workspaces, local workspaces, and aggregation query workspaces. Take note of the following rules when using tags:


* If the tag key to be bound already exists in the workspace, the new tag value will overwrite the original tag value. Proceed with caution.

* A tag consists of a tag key and a tag value. Both the key and the value are case‑sensitive. The value can be empty.

* Within the same workspace, the keys of multiple tags cannot be the same, and each key can only map to one value.

* Up to 50 tags can be added to a single workspace.


<span id="Huu9lBbE"></span>
## Design principles

Tags are important grouping tools for personnel, finance, and asset management. They help you quickly and accurately group and manage resources across categories. When adding tags to resources, you can create tags by following the principles below:


* **Collective exhaustion**


This principle means that when planning resources, you need an overall plan for tags (prioritizing tag keys) and need to add planned tag keys and their corresponding tag values to resources. This helps you efficiently retrieve resources by tag.


* **Mutual exclusivity**


This principle means avoiding two or more tag keys for the same attribute. For example, if you use key=owner to indicate the owner, you cannot use other tag keys with the same meaning, such as own and belonger.


* **Simplified design**


This principle is used to simplify the use of tag keys. When you design tags, use tag keys with fixed dimensions to reduce operation errors caused by an excessive number of tag keys.


* **Limited values**


This principle is used to retain only core tag values and remove excess tag values for resources. This principle simplifies procedures such as resource management, access control, and automated O&M.


* **Consideration of future consequences**


Modifying tags may affect tag\-based resource management, access control, and automated O&M. When planning tags, consider the impact of adding or removing tag values to make future tag changes more flexible.

<span id="KYWEnqKC"></span>
## Add tags

<span id="cQmtdEA3"></span>
### Method 1: Add tags when creating a workspace

The following steps describe how to add tags when creating a workspace. For other parameter configurations, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces?lang=en).


1. Log in to the [VMP console](https://console.byteplus.com/prometheus).

2. In the left navigation pane, click **Workspace**. On the page that appears, click **Create**.

3. On the "Create workspace" page, add tags to the workspace in key\-value pairs for the **Label** parameter.


<span id="3PWxT4RA"></span>
### Method 2: Modify tags for an existing workspace


1. On the "Workspace" page, find the target workspace and click the "Edit" icon in the **Label** column.

2. In the **Edit label** dialog box, click **Add Tag**, configure the key\-value pairs of tags, and then click **Confirm**.

3. Return to the "Workspace" page and hover over the tag icon of the target workspace to view all tags added to the workspace.


<span id="FYC203dy"></span>
## Filter by tag


1. In the workspace list, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8213f9608913fdf429fcf33dcd6db887.png) </span>icon in the "Label" column.

2. Click **Add Tag** in the pop\-up window. Add tags based on the filtering criteria, and click "Confirm" to filter workspaces that meet the criteria.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When filtering workspaces by tags, you can add up to 50 tags.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When adding multiple tags for workspace filtering, the AND logic applies. This means only resources with all the specified tags will be matched.   </div>
   


<span id="WcICUyg1"></span>
## Tag\-based cost allocation

You can convert resource tags into cost allocation tags to enable tag‑based billing. This helps you efficiently calculate and analyze cloud resource usage costs.


1. Create a workspace or add tags to an existing workspace. For details, see [Adding tags](https://docs.byteplus.com/en/docs/VolcengineManagedServiceforPrometheus/Releasenotes-5?lang=en).

2. Navigate to [Billing center > Bill tags](https://console.byteplus.com/finance/bill/tag).

3. Search for the target tag and click the switch in the "Actions" column. In the pop\-up message, click **Confirm** to enable the bill tag.

4. Navigate to [Billing center > Bill details](https://console.byteplus.com/finance/bill/detail).

5. Click **Bill details** to switch to the detailed bill query page.

6. Filter bills by selecting tags and click **Export the month bill/detail** to export bill data in PDF format for further statistical analysis.


<span id="o8TmHU7m"></span>
## Tag‑based grouping


1. Log in to the [Resource management console](https://console.byteplus.com/resourcemanager?_vtm_=a106466.b106468.0_0.0_0.0.254_7678967082247620105).

2. In the left navigation pane, click **Tag management \> Tags** to go to the Tags page.

3. Search for the target tag by name, and click the number in the **Number Of tag resources** column to view the list of all resources bound to this tag. This achieves tag\-based grouping.


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
