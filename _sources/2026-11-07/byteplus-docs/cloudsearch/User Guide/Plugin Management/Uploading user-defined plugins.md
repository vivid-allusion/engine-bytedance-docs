---
title: "Uploading user-defined plugins"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/custom-plugins"
---

Cloud Search supports user\-defined plugins. You can upload user\-defined plugins as needed.

<span id="2817d7f3"></span>
## Background information

Before you prepare a user\-defined plugin package, familiarize yourself with the relevant requirements for the plugin\-descriptor.properties and plugin\-security.policy files.

<span id="94451f5d"></span>
### plugin\-descriptor.properties

You must declare the **plugin name**, **plugin version**, and **instance version** in the `plugin-descriptor.properties` file and place the file in the root directory extracted from your ZIP package.

The key fields in the plugin\-descriptor.properties file are described as follows:


* name: the plugin name.

* version: the version of the plugin.

* description: a brief functional description of the plugin. After the plugin package file is uploaded, the description of the plugin is displayed on the **User\-defined plugin** tab of the ES instance details page.

* elasticsearch.version: the Elasticsearch version. If the Elasticsearch version declared by the plugin is inconsistent with the version of the target instance, the upload fails.


<span id="f2da71e7"></span>
### plugin\-security.policy

The plugin\-security.policy file of a user\-defined plugin cannot contain the following sensitive permissions:


* File permissions: Arbitrary read, write, and execute operations on files are not allowed.

* Network permissions: Operations including but not limited to listening to or initiating network requests are not allowed.


<span id="e0989806"></span>
## Precautions

When you install a user\-defined plugin on an instance, the user\-defined plugin may affect the stability of the instance. Make sure that the availability and security of the user\-defined plugin are guaranteed.


* The file extension of your package file must be `.zip`. The file name can contain only uppercase letters, lowercase letters, digits, hyphens ( \- ), and periods ( . ). The name must be 8–128 characters in length.

* The file size is up to 100 MiB.

* A maximum of 5 different versions of plugin files can be uploaded for each plugin. The file name must be unique.

* When you upload a user\-defined IK plugin, it cannot have the same name as the built\-in IK plugin. In addition, the Analyzer and Tokenizer in the code cannot have the same name.

* When you upload a user\-defined plugin, the Elasticsearch version in the plugin\-descriptor.properties file must be consistent with the version of the target instance.

* When the instance is upgraded, the user\-defined plugin is not updated. You must upload it again.

* If an issue such as an upload failure, installation freeze, or uninstallation freeze occurs when you upload or install the user\-defined plugin, troubleshoot the issue by referring to [Troubleshooting custom plugin installation issues](https://docs.byteplus.com/en/docs/cloudsearch/custom-plugin-issues).


<span id="de69f3d6"></span>
## Procedure


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar, select **Instance Management \> Plugin Management** and click the **User\-defined plugin** tab.

5. On the **User\-defined plugin** page, click **Upload file**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4be1d44595d34d11b6348bbbd7923888~tplv-goo7wpa0wc-image.image) </span>

6. In the **Upload plugin** dialog box, select the user\-defined plugin files from the local directory, check the relevant prompt information, and then click **OK**.

   In case error message occurs during file uploading, modify the plugin file accordingly.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a54acc5c8554f77a6a0d562ac0e2d4b~tplv-goo7wpa0wc-image.image) </span>


<span id="f048167b"></span>
## Viewing plugin files

A maximum of 5 different versions of plugin files can be uploaded for each plugin and only 1 of them can be installed. You can view the list of plugin files and installed plugin versions.


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar, select **Instance Management \> Plugin Management** and click the **User\-defined plugin** tab.

5. On the **User\-defined plugin** page, select the target plugin and click the button `+` in front of the plugin.

6. View the list of plugin files and installed plugin versions.
