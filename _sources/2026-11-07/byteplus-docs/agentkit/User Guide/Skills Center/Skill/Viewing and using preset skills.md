---
title: "Viewing and using preset skills"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Preset_Skills"
---

**Preset skills** are standardized skills provided by the platform by integrating self\-developed capabilities and high\-quality open\-source capabilities, covering various scenarios such as creative design and technical task execution. By directly using **preset skills**, you can quickly extend an **agent**’s task processing capabilities, reduce the cost of skill creation, and shorten the agent development cycle.

Preset skills have been standardized and packaged, and **can be directly added to a skills space for agents to call**. If you need to perform further development based on a preset skill, you can create an independent copy by cloning, then modify and publish it according to your business scenario.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before downloading and using a skill, whether created by you or preset by us, carefully review the license agreement for the Skill to ensure lawful and compliant use. If you violate the relevant license agreement, you are solely responsible for the consequences, and we reserve the right to terminate your use of the AgentKit service.</div>


<span id="Svgx2S3y"></span>
## Benefits


* **Reduce creation costs**: You can obtain available capabilities without developing from scratch, reducing duplicated efforts.

* **Improve development productivity**: Supports fast adaptation to various business scenarios, accelerating **agent** capability building and launch.

* **Cover multiple scenarios**: Covers common scenarios such as creative design and technical task execution, meeting diverse business needs.

* **Support flexible expansion**: Can be used directly and supports further development after cloning, balancing out\-of\-the\-box and customization needs.


<span id="Oq94ufgC"></span>
## View preset skills


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills Center".

3. Select "Skills  **\>**  Preset by the platform".

