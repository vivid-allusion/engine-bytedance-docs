---
title: "Configuring application group"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-client-application-grouping"
---

After adding multiple Single Sign\-On (SSO) applications, you can configure how they are displayed within the portal, with support for organizing applications into groups. Furthermore, you can enable a portal customization feature for employees, allowing them to flexibly adjust the grouping and display of applications according to their preferences.

<span id="61303ed8"></span>
# Enabling the custom application display function

SealSuite provides the custom application display function. By setting up this feature, employees can customize the display of application groups on the SealSuite portal, enhancing work efficiency.


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **SSO**.

3. On the **SSO** page, in the upper right corner, click **Application Group Management**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/610a93e2b4214f54b305e348e21aa5a3~tplv-goo7wpa0wc-image.image) </span>

4. In the **Application Group Display Configuration** area, follow the instructions below to enable the corresponding **Application Group Display** features. The custom application display features include the following options:

   * **Allow users to hide the preset groups**: Once this feature is enabled, employees can hide application groups set by the administrator, except for the applications group, on the SealSuite portal.

   * **Allow users to edit the preset groups**: Once this feature is enabled, employees can edit preset application groups and add new application groups on the SealSuite portal.

   * **Show apps with no permissions**: Once this feature is enabled, employees can view applications they do not have permission to access on the SealSuite portal.


<span id="fe122ed0"></span>
# Managing application group

SealSuite provides a default **Recommended Apps** group, where the applications are visible to all users. You must add applications to the application group; otherwise, employees cannot access or use the applications on the portal.


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **SSO**.

3. On the **SSO** page, in the upper right corner, click **Application Group Management**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/610a93e2b4214f54b305e348e21aa5a3~tplv-goo7wpa0wc-image.image) </span>

4. On the **Application Group Management** page, find the **Application Group Configuration** area, and click on **Edit** on the right side of **Recommended Apps** to add recommended applications.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d3da804152a44cea11e4af932ba87c0~tplv-goo7wpa0wc-image.image) </span>

5. On the **Edit Application Group** page, complete the following configurations and click **Confirm**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |Application Group Name |The **Recommended Apps** is the default grouping provided by SealSuite, and its group name is not supported for modification. |
   |Select Applications |Select one or more applications. Support searching for specified applications using application name. |
   


<span id="b3f1815f"></span>
# Configuring application group

<span id="85f2c94d"></span>
## Adding application group


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **SSO**.

3. On the **SSO** page, in the upper right corner, click **Application Group Management**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/610a93e2b4214f54b305e348e21aa5a3~tplv-goo7wpa0wc-image.image) </span>

4. On the **Application Group Management** page, click on **Add New Application Group**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01cf749c009a4d3c931977d153e19bca~tplv-goo7wpa0wc-image.image) </span>

5. On the **Add Application Group** page, complete the configuration according to the instructions below and click **Confirm**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |Application Group Name |Enter an application group name. SealSuite enables configuring the application group name in both Chinese and English. You can click the multi\-language icon to the right of the **Application Group Name** input box, which will direct you to the **Multi\-language Configuration** page. Here, you can set the **Default** as well as specify the **Chinese** or **English** application group name. Among them, the **Default** is mandatory. If the corresponding value is left blank, SealSuite will display the **Default** value. |
   |Select Applications |Select one or more applications. Support searching for specified applications using application name. |
   |Select in\-scope members |Configure the workflow scope for the application group based on either the **Department** or the **Role** dimension. |
   


<span id="3efaa431"></span>
## Previewing application display

After adding the application group, you can use the **Preview** feature to view how the application group will appear on the employee portal.


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **SSO**.

3. On the **SSO** page, in the upper right corner, click **Application Group Management**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/610a93e2b4214f54b305e348e21aa5a3~tplv-goo7wpa0wc-image.image) </span>

4. On the **Application Group Management** page, locate the **Application Group Configuration** section and click the **Preview** icon to its right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40e4326492c947228edc52c49b1f6e9e~tplv-goo7wpa0wc-image.image) </span>

5. On the **Preview Application Display** page, view the application display situation on the user portal.

   In the search box at the top of that page, you can search the application display status on a specific employee portal by **Department**, **User**, or **Role** dimensions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/765215e01bd84ddeb21bae3abee2c47e~tplv-goo7wpa0wc-image.image) </span>

   The search results will be displayed in the **Application Display** area. If you don't enter a department, user, or role in the search box, SealSuite will automatically display the application group configured by the current administrator account.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Preview</strong> feature only supports viewing the application group display configured in the SealSuite Admin Console by the current administrator account; it does not support viewing the custom application display on the portal.   </div>
   

<span id="bf10f6dc"></span>
## Editing or Deleting application group


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **SSO**.

3. On the **SSO** page, in the upper right corner, click **Application Group Management**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/610a93e2b4214f54b305e348e21aa5a3~tplv-goo7wpa0wc-image.image) </span>

4. On the **Application Group Management** page, you can perform the following actions in the application group:

   1. Adjusting application group order

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Order adjustment is not supported for recommended applications group.      </div>
      

      1. In the top left corner of the custom application group card, long\-press the edit icon to drag the card to the appropriate position.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fae7be3c41ae47219705d6d5ce569c08~tplv-goo7wpa0wc-image.image) </span>

      2. After adjustment, the page will prompt that the order of the application group cards has been successfully adjusted.

   2. Editing application group card

      1. Click the **Edit** button on the specified application group card.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87023b67b39541f785556c3d72851b44~tplv-goo7wpa0wc-image.image) </span>

      2. On the **Edit Application Group** page, you can perform the following actions:

         1. Edit the configuration information of the application group.

            For instructions on the configuration item, please refer to [Configuring application group](https://docs.byteplus.com/docs/sealsuite/docs-configuring-client-application-grouping).

         2. Adjust the order of applications within the application group.

            Long press the edit icon on the left side of the application to adjust the order of applications.

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62820ca9579343619315b900d822724a~tplv-goo7wpa0wc-image.image) </span>

      3. Click **Confirm** to apply the configuration changes.

   3. Deleting application group card

      1. Click the **Delete** button on the specified application group card.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/822c6493a8084b0381c56f5005c0ca01~tplv-goo7wpa0wc-image.image) </span>

      2. In the confirmation dialog box, click **Confirm**.
