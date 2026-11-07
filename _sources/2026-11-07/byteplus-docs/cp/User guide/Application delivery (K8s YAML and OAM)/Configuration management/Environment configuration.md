---
title: "Environment configuration"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Environment_configuration"
---

Environment configuration is used to manage configuration items and their values in each environment instance and to record every configuration change. This article introduces actions related to environment configuration.

<span id=".57yW6L6R6YWN572u"></span>
## Edit configuration

Enable or disable custom configuration items and set their values in the target environment instance.


1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp), and in the left navigation bar, select **workspace**.

2. Click the target workspace name, and in the left navigation bar of the current workspace, select **Application Delivery \> Application Management**.

3. Click the target application card to open the application. Click **Configuration**, and then switch to the configuration tab.

4. Click **Environment configuration** to switch to the environment configuration module. Select the target environment instance card, then click **Edit configuration values**.

5. On the configuration editing page, you can enable or disable configurations as needed.

   * Enable the configuration

      1. Bulk select the configuration items to enable in the disabled configuration list on the left, then click **Enable**. The selected configuration items will move to the enabled configuration list on the right.

      2. Enable the configuration list, and set the value of each configuration item. You can enter a specific value or leave it blank.

   * Configuration deactivation

      1. In the enabled configuration list on the right, select in bulk the configuration items that need to be disabled, then click **Disable**. The configuration items will be moved to the not enabled configuration list on the left.

   * Modify enabled configuration item values

      1. In the list of enabled configurations on the right, locate the configuration item to be modified, click the edit icon, and change its value.

6. Click **OK** to complete editing the configuration.


<span id=".562b6YCJ6YWN572u"></span>
## Filter configuration

Quickly filter the configuration of the target environment instance in scenarios with multiple environment instances.


1. On the configuration tab of the current application, click **Environment configuration** to switch to the environment configuration module.

2. Filter the target environment type.

   The upper right corner displays **All**, **Development**, **Testing**, **Staging**, and **Production** environment types. Click to switch to the configuration for the corresponding environment type.

3. Further filter the target environment instances.

   After completing Step 2, click the system icon in the upper right corner. When the environment instance information dialog appears, check the target environment instance and click **OK**. The configuration for the corresponding environment instance can then be displayed.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To further filter target environment instances where configuration is not enabled, in the environment instance information box in Step 3, click the funnel icon and select <strong>Show only instances with configuration disabled</strong>.</div>


<span id=".5om56YeP5aSN5Yi26YWN572u"></span>
## Batch copy of configurations

Batch copy enabled configuration items and values from the source environment to multiple environments, allowing users to reuse existing environment configurations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After a batch copy is successful, the existing configuration of the target environment will be overwritten.</div>



1. In the configuration tab of the current application, click **Environment configuration** to switch to the environment configuration module.

2. Click the **Batch copy** button in the upper right corner. On the batch copy configuration page, select the source environment instance and the target environment instance. Target environment instances support multi\-selection.

3. Select the configuration items to copy in bulk, and click **Confirm**.

4. In the secondary confirmation dialog, click **confirm**.

   The selected configuration items from the source environment will immediately take effect in the target environment, and the target environment's previous configuration will be overwritten.


<span id=".5p-l55yL546v5aKD6YWN572u5Y-Y5pu06K6w5b2V"></span>
## View environment configuration change records

Allows users to view configuration change records for each environment instance, facilitating the tracing and auditing of every change.


1. On the configuration tab of the current application, click **Environment configuration** to switch to the environment configuration module.

2. Click the **Change history** button in the upper right corner. On the Environment configuration change history page, click the target environment instance name to view the configuration change history for that environment instance.

   The list displays all change records, the creator, and the creation time.

3. Click the change record ID to view the details of this change.