4. Hover the mouse over the target **skill** card and click the "View details" button to view the following information.

   
   |Tab |Parameter​ |Description |
   |---|---|---|
   |Basic information |Skill metadata |Displays the skill name, ID, and description. |
   ||Other information |Displays the status, creation time, and update time information of the current **skill**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Status: Displays the availability status of the current <strong>skill</strong> version.</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>Available</strong>: Indicates that the <strong>skill</strong> version has been created and the current version is running. It can be called by <strong>agents</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>Unavailable</strong>: Indicates that the <strong>skill</strong> version failed to be created and the current version cannot be called. We recommend checking the file content and metadata, then creating or publishing it again.</div><br> |
   ||Skills spaces added |Displays all skills spaces associated with the current skill version. You can view space details here and add or remove the skill to/from spaces. For details, see [Adding to/Removing from skills spaces](https://docs.byteplus.com/en/docs/347/90859#W1UuGFBB). |
   |Skill details |\- |Displays the package directory structure and code details of the current skill version. |
   |Version management |\- |Displays the skill version information. You can also click the "View" button to view the basic information and code package details. |
   


&nbsp;

<span id="7dAg4zm8"></span>
## Use preset skills

<span id="TToENmRk"></span>
### One\-click clone

When further development for a **preset skill** is required, you can quickly create a **skill** copy through one\-click cloning. After cloning, you can [modify](https://docs.byteplus.com/en/docs/agentkit/Updating_Skills?lang=en) and [publish](https://docs.byteplus.com/en/docs/agentkit/Publishing_Skills?lang=en) it as needed while preserving the original capability framework, improving **skill** creation efficiency and reducing repeated development costs.


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills Center".

3. Select "Skills  **\>**  Preset by the platform".

4. Hover the mouse over the target **skill** card and click **One\-click clone**. You will be redirected to the skill creation page, with the target **skill** automatically selected. For the complete parameters and procedure for cloning a preset skill, see [Creating skills](https://docs.byteplus.com/en/docs/agentkit/create_skills?lang=en).


<span id="W1UuGFBB"></span>
### Add or remove a **skill** to/from skills spaces


* **Add to spaces**

   **Preset skills** can be directly added to **skills spaces** without cloning or further development. You can add a target **preset skill** to one or more **skills spaces** as needed, allowing associated **agents** to search for and call it, thereby quickly extending the agent’s task processing capabilities.

* **Remove from spaces**

   You can disassociate a **preset skill** from a specified **skills space** as needed.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Once removed, the <strong>skill</strong> will no longer belong to the current <strong>skills space</strong>, but the <strong>skill</strong> itself will not be deleted. To use it later, you can re\-add it to the corresponding space.   </div>
   

**Prerequisites**

[A skills space has been created](https://docs.byteplus.com/en/docs/agentkit/Skills_space?lang=en).

**Procedure**


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills Center".

3. Select "Skills  **\>**  Preset by the platform".

4. Hover the mouse over the target **skill** card and click the "View details" button to open the details page.

5. On the **Basic information** page, in the **Skills spaces added** section, add or remove the **skill** to/from **skills spaces** as needed.

   * **Add to skills spaces**

      1. Click "Add".

      2. In the **Add to skills spaces** dialog box, select the target spaces.

         * Click the "Select the version to add to the space" drop\-down list and select the **skill** version to be added to the space.

         * In the "Select skills space" drop\-down list, select one or more target spaces.

      3. After confirming the version and space information, click the "Confirm" button to complete the operation.

   * **Remove from skills spaces**

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Before performing the removal operation, we recommend confirming that the target <strong>preset skill</strong> is not relied upon by relevant <strong>agents</strong> or business processes to avoid impacting existing business.      </div>
      

      1. In the **Skills spaces added** section, find the target skills space and click the "Remove from this skills space" button in the "Actions" column.

      2. After confirming the removal information is correct, click the "Remove" button to complete the operation.


<span id="hQq6iRFQ"></span>
## Appendix

This appendix provides links to repositories of sample self\-developed skills and open\-source skills. You can refer to these samples for skill development, learning, and further modification.

<span id="jRTGxU5K"></span>
### Self\-developed skills


|Category |Term |Description |
|---|---|---|
|Agent development |[veadk-go-skills](https://github.com/bytedance/agentkit-samples/tree/main/skills/veadk-go-skills) |Generates Go code for creating agents based on [veadk-go](https://github.com/volcengine/veadk-go). |
||[veadk-skills](https://github.com/bytedance/agentkit-samples/tree/main/skills/veadk-skills) |Generates Python code for creating agents based on [v](https://github.com/volcengine/veadk-python)[e](https://github.com/volcengine/veadk-python)[adk-python](https://github.com/volcengine/veadk-python). |


<span id="3KurlXhy"></span>
### Open\-source skills


|Category |Term |Description |
|---|---|---|
|Creative design |[slack-gif-creator](https://github.com/anthropics/skills/tree/main/skills/slack-gif-creator) |Knowledge and practical tools for creating animated GIFs optimized for Slack. Applicable to animated GIF production for Slack scenarios. |
||[theme-factory](https://github.com/anthropics/skills/tree/main/skills/theme-factory) |A toolkit used to configure theme styles for various documents. Applicable to scenarios such as unified document styling and rapid theme configuration. |
||[algorithmic-art](https://github.com/anthropics/skills/tree/main/skills/algorithmic-art) |Creates algorithmic art using p5.js (an open\-source creative coding library), supporting seed randomness and interactive parameter exploration. Applicable to algorithmic art generation and creative visualization scenarios. |
||[canvas-design](https://github.com/anthropics/skills/tree/main/skills/canvas-design) |Creates polished visual assets in .png and .pdf formats by applying design principles. Applicable to scenarios such as creating posters, artwork, and static designs. |
||[frontend-design](https://github.com/anthropics/skills/tree/main/skills/frontend-design) |Creates production\-grade, well\-designed front\-end interfaces with unique styles. Applicable to high\-quality web interface development and UI design scenarios. |
|Technical tasks |[webapp-testing](https://github.com/anthropics/skills/tree/main/skills/webapp-testing) |A toolkit for interacting with and testing local web applications using Playwright. Supports verifying front\-end features, debugging UI behavior, capturing browser screenshots, and viewing browser logs. |
||[skill-creator](https://github.com/anthropics/skills/tree/main/skills/skill-creator) |Provides guidance for creating skills. Applicable to skill development, extension, and maintenance scenarios. |
||[mcp-builder](https://github.com/anthropics/skills/tree/main/skills/mcp-builder) |Used to guide the creation of high\-quality Model Context Protocol (MCP) servers, enabling large language models to interact with external services through tools. Applicable to building MCP servers and integrating external APIs or services using Python (FastMCP) or Node/TypeScript (MCP SDK). |
||[web-artifacts-builder](https://github.com/anthropics/skills/tree/main/skills/web-artifacts-builder) |A set of tools for creating complex multi\-component claude.ai HTML components using front\-end Web technologies (React, Tailwind CSS, shadcn/ui). Applicable to complex components requiring state management, routing, or shadcn/ui components, not applicable to simple single\-file HTML/JSX components. |
|Enterprise applications |[internal-comms](https://github.com/anthropics/skills/tree/main/skills/internal-comms) |A Skill used to assist in writing various enterprise internal communication materials in common company formats. Applicable to writing various internal communication documents, including status reports, management reports, third\-party updates, company briefings, FAQs, incident reports, project progress, and more. |
||[brand-guidelines](https://github.com/anthropics/skills/tree/main/skills/brand-guidelines) |Applies Anthropic's official brand colors and fonts to various assets to align them with Anthropic's visual style. Applicable to scenarios requiring compliance with brand colors, design specifications, visual formats, or corporate design standards. |
