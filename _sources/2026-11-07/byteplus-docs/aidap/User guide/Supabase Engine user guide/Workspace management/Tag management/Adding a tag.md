---
title: "Adding a tag"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Adding_a_tag"
---

The AI Native Database Platform supports adding tags to workspaces. Tags classify workspaces, facilitating workspace search and resource aggregation. This topic introduces the procedure for creating and adding tags to workspaces.

<span id="MXF0INtg"></span>
## Tagging rules

The tagging rules are as follows.


|**Limits** |**Decscription** |
|---|---|
|Tag key |* Supports letters or characters of any language, digits, spaces, and the following special characters: `_.:/=+-@`.<br><br>* volc: is a system\-reserved tag key. When adding tags, the tag key cannot start with `volc:`, regardless of the case.<br><br>* The tag key must be 1 to 128 characters in length. |
|Tag value |* Supports letters or characters of any language, digits, spaces, and the following special characters: `_.:/=+-@`.<br><br>* The tag value must be 0 to 256 characters in length. A length of 0 indicates that the tag value is empty. |
|Tag quantity |* The total tag quantity is unlimited, but each Workspace can add up to 50 tags.<br><br>* You can add up to 20 tags at a time. |


<span id="lFt002vN"></span>
## **Procedure**


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_34399bab70d1c5911d50656ab777319f.png) </span>**Workspaces** to enter the Workspace list

4. In the Workspace list, click  **...**  \> **Configure** on the target Workspace row to enter the **Workspace settings** page.

5. On the **Workspace settings** page, click  **+Add tag** in the **Tag** area to add a new or an existing tag to the workspace. After adding, click **Save**.

   * **Add a new tag**

      Enter the new **Tag key** and **Tag value** in the corresponding text boxes, then press **Enter**. When setting tags, follow the tag setting rules. For more information, refer to Tag setting rules.

   * **Add an existing tag**

      Click the tag key and tag value text boxes and select an existing tag key and its corresponding tag value from the drop\-down list.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also add multiple tags by clicking the <strong>Add tag</strong> button repeatedly.   </div>
   

<span id="PHfssGUk"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/en/docs/aidap/AddTagsToWorkspaces) |Call the AddTagsToWorkspaces API to add tags to the workspace. |
