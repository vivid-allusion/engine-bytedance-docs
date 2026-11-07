---
title: "Managing built-in plugins"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/manage-built-in-plugins"
---

Cloud Search provides various plugin features through more than 20 plugins, including plugins supported by open source Elasticsearch and self\-developed plugins.

<span id="146cb8a0"></span>
## Installing built\-in plugins

There are some plugins in the instance plugin list with the status of **Not installed**. If you need to use these plugins, you can install them as needed. Installing the plugin triggers the restart of the instance. We recommend that you install plugins during off\-peak periods.


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar, select **Instance Management \> Plugin Management** and click the **System built\-in plugin** tab.

5. On the **System built\-in plugin** page, click **Bulk install/upgrade/uninstall**.

6. In the **Actions** column of the target plugin, check **Install,**  and select the version of the plugin you want to install, and then click **Bulk submit**.

   You can also check multiple built\-in plugins to install them in a batch.

7. In the **Bulk submit** dialog box, review the prompt message for installing the plugin, and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Installing a built\-in plugin triggers a cluster restart. We recommend that you install plugins during off\-peak periods.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the target plugin has already been installed, the system uninstalls the historical version of the plugin and then installs the specified version of the plugin.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3a4c2071f9e467bbfd5f9b658dc37a7~tplv-goo7wpa0wc-image.image) </span>

8. View the installation progress.

   After the installation steps are complete, the status of the plugin is displayed as **Installing**. When the status changes to **Installed**, the plugin is installed successfully and available for use.


<span id="795c9ba9"></span>
## Upgrading built\-in plugins

If there are multiple versions of the plugin, you can upgrade the version of the plugin according to your business needs.


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar, select **Instance Management \> Plugin Management** and click the **System built\-in plugin** tab.

5. On the **System built\-in plugin** page, click **Bulk install/upgrade/uninstall**.

6. In the **Actions** column of the target plugin, check **Upgrade,**  and select the target version to upgrade to, and then click **Bulk submit**.

7. In the **Bulk submit** dialog box, review the prompt message and the upgraded plugin version, and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Installing a custom plugin triggers a cluster restart. We recommend that you install plugins during off\-peak periods.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the target plugin has already been installed, the system uninstalls the historical version of the plugin and then installs the specified version of the plugin.   </div>
   

8. View the upgrade progress.

   After the upgrade steps are complete, the historical version of the plugin is displayed as **Uninstalling** and the new version of the plugin is displayed as **Installing**. When the plugin version is displayed as the new version, it means that the plugin upgrade is successful.


<span id="e482bd25"></span>
## Uninstalling built\-in plugins

Built\-in plugins that you installed manually can be uninstalled. When you no longer need such a plugin, you can uninstall it. Uninstalling a plugin triggers a cluster restart. We recommend that you uninstall plugins during off\-peak periods.


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar, select **Instance Management \> Plugin Management** and click the **System built\-in plugin** tab.

5. On the **System built\-in plugin** page, click **Bulk install/upgrade/uninstall**.

6. In the **Actions** column of the target plugin, check **Uninstall**, and then click **Bulk submit**.

   You can also check multiple built\-in plugins to uninstall them in a batch.

7. In the **Bulk submit** dialog box, confirm the plugins that need to be uninstalled, and then click **OK**.

8. View the uninstallation progress.

   After the uninstallation steps are complete, the status of the plugin is displayed as **Uninstalling**. When the status changes to **Not installed**, the plugin is uninstalled successfully.
