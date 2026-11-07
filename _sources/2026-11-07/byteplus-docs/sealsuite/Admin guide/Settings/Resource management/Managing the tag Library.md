---
title: "Managing the tag Library"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-the-tag-library"
---

The **Tag Library** provides a unified classification system for enterprise resources, enabling administrators to logically group and manage large volumes of resources (such as applications and security policies). This feature is widely used across SealSuite modules for resource control and permission isolation. It supports batch orchestration and automatic inheritance of rules based on tags, eliminating the need for repetitive configuration when new resources are associated. It also allows you to apply differentiated control policies based on the security requirements of different business categories, improving both policy distribution flexibility and operational efficiency.

<span id="cea3a3e8"></span>
## Creating a Tag


1. Log in to the Admin Console.

2. In the left navigation pane, go to **Settings** \> **Resources** \> **Tag Library**.

3. Click  **+ Add Tag Label** on the right side of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05cecb40872944ffad3931544f5e34a4~tplv-goo7wpa0wc-image.image) </span>

4. Configure the following parameters in the dialog box:

   
   |**Parameter** |**Description** |
   |---|---|
   |**Label Type** |Specifies the business modules where the tag is visible and applicable. Options include: **Global**, **Application Gateway**, **SSO**, **Data Security**, and **Device Group**.<br><br>Tags serve two primary functions in each module:<br><br><br>* **Classification and Batch Orchestration**: Groups resources with identical attributes to enable batch policy delivery and automatic policy inheritance.<br><br>* **Fine\-grained Permission Isolation**: Defines data isolation boundaries. By restricting the scope of management tags within "Administrator Permissions," you ensure administrators only access resources within their authorized scope, preventing unauthorized access. For more information, see [Configuring Administrator Access](https://docs.byteplus.com/docs/sealsuite/docs-adding-administrator_1). |
   |**Label Name** |Enter a display name for the tag. The name can contain Chinese, English, and numbers. |
   |**Label Value** |Enter a unique identifier for the tag, used for API calls and internal logic. Must be globally unique. Only English letters, numbers, and underscores are allowed. |
   

5. Click **Confirm** to complete the creation.

6. After creation, go to the corresponding resource management page (such as Application Gateway application details, SSO application details, or the creation/edit page for Data Security policies and rules) to associate the tag with resources. This enables tag\-based differentiated policy distribution and fine\-grained permission control.


<span id="03785c22"></span>
## Managing Tags

On the **Tag Library** list page, administrators can perform the following actions to maintain existing tags:


* **View Tag Details**: The list provides a centralized view of all tags, including those added manually on this page and those created inline within specific application settings. Use the filters at the top of the list to search by **Name** or **Type**.

* **Edit**: Click **Edit** in the action column to modify a tag's name or its unique value.

* **Delete**: Click **Delete** for tags that are no longer required.

   * **Caution**: Deleting a tag automatically removes its association with all linked applications but does not delete the applications themselves. Verify if any security policies depend on the tag before proceeding with deletion.
