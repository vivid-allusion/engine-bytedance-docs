---
title: "Managing departments"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-departments"
---

To build your company's organizational structure in SealSuite, you can use the User Directory function. This guide provides step\-by\-step instructions for manually adding, editing, and deleting departments and subsidiaries to accurately reflect your corporate hierarchy.

<span id="2f3ff6b2"></span>
# Use cases

To create a secure digital workplace using SealSuite, you must first establish the corporate organizational structure. SealSuite offers the following methods for building your corporate organizational structure:


* Manual configuration: Manually add department and user information. Additionally, employee actions such as onboarding, offboarding, and transfers within the company must be manually configured in the SealSuite Admin Console. For instructions, please refer to this article and [Managing users](https://docs.byteplus.com/docs/sealsuite/docs-managing-members).

* Connecting to third\-party data sources: SealSuite enables the rapid import of existing organizational structures from DingTalk or Feishu into SealSuite. This method saves time for the enterprise administrator by eliminating the need for manual configuration of the organizational structure. For specific operations, please refer to [Setting up account systems and identity authentication](https://docs.byteplus.com/docs/sealsuite/docs-managing-account-settings).


<span id="96469213"></span>
# Adding a department or subsidiary


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **User Directory**.

3. On the right of the **department structure**, click the plus sign (+), and then select either **New sub\-department** or **New subsidiary**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/268e6f0c6e834034860139762adac89c~tplv-goo7wpa0wc-image.image) </span>

   * If you choose **New sub\-department**, you need to configure the **Department Name** and **Parent Department** in the **New Department** dialog box and then click **Confirm**.

   * If you choose **New subsidiary**, you need to configure the **Subsidiary Name** and **Parent Department** in the **New subsidiary** dialog box, and then click **Confirm**.


<span id="b685bc06"></span>
# Adding a subdepartment


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \>**User Directory**.

3. Click the icon on the right side of the specified subsidiary or department, and select **New sub\-department**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88ef9049d5c042bd9888fed1ec30a179~tplv-goo7wpa0wc-image.image) </span>

4. In the **New Department** dialog box, configure the **Department Name** and the **Parent Department**, and then click **Confirm**.


<span id="00dd52ed"></span>
# Editing a department or subsidiary


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \>**User Directory**.

3. Click the icon on the right side of the specified subsidiary or department, and select **Edit department**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fdffc93bc4f44a79991120103e71652~tplv-goo7wpa0wc-image.image) </span>


<span id="123e0de9"></span>
# Deleting a department or subsidiary

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This operation is irreversible. Review the following impacts before proceeding:</div>



* <div data-tips="true" data-tips-type="warning">If you delete a department or subsidiary that has subdepartments but no members, its subdepartments are also deleted.</div>


* <div data-tips="true" data-tips-type="warning">If you delete a department or subsidiary that contains members and memberless subdepartments, its members are moved to the parent department.</div>


* <div data-tips="true" data-tips-type="warning">You cannot delete a department or subsidiary if its subdepartments contain members. You must first move the members or delete the subdepartments.</div>


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \>**User Directory**.

3. Click the icon on the right side of the specified subsidiary or department, and select **Delete Department**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6cb6f12016a49afb78deb1ae00cdc68~tplv-goo7wpa0wc-image.image) </span>

4. In the **Warning** dialog box, click **Confirm Deletion**.


<span id="93f4c78d"></span>
# Next steps

After setting up your departments, you can manage the employees within them. For instructions, please refer to [Managing users](https://docs.byteplus.com/docs/sealsuite/docs-managing-members).
