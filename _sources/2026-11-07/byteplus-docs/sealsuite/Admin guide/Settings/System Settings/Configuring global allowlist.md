---
title: "Configuring global allowlist"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-global-allowlist"
---

To create exceptions to security and management policies in SealSuite, you can use the Allowlist feature. This guide provides step\-by\-step instructions on how to add, edit, and remove allowlist entries for specific users or devices, exempting them from policies associated with designated feature modules.

<span id="a28d515c"></span>
# How to Add an Allowlist


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **System** **Settings** \> **Allowlist**.

3. On the **Allowlist** page, choose whether to create an allowlist based on **User** or **Device**.

   * **Creating a User\-Based Allowlist**

      1. On the **User** tab, click **Add User**.

      2. In the **Add User** dialog box, complete the following:

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab651227a7234122a81f1fae2167229b~tplv-goo7wpa0wc-image.image) </span>

         
         |**Parameter** |**Description** |
         |---|---|
         |**Scope** |Define which employees this allowlist applies to by selecting a **Department** or **Role**. |
         |**Effective scope** |Select one or more SealSuite feature modules that these employees should be exempt from. Policies from the selected modules will not apply to them. |
         

      3. Click **Confirm** to save the configuration.

   * **Creating a Device\-Based Allowlist**

      1. On the **Device** tab, click **Add Device**.

      2. In the **Add Device** dialog box, complete the following:

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/088055af7a0a494ba512e1ae19eb8184~tplv-goo7wpa0wc-image.image) </span>

         
         |**Parameter** |**Description** |
         |---|---|
         |**Scope** |Define which devices this allowlist applies to by selecting an individual **Device** or a **Group**. |
         |**Effective scope** |Select one or more SealSuite feature modules that these devices should be exempt from. Policies from the selected modules will not apply to them. |
         

      3. Click **Confirm** to save the configuration.


<span id="a9739835"></span>
# How to Edit or Remove an Allowlist

On the **Allowlist** page, you can view and manage your existing allowlists on their respective tabs.


* The **User** tab shows which users, departments, and roles are exempt from which feature modules.

* The **Device** tab shows which devices and groups are exempt from which feature modules.


From these lists, you can perform the following actions:


* **To edit the modules:**  Click the pencil icon in the **Effective Scope** column to add or remove modules from an existing allowlist entry.

* **To remove an entry:**  Click **Remove** in the **Action** column.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Removing an allowlist entry is immediate and permanent. However, it may take some time for policies to be reapplied to the affected users or devices (e.g., up to 15 minutes for the Anti\-Tampering policy). Please proceed with caution, as this action cannot be undone.   </div>
