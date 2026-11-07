---
title: "Skill Center"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Skill_Center"
---

The iDA Skill Center is used to manage and use various agent skills in a unified manner, helping you quickly invoke corresponding capabilities according to scenarios and improve task processing efficiency. For example, it is suitable for automated customer service Q&A, data report generation, code\-assisted writing, and other task scenarios. This document will explain the process of viewing, configuring, and using Skills, so that you can quickly understand the functions and basic operation methods.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af05e9377863433da577e87389c9b5bf~tplv-goo7wpa0wc-image.image) </span>

<span id="1413b643"></span>
# Precautions


* After the skill is released, it will be displayed in the Skill Market on the dialogue side, and you need to manually add it on demand before you can use it. The administrator can bind the release skill to the agent, and all users of the agent can use the skill in this agent after binding.


<span id="184885b5"></span>
# Create skills

The Skill Center supports two types of creation: **creating skills through conversation or uploading skills**. The following is a detailed description of the two creation methods:


|Creation method |Applicable scenario |Core Results |
|---|---|---|
|Create through conversation |Only skill objectives, usage scenarios or ability descriptions, and no complete skill file yet. |Enter the conversation and use the skill to create a skill, and the system will generate a skill file; after the creation is completed, you can continue to debug or publish it to the Skill Center. |
|Upload skills |There are already `Skill.zip` or `SKILL.md` files in the local area that need to be published to the Skill Center. The file size limit is **50MB.**  |After uploading the file, it will automatically parse the basic information, enter the skill configuration panel, and fill in the usage scenarios, examples, permissions, and authorized agents before publishing. |


<span id="e2f12004"></span>
## Upload skill

Upload skills to create scenarios where you have a skills file ready and need to publish skills to the Skill Center by uploading `Skill.zip` or `SKILL.md`. This method does not rely on dialogue generation, and focuses on file upload, basic information completion, usage scenario selection, permission configuration, agent authorization, and release confirmation.


1. Log in to iDA, navigate to select Skill Center at the top of the agent list, and enter the Skill Center.

2. Click **Create Skill → Upload Skill** in the Skill Center to open the "Upload New Skill" pop\-up window. Drag and drop files to the upload area, or click the **click to upload button**; only Skill.zip and SKILL.md are supported.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ab72b9e0b3a4f4797ae0615df8e336e~tplv-goo7wpa0wc-image.image) </span>

3. After the file upload verification is passed, enter the skill configuration, and the system will resolve the skill name, description and file resource directory.

4. You can modify and complete the relevant configuration as needed. After confirming that it is correct, click **Save Only** or **Publish**; after publishing, the skills will be displayed according to the scope of permission.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6d14f5b1a214b979fc743dca2480d00~tplv-goo7wpa0wc-image.image) </span>

   
   |Skill profile |Required field |Description |
   |---|---|---|
   |Skill file |Yes |Shows the currently uploaded skill pack file. You can click **Replace** on the right to re\-upload. |
   |Skill name |Yes |The system identification name of the skill, used for skill registration, identification, and invocation, must be a combination of lowercase and dash. |
   |Display name |Yes |The name of the skill displayed in the Skill Center. |
   |Skill description |Yes |Describe the skills' abilities, applicable scenarios, and output effects. |
   |Version description |No |Record the version changes uploaded, modified, or published this time. |
   |Usage scenario |No |Bind the applicable scenario tag for the skill. For information on how to create and manage scene labels, see the "Scene Management" section of this document. |
   |Prompt example |No |A typical way to demonstrate skills.<br><br>**Add Example:**  Click the Add Example button to add a prompt example.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db26151d6a5643ffbd154aeb10e6b12e~tplv-goo7wpa0wc-image.image) </span> |
   |Available roles |Yes |To control which members the skill is visible or available to, select All Members/Creator Only/Designate Members.<br><br>When selecting a specified member, drop down to select a specific user. |
   |Set as Featured Skills |No |Once enabled, skills can be displayed in a "curated" category; suitable for highly versatile and high\-quality skills. |
   |Agent authorization |No |You can select or enter the agent name search; control the agent call range, which is not equivalent to the member visible range. |
   |**File details** | |Display previews of resource directories and file content, focusing on `name`and `description` in SKILL.md.<br><br>And other information; used to confirm whether the uploaded package is complete and whether the skill definition is correct. |
   


<span id="1166af87"></span>
## Create through conversation

Creating skills through conversation is suitable when you are not ready to Skill.zip or SKILL.md files, but have clearly defined the skills you want to create abilities, use scenarios, or perform effects. The system generates skills based on your natural language description through "Skill Creation", and supports continued adjusting and validation before release.


1. In the upper right corner of the skill center page, click **Create Skill → Create Through Conversation.**  The system will automatically jump to the conversation page and automatically select "Skill Creation", you can directly enter the skill description and initiate a session.

2. Once on the conversation page, describe the skill you want to create in the text box. The following information is recommended:

   * What problem should the skills solve?

   * In what scenario is the skill triggered?

   * What inputs does the skill need to process?

   * What results should the skill output?

   * Whether you need to use files, data sources, web search, or other tools

   * Do you need to post to the Skill Center?


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Example: Use <strong>Skill Creation</strong> to help me create a skill and post it to Skill Center: I need a "Contract Risk Summary" skill. When uploading a contract PDF or Word file, automatically extract the contract subject, amount, term, payment terms, breach of contract liability, and exception risk, and output an English summary. Applicable scenarios are legal review and procurement contract pre review.</div>



