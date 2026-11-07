---
title: "Skill"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/skill"
---

Skill is a reusable capability unit in the Marketing Interaction Assistant, built on top of the MCP tool as an editable, testable, and reusable standard capability asset. Enterprises can encapsulate CRM, orders, memberships, work orders, knowledge bases, reports, approvals, and other systems as Skills, which can ultimately be used to expand agent capabilities. This article describes how to manage and use Skills in Marketing Interoperability Assistant.

# Function introduction

Marketing Interactive Assistant Skill supports natural language creation, which greatly reduces the threshold for building skills and improves the efficiency of skill building. You only need to tell the agent your appeal in natural language, and the AI can generate the skill configuration. In addition, if you already have skills, you can upload the skills to the Marketing Interactive Assistant by importing the Skill profile. Later, when you build an agent, you can add the published Skills to the agent to enrich its capabilities.

# Typical scene

|**Business scenario** |**Packageable Skills** |**Business value** |
|---|---|---|
|Customer service |Inquire about orders and generate replies, create work orders, and determine complaint levels |Improve agent efficiency and response consistency |
|Sell |Query customer portraits, generate follow\-up messages, and generate plan summaries |Reduce sales lead time |
|Finance |Inquire about product risk level, check appropriateness, generate compliance |Enhancing professional services and compliance |
|Store |Query inventory, inquire about activities, generate recommended words, and summarize business daily |Improve first\-line response efficiency |
|Operate |Aggregate activity data, identify anomalies, and generate review recommendations |Enhance operational analysis and decision\-making efficiency |

# New Skills

1. Log into the Marketing Agent console and select **Marketing Interactions** in the left navigation bar.

2. Select **Skill** in the left navigation bar of the Marketing Interactive Assistant, and select **New Skill** in the upper right corner of the page.

   When creating a new skill, it supports creating skills through conversation, and supports uploading files containing skill configurations to import skills.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dedb43aff7d145afb207467108445672~tplv-goo7wpa0wc-image.image)

   * **Method 1: New Skill \> Conversation Creation**

      This method can be built by natural language input Skill requirements (suggestions include: the core purpose of the skill and the target user, the input information that the user needs to provide when using it, the desired output format and style, and whether to call the tool), and then sent to the agent, the AI intelligence completes the construction of the Skill.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a59ff17b55049568b1f7989805b7103~tplv-goo7wpa0wc-image.image)

   * **Method 2: New Skills \> Import Skills**

      In the **upload new skill** pop\-up window, support the import of  **.zip** format Skill files, the maximum size of a single file does not exceed 3MB, and supports batch import (up to 10 files).

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/983cbbc64e6d4f98819684ade40d1bbe~tplv-goo7wpa0wc-image.image)

3. After creating a new one, go to the **editing skills** page.

   * On the left side of the page, support for entering Skills in natural language to modify requirements, and AI intelligently adjusts current Skills.

   * On the right side of the page, support editing Skill display name, Skill description (required, will be updated to the Skill.md file after saving), and support viewing skill files.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e71643dc1d054700965113afdc58b144~tplv-goo7wpa0wc-image.image)

4. Debugging Skills.

   When you're done editing Skill, click **Debug Preview** in the upper right corner of the page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b15ebe95781e456c98b39edfea355b6a~tplv-goo7wpa0wc-image.image)

   Enter test questions to debug Skills as expected.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5243321177340e98928c8451d0cf98a~tplv-goo7wpa0wc-image.image)

5. Select Save or Publish Skills.

   After editing and debugging, select **Save Only** or **Save and Publish** Skill in the upper right corner of the page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40d9a70cb7a04b38990585cfa0c469df~tplv-goo7wpa0wc-image.image)

   * **Save Only:**  After customizing the release notes, the current version content is saved, but not published. The corresponding skill status is **draft**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ceb608f131f4863a057da14cdb433cb~tplv-goo7wpa0wc-image.image)

   * **Save and publish:**  After customizing the release notes, save the current version content and publish the skill. The corresponding skill status is **Published**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70fc4008fe664008ae44781cb2fda89e~tplv-goo7wpa0wc-image.image)

      Published Skills can be used by agent associations, for details, please see [New Autonomous Planning Agent](https://docs.byteplus.com/docs/dataagent/New_Autonomous_Planning_Agent).

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae5c48cb3ea14d2f99ec0d93aec33bb3~tplv-goo7wpa0wc-image.image)

# View Call Experience and Skill Tuning

On the Skill details page, you can enter the call experience page to view the recent call records of Skill, and support AI\-based intelligent tuning of Skill.

