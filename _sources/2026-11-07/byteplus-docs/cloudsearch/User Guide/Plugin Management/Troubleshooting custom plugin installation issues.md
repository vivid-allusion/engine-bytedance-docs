---
title: "Troubleshooting custom plugin installation issues"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/custom-plugin-issues"
---

This topic describes how to troubleshoot issues such as upload failures, installation freezes, or uninstallation freezes in the use of custom plugins.

<span id="cd45837f"></span>
## plugin upload failure

The general requirements for plugin package files are as follows:


* The plugin package file must be in the ZIP format. The file name can contain only uppercase letters, lowercase letters, digits, hyphens ( \- ), and periods ( . ). The file name must be 8–128 characters in length.

* The plugin package file must be less than 100 MiB in size.

* Up to 50 plugin package files can be uploaded to a single instance.

* The name of the plugin package file must be unique within the instance.


The plugin package file name is different from the plugin name. The package file name refers to the name of the ZIP file to be uploaded. The plugin name is extracted from the `plugin-descriptor.properties` file in the ZIP package file. The following table describes possible reasons for plugin upload failures.


|**Issue Type** |**Common Reason** |**Solution** |
|---|---|---|
|Duplicate name |The system does not allow you to upload a plugin that has the same name as a system or custom plugin. |If the plugin to be uploaded has the same name as a system plugin, use the system plugin.<br><br>If the plugin has the same name as a custom plugin, confirm whether you selected the correct plugin package file. If you want to upgrade a custom plugin, first uninstall and delete the current custom plugin, then upload a later version of the plugin with the same name. |
|Instance version mismatch |The Elasticsearch version declared by the plugin does not match the version of the target Cloud Search instance. |Confirm whether the Elasticsearch version declared by the plugin is consistent with the Cloud Search instance version. If the versions are inconsistent, update the plugin, make sure that the same version of the plugin can be successfully installed in the local Elasticsearch service, and then upload the plugin. |
|Lack of the plugin\-descriptor.properties file |The `plugin-descriptor.properties` file does not exist or is not located in the root directory extracted from the ZIP file. |Repackage a ZIP plugin file with the correct directory. Make sure that the root directory extracted from the ZIP file contains the plugin\-descriptor.properties file and the JAR file. |
|Security issue |The plugin defines sensitive file or network permissions. As a result, the upload request is denied due to excessive permissions. |View the permission definition in the `plugin-security.policy` file, and delete the relevant sensitive permissions.<br><br>For more information on the plugin\-security.policy file, refer to [plugin-security.policy](https://docs.byteplus.com/en/docs/cloudsearch/custom-plugins). |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Installing a plugin on a Cloud Search instance triggers a cluster restart. If the plugin has a code defect, the instance nodes fail to start after the installation, and the stability of the cluster is compromised.</div>


<div data-tips="true" data-tips-type="warning">Any custom plugin you want to upload and install on a Cloud Search instance must be installed and tested in your self\-managed Elasticsearch service in advance. The plugin can be uploaded and installed to the Cloud Search instance only if it passes the installation test.</div>


<div data-tips="true" data-tips-type="warning">Run the following command to locally install a plugin: <code>./bin/elasticsearch-plugin install file:///path-to-your-plugins.zip</code></div>


<span id="19e42ebd"></span>
## plugin staying in the Installing state for a long time

Possible reasons for causing a plugin to stay in the **Installing** state for a long time include:


* Installing a plugin requires a rolling restart of the entire Cloud Search instance. If the cluster contains a large number of nodes, the restart process takes a longer period of time.

* The plugin has a code defect. As a result, the instance nodes fail to restart after installation, and the stability of the cluster is compromised.

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We strongly recommend that you install and test the plugin in your self\-managed environment and confirm that the plugin is free of errors before you upload it to a Cloud Search instance for installation. If the Cloud Search instance fails to restart due to plugin defects, contact our technical support.   </div>
   

<span id="1a54ddcd"></span>
## plugin staying in the **Uninstalling** state for a long time

Possible reasons for causing a plugin to stay in the **Uninstalling** state for a long time include:


* Uninstalling a plugin requires a rolling restart of the entire Cloud Search instance. If the cluster contains a large number of nodes, the restart process takes a longer period of time.

* The plugin to be uninstalled is being used by some indices. As a result, the nodes fail to restart after uninstallation.

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We strongly recommend that you confirm that the plugin is not used by any index before you uninstall it. If a cluster status exception occurs due to the uninstallation of a plugin in use, contact our technical support.   </div>
