---
title: "Updating skills"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_Skills"
---

Skills support continuous iteration. You can update a skill to improve its functionality and stability, enabling agents to be more effective across a wider range of business scenarios.

## Instructions

AgentKit supports two skill update methods. Choose the one that fits the complexity of your changes.

|Update method |Actions |Applicable scenario |
|---|---|---|
|Update skill code package |Overwrite the target skill's code files entirely by uploading a package, entering a TOS storage path, or copying a preset skill. |Complex changes such as feature iteration, structural refactoring, or large\-scale content updates. |
|Edit skill file |Directly modify the code file or directory structure of a skill in the console. |Lightweight changes such as minor bug fixes, parameter adjustments, or copy updates. |

## Prerequisites

A skill has been created. For details, see [Creating skills](https://docs.byteplus.com/en/docs/agentkit/create_skills).

## Procedure

### Method 1: Update the skill code package

> **warning**

> This method **directly overwrites the existing skill code**. The overwrite cannot be rolled back on the page. Verify that the package content is correct before updating to avoid disrupting production applications.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Select the "Skills" tab.

4. In the "Actions" column of the target skill, click the "Update" button.

5. On the "Update skill" page, select the corresponding update method and complete the parameter configuration. The update configuration is generally consistent with that for creating a skill. For more information, see [Creating skills](https://docs.byteplus.com/en/docs/agentkit/create_skills).

6. After the skill is updated, it must be published to the currently associated skills space before agents can call the updated version. **The system selects the associated skills space by default. Keep the default selection and** click "Confirm".

7. Verify that the update content is correct, and then click "Confirm" again to complete the skill update and publish the new version.

### Method 2: Edit the skill file

> **warning**

> Before uploading or updating a skill package, make sure the package meets the following requirements.**Noncompliant packages may cause updating or publishing to fail**.

* > **Package structure requirements**

   * > **Root directory**

      * > The package **contains exactly one root directory folder** after extraction, and the folder name must be consistent with the skill name.

      * > If no root directory folder exists after extraction, the platform **automatically creates one with the same name** as the root directory.

   * > **`SKILL.md`****location:**`SKILL.md`must be placed **under the root path** of the root directory folder, not in any subdirectory.

   * > **`SKILL.md`****lifecycle:**`SKILL.md`**cannot be deleted or renamed.**

* ### > SKILL.md field requirements

   > The SKILL.md header contains metadata fields such as `name` and `description` that identify the skill. These fields must meet the following requirements:

   * > **`name`****field**: Skill name, used to uniquely identify the skill. The value must meet the following requirements:

      * > It must not be empty and can be up to 64 characters in length.

      * > It can contain only lowercase letters, digits, and hyphens (\-). If the skill name contains uppercase letters, the platform will automatically convert them to lowercase.

      * > **It cannot contain the reserved field****`agentkit`**.

      * > The `name` field in the **`SKILL.md`** header cannot be modified.

   * > **`description`****field:**A description of the skill's functionality and purpose. The value must meet the following requirements:

      * > It cannot be empty and cannot exceed **1024 characters.**

      * > XML tags cannot be contained.

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Select the "Skills" tab.

4. In the skill list, click "Details" in the "Actions" column of the target skill.

5. On the skill details page, edit the skill file content or directory as needed.

   * **Edit file content**

      Select the target file in the left directory tree, and then edit the file content in the right panel. After the file content is edited, click "Save" to save the changes to the current file.

      > **tip**

      > Saving commits the current edits as **a new version** of the skill. This only affects the skill itself and does not update the version already published to the skills space.

   * **Edit the directory**

      In the **Project file** directory tree, right\-click the target file or folder to **rename, delete, create a file, or create a folder**. Click "Save" to save the directory structure changes.

      > **warning**

      * > Deleting a file or folder removes it from the skill immediately**and cannot be rolled back. Proceed with caution**.

      * > Saving commits the current edits as a new version of the skill. This only affects the skill itself and does not update the version already published to the skills space.

6. After confirming that the updates are correct, click "Publish" in the upper\-right corner of the page.

7. In the "Publish" panel that appears, select the target skills space and click "**Publish anyway**" to sync the latest version of the skill to that space, making the skill available for agents to call.

   > **tip**

   > If the skill has never been published to any skills space, you cannot publish it here after an update. Instead, click the [Add to skills space‌](https://docs.byteplus.com/en/docs/agentkit/Adding_and_Removing_Skills_in_Skills_Spaces?lang=en) button to publish it.

## Subsequent steps

Updating a skill only generates a new version of this skill. ** The new version does not take effect automatically.**  You need to manually **publish the new version to the specified skills space, then the updated capabilities can take effect in the corresponding skills space**. For details, see ** ** [Publishing skills](https://docs.byteplus.com/en/docs/agentkit/Publishing_Skills?lang=en).
