---
title: "Updating agent configuration"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Updating_agent_configuration_"
---

After a shared Claw is created, the system automatically generates its initial version 1.0.0. After each subsequent publishing and update, the system will generate a new independent version, allowing you to view and manage configurations from different stages.

This topic describes how the administrators of a shared Claw update the agent configuration and publish the agent.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">When you edit or test a shared Claw agent for the first time, the system automatically spins up an independent tested agent within the shared Claw. The tested agent is only visible to shared Claw administrators in the workspace and is not registered in the Application Center. Therefore, it is invisible to other callers.</div>


* <div data-tips="true" data-tips-type="default">Edits made in the test agent are saved as a draft and do not affect the online agent. You can also exit editing and keep the draft for further modifications and publishing later.</div>



<span id="1FrAOpo2"></span>
## **Step 1: Edit the agent**


1. Log in to the ArkClaw console as the shared Claw administrator and switch to the target shared Claw instance page in the left pane.

2. In the left navigation pane, select "Agent center".

3. Click the "Edit" button on the target card.

   > If the baseline version of the current draft is inconsistent with the latest online version, the system displays the "A new version is available online" prompt. You can select one of the following options based on your needs:

   > * Ignore: Continue editing on the current draft.

   > * Reset draft based on online version: Recreate the draft using the latest online version.

4. (Optional) If the system displays a plugin upgrade dialog box, click "Upgrade now" to complete the plugin installation.

5. Update the model, skills, tools, or .MD files of the target Claw agent based on your needs. For detailed instructions, see [Updating agent configuration](https://docs.byteplus.com/en/docs/ArkClaw/Updating_agent_configuration).


<span id="QBVcJPwS"></span>
## **Step 2: Test the agent (optional)** 

After the agent configuration is complete, we recommend that you test and verify the prompts and message channels to make sure that the task configuration takes effect as expected and the overall settings meet your business requirements.


<Tabs>
<Tab zoneid="HNAudiv9jd" title="Test prompts">
<TabTitle>Test prompts</TabTitle>

The agent comes with multiple preset scenario prompts by default. You can select one to quickly start a conversation and verify the configuration.


1. Click a preset prompt.

2. After confirming that the prompt (prefilled content) is correct, manually send the content directly, or edit and optimize the prompt (prefilled content) based on your business requirements before manual sending.

3. Review the agent's response and verify whether the output meets your business expectations.

4. If the response does not meet expectations, adjust the relevant configuration and test again. Repeat this process until the output meets your business requirements.


</Tab>
<Tab zoneid="QnG4S0LT4J" title="Test message channels">
<TabTitle>Test message channels</TabTitle>

Configure the required message channel and complete test verification to ensure that the task configuration has taken effect.


1. On the test preview page, click the "Test message channel" drop\-down list.

2. In the configuration section for the corresponding message channel, click the "Click to configure" button and complete configuration following on\-screen instructions. You may also refer to the following documents:

   * Telegram: For details, see [Integrate Telegram](https://docs.volcengine.com/docs/87732/2597087#E4K2B1qe).

   * Lark/FeiShu: For details, see [Integrate a Lark/Feishu bot](https://docs.volcengine.com/docs/87732/2597087#kb3SLona).

   * Slack: For details, see [Integrate a Slack bot](https://docs.volcengine.com/docs/87732/2597087#ZoDTlgDS).

   * WeCom: For details, see [Integrate a WeCom bot](https://docs.volcengine.com/docs/87732/2597087#h4fKxncA).

   * Microsoft Teams: For details, see [Integrate a Microsoft Teams bot](https://docs.volcengine.com/docs/87732/2597087#mQ97pQO7).

3. After the configuration is complete, the status of the message channel changes to "Added".

4. Hover the mouse over the target message channel configuration section and click "Go to chat" to open the corresponding message channel client and start a conversation test.

5. If the corresponding message channel responds as expected to instructions, the configuration has taken effect.


</Tab>
</Tabs>


<span id="YSyuW9vE"></span>
## **Step 3: Save configuration modifications (optional)** 

After editing, you can click "Save draft" to manually save the current configuration. After the draft is saved, the page records and displays the name of the most recent editor and the save time, so you can track updates to the currently active version.

> If the system detects that another administrator has edited and saved the configuration after you entered the page, the page displays the name of that editor and the save time. You can select one of the following options:

> * Load latest draft: Discard your current edits and load the latest version saved by the other administrator.

> * Overwrite and save: Overwrite the latest version saved by the other administrator with your current edits.

<span id="QJq8QOnt"></span>
## Step 4: Run a self\-check (optional)

After the relevant configuration is **saved as a draft**, you can run a self\-check to automatically verify whether the skills, tools, and configuration items are available in the current environment, and determine whether the agent draft meets the runtime requirements of the shared Claw environment.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The self\-check feature requires the <code>shared-claw-agent-pack-audit</code> skill, which is enabled by default. If it is not currently enabled, enable it before using the self\-check feature. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring_skills_for_my_agents?TagIDs=2,522,512&lang=en&type=preview">Configuring skills for my agents</a>.</div>



1. Click the "Run self\-check" button to start the check.

2. View the check results

   * If the message "The current agent configuration meets the shared Claw runtime compatibility requirements and can run normally" is displayed, the agent meets the runtime requirements of the shared Claw environment.

   * If the result indicates that the shared Claw runtime compatibility requirements are not met, you can adjust the relevant configuration and run the self\-check again until the check passes before publishing. Alternatively, you can choose to ignore the check results and publish directly based on your actual situation.


<span id="5nfHSaTr"></span>
## **Step 5: Adjust prompts and publish the agent**


1. Click the "Publish" button in the upper\-right corner of the page.

2. (Optional) On the displayed page, you can manually adjust the prompts or click "Generate automatically" to quickly generate recommended prompts. These prompts allow employees without shared Claw administrator permissions to quickly start a conversation. For details, see [Initiating tasks](https://docs.byteplus.com/en/docs/ArkClaw/Initiating_tasks?lang=en).

3. Click "Confirm" to republish the agent for the new configuration to take effect. A new version is generated at the same time. [How to manage agent versions?](https://docs.byteplus.com/en/docs/ArkClaw/Managing_agent_versions)

   > If the baseline version of the current draft is inconsistent with the currently running online version, the system displays the "A new version is available online" prompt after you click "Confirm". The prompt indicates which version the current draft is based on and which version is currently running online. You can:

   > * Click "Publish anyway" to publish the current draft as a new version directly. After publishing, a new independent version is generated without affecting the configuration of the currently running online version.

   > * Click "Cancel publishing" to return to the editing page, reconfirm the configuration, and then proceed.
