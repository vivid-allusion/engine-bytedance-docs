---
title: "Removing a tag"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Removing_a_tag"
---

After adding tags to a workspace, you can remove tags from the wWorkspace at any time based on business requirements. This topic describes how to remove a tag.

<span id="M0QtfFid"></span>
## Precautions

Batch removal of tags from the workspace is supported, with up to 20 tags per batch.

<span id="dhyjOfef"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1e5e28abf266cb28cea82c8a666f64b5.png) </span> **Workspaces** in the middle navigation bar to access the workspace list.

4. In the Workspace list, click  **...**  \> **Configure** on the row of the target workspace to enter the **Workspace settings** page.

5. In the **Workspace settings** page's **Tag** area, click<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_edb9b90a05db5eef69f3256a74ebd0b3.png)<sub> </sub></span> on the right side of the target tag, and click **Save**.


<span id="iOHmtEgR"></span>
## Related APIs


|API |Decscription |
|---|---|
|[RemoveTagsFromResource](https://docs.byteplus.com/en/docs/aidap/RemoveTagsFromWorkspaces) |Call the RemoveTagsFromWorkspaces API to remove tags from the workspace. |