1. Log into the Marketing Agent console and select **Marketing Interactions** in the left navigation bar.

2. Select **Skill** in the left navigation bar of Marketing Interactive Assistant.

3. Click the desired skill card to go to the skill details page.

4. At the top of the details page, click **Call Experience**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f890eb567bd498e8ab73c28ea37d2fc~tplv-goo7wpa0wc-image.image)

5. On the **call experience** page, the following operations are supported.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af125e51ae7a4714988e2549b7cfb157~tplv-goo7wpa0wc-image.image)

   * At the top of the page, support for UserID precision search call records; support setting time range, version, status filter call records.

   * The information that can be viewed includes the total number of Skill calls, the average call success rate, the call version, the UserID, the status, the Session ID, the call time, and the context.

   * Click **View Context Details** in the **Operation** column to view context detail data for the current call record.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c43ea03e4f874da5ab9485d6da3e46da~tplv-goo7wpa0wc-image.image)

6. (Optional) In the upper right corner of the **call experience** page, click **Skill intelligent tuning**, which can calculate the optimal instruction configuration, retry delay policy and high concurrency coping scheme based on log sample analysis.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc0aa850e951475b86b52a0934fb22f0~tplv-goo7wpa0wc-image.image)

   You need to complete the following configuration items:

   * Select the optimized version: that is, the version number of the skill that needs to be optimized.

   * Select a diagnostic model for evaluation: Select the large model to be used for intelligent tuning.

   * Call to record the number of samples to analyze: Set the number of samples to analyze.

7. Wait for the AI analysis to complete and check the tuning results.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7eccbafc99c44a76a743a53d030040d9~tplv-goo7wpa0wc-image.image)

   1. Select the optimization recommendations to be adopted.

   2. In natural language, choose to fill in the custom optimization direction.

   3. Select whether to release immediately after optimization.

   4. Click **Confirm and write the optimization plan**.

      To modify the Smart Tuning configuration, click **Back to Modify**.

   5. Wait for the AI intelligent tuning to complete, and click View Skill Configuration to view the tuning results.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ce7ef4315be4170b7af587147d584be~tplv-goo7wpa0wc-image.image)

# View the skill version

1. Log into the Marketing Agent console and select **Marketing Interactions** in the left navigation bar.

2. Select **Skill** in the left navigation bar of Marketing Interactive Assistant.

3. Click the skill card you want to view the version of to go to the skill details page.

4. Click the version number in the upper right corner of the details page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86169a44e1f44263aa10ff6136a143d8~tplv-goo7wpa0wc-image.image)

   View version history, history information includes historical version number, version description, creation time, and operator information.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f878a7f4dc184da4be411cbcb80e4ad5~tplv-goo7wpa0wc-image.image)

5. (Optional) Copy to a new version based on the specified version.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6193b1bf4abd4c7596c484dc11524fce~tplv-goo7wpa0wc-image.image)

6. (Optional) Version comparison.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f0ea6b1017142c79aa7d28ddf44dffe~tplv-goo7wpa0wc-image.image)

   In the **version comparison** pop\-up, specify the version comparison and click **Start Comparison**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2554f589b1fb4be79ed0762e9e511f4f~tplv-goo7wpa0wc-image.image)

# Copy/Delete/Download Skills

1. Log into the Marketing Agent console and select **Marketing Interactions** in the left navigation bar.

2. Select **Skill** in the left navigation bar of Marketing Interactive Assistant.

3. Hover the mouse over the skill card.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6527fb213b7474692c703c622b5c41c~tplv-goo7wpa0wc-image.image)

   * Click **Delete** to delete the current skill after a second confirmation. The deleted skill no longer supports being called by the agent.

      > **注意**

      > Once the skill is deleted, it cannot be restored. Please proceed with caution.

   * Click **Copy** and edit the skill name, ID and description in the **Copy Skill** pop\-up window to quickly copy and build a new skill based on the current skill

   * Click **Download** to download the skill file locally as a compressed package.

# Batch export/delete skills

1. Log into the Marketing Agent console and select **Marketing Interactions** in the left navigation bar.

2. Select **Skill** in the left navigation bar of Marketing Interactive Assistant.

3. Hover your mouse over the skill card and click **Select**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9de2bd8c370e44c2b01a808ccc07351f~tplv-goo7wpa0wc-image.image)

4. Support batch selection of multiple Skills, and choose to export or delete.

   > **注意**

   > Once the skill is deleted, it cannot be restored. Please proceed with caution.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb13c2820a1e405f93c3b8ccdb71aa19~tplv-goo7wpa0wc-image.image)
