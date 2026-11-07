---
title: "Installing user-defined plugins"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/install-user-defined-plugins"
---

Cloud Search supports user\-defined plugins. You can install user\-defined plugins as needed.

<span id="ab2af601"></span>
## Before you begin

Installing a plugin on an instance triggers a cluster restart. If the plugin has a code defect, the instance nodes fail to start after the installation, and the stability of the cluster is compromised.

Any user\-defined plugin you want to upload and install on a Cloud Search instance must be installed and tested in your self\-managed Elasticsearch service in advance. The plugin can be uploaded and installed to the Cloud Search instance only if it passes the installation test.


1. Run the following command to install the plugin in your local Elasticsearch service.

   `./bin/elasticsearch-plugin install file:///path-to-your-plugins.zip`

2. Restart the cluster to load the plugin

3. Verify that the plugin is installed successfully.

   Run the `GET /_cat/plugins?v` command to get the plugin information and determine whether the plugin is installed successfully.


<span id="2ed3b487"></span>
## Procedure

After user\-defined plugins are uploaded, you can install them.


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar, select **Instance Management \> Plugin Management** and click the **User\-defined plugin** tab.

5. On the **User\-defined plugin** page, click **Bulk install/upgrade/uninstall.** 

6. In the **Actions** column of the target plugin, check **Install,**  and select the version of the plugin you want to install, and then click **Bulk submit**.

   You can also check multiple user\-defined plugins to install them in a batch.

7. In the **Bulk submit** dialog box, review the prompt message for installing the plugin, and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Installing a user\-defined plugin triggers a cluster restart. We recommend that you install plugins during off\-peak periods.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the target plugin has already been installed, the system uninstalls the historical version of the plugin and then installs the specified version of the plugin.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The user\-defined plugin may affect the stability of the instance. Make sure that the availability and security of the user\-defined plugin are guaranteed.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a10138f0102e4cce9b060efc37a39d7d~tplv-goo7wpa0wc-image.image) </span>

8. View the installation progress.

   After the installation steps are complete, the status of the plugin is displayed as **Installing**. When the status changes to **Installed**, the plugin is installed successfully.


<span id="ce3890b6"></span>
## Upgrading user\-defined plugins

A maximum of 5 different versions of plugin files can be uploaded for each plugin and only 1 of them can be installed. After the plugin is installed, you can upgrade the version of the plugin according to your business needs.


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar, select **Instance Management \> Plugin Management** and click the **User\-defined plugin** tab.

5. On the **User\-defined plugin** page, click **Bulk install/upgrade/uninstall.** 

6. In the **Actions** column of the target plugin, check **Upgrade,**  and select the target version to upgrade to, and then click **Bulk submit**.

7. In the **Bulk submit** dialog box, review the prompt message and the upgraded plugin version, and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Installing a user\-defined plugin triggers a cluster restart. We recommend that you install plugins during off\-peak periods.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the target plugin has already been installed, the system uninstalls the historical version of the plugin and then installs the specified version of the plugin.   </div>
   

8. View the upgrade progress.

   After the upgrade steps are complete, the historical version of the plugin is displayed as **Uninstalling** and the new version of the plugin is displayed as **Installing**. When the plugin version is displayed as the new version, it means that the plugin upgrade is successful.
