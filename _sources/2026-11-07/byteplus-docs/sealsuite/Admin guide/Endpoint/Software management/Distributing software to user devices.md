---
title: "Distributing software to user devices"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-distributing-software-to-user-devices"
---

To centrally manage and deploy software to user devices, you can use the software distribution feature. This guide provides step\-by\-step instructions on how to add software packages, configure distribution tasks with options like scheduling and security verification, and manage both the software list and distribution records.

<span id="bd6d6af3"></span>
# Instruction for use


* The software distribution module provides the security verification capability, which can be enabled by you according to your operational needs. With the capability enabled, you need to enter the corresponding private key or software signature when adding software that you want to distribute. This ensures authorized and secure installation packages are used during the distribution process. For more information on how to enable the security verification capability, please refer to [Select to enable security verification](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/6565917a1ef8eb02f973c947?docLang=en&bv=652fd8f3fb401502ea5effe0#2dc1d2f0).

* Currently, SealSuite only supports distributing Windows or Mac software to user devices. It is recommended to use the procedures listed below to distribute software:

   1. [Adding software that you want to distribute](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/6565917a1ef8eb02f973c947?docLang=en&bv=652fd8f3fb401502ea5effe0#420ab0c0)

   2. [Distributing software to specific user device](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/6565917a1ef8eb02f973c947?docLang=en&bv=652fd8f3fb401502ea5effe0#8f6a2354)

* The software distribution feature consists of the software list and distribution record components. For more information on how to manage these components, please refer to [Managing software list](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/6565917a1ef8eb02f973c947?docLang=en&bv=652fd8f3fb401502ea5effe0#0d6f9060) and [Managing distribution record](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/6565917a1ef8eb02f973c947?docLang=en&bv=652fd8f3fb401502ea5effe0#03728cd1).


<span id="2dc1d2f0"></span>
# Enabling security verification as needed


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **Distribution**.

3. In the upper right corner of the **Distribution** page, click **Security check not enabled**.

4. In the dialog box **Do I need to enable security verification to add software?**  that appears, select **Enable** or **Disable**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To enable this feature and obtain the distribution private key and software signature, please contact the SealSuite service provider.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2904fb05de941719f4edfe00e32a84e~tplv-goo7wpa0wc-image.image) </span>


<span id="420ab0c0"></span>
# Adding software that you want to distribute


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **Distribution**.

3. On the **Software List** tab of the **Distribution** page, click  **+ Add Software**.

4. In the **Add Software Package** dialog box, complete the following configurations and click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a4a757134e04069920c63c3b17d6174~tplv-goo7wpa0wc-image.image) </span>

   
   |**Field** |**Description** |
   |---|---|
   |**Upload package** |Select how the software is added: **Prefer packages** or **Prefer download links**.<br><br><br>* **Prefer packages**: **Upload package** is required, and **Download link** is optional.<br><br>* **Prefer download links**: **Download link** is required, and **Upload package** is optional. Software distributed solely via download link has no size limit. Endpoints download the package directly through an HTTP request.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For large software packages exceeding 500 MB (such as design tools or development environments), we recommend selecting <strong>Prefer download links</strong>. Upload the package to your internal OSS storage or an external\-download\-capable server, and enter the direct link in <strong>Download link</strong> below. When an endpoint receives the distribution task, it downloads the package directly from the link without routing through the SealSuite server, ensuring a stable and efficient download experience.</div><br> |
   |**Upload package** |Supported formats: exe, msi, bat, and pkg. The maximum package size is 500 MB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">After you upload a package, SealSuite automatically detects the target operating system (Windows or macOS). Make sure the package you upload is correct and functional.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the uploaded package is provided by SealSuite, SealSuite automatically detects and populates the package information and enables <strong>Verify successful installation on endpoint</strong> by default. You only need to fill in the <strong>Remarks</strong> field.</div><br> |
   |**Download link** |Enter the OSS download URL for the software package.<br><br><br>* If both **Upload package** and **Download link** are configured, make sure the download link points to the same file as the uploaded package.<br><br>* After you enter a link, the system automatically validates the URL format. If you select **Prefer download links**, you must provide a valid download link; otherwise the configuration cannot be saved. |
   |**Remarks** |Enter custom remarks. |
   |**Software signature** |Required if you have enabled security verification.<br><br><br>* You can view how to obtain the software signature through interface prompts.<br><br>* On the right side of the **Software signature**, click **Close private key entry** or **Enable private key input**, and select private key information. |
   |**Detect if the software was successfully installed on employee** **devices** |When enabled, the system checks whether the software package is successfully installed on the target endpoint. If you enable this option, configure the following parameters:<br><br><br>* Windows packages: Configure **Full software name** and **Software publisher**. You can obtain the values manually following the on\-screen instructions.<br><br>* macOS packages: Configure **Bundle ID**. You can obtain the value manually following the on\-screen instructions. |
   


<span id="8f6a2354"></span>
# Distributing software to specific user device


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **Distribution**.

3. On the **Software List** tab of the **Distribution** page, locate the specific software package.

4. In the **Action** column of the software package, click **Distribute**.

5. On the **Add distribution task** page, complete the following configurations and click **Start distribution**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62fa94c156d04a3598d30af42cc279fd~tplv-goo7wpa0wc-image.image) </span>

   The description of configuration items is as follows:

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Distribution time** |* **Immediate**: In this option, the software package will be distributed to the specified devices as soon as you add the distribution task.<br><br>* **Scheduled**: In this option, you need to specify the time when you want the software to be distributed. |
   |**Operating parameters (configure software silent installation parameters)**  |SealSuite supports silent installations of software. You can enable a silent installation for the specified software package by configuring command\-line parameters as needed, allowing the installation process to proceed without any user input. |
   |**Distribution scope** |Set the distribution scope of software packages within the enterprise.<br><br><br>* If **Employee** is selected, you need to set the scope by **Department** or **Role**.<br><br>* If **Device** is selected, you need to set the scope by **Device** or **Group**. |
   |**Distribution effective time** |Specify the effective duration of the current distribution task, which can be **One week** or **Scheduled**. The software package as defined in the distribution task can only be distributed to specific users or devices during the specified effective period. When the effective period ends, the distribution task will automatically expire and the software package will no longer be distributed. |
   |**Distribution frequency control** |Control the number of software packages distributed simultaneously.<br><br><br>* If **Disable** is selected, it indicates that the distribution frequency is not controlled.<br><br>* If **Enable** is selected, you need to set the number of distribution devices per minute. |
   |**Distribution speed limit (single device)**  |Specify the transfer rate at which the specific software package is distributed to a single device.<br><br><br>* If **Disable** is selected, this indicates that there is no restriction on the distribution transfer rate.<br><br>* If **Enable** is selected, you need to set the single\-device transfer rate in KB/s. |
   

6. In the **Distribution Record** tab of the **Distribution** page, view the execution statuses of all distribution tasks.

   You can see the distribution progress in the distribution record list. Click the package name to open the details page to view the specific distribution status.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02756e0e45ea4cb29c6c9cf92a01e234~tplv-goo7wpa0wc-image.image) </span>


