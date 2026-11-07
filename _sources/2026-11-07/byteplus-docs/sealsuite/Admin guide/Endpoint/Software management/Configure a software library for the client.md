---
title: "Configure a software library for the client"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-software-libraries-for-client"
---

You can add frequently used enterprise software to the software library in the Admin Console, which will synchronize all the software within the library to the software library on the SealSuite client. This allows users to download their desired enterprise software to their SealSuite clients. This article introduces how to configure the software library in the Admin Console.

<span id="e63ed9ea"></span>
# Instruction for use

The software library currently supports adding software for Windows or Mac systems.

<span id="fca4b4c4"></span>
# Adding software


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **Library**.

3. On the **Library** page, click **Add Software**.

4. On the **Add** **New software** page, complete the following configurations and click **Confirm**.

   
   |**Configuration Items** |**Description** |
   |---|---|
   |**Software Name** |Enter the software name in both English and Chinese. |
   |**Software Description** |Enter a description of the software in both English and Chinese. |
   |**Software classification** |The default classification is **Other**. You can add a category to the **Software classification** drop\-down list by clicking **Add** item in the lower right corner of the list. The added category will be used to group different enterprise software and display them under the corresponding category in the software library on the SealSuite client. |
   |**Icon** |In this option, you can choose to upload an icon for the software, which will be displayed in the software library on the SealSuite client. If the icon is not uploaded, the default icon will be used. |
   |**Visibility** |Specify the usage scope for the software. Available options include **Full** and **Restricted**. If you select **Restricted**, you need to set the specific usage scope based on the **Department** or **Role** dimension. |
   |**Add version** |Specify the way to add different versions for the current software. You can choose either **Upload package** or **Enter download link**. |
   |**OS** |Select the corresponding operating system for the software, select **Windows** or **Mac**, and multiple selections are supported.<br><br><br>* SealSuite supports uploading a software package for Windows in the following formats: exe, msi, bat, zip, rar, and tar.gz. Besides, the size of the package needs to be no greater than 2 GB.<br><br>* SealSuite supports uploading a software package for Mac in the following formats: pkg, dmg, zip, rar, and tar.gz type software packages, with a size not exceeding 2 GB.<br><br>* If **Add version** is set to **Upload package**, then you need to upload the software package that matches the operating system. After uploading the software package, you need to set the **Version number** and **Whether to upload this version**.<br><br>* If **Add version** is set to **Enter download link**, it is necessary to enter the **Download link**, **Software package MD5**, and **Version number** that matches the operating system.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can choose to fill in the Software package MD5 option.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the MD5 value of the software package is empty, the SealSuite client will not verify MD5 after the software version is launched.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the MD5 value of the software package is not empty, the SealSuite client will verify MD5 after the software version is launched. If the verification fails, users cannot download the current software and are prompted to contact the administrator to solve the verification failure.   </div><br>    |
   |**Mac packages differentiate between Apple and Intel chips** |After selecting **Mac** as the **OS**, if you need to add software for Mac computers with Apple silicon or for Mac computers with an Intel processor, you can check this option. |
   |**Support for specified parameters** |If you need to configure command\-line parameters for a silent installation or specify an installation directory for the software, you can check the **Support for specified parameters** option. After checking this option, you can specify the following parameters:<br><br><br>* **Silent installation**: Specify silent installation parameters such as `/S`.<br><br>* **Specify directory**: Specify installation directory parameters such as `installdir`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the administrator needs to distinguish the order of receiving parameters, you can click the position adjustment icon on the right side of the silent installation and specified directory parameters to adjust the parameter order.</div><br> |
   |**Detect if the software was successfully installed on employee devices** |When this option is enabled, SealSuite counts the devices in your enterprise on which the software is installed and displays the count in the **Number of installations** column of the **Library** list. You also need to configure the following software parameters.<br><br><br>* If you are adding software for Windows, you need to specify the **Application Name** and **Publisher** of the software.<br><br>* If you are adding software for Mac, you need to specify the **Bundle ID.**  |
   

5. In the software library list, locate the added software and click on it.

6. On the **Version list** tab of the software details page, turn on the **Status** switch.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d72b0616d284c198e98013258c576ba~tplv-goo7wpa0wc-image.image) </span>

   After the software is launched, it will be synchronized to the software library on the SealSuite client, in which users can select their desired software for installation.


<span id="6a636077"></span>
# Managing software


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **Library**.

3. On the **Library** page, you can perform the following operations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a09573cb75ea4041a1f2456d8054eb88~tplv-goo7wpa0wc-image.image) </span>

   * As shown in areas ① and ② above, you can search for your target software by using filtering conditions such as operating system, software status, category, and software name.

   * As shown in area ③ above, you can view software\-related information such as **Software Name**, **Visibility**, **Category**, **Shelf status**, **Shelf version**, **Number of installations**, **Downloads**, and **Software information**. You need to pay attention to:

      * If you enable **Detect if the software was successfully installed on employee devices** when adding software, SealSuite counts the devices in your enterprise on which the software is installed and displays the count in the **Number of installations** column.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">If this option is not enabled, the <strong>Number of installations</strong> column displays 0 by default.         </div>
         

      * **Downloads**: The total number of times users start a download from the software library and successfully obtain a download link. Once a link is obtained, the download is counted even if it is interrupted or the installation fails. Repeated downloads of the same software by the same user are counted separately.

      * Click **View Information** in the **Action** column to view basic information of the current software.

         * In the upper right corner of the **General** page, click **Edit** to adjust information such as **Software Name**, **Software Description**, **Software classification**, and **Visibility**.

         * Manually added **Software classification** supports deletion. If a certain category is deleted, all software included in that category will be changed to **Other**.

      * In the **Action** column, click **View version** to view the corresponding version information of the software. On the page that appears, you can add new versions, modify the published statuses of existing versions, and edit or delete a specific version. For more information on how to manage software versions, please refer to [Managing software version](https://docs.byteplus.com/en/docs/31/9207#b2203033).

      * Click **Delete** in the **Action** column, the software will be deleted and users can no longer download the deleted software on their SealSuite client.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
         

         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Please proceed with caution when deleting software, because software cannot be restored after being deleted.         </div>
         

<span id="b2203033"></span>
# Managing software version


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **Library**.

3. On the **Library** page, locate the specific software and click **View Information** in the **Action** column.

4. In the **Version list** tab, you can perform the following operations:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4d1713b893e4b979e65c34855df5398~tplv-goo7wpa0wc-image.image) </span>

   * **New Version**: If there is a software update for a specific software, you can upload the latest version of the software to the Admin Console by clicking **New Version** and completing the provided configuration items on the page that appears. You can select either **Upload package** or **Enter download link** as the uploading method.

   * **Status**: Set the published statuses of one or more versions of the software. If you publish multiple versions at a time, the SealSuite client will display the latest version.

   * **Edit**: Currently, you can edit the **Version number** and **Whether to upload this version** fields. If you are editing a software for Windows, you can choose to configure the **Support for specified parameters** option.

   * **Delete**: Delete the current software version.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Please proceed with caution when deleting a software version, because a software version cannot be restored after being deleted.      </div>