3. After submitting a requirement, the system will first check whether you have similar skills within your current visibility.

   * If similar skills exist, the system will display a list of similar skills, including display name, skill name, description, and skill address, and ask whether to continue creating new skills.

   * If no reusable skill exists: The system continues to call **skill authoring** to create a new skill based on your description.

4. After the skill is generated, you can continue to make modification requests for iDA or click the skill file generated by iDA to enter the editing page for manual modification, such as modifying the skill name, supplementing trigger conditions, adjusting the output format, increasing usage restrictions, optimizing skill descriptions, adding or deleting references, etc.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dff59ff817c34481b293261458cf14a0~tplv-goo7wpa0wc-image.image) </span>

5. After the modification is completed, click the "Publish" button at the bottom of the skill editing page to publish to the Skill Center.


**Demo:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6aaf766a476e46afaed9956212caabe1~tplv-goo7wpa0wc-image.image) </span>

<span id="cf050a17"></span>
# Skill list

Successfully created and published skills are displayed in the Skill Center in the form of a list, which supports editing, downloading, taking offline, copying, and deleting individual skills. The Skill Center supports searching by skill name, usage scenario, and you can filter by scenario classification or status (All Status/Published/Unpublished/Draft).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43a136054ca940c0bb32d919a4f35e37~tplv-goo7wpa0wc-image.image) </span>


|Area |Name |Function Description |
|---|---|---|
|1 |Skill Category Switch |Used to switch list ranges by skill source or type, including **All, Created by me**, **Featured**, and **Official** categories; the number after "All" indicates the current skill count. |
|2 |Filter, search area |Used for quick filtering, search skills, including scene filtering, status filtering, available role filtering, support for searching by skill name. |
|3 |Skill operation |Used to perform administrative operations on a single skill, common operations include editing, downloading, and more.<br><br><br>* Edit: Click the Edit button to enter the skill configuration page to publish or modify the skill;<br><br>* Download: Export current skills to local storage for easy backup, migration, or reuse.<br><br>* Take offline: Withdraw the published skill so that it **stops serving** and the user can no longer invoke it. It is often used for version updates or emergency fixes.<br><br>* Copy: Quickly generate a **draft copy** based on current skills for **iterative optimization** or creating similar skills, the original version is not affected;<br><br>* Delete: The skill is **completely removed**, and the data cannot be recovered. |


<span id="55a9777b"></span>
## View skill details

Click on a specific skill in the skill list to enter the skill details to view the skill details, including the skill's display name, skill name, skill label, creator, and other information. Here are the relevant operating instructions in the skill details:


|Function item |Detailed description |
|---|---|
|**Basic information** |After clicking "Edit Basic Information", you can modify the following content in the pop\-up window:<br><br><br>* Name of skill display: Limit to 20 characters.<br><br>* Skill Name: Must be a combination of lowercase and dash.<br><br>* Scene Configuration: Select the scene label you want to bind.<br><br>* Usage Scenario: Limit to 150 characters.<br><br>* Skill instructions: Support Markdown format, can switch between edit and preview.<br><br><br>After modification, click the "Save and Publish" button, and the system will automatically generate a version record.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbce5ca009534c03900a7663e57e1c9d~tplv-goo7wpa0wc-image.image) </span> |
|**Historical version** |After the basic information is edited, the system will automatically generate a version record. By switching the historical version tab, you can view the release records of all historical versions of the skill. Support selecting historical versions for rollback, view details and download operations.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1745b0528bd44f3c9eab97499930fb86~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When there is only one version of the skill, rollback operations are not supported.</div><br> |
|**Download skills** |Click the **Download skill** button to package the current skill file in `.zip` format and download it locally, which can be used for backup or migration. |
|**Taking offline** |Take offline with the published skill, which is invisible and cannot be called by the agent after going offline; the offline operation needs to be confirmed twice, and it can be online again after taking offline. |
|**Copy** |Quickly generate a **draft copy** based on current skills for **iterative optimization** or creating similar skills, the original version is not affected; |


<span id="4b41f978"></span>
# Scene management

Scenario management is used to classify and label agents, skills, or related resources for unified maintenance, quick retrieval, and efficient management. With scenario management, you can organize your content structure more clearly, improving search efficiency and ease of use. You can bind created scene labels to skills when you create or edit them.


1. Click **Scene Management** under the Scene Filter box in the Skill Center, and the scene management pop\-up window will pop up.

2. Enter a new scene name in the text box at the top of the pop\-up window and press Enter to add it. It is recommended to use concise and clear scene names to avoid repetition or overly broad meanings.

3. After the addition is successful, it will be displayed in the scene management, and you can edit and delete the scene.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24f5560011354dbe94db99d6f7f99426~tplv-goo7wpa0wc-image.image) </span>

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01bf59d847b84e8c9bc41fd5919df422~tplv-goo7wpa0wc-image.image" width="400px" />   </div>
   


<span id="6fc6172e"></span>
## Binding scene

Skills can bind a successfully created scenario when creating skills, and supports modification when editing skills in skill details.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2c207d0a0974e6da4f5224ced2a8e62~tplv-goo7wpa0wc-image.image) </span>
