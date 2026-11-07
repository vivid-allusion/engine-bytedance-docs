---
title: "Using Hermes Agent"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Using_Hermes_Agent__"
---

To enhance the intelligent processing capabilities of your ArkClaw in complex task scenarios, BytePlus integrates Hermes Agent into ArkClaw as a runtime capability. Hermes Agent can run directly within ArkClaw and share conversation context and memory with ArkClaw. This allows Hermes Agent to more accurately understand your needs and maintain consistency across multi\-turn interactions. While ArkClaw is designed for general assistant scenarios in daily work and life, Hermes Agent is better suited for handling highly repetitive and structured complex tasks. Hermes Agent can also accumulate reusable skills from completed tasks, improving efficiency for similar tasks in the future. The collaboration between ArkClaw and Hermes Agent enables ArkClaw to continuously optimize its service performance during usage. This offers a more professional and tailored intelligent experience for you.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is in Beta. Welcome to explore. If you experience any problems, exceptions, or have any suggestions during use, you may inform us via the <a href="https://docs.byteplus.com/en/docs/ArkClaw/Feedback_?lang=en">feedback</a> feature.</div>


<span id="6JC9QoHo"></span>
## Background

Hermes Agent is an open\-source, autonomous agent framework developed by the renowned AI research lab Nous Research, with the core philosophy of "Grows With You". It is not a simple chatbot, but a personal AI assistant designed for long\-term user companionship, with continuous learning and evolution throughout the process. Hermes has powerful self\-evolution capabilities that include learning from conversations, automatically generating and optimizing reusable skills, and maintaining persistent cross\-session memory. These capabilities precisely compensate for the limitations of ArkClaw in personalization and long\-term knowledge accumulation. [Learn more](https://github.com/NousResearch/hermes-agent).

A core feature of Hermes is its built\-in Closed Learning Loop mechanism.


<columns>
<columnsItem zoneid="NllzL6TndY">


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

**Memory and learning**

Hermes is equipped with a persistent memory system that can retain user preferences, work habits, and details of previous tasks across multiple conversations. Rather than only recording information passively, it actively extracts and summarizes experience from complex task execution to form reusable methodologies.

</card>



</columnsItem>
<columnsItem zoneid="QhGZWDyR55">


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

**Skill evolution**

This is the most revolutionary characteristic of Hermes. Upon completion of a complex task, it automatically abstracts and solidifies problem\\-solving steps and methods into a reusable skill. This skill can be invoked directly when similar problems arise in the future, and are continuously refined and improved through subsequent usage to achieve genuine self\\-evolution.

</card>



</columnsItem>
</columns>



<columns>
<columnsItem zoneid="G0paqWreBi">


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

**Powerful tool and model ecosystem**

Hermes incorporates more than 47 built\\-in native tools that cover file operations, web browsing, code execution, Docker, and other scenarios. Meanwhile, it provides strong tool expansion capabilities through the MCP standard protocol, and supports one\\-click switching among more than 200 mainstream large language models via OpenRouter. You can always select the most suitable tools and models for specific tasks.

</card>



</columnsItem>
<columnsItem zoneid="t8HMMcO1HW">


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

**Automation and collaboration**

With its built\\-in Cron scheduled task system, Hermes can independently execute periodic tasks such as daily report generation and regular inspection. It also supports splitting complex tasks and assigning them to multiple parallel sub\\-agents for processing, which greatly improves efficiency and capability in handling complicated problems.

</card>



</columnsItem>
</columns>


<span id="pE35yYxk"></span>
## Applicable scenario


* **Execution of long\-horizon tasks**

   Conventional chat models often lose context or stall when handling multi\-step, long\-duration tasks. Hermes is purpose\-built for complex task orchestration, with strong task decomposition, state memory, and goal management capabilities. It maintains high focus during tasks lasting several hours until the final goal is achieved.

* **Handling of repetitive and structured complex tasks**

   If you frequently perform similar workflows with minor variations, such as compiling weekly data reports, regularly inspecting service status, or generating code from templates, the self\-evolving skill capability of Hermes delivers exceptional value. It learns and solidifies your complete first\-time workflow as a reusable skill. For subsequent tasks, you only need to issue a simple natural language instruction. Hermes will automatically invoke the skill to complete most work, greatly improving efficiency.


<span id="Miw8X0xf"></span>
## Considerations


* The Hermes feature is supported only when **collaboration mode** is disabled.

* This feature is only available for ArkClaw instances running version `ark-1.2.3` **or later**. You can check your ArkClaw version and perform upgrades on the "Status and usage" tab of the ArkClaw details page. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_status_and_usage).

