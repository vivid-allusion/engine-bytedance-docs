---
title: "Configure AI Protection Policy"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-ai-protection-policy"
---

The **Policy Configuration** page of AI Access Security is the protection policy distribution center for this module. By configuring protection rules of different dimensions, enterprises can effectively identify and prevent data leakage and operational risks brought by the use of AI Agents, without affecting employees' office efficiency.

For scenarios where employees converse with AI via browsers, developers collaborate using command\-line interfaces (CLI), and AI applications call Skills to execute tasks, AI protection policies can provide identification and risk blocking capabilities.

## Prerequisites

You need to complete the following configurations in order before you can configure and validate AI protection\-related policies.

1. **Configure the enterprise self\-signed root certificate and the certificate automatic installation scope**. Client trust in the enterprise CA certificate is a prerequisite for SWG to perform decryption inspections on HTTPS traffic. Ensure that you have referred to the **First\-time setup** steps in [Configure traffic routing policies](https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies) to correctly configure the enterprise self\-signed root certificate and its automatic installation scope.

2. **Configure the SSL Decryption Policy**. For HTTPS traffic, the system needs to obtain plaintext content through decryption to perform semantic auditing and API extraction. Make sure to refer to [Configure SSL decryption policies](https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies) and set AI\-related applications or domains to "Decrypt" in the **SSL Decryption Policy**; otherwise, the system can only achieve basic domain\-level identification or blocking, and protections like semantic guardrails (such as DLP, intent recognition) will fail.

3. **Configure the Large Model Semantic Protection Policy**. After enabling the AI Access Security feature, you must configure the protection policy before entering the AI Access Security page for the next steps. For details, please refer to [Configure LLM Semantic Guardrail Policies](https://docs.byteplus.com/en/docs/31/113701#configure-llm-semantic-guardrail-policies).

## Enable AI Security

Before configuring any specific AI protection policy, you must enable the global AI Security feature.

1. Log in to the Admin Console.

2. In the left navigation pane, select **SWG** \> **AI Access Security**.

3. On the feature guide page, click **Enable AI Security**.

## Configure LLM Semantic Guardrail Policies

This is the core protection module for web\-based or desktop AI applications. It provides control over **the semantic content of prompts** .

> **Note**

> **Configuration recommendations**

> Asset discovery depends on log reporting. To comprehensively collect statistics on AI applications and models used within the enterprise, we recommend the following configuration:

1. > **Full discovery**: Configure a low\-priority policy that applies to all employees, selects all AI applications and models, sets the action to "Observe \- Record all logs", and leaves the protection content empty. This policy ensures that all AI access behaviors are recorded and summarized in **Asset Discovery**.

2. > **Precise control**: Configure high\-priority policies for specific high\-risk applications or sensitive user groups. Set the action to "Observe \- Only record logs that trigger protection content" or "Block", and select specific detection categories in the protection content. This allows you to collect full asset statistics while precisely auditing or blocking specific risky behaviors.

1. Log in to the Admin Console.

2. In the left navigation pane, choose **SWG** \> **AI Access Security** \> **Policy Configuration**.

3. Switch to the **Large Model Semantic Guardrail** tab and click  **+ New Policy** in the upper\-right corner.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f19f5b045fa48418b4f33997c135912~tplv-goo7wpa0wc-topic.webp)

