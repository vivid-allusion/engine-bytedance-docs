---
title: "Manually creating skills"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/create_skills"
---

A **skill** is an on\-demand, modular capability unit. It standardizes and encapsulates the knowledge, operation processes, tool scripts, and associated resources required for a specific task. **Agents** can then stably execute the specified task, as if calling a function. You can create a skill by cloning a **preset skill**, **uploading a compressed package**, or pulling a file from **TOS**.

## Background information

During agent application development, task processing logic may be scattered across prompts, scripts, and knowledge files. Such scattered logic is costly to reuse, difficult to maintain, and unstable in execution. Encapsulating the related logic into a standardized skill enables capability reuse, version management, and unified deployment. It also improves the development and maintenance efficiency of agent applications.

A **skill** uses a progressive disclosure mechanism to provide the model with relevant content based on task requirements. This avoids loading a large amount of irrelevant information at one time, reducing token consumption. Typical application scenarios include intelligent customer service Q&A, automated office workflows, parameter verification for industrial equipment, and multimodal content generation.

## Prerequisites

Prepare the following conditions as needed, based on the **skill creation method** that you select and on **whether you need to associate the skill with a skills space**.

* **Upload compressed package**

   To create a skill via **Upload compressed package**, prepare in advance the complete [compressed code package](https://docs.byteplus.com/en/docs/347/88225#4e9LUxKM) required for building the skill. After the upload, the platform parses the configuration, script, and resource files in the compressed package and creates the skill.

* **TOS**

   To create a skill via **TOS**, upload the [compressed skill code package](https://docs.byteplus.com/en/docs/347/88225#4e9LUxKM) to a TOS bucket in advance and **obtain the TOS file address**. The platform pulls the code package from the TOS address and creates the skill. For more information, see [Uploading objects to BytePlus TOS](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1?lang=en).

* **A skill has been associated with a skills space during creation**

   To add a skill to the target skills space while you create the skill, [create the skills space](https://docs.byteplus.com/en/docs/agentkit/Skills_space) in advance.

   > **tip**

   > When creating a skill, you may skip adding it to a **skills space**. You can add it to the target skills space at any time later. For details, see [Adding/Removing skills](https://docs.byteplus.com/en/docs/agentkit/Adding_and_Removing_Skills_in_Skills_Spaces?lang=en).

   ## Skill code package requirements

Before you create a skill, make sure that the directory structure of the ZIP file and the **SKILL.md** metadata file meet the following requirements. You can also click **Download example** on the skill creation page to obtain the sample package. For details, see [Procedure](https://docs.byteplus.com/en/docs/agentkit/create_skills#C2KMgEGx) below.

> **warning**

> If you use the **Upload compressed package** method to create skills by uploading multiple code packages, the folder name (the skill name) in each code package must be unique.

### Directory structure

* After the ZIP file is decompressed, there must be one and only one root directory, and the directory name must be the same as the skill name. If no root directory exists, the platform automatically creates a directory with the same name as the skill.

* The ** SKILL.md ** file must be placed directly in this root directory, not in a subdirectory.

### SKILL.md metadata

|**Field** |**Description** |
|---|---|
|**name** |Defines the skill name in the SKILL.md ZIP file. The value must meet the following requirements:<br><br><br>* It must not be empty and can be up to 64 characters in length.<br><br>* It can contain only lowercase letters, digits, and hyphens (\-). If the skill name contains uppercase letters, the platform will automatically convert them to lowercase.<br><br>* It cannot contain the reserved field` agentkit`. |
|**description** |Describes the features and applicable scenarios of a skill. The value must meet the following requirements:<br><br><br>* It must not be empty and can be up to 1,024 characters in length.<br><br>* XML tags cannot be contained. |

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Click "Create skill  **\>**  Manual" to open the creation page, and configure the related parameters according to the table below.

   * **Basic information**

      |Parameter​ |Description |
      |---|---|
      |Creation method |Select the target creation method. The following methods are supported: "Clone with preset skill", "Upload compressed package", and "TOS".<br><br><br>* **Clone with preset skill**<br><br>   [Preset skills](https://docs.byteplus.com/en/docs/agentkit/Preset_Skills) are skills independently developed by the platform or officially certified by mainstream model providers. To **perform secondary development based on a preset skill**, use the "Clone with preset skill" method to create an **independent copy**, which reduces initial development and configuration costs.<br><br>   > **tip**<br>   <br><br>   * > After the clone is created, you can go to the skill details page to modify the content and publish a new version based on your business scenarios.<br>   <br><br>   * > If you only need to use a **preset skill** directly, you do not need to create it on this page. Instead, add the preset skill to a skills space. For operations, refer to [Adding skills](https://docs.byteplus.com/en/docs/agentkit/Skills_space).<br>   <br><br>* **Upload compressed package**<br><br>   If you select the **Upload compressed package** method to create a skill, you can upload the locally stored skill code package to the platform. You can upload one or more packages at a time.<br><br>* **TOS**<br><br>   Create a skill by pulling the corresponding skill ZIP file via a TOS address. If you select this method, you need to upload the skill ZIP file to TOS in advance. For details, see [Uploading objects to BytePlus TOS](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1?lang=en).<br><br>   > **warning**<br>   <br><br>   > Pulling a file from TOS is a one\-time operation. After the source file in TOS is **updated**, existing skills **will not automatically sync the changes**. You need to update the skill in AgentKit and publish a new version. For details, see [Updating skills](https://docs.byteplus.com/en/docs/agentkit/Updating_Skills) and [Publishing skills](https://docs.byteplus.com/en/docs/agentkit/Publishing_Skills).<br>    |
      |Clone with preset skill<br><br> |Select the card for the target **preset skill**. If the target skill is not displayed on the current page, click **View more preset skills** to browse more preset skills.<br><br>> **tip**<br><br><br>> Configure this parameter only when **Creation method** is set to "Clone with preset skill".<br> |
      |Compressed package |Upload one or more skill code packages based on your needs.<br><br><br>* Click **Click to upload** and select one or more local skill code packages to complete the upload.<br><br>* To upload more compressed packages in a batch, click **Continue upload** and upload more packages. You can upload up to **30 ** compressed packages at one time.<br><br><br>> **tip**<br><br><br><br>* > The system **generates a separate skill** for each uploaded compressed package.<br><br><br>* > Configure this parameter only when Creation method is set to "**Upload compressed package**".<br> |
      |TOS address |Enter the access address of the skill ZIP file in TOS. Address format: `https://${Bucket name}.${TOS domain name}/${Full object path}`. For the procedure for uploading compressed packages to TOS, refer to [Upload a file](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1).<br><br>> **tip**<br><br><br>> Configure this parameter only when Creation method is set to "**TOS**".<br> |
      |Skill name/description |By default, the page displays the name and description of the source preset skill. Change the skill name.<br><br>> **tip**<br><br><br><br>* > The name of the cloned skill **cannot be the same as the name of the source preset skill**, and all skill names must be unique within the tenant.<br><br><br>* > Configure this parameter only when **Creation method** is set to "Clone with preset skill".<br> |
      |Add to skills space |Click the "Add to skills space" drop\-down list, and then select the **existing skills space(s)**  in the current region.<br><br>> **tip**<br><br><br><br>* > When creating a skill, you may skip adding it to a skills space. You can add it to the target skills space later as needed. For details, see [Adding/Removing skills](https://docs.byteplus.com/en/docs/agentkit/Adding_and_Removing_Skills_in_Skills_Spaces?lang=en).<br><br><br>* > If none of the available skills spaces meet your business requirements, click "Create" to [create a skills space](https://docs.byteplus.com/en/docs/agentkit/Skills_space), and then select the new skills space.<br><br><br>* > After the newly generated skill (initial version: v1) is added to a skills space, it can be called by agents **without any publishing operation**.<br> |

   * **Advanced configuration**

      |Parameter​ |Description |Sample value |
      |---|---|---|
      |Project |A **project** is a collection of resources. You can add the currently created skill to the specified **project** and manage it by project, achieving resource isolation and data security control. For more information, refer to[ Project management](https://docs.byteplus.com/en/docs/agentkit/Managing_projects).<br><br><br>* The system selects the **default** project by default. A resource can belong to only one **project**. To change the project associated with the skill, click the "Associated project" drop\-down list and select the target project.<br><br>* After the project is selected, the created skill can only be accessed and used by users with permissions for that project.<br><br>* If the existing **projects** do not meet your business needs, you can click "Create project" to create one. After you create the project, return to this page and select the new **project**. |default |
      |Tag |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources.<br><br>Click "+ Add tag", select an existing tag or enter a new tag, and then associate the tag with the skills space. For more information, refer to [Tag management](https://docs.byteplus.com/en/docs/agentkit/Tag_management).<br><br>> **tip**<br><br><br>> Up to 20 tags can be added.<br> |Key1:Value1 |

4. Click "Create" to complete the operation.

## What to do next

After you create a skill, you can continuously iterate on the skill content and generate multiple versions to adapt to changing business requirements. Updating a skill only generates a new version. ** You need to publish it for the capabilities of the new version to take effect in the target skills space.**

1. [Update the skill](https://docs.byteplus.com/en/docs/agentkit/Updating_Skills)

   Skills support continuous iteration. You can update a skill to improve its functionality and stability, enabling agents to be more effective across a wider range of business scenarios.

2. [Publish the skill](https://docs.byteplus.com/en/docs/agentkit/Publishing_Skills?lang=en)

   After confirming that the new version content and test result are correct, publish the current version to the target skills space so that the capabilities of the new version take effect in the space.
