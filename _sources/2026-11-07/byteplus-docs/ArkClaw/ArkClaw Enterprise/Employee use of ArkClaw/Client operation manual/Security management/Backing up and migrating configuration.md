---
title: "Backing up and migrating configuration"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/backing-up-and-migrating-configuration"
---

With configuration backup and migration, you can export built\-in rules, custom rules, permission levels, and writable directories as configuration files, and import them to other devices or environments.

## Export or import a configuration

1. Log in to the ArkClaw client locally.

2. Switch to the target ArkClaw.

3. Click "![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_733c3e75c42df2726b84b0bb6a1cd7bc.png)\> Security management".

4. In the "Configure backup and migration" section of the **Overview** tab, click "Export configuration" or "Import configuration" as needed.

   **Export settings**

The exported file contains built‑in rules, custom rules, permission levels, writable directories, and other configuration. Keep the file secure. If it is unclear whether the file contains sensitive information, we recommend against uploading it to public code repositories or sending it to unrelated personnel.

   1. In the pop\-up dialog box, configure the following parameters.

      * **Save as**: Confirm or modify the configuration file name. The system automatically generates a default name.

      * **Tags**: Optional. Add file tags as needed.

      * **Where**: Select the directory where you want to save the file.

   2. Click "Save" to export the current configuration to the selected directory.

   **Import configuration**

Only JSON configuration files that meet the requirements can be imported. Before import, we recommend using **Export configuration** to generate a standard configuration file, then modifying or migrating based on that file.

   1. In the pop\-up dialog box, select the target JSON configuration file.

   2. Click the "Open" button.

   3. In the **Import security configuration** dialog box, select an import method.

      * **Import and merge**: Existing rules are kept. For rules with duplicate names, the newly imported ones take precedence.

      * **Import and replace**: Clear existing custom rules, then import the rules from the configuration file.

   4. View the differences between the configuration to be imported and the existing configuration.

      The system displays changes by configuration type, for example, built\-in rules, permission levels, writable directories, skill and connector lists, and custom rules. If the custom rules in the import file have duplicate names with existing rules, they will be marked as **Duplicate names** on the page.

   5. After confirming that everything is correct, click the "Confirm import" button.