* When Hermes Agent is enabled for the first time, the system automatically uses the current model configuration of ArkClaw as the initial Hermes Agent configuration. When Hermes Agent is enabled, the model configurations of Hermes and ArkClaw become independent and do not affect each other. To change the model used by Hermes, see [How do I replace the model used by Hermes Agent?](https://docs.byteplus.com/en/docs/ArkClaw/Hermes_Agent_FAQ__#v74PxqcF) for details.

* Specification limits

   * Starting from **00:00:00 on May 21, 2026**, newly created **ArkClaw Starter** instances will no longer support the Hermes feature. Existing instances created before this date are not affected, but due to resource configuration limitations, the smoothness of Hermes operations may be compromised.

   * To use this feature or to obtain a better user experience, we recommend that you contact the administrator to upgrade the instance to **Standard** or a higher edition, or [create an instance with a higher specification](https://docs.byteplus.com/en/docs/ArkClaw/Creating_ArkClaw?lang=en).


<span id="AftdJI5y"></span>
## Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target ArkClaw page.

3. For first\-time use, install the Hermes Agent plugin by clicking "+ \> Hermes \> Install plugin".

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The installation process takes about 5\-10 minutes. Wait patiently.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you are prompted that "The current ArkClaw version is outdated. Please upgrade first before installing the plugin.", click the "Upgrade and install plugin" button to upgrade the ArkClaw version and install the Hermes Agent plugin.   </div>
   

4. After the plugin is installed, refresh the current page or create a new session.

5. Enable the Hermes feature. Subsequently, all conversations and tasks sent to ArkClaw will be processed and replied by Hermes.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also use the <code>/model hermes</code> quick command in the ArkClaw web chat box or third\-party message channels (such as Feishu or DingTalk) to quickly enable this feature.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Note that when you enable the Hermes Agent feature by using the quick command, the state of the Hermes button in the ArkClaw console does not update synchronously. The actual execution state prevails. For example: After the <code>/model hermes</code> command is executed, subsequent tasks will be processed by Hermes.   </div>
   

6. If you temporarily do not need to use Hermes, you can disable this feature via the console or quick command. After you disable Hermes, all conversations and tasks sent to ArkClaw will be handled and replied by ArkClaw.

   * **Disable** ** through ** **the console:** 

      Disable the Hermes feature. The feature is disabled when the toggle button appears light gray.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If your ArkClaw uses inference services from third\-party large models with <a href="https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_ArkClaw_inference_models__?lang=en">custom model configurations</a>, you can currently <strong>disable this feature only via a quick command</strong>.      </div>
      

   * **Disable via quick command**

      You can use the following quick commands in the ArkClaw web chat box or third\-party message channels (such as Feishu or DingTalk) to quickly disable Hermes Agent.

      * `/model ark`: Applicable when ArkClaw uses a model from ModelArk [Coding Plan](https://docs.byteplus.com/en/docs/ModelArk/2276791) or ModelArk ["Foundation models"](https://console.byteplus.com/ark/region:ark+cn-beijing/model?groupType=ModelGroups&vendor=Bytedance&view=DEFAULT_VIEW).

      * `/model custom`: Applicable when ArkClaw uses third\-party large models via [custom model configurations](https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_ArkClaw_inference_models__?lang=en).

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">When you disable the Hermes Agent feature by using the quick command, the state of the Hermes button in the ArkClaw console does not update synchronously. The actual execution state prevails. For example, after the <code>/model ark</code> command is executed, subsequent tasks will be processed by ArkClaw. Even if the Hermes button does not appear gray, the actual switch result is not affected.      </div>
      

<span id="IAv0tR2F"></span>
## Usage examples

This section uses game review data analysis as an example to show how to use Hermes to complete tasks, accumulate skills, and reuse those skills for similar tasks later.

**Sample ** **prompt** **:** 


* First task:   Hermes, please help me write a script to scrape the latest 100 1\-star and 2\-star reviews for Escape from Duckov (App ID: 6743841750) from the Apple App Store. Use a model to analyze the top 3 core pain points that users complain about the most, and share the conclusions with me. Once the process runs successfully, consolidate this workflow into a Skill.

* Subsequent task:  Using the previously consolidated Skill, help me analyze Honkai Impact 3rd (App ID: 1143402987) in the App Store.
