---
title: "Agent templates"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Agent_templates"
---

An agent template is preset to create an agent in a Claw instance. Employees can create dedicated agents based on agent templates or use a template directly to initiate a task. A single Claw instance supports creating multiple distinct types of agents to fulfill task requirements across different scenarios.

## Agent template types

Agent templates are divided into two types:

* **BytePlus featured**: Official templates recommended by the platform. They are visible to all employees by default. If your enterprise does not need them, administrators can disable them. For details, see the **Enable or disable BytePlus featured templates** section below.

* **Enterprise\-recommended**: Agent templates created by enterprise administrators or by employees and approved by administrators. Administrators can set the employee visibility scope of each template. Employees cannot access templates that are not visible to them.

## BytePlus featured

### Enable or disable BytePlus featured templates

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Template Center".

3. Click "Agent templates" \> "BytePlus featured".

4. Manage BytePlus featured templates.

   * **View template information**: Click the target card to view the name, description, code of conduct, and workflow of the template on the template details page.

   * **Enable/disable BytePlus featured templates**: Click the "Enable/Disable BytePlus featured" switch next to the search box.

      When enabled, BytePlus featured templates are displayed in "Agent Center" \> "Agent Gallery" for employee Claw instances in the employee\-side console and can be used directly. When disabled, these templates are invisible and unavailable.

## Enterprise\-recommended

### Create templates

> **warning**

> Capabilities described in this section are in beta and are only available after being enabled. To apply for a trial, contact your account manager.

#### Create and release an agent template

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Template Center".

3. On the "Agent Template" \> "Enterprise\-recommended" tab, click "Create template".

4. Select any supported method to create a template.

   **Custom creation**

> **tip**

   > Custom creation supports two methods:

   * > **Manual template creation via configuration parameters:** Define and create agents by manually entering template configuration details, such as name, description, skills, and tools. This method is suitable for complex customization scenarios.

   * > **Quick creation via prompts/natural language:** Leverage platform\-preset prompts or natural language descriptions to generate agent templates automatically. This method is suitable for quickly building common agent templates.

   **Method 1: Manual template creation via configuration parameters**

   Click "Custom creation". On the left side of the agent creation page, configure agent parameters.

      * **Name**: Enter a name for the agent. We recommend using a clear and easy\-to\-understand name to facilitate subsequent identification and management.

      * **Description**: Briefly describe the core features and application scenarios of the agent to facilitate subsequent matching with corresponding business requirements.

      * **Skills**: By default, skills are preset. You can click "Edit all" or "+ Add" in the **Skills** section to add skills.

         * Intelligent creation: In the dialog box that appears, describe the required skill (for example, "Help me create a capability for searching North American media news across the entire web"). Then, click the "Create" button. The system will automatically draft, verify, and associate the skill with the agent.

         * Add from SkillHub: In the dialog box that appears, use the category tabs at the top (such as Data analysis or IT O&M) or the search box to find and add an existing mature skill.

         * Upload a skill: In the dialog box that appears, drag and drop a local `.zip `file that meets the specifications (within 10 MB) to upload and apply it.

      * **Tools**: By default, tools are preset and enabled. You can click "Edit all" in the **Tools** section to make adjustments based on actual needs and grant the agent the necessary capabilities to call external tools.

      * **Code of conduct/Workflow/Agent profile/User profile**: Switch to the corresponding configuration page (e.g., "Agent profile"), and edit the code of conduct, workflow, agent profile, and user profile separately to give ArkClaw a dedicated identity, response guardrails, standard operating procedures, and user\-awareness capabilities. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_md_files__?lang=en)

   **Method 2: Quick creation via prompts/natural language**

      1. Click "Custom creation". On the left side of the agent creation page, select a suggested prompt or directly enter a description of the target agent in the text box below.

      2. Click the send icon to submit your agent description.

      3. The system generates a ‌solution outline‌ based on your requirements description. Review whether the proposed agent name, core features, and other information meet your expectations.

         * **Yes**: Click "Start Building". The system automatically completes the agent's basic configuration and initialization setup based on the solution outline.

         * **No**: Click "Request Modification" and provide detailed modification notes. The system regenerates a solution outline. Repeat the process until it meets your expectations.

      4. After the agent is created, its complete configuration pane is displayed on the right side of the page. Thoroughly review the agent configuration information: skills, tools, code of conduct, workflow, agent profile, and user profile. If adjustments are needed, directly modify the corresponding information.

   **Upload ZIP package and create**

1. Click "Upload ZIP package and create". This allows you to upload a ZIP file for automatic parsing and rapid agent creation. We recommend downloading the sample file first and modifying your ZIP package according to the sample file's structure to avoid upload failures.

   2. Click "Upload file", or click the upload area and select the target ZIP file, or drag the ZIP file directly into the dashed box. Wait for the file upload to complete.

      > **tip**

      > Each upload supports only one ZIP file. During the upload, the system automatically checks the template structure.

   3. When the upload is complete, the full configuration panel for the agent is displayed on the right side of the page. You can review the agent's configuration and make changes directly if necessary.

      * **Skills**: By default, skills are preset. You can click "Edit all" or "+ Add" in the **Skills** section to add skills.

         * Intelligent creation: In the dialog box that appears, describe the required skill (for example, "Help me create a capability for searching North American media news across the entire web"). Then, click the "Create" button. The system will automatically draft, verify, and associate the skill with the agent.

         * Add from SkillHub: In the dialog box that appears, use the category tabs at the top (such as Data analysis or IT O&M) or the search box to find and add an existing mature skill.

         * Upload a skill: In the dialog box that appears, drag and drop a local `.zip `file that meets the specifications (within 10 MB) to upload and apply it.

      * **Tools**: By default, tools are preset and enabled. You can click "Edit all" in the **Tools** section to make adjustments based on actual needs and grant the agent the necessary capabilities to call external tools.

      * **Code of conduct/Workflow/Agent profile/User profile**: Switch to the corresponding configuration page (e.g., "Agent profile"), and edit the code of conduct, workflow, agent profile, and user profile separately to give ArkClaw a dedicated identity, response guardrails, standard operating procedures, and user\-awareness capabilities. [Learn more.](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_md_files__?lang=en)