<span id="0d6f9060"></span>
# Managing software list


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **Distribution**.

3. In the **Software List** tab of the **Distribution** page, locate the specific software package and select **Distribute**, **Edit**, or **Delete**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf78ee11a3fa4575bc474107ff6a21e0~tplv-goo7wpa0wc-image.image) </span>

   * **Distribute**: Configure a distribution task for the software package and distribute it to your target devices. For more information, please refer to [Distributing software to specific user device](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/6565917a1ef8eb02f973c947?docLang=en&bv=652fd8f3fb401502ea5effe0#8f6a2354).

   * **Edit**: Edit information for the software package, including **Remarks**, **software full name**, **software publisher**, and **BundleID**.

      The **software full name** and **software publisher** fields apply to Windows packages, and the **BundleID** field applies to Mac packages. If you do not know the default values for these fields, click **Guide** next to the corresponding field for instructions.

   * **Delete**: This operation deletes the selected software package and its corresponding distribution tasks that are in progress.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The resource cannot be restored after being deleted. Please operate with caution.      </div>
      

<span id="03728cd1"></span>
# Managing distribution record


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **Distribution**.

3. On the **Distribution** page, click the **Distribution Record** tab.

4. In the **Distribution Record** tab, you can view, edit or delete distribution tasks.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd13fccea46d4f72a2af22f04513292e~tplv-goo7wpa0wc-image.image) </span>

   * Click **View** in the **Action** column to view detailed information about the distribution task.

   * For a scheduled distribution task that has not yet been executed, you can click **More** \> **Pause** in the **Action** column, or click **Edit** to edit the distribution task.

   * If you do not enable the **Detect if the software was successfully installed on employee devices** option when adding a software package, you will see **Unable to get** in the **Installation result** column.

   * Please proceed with caution when deleting a distribution task, because this action cannot be undone.

      Deleting a distribution task while it is executing does not interrupt installations that are already in progress on specific devices.
