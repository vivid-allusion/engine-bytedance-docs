---
title: "Integrate the WeCom Application"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Integrate_the_WeCom_Application"
---

This article describes how to integrate DataWind SaaS with WeCom and configure the approval workflow.

<span id="115ec8cb"></span>
# Note


* When administrators configure, ensure that all steps are performed in order, especially permission authorization and enterprise ID configuration. Any omissions or incorrect configurations will cause the approval workflow to not function properly.

* When regular users bind their Volcano Engine account, ensure that the logged\-in Volcano Engine account matches their business permissions. After binding, you must not change the binding arbitrarily to avoid affecting approval operations.


<span id="56306a0c"></span>
# Preparation

Before starting the configuration, contact the DataWind Intelligent Data Insight team to obtain the application installation QR code. This QR code can be embedded in H5 or Web pages, making it convenient for enterprise administrators to install the application centrally.

<span id="301bd598"></span>
# Configure WeCom integration and approval workflow

<span id="f7dad2a1"></span>
## Install the application


1. The WeCom administrator uses WeCom to scan the QR code obtained during preparation to access the **Intelligent Data Insight**\-**Installation Test** third\-party application installation page.

2. In the visible range field, click the **Modify** button and select all users who need to initiate or participate in approvals. Ensure that no users are omitted from the user range; otherwise, users not included will not be able to use the approval function.

3. Select "I have read and agree to the Platform User Agreement", then click the **Agree to the above authorization and add** button to complete the application installation. At this point, the page will display "X users selected", where X is the number of users set in the visible range. The application will also obtain basic permissions such as enterprise information, employee information, and approvals.)


<span id="c592487f"></span>
## Set application permissions


1. Log in to the WeCom admin console with an administrator account, click the **Applications** tab in the left navigation bar to enter the applications page.

2. In the **Applications** page, under the **Third\-party** module, find the **Intelligent Data Insight** application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a131786b467944de9e7f26c3cd43f90c~tplv-goo7wpa0wc-image.image) </span>

3. Configure core permissions. Click the application name to enter the details page of the Intelligent Data Insights application, locate the **Authorization Information** module, and the current page will display the message "No permissions authorized yet, authorize now".

   Caution: Since approval flow nodes may include the applicant's direct supervisor, it is essential to authorize the "Organizational Structure Information" permission. Once authorized, the application can obtain the company's organizational structure information, which is used to retrieve the username of the supervisor in the user's information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60834939c35b4ba78d476596247202f5~tplv-goo7wpa0wc-image.image) </span>

4. Click the **Authorize Now** button, select the permissions for Organizational Structure Information, Company Information, Company Employee Information, and Approval, and after confirming authorization, the permission status will be updated to "Authorized" to ensure the approval flow operates normally.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31c7c001abd44ca096189b847d951e6c~tplv-goo7wpa0wc-image.image) </span>


<span id="ae927a37"></span>
## Office platform integration configuration


1. Log in to the WeCom admin console using an administrator account, click **My Company** in the top navigation bar, then click the **Company Information** tab in the side navigation. On this page, find the **Company ID** field and copy the Company ID information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5ec90a6b02444c19389e137ba3ac97f~tplv-goo7wpa0wc-image.image) </span>

2. Use the **Volcano Engine main account** to log in to [Volcano Engine](https://console.volcengine.com/auth/login/?scene=bi&redirectURI=https%3A%2F%2Fconsole.volcengine.com%2Fbi%2Fdatawind), go to the Intelligent Data Insights product page, click the **Settings** button in the upper right corner to enter **System Management**, and select Office Platform Integration from the side navigation.

3. On the Office Platform Integration page, select **WeCom**, click the **Edit** button, enter the Company ID obtained in Step 1 into the corresponding input box, click the **Save** button, and when the page displays "Installed", the office platform integration is complete.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c5806ca35d0490199c60630e0192e13~tplv-goo7wpa0wc-image.image) </span>


<span id="385e8a21"></span>
## Approval flow configuration


1. Keep the Volcano Engine main account logged in, and in the **System Management** navigation bar, select **Application/Approval Settings**.

2. In **Application Settings**, select **Display When No Permission** and then **Initiate Approval Application**. After enabling, the approval process of Intelligent Data Insights will be integrated with WeCom approval, enabling end\-to\-end linkage for approval initiation and approval receipt.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df5677d885644c539f35623dae1d65d2~tplv-goo7wpa0wc-image.image) </span>


<span id="dadf7764"></span>
# Bind account

The resource administrator responsible for initiating approval workflows and receiving approvals must perform a one\-time binding operation before first use to associate the Volcano Engine account with the WeCom account.

All accounts must complete the association between the Volcano Engine account and the WeCom account before using Smart Data Insight in WeCom.

**Steps**:


1. Log in and open WeCom with your standard account, select **Workbench** in the side navigation, find **Smart Data Insight application** in the application list, and click to open it.

   If the "Smart Data Insight" application is not found in the Workbench, it indicates that the visibility range was not set correctly during installation. Use an administrator account or contact the administrator to modify the application's visibility range on the application management page, ensuring your account is within the visible range. For detailed steps, see [Set application permissions](https://bytedance.larkoffice.com/wiki/LZ4OwVRXdiISPakLpsnc0QwQnmd#share-XMC8dr8TXoUdkLx8GdqlxAAgghf) above.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d89bce0c2b14be2afac68bc564aa942~tplv-goo7wpa0wc-image.image) </span>

2. After opening the Smart Data Insight application, you will enter the Volcano Engine login page. You can choose to log in with the primary account or an IAM sub\-user account, enter the Volcano Engine account username/ID and password, and click the **Log in now** button.

   If you forget your password, click the **Forgot password** button to retrieve it. You can also choose other methods such as Enterprise Federation login or Toutiao login.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/217c310727314a16b8545729ace72b78~tplv-goo7wpa0wc-image.image) </span>

3. After a successful login, click the **Bind WeCom** button in the upper right corner of the product page, then click the **Bind now** button. The system will automatically complete the binding between the Volcano Engine account and the current WeCom account.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2040f3d09fc54988911185cabe786d26~tplv-goo7wpa0wc-image.image) </span>

   When the page displays "Binding successful", the page will show the bound account information (such as WeCom ID and Volcano Engine account information), indicating that the binding is complete.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0002fc8e9ec44ecfbdf9a2aa1813b9a8~tplv-goo7wpa0wc-image.image) </span>

4. (Optional) To change the bound account later, click the "**Change binding**" button on the binding success page and follow the prompts to complete the rebinding operation.