5. After confirming there are no issues, release the agent or save it as a draft.

   * **Release the agent**: Click "Create & Release" in the upper\-right corner. In the pop\-up dialog box, enter the release notes and click "Confirm Release" to complete the operation. Released agent templates are displayed under "Agent Center" \> "Agent Gallery" \> "Enterprise Template" in the employee\-side console for employees to use.

   * **Save as a draft**: Click "Save" in the upper\-right corner to save the constructed agent data. Later, you can release it as an enterprise\-recommended agent template by clicking "Release" on the card on the "Agent Template" \> "Enterprise\-recommended" tab.

#### Edit agent templates

> **tip**

> After editing an agent template, ‌you need to release it to have the latest version displayed in the employee\-side console.

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Template Center".

3. On the "Agent Template" \> "Enterprise\-recommended" tab, hover over the template card with a "Draft" status mark and click "Edit" to re\-edit the agent configuration.

4. Click "Create & Release" in the upper\-right corner. In the pop\-up dialog box, enter the release notes and click "Confirm Release" to complete the operation.

#### View Agent template versions

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Template Center".

3. On the "Agent Template" \> "Enterprise\-recommended" tab, hover over the target template card and click "..." \> "Version History".

   > **tip**

   > All agent templates displayed on the "Enterprise\-recommended" tab support viewing version records.

5. On the "Version History" page, you can view detailed version records, such as version number, operator, release time, and agent configuration.

#### Delete agent templates

> **warning**

* > **Deleted agent templates are no longer displayed in the employee\-side console. Deleted templates are irrecoverable. Proceed with caution.**

* > If you delete an agent template, agents already created based on this template remain unaffected and continue operating normally.

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Template Center".

3. On the "Agent Template" \> "Enterprise\-recommended" tab, hover over the target template card and click "..." \> "Delete".

4. In the dialog box that pops up, click Delete.

### Manage templates

#### Set agent templates' visibility scope

> **tip**

> You can only modify the visibility scope of ‌released agent templates. Templates in the "Pending Review" or "Draft" state ‌do not support visibility scope configuration.

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Template Center".

3. On the "Agent Template" \> "Enterprise\-recommended" tab, hover over the target template card and click "..." \> "Edit Visibility Range".

4. In the pop\-up dialog box, set the agent template's visibility scope and click "Confirm" to complete the operation.

   * **Allow all**: The agent template is available to all employees in the enterprise.

   * **Controlled access**: This agent template is available to specified departments, user groups, or users. Only authorized employees can view and use this application.

   * **Deny all**: The agent template is not available to any employee.

#### Set categorization tags for agent templates

> **tip**

> As the number of enterprise\-recommended templates grows, employees' search efficiency declines, and administrators struggle to feature priority templates. Agent template tagging enables administrators to categorize and prioritize enterprise\-recommended templates by business scenario. Employees can then quickly locate needed templates by tags in the Agent Gallery.

* > Up to 20 categorization tags can be added per ArkClaw space. A single agent template can belong to multiple categories. Modifying a category name does not affect the template associations with that category.

* > Agent templates marked as "Invisible to all employees" will not be visible to employees even if categorized.

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Template Center".

3. On the "Agent templates" \> "Enterprise\-recommended" tab, click "Add category".

4. Set the category name, select the templates that belong to this category, and click "Confirm" to complete the operation.

   > **tip**

   > The tag name must be 2 to 20 characters long. Within the same ArkClaw space, category names cannot be duplicated.

5. (Optional) Set the sorting order for your enterprise's agent templates in the category. In the category, click the sorting field in the upper\-right corner to set a sorting type for templates within this category.

   * Supported sorting fields include **By update time** and **By usage**. If you sort by update time, templates updated closer to the current time appear first. If you sort by usage, higher\-usage templates appear first.

   * We recommend sorting items in frequently updated groups by update time and sorting items in popular groups with stable operations by usage.

6. (Optional) Add a new template to an existing category with a specific tag. Select the category tag and click "..." \> "Edit category". Then, add the target template to the category.

7. (Optional) Adjust the order of category tags. Find the target category tag, move the pointer over the ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_261135650d71a4ead1ec1c2391058ab1.png) icon, and click and drag to adjust the tag order.

8. (Optional) Delete the category. Select the category tag and click "..." \> "Delete". In the pop\-up dialog box, click "Delete" to delete the category.

   > **tip**

   > After deleting a category, the agent templates within that category can be viewed under "All".

### Review templates

#### Review agent templates submitted by employees

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Template Center".

3. Click "Review agent template" in the upper\-right corner of the page to enter the "Publishing request review" page.

4. Click the target application record in the list to check whether the agent's name, skills, code of conduct, workflow, and other information meet enterprise requirements, and then approve or reject the agent template application.

   * **Approve**: The agent template will be automatically released and displayed under "Agent Center" \> "Agent Gallery" \> "Enterprise Template". It is accessible to all enterprise employees. Employees can add this template as their own agent and initiate tasks using the agent.

   * **Reject**: The template will not be released. It remains as a ‌personal template‌ of the submitting employee under "Agent Center" \> "My agents", accessible ‌only to that employee.