4. On the **Add a protection policy** page, complete the following configurations and click **Confirm**.

   * **General**

      |Configuration Item |Description |
      |---|---|
      |**Policy Name** |Customize an easy\-to\-identify policy name. We recommend naming the policy based on the control objective, such as “Core Code Leakage Prevention Policy” or “All\-Employee AI Usage Audit.” |
      |**Priority** |Set a value from 0 to 100. **A higher value indicates a higher priority.**  When multiple policies conflict, the system executes only the policy with the highest priority. If multiple policies have the same priority, the system executes the policy that was most recently added or modified. |
      |**AI apps and models** |Specify the control scope of the policy. You can select by **AI application** or **Model Provider**.<br><br><br>* **AI Application**<br><br>   Covers mainstream web AI (such as Doubao, ChatGPT, DeepSeek, Kimi, etc.), client AI (such as Cursor, Trae), and enterprise embedded applications (such as Workbuddy).<br><br>* **Model Provider**<br><br>   * **Known Vendors**: Supports batch checking of mainstream model providers like OpenAI, Anthropic, Google (official, transfer station, self\-built) to control all related applications and models under the provider with one click.<br><br>   * **Unknown Vendors**: When enabled, the system will automatically discover unknown brand models and generate assets for protection. If disabled, it will stop adding and updating corresponding assets, but existing assets, protection policies, and audit logs will not be affected. |

   * **Action**

      Determines how the system handles access behaviors that match the policy.

      * **Observe**: Allows users to access the application normally and records related logs.

         * **Record all logs**: Records all access behaviors by policy subjects to the selected applications, regardless of whether protection content is triggered.

         * **Only record logs that trigger protection content**: Generates audit logs only when the access behavior matches the "Protection Content" below.

      * **Block (Beta)** : Blocks access requests that match the protection content. The blocking feature is currently in Beta, and its effectiveness may vary. Use it with caution.

   * **Audit content**: Determines whether the system captures the interaction body when employees use AI applications.

      * **AI Conversation Content Audit**: Disabled by default. Enabling this setting records full user input, model responses, and multi\-round session history for AI application usage within the policy scope to support event traceability and auditing. When disabled, the system only reports access and risk metadata without storing the session body. This mode suits sensitive scenarios requiring high privacy protection or strict data compliance, though it precludes context\-based traceability.

      > **Note**

      > Introduced in version **3.3.9**. For legacy policies, this setting is enabled by default after the system upgrade. Administrators may manually disable it to meet specific compliance requirements. Disabling this feature renders context traceability and request content in historical logs unavailable for viewing.

   * **Protection Content:**  Required only when the action is **Observe \- Only record logs that trigger protection content**. Only user **input** detection is supported currently. Model output detection is not supported yet. See the detection categories below.

      |Detection classification |Description |
      |---|---|
      |**Role Play** |The attacker defines or restricts the model’s role attributes to induce the model to respond in the language style of that role, thereby bypassing security restrictions and generating responses that may involve intellectual property, ethics, or other inappropriate content. |
      |**Privilege Escalation** |The attacker attempts to induce the model to enter a higher\-privilege state, such as developer mode, causing the model to bypass existing security restrictions and execute arbitrary instructions. For example, the model may ignore established security rules, generate uncontrolled output, or perform operations beyond the authorized scope. |
      |**Adversarial Prefix and Suffix** |Special strings are added before or after malicious prompts to interfere with model judgment, causing the model to generate unexpected or uncontrollable responses. For such malicious or malformed prompts, the model should identify and filter meaningless characters during output processing, then respond based on the normal content, or indicate that the content cannot be recognized. |
      |**Instruction Overriding** |Deceptive or misleading instructions are added to the input prompt in an attempt to override or interfere with the execution of the original instructions and induce the model to generate specific output. |
      |**Obfuscation and Encoding** |Meaningless symbols are used to disrupt filters, or encoding and encryption methods are used to bypass the model’s security protection mechanisms. |
      |**Few\-shot Learning Attack** |The attacker provides a small number of malicious examples to induce the model to generate malicious or misleading output. |
      |**System Prompt Stealing** |Malicious prompt instructions are added to the user’s original input prompt in an attempt to obtain the original system or user prompt information. |
      |**Other Prompt Attack** |Other prompt attacks beyond the categories listed above. |

   * **Scope**

      Select the departments, members, roles, or specific endpoint devices or device groups to which the policy applies.

5. **Configuration results**

   * **Observe mode**: Users are unaware of the policy. The system automatically generates protection logs in the backend, recording details such as access time, user, prompt content, and identified risks.

   * **Block mode**: After a user submits a non\-compliant Prompt, the browser or application receives a connection reset or a security blocking page issued by SealSuite, indicating that the behavior has been blocked by the enterprise security policy.

   * Log audit: After the policy is triggered, related logs are recorded under **SWG** \> **AI Security** \> **Protection Logs** \> **AI App / Large Model APIs**. For details, see [AI Protection Log Audit](https://docs.byteplus.com/docs/sealsuite/ai-protection-log-audit).

## Configure CLI Security Policies

CLI security policies control command\-line tools commonly used by developers. They prevent developers from bypassing the enterprise SWG through non\-standard CLI tools or calling large language model APIs from terminal environments without auditing.

> **Note**

> Asset discovery depends on log reporting. To comprehensively collect statistics on CLI applications used within the enterprise, we recommend first configuring a low\-priority policy that applies to all employees, selects all CLI applications, and sets the action to "Observe". This policy ensures that all CLI access behaviors are recorded and identifies potential non\-standard or “shadow” CLI tools in **Asset Discovery**.

1. Log in to the Admin Console.

2. In the left navigation pane, choose **SWG** \> **AI Access Security** \> **Policy Configuration**.

3. Switch to the **CLI Security** tab and click  **+ Add a Policy** in the upper\-right corner.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b3cb8732f744a8188d28dbb57c953e3~tplv-goo7wpa0wc-topic.webp)

