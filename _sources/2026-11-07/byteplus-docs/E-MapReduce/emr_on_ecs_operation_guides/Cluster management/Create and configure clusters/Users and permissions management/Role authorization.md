---
title: "Role authorization"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_role_authorization"
---

<span id="使用场景"></span>
## Use cases

To create a sub\-account dedicated to managing or using EMR functionality under the primary account, this document can guide you in configuring permissions correctly for the corresponding sub\-account.

<span id="默认授权情况"></span>
## Default authorization status

The primary account has all permissions by default, while the sub\-account has no permissions by default. The primary account needs to grant permissions to the sub\-account through the **Access control** functionality.

<span id="授权步骤"></span>
## Authorization steps


1. Log in to the primary account, access any page under Volcano Engine, and use the **top navigation in the upper right corner**—the location of the user avatar and username. Hover the mouse to display the dropdown menu, select **Access control**, and enter the authorization page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bcb4e6f99674c20a3cf0c20fbee6969~tplv-goo7wpa0wc-image.image) </span>

2. On the Access control page, you can perform a series of operations related to roles and permissions. The following instructions, combined with the page's operation guide, will help you configure the correct EMR permissions for the corresponding sub\-account.

   1. If you do not have the corresponding sub\-account, you can add one on the access control page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/498d9b9c72df45f5a3c1b18767e084b5~tplv-goo7wpa0wc-image.image) </span>

   2. We have prepared three preset permissions for you: EMRFullAccess, EMRDeveloperAccess, and EMRReadOnlyAccess. For details on the access scope controlled by each permission, refer to [Roles and permissions](https://docs.byteplus.com/docs/E-MapReduce/105450).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you have special requirements, you can also add your own policy as a Customer managed policy. If you need assistance, please submit a ticket directly. We will provide dedicated support for you.      </div>
      

   3. On the **User management** tab, click the sub\-account you want to authorize to enter the configuration interface. In the associated policy section, select the corresponding EMRFullAccess, EMRDeveloperAccess, EMRReadOnlyAccess, or your own Customer managed policy.

   4. After completing the authorization process, log in to the corresponding sub\-account through the login interface so that the sub\-account can use EMR functionality normally.