4. On the **Add CLI Security Policy** page, complete the following configurations and click **Confirm**.

   * **General**

      |Configuration Item |Description |
      |---|---|
      |**Policy Name** |Customize an easy\-to\-identify policy name. We recommend naming the policy based on the control objective, such as “Core Code Leakage Prevention Policy” or “All\-Employee AI Usage Audit.” |
      |**Priority** |Set a value from 0 to 100. **A higher value indicates a higher priority**. When multiple policies conflict, the system executes only the policy with the highest priority. If multiple policies have the same priority, the system executes the policy that was most recently added or modified. |
      |**CLI Application** |The system has a built\-in library of definitions for mainstream AI collaboration tools. Currently, it supports the identification of the following tools: lark\-cli, github\-cli, wecom\-cli, dingtalk\-cli and bytedcli. |

   * **Action**

      * **Observe**: Allows users to use CLI applications normally and records related logs.

      * **Intercept (Beta)** : Intercepts CLI requests from unauthorized tools or high\-risk behaviors. You can select from three risk levels: **High risk**, **Medium risk**, and **Low risk**. At least one level must be selected. The system intercepts CLI requests that match the selected risk levels and generates logs. This feature is currently in Beta, and its effectiveness may vary. Use it with caution.

   * **Scope**

      Select the departments, members, roles, or specific endpoint devices or device groups to which the policy applies.

5. **Configuration results**

   * **Observe mode**: Developers can execute CLI commands normally. The system records API call paths and behavioral intent in the backend.

   * **Intercept mode**: CLI requests that match the selected risk levels are forcibly terminated, and the terminal command\-line interface usually returns a network connection error.

   * Log audit: After the policy is triggered, related logs are recorded under **SWG** \> **AI Security** \> **Protection Logs** \> **CLI**. For details, see [AI Protection Log Audit](https://docs.byteplus.com/docs/sealsuite/ai-protection-log-audit).

## Configure Skill Safety Policies

Skill Safety identifies supply chain risks in the download links of Agent tools and Skills, preventing employees from downloading malicious Skill files that contain malicious dependencies or compromised third\-party components.

> **Note**

1. > The policy configuration here is used only to determine whether to “Deny” risky Skill downloads. It is not a switch for log auditing or asset discovery. As long as the global AI Security switch is enabled, the system automatically records logs for all Skill download links, ensuring continuous auditing and asset visibility for supply chain risks.

2. > Gateway\-side Skill safety policies focus on blocking risks at the download source. To periodically scan and clean up Skill files that already exist on endpoints, see [Configuring Skill security check policy](https://docs.byteplus.com/docs/sealsuite/configuring-skill-detection-policy).

1. Log in to the Admin Console.

2. In the left navigation pane, choose **SWG** \> **AI Access Security** \> **Policy Configuration**.

3. Switch to the **Skill Safety** tab and click **Edit** on the right side of the page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fd215c04265481a9a5cc207e162fd06~tplv-goo7wpa0wc-topic.webp)

4. In the dialog box, complete the following configurations and click **Confirm**.

   * **Risk level determination**: The system automatically identifies the characteristics of Skill download sources based on the built\-in threat intelligence engine and determines the risk level, including high risk, medium risk, and low risk. Administrators do not need to manually define risk levels. They only need to configure actions for different risk levels.

   * **Action**: To protect enterprise security, the system blocks Skill downloads at the **High Risk**, **Medium Risk**, and **Low Risk** levels by default. Administrators can modify the action based on actual needs.

      * **Deny**: Prohibits Skill downloads that match the corresponding risk level and records blocking logs.

      * **Allow**: Allows the download behavior, but still reports audit logs for subsequent traceability.

   * **Blocking page config**: When the action is "Deny", employees see a blocking prompt in the browser. Administrators can customize the prompt content. Multi\-language versions of the notification title and content are supported. Administrators can also use the preview pane to verify the display effect of the blocking page in real time.

   * **Scope**: Select the departments, members, roles, or specific endpoint devices or device groups to which the policy applies.

5. **Configuration results**:

   * **Policy effect**: The system performs blocking only when the action is **Deny** and the download behavior matches the corresponding risk level.

   * **Log audit**: Regardless of how the policy is configured here, even if no blocking rules are configured, as long as AI Security is enabled, the system silently audits all Skill download behaviors. Related records can be viewed under **SWG** \> **AI Access Security** \> **Protection Logs** \> **SKILL**. For details, see [AI Protection Log Audit](https://docs.byteplus.com/docs/sealsuite/ai-protection-log-audit).
