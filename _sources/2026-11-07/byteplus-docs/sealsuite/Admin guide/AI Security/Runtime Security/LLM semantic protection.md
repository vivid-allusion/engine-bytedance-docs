---
title: "LLM semantic protection"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/large-model-semantic-protection"
---

LLM Semantic Protection checks prompts that employees send through AI websites, client applications, or model APIs. It identifies prompt attacks and logs or blocks requests based on policy.

## Feature introduction

When employees use AI applications, their input may contain instructions that induce the model to ignore original rules, elevate privileges, or disclose system prompts. administrators can configure protection rules for AI applications and model providers used by the enterprise. These rules help identify who initiated the requests, which risk types were triggered, and whether access must be blocked.

After traffic diversion and HTTPS decryption are configured, the Secure Web Gateway extracts prompts from AI requests that pass through the gateway and identifies prompt attacks. Policies support observation or blocking. Observeing allows access and records logs based on the configuration. Blocking denies requests that match protected content. Semantic detection currently applies to user input only and does not inspect model output.

To review specific conversations, enable **AI Conversation Content Audit** in the policy. This records user input, model responses, and multi\-turn session content. For example, after finding a privilege escalation risk log, you can view the related conversation to understand what the user entered and how the model responded. If you only need access and risk event statistics, disable session content audit. Logs retain only the time, person, application, matched policy, and other metadata.

## Prerequisites

Semantic detection requires access to AI request content that passes through the Secure Web Gateway. Before configuration, complete authorization, traffic access, and decryption preparation in the following order.

1. Activate **Secure Web Gateway** license, and grant administrators the menu and operation permissions for the corresponding features.

2. Configure the enterprise self\-signed root certificate, certificate auto\-installation scope, and traffic diversion policy, so target traffic passes through the Secure Web Gateway.

   After the client trusts the enterprise CA certificate, the gateway can decrypt and inspect HTTPS traffic. For details, see the initial configuration preparation and traffic diversion steps in [Configure a traffic diversion policy](https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies).

3. Configure an SSL decryption policy, and set the AI applications or domains that require inspection to **Decrypt**.

   Undecrypted HTTPS traffic supports only basic domain\-level identification or blocking. It cannot obtain prompt bodies for semantic detection, or extract related API content. For details, see [Configure an SSL decryption policy](https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies).

4. Go to **Secure Web Gateway \> AI Access Security**, and click **Enable AI Access Security** on the feature guide page.

## Add a semantic protection policy

A semantic protection policy specifies the AI applications or model providers, detection categories, action, and effective objects to inspect. After the policy is configured, matched access behavior is logged or blocked based on the rules, and corresponding audit logs are generated.

> **tip**

> Asset Inventory depends on log reporting. To collect comprehensive statistics about AI applications and models used in the enterprise, first configure a low\-priority policy that covers all employees. Select all AI applications and models, set the action to **Observe \> Record all logs**, and leave the protected content empty. Then configure high\-priority policies for high\-risk applications or specific personnel. Select **Observe \> Only record logs that trigger protection content** or **Block**, and select the detection categories to inspect. The scope recorded by a high\-priority policy depends on its log option. Asset statistics are also updated based on reported logs.

1. Log in to the SealSuite Admin Console.

2. Go to **AI Security \> Runtime Security \> LLM Semantic Protection**.

3. Switch to the **Policy Management** tab, and click **New Policy**.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-34.png)

4. On the **Add a protection policy** page, complete the following configuration, and click **Confirm**.

   * **Basic information**

      |Configuration item |Description |
      |---|---|
      |Policy name |Customize an easy\-to\-identify policy name. We recommend naming it by control objective, such as "All\-employee AI usage audit" or "Prompt attack protection". |
      |Priority |Set a value from 0 to 100. The default value is 50. A larger value indicates a higher priority. If an access request matches multiple policies, the system executes only the policy with the highest priority. If values are the same, the system executes the policy that was most recently added or modified. |
      |AI applications and models |Select the AI applications or model providers to control. Multiple selections are supported.<br><br><br>* **AI applications**: Select web applications, such as Doubao, ChatGPT, DeepSeek, and Kimi, or client applications, such as Cursor and Trae. Available applications are subject to the page list.<br><br>* **Model providers**: Select known providers such as OpenAI, Anthropic, and Google. These providers include official, relay service, and self\-built sources. Use this option to control related applications and models by provider. It also applies when enterprise embedded applications call model APIs.<br><br>* **Unknown vendors**: After this option is selected, the system discovers unknown models accessed in the enterprise and generates assets for protection. After this option is cleared, the system stops adding and updating corresponding assets. Existing assets, protection policies, and audit logs are retained. |

   * **Action**

      |Configuration item |Description |
      |---|---|
      |Observe |Allow users to access normally, and record logs in the following ways.<br><br><br>* **Record all logs**: Record access behavior of effective objects for selected applications and models, regardless of whether protected content is triggered.<br><br>* **Only record logs that trigger protection content**: Generate audit logs only when access matches the selected detection categories. |
      |Block (Beta) |Block access requests that match protected content. Blocking is in Beta. Blocking results may be inaccurate. Use this feature with caution. |

   * **Audit content**

      |Configuration item |Description |
      |---|---|
      |AI Conversation Content Audit |Disabled by default when a policy is created. After it is enabled, user input, model responses, and multi\-turn session content within the policy scope are recorded. You can view specific interactions in log details. After it is disabled, only access and risk events are reported. Session bodies are no longer recorded or stored, and session content cannot be viewed in details. If session data is subject to privacy or compliance requirements, use this option to decide whether to enable auditing.<br><br>> **tip**<br><br><br>> When upgrading from a version earlier than 3.3.9, **AI Conversation Content Audit** is enabled by default for historical policies. administrators can manually disable it. After it is disabled, request content and session content in historical logs for the policy can no longer be viewed.<br> |

   * **Protected content**

      |Configuration item |Description |
      |---|---|
      |Detection categories |Select the prompt attack types to identify. If the action is **Block** or **Observe \> Only record logs that trigger protection content**, select at least one detection category. Only user input is currently inspected. Model output is not inspected. |

      The meanings of each detection category are as follows.

      |Detection category |Description |
      |---|---|
      |Role\-play |Sets or restricts the model's role attributes to induce the model to use that role's language style, bypass safety restrictions, and generate responses that may involve intellectual property, ethics, or other inappropriate content. |
      |Privilege escalation |Induces the model to enter a higher\-privilege state, such as developer mode. This causes the model to bypass original safety restrictions, ignore established rules, and produce uncontrolled output or perform operations beyond the authorized scope. |
      |Adversarial prefixes and suffixes |Adds special strings before or after malicious prompts to interfere with model judgment and cause unexpected or uncontrollable responses. For example, meaningless characters are used to disrupt the model's identification of normal content and attack instructions. |
      |Goal hijacking |Adds deceptive or misleading instructions to prompts to override or interfere with original instructions and induce the model to produce specific output. |
      |Obfuscation and encoding |Uses meaningless symbols to break filters, or bypasses model safety protection through encoding or encryption. |
      |Few\-shot attack |Provides a small number of maliciously inclined answer examples to induce the model to generate malicious or misleading output. |
      |Prompt extraction |Adds malicious instructions to the user's original input in an attempt to obtain the original system or user prompt information. |
      |Other prompt attacks |Other prompt attacks outside the preceding categories. |

   * **Effective objects**

      |Configuration item |Description |
      |---|---|
      |Effective objects |Select the departments, members, roles, specific endpoint devices, or device groups to which the policy applies. |

5. Check access after configuration.

   * **Observe**: Employees can use AI normally. The backend records access time, personnel, and risk types based on the selected log method. If session content audit is enabled, input and response bodies are also recorded.

   * **Block**: After a prompt sent by an employee matches protected content, the request is blocked. The browser or application may display a connection reset message or a SealSuite security block page.

   * Go to the **Audit Log** tab to check access records, matched policies, and executed actions. View specific session content if needed.

You can also configure policies on the **Secure Web Gateway \> AI Access Security \> Policy Management \> LLM semantic guardrails** page.

## Manage policies

On the **AI Security \> Runtime Security \> LLM Semantic Protection \> Policy Management** page, you can view the AI applications and models, effective objects, priority, and creation and update times of each policy. You can also perform the following operations.

|Operation |Description |
|---|---|
|Adjust priority |Modify the policy priority to adjust the execution order when multiple policies are matched at the same time. |
|Enable or disable |Enable or disable a rule through the policy switch. |
|Copy |Create a new policy based on an existing policy. |
|Edit |Modify controlled applications, detection categories, audit content, action, or effective objects. |
|Delete |Delete a policy that is no longer used, and confirm the deletion as prompted on the page. |

## View audit logs

To check which AI websites or model APIs employees used, what risks their input triggered, and whether policies handled requests as expected, view the audit logs for semantic protection. Logs are divided into **AI Website** and **Large Model API**, which record application conversations and model interface calls respectively.

1. Go to **AI Security \> Runtime Security \> LLM Semantic Protection**, and select the **Audit Log** tab.

2. Select **AI Website** or **Large Model API**, and filter records by trigger time, employee, device, matched policy, action, and detection category. AI websites also support filtering by AI application and request content. LLM APIs support filtering by model source type, model provider, model name, current user prompt, and current tool call.

3. View matched records, and use the matched policy, detection category, and executed action to verify why the request was recorded or blocked.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-35.png)

|Field |Description |
|---|---|
|Trigger time |The time when access triggered the log. |
|Employee |The employee who initiated the access. |
|Software name |The application name identified in AI website logs. |
|Model provider |The provider called in LLM API logs. Use this field to distinguish which service receives the request and view the associated URL. |
|Model source type |The LLM API source, including official, relay service, self\-built, and unknown. Use the filter with the same name to find requests from a specific source type. |
|Model name |The model used for the request. |
|Request content |The prompt or request body that the user sent to AI in AI website logs. The corresponding policy must enable **AI Conversation Content Audit** to record and view specific content. |
|Current user prompt |The user prompt that the employee sent to AI in the current LLM API request, reported by the Secure Web Gateway. The corresponding policy must enable **AI Conversation Content Audit** to view it. |
|Current tool call |Whether the current LLM API interaction includes a tool call. The value is **Yes** or **No**. |
|Device |The Endpoint that initiated the request. |
|Matched policy |The protection policy that handled the request. Click the policy name to view its configuration. |
|Action |The result indicating whether the access was allowed or blocked. |
|Detection category |The identified prompt attack type, such as role\-play or goal hijacking. |

You can also view these logs on the **Secure Web Gateway \> AI Access Security \> Protection logs** page through the corresponding tabs for AI applications and LLM APIs.

## View log details and session content

Click **View details** in the **Operation** column of the target log. Use the request information, specific conversation, and employee device information to check the risk content and its source.

|Information category |Description |
|---|---|
|Event information |View the trigger URL, application or model provider, model name, action, and detection category. Verify the access target and policy handling result. |
|AI session content |View user input, model responses, and multi\-turn sessions in interaction order. Use the context to check whether continuous instructions induce the model to escalate privileges or ignore rules. The corresponding policy must enable **AI Conversation Content Audit**. |
|System prompt |If an LLM API log contains this item, view the system prompt included in the request to understand the role or rules set for the model. |
|Tool list |If an LLM API log contains tool definitions, view the available tools and their parameter definitions. Use them with actual calls in the session to understand tool purposes. |
|Detailed logs |View network request information, such as the client IP address, request method, URL, and path. For LLM APIs, switch to the **Detailed logs** tab. For AI websites, click **View details** in event information to view the original packet, which helps check request content or troubleshoot access issues. |
|Employee information |View the name, department, and account status to confirm the person who initiated the access. |
|Device information |View the operating system, IP address, and device ID to confirm which Endpoint initiated the access. |

Session content may involve business data. To expand sensitive content, click **View sensitive content**, and then click **Confirm view**. If the enterprise has configured secondary authentication for sensitive administrator operations, complete verification as prompted before viewing the content.

## Archive logs

For records that have been audited or no longer require attention, administrators with archive permissions can click **Archive** in the **Operation** column of the log list, and then click **Confirm archive**. Archived logs are no longer displayed in the list or details. Archive operations are recorded in administrator audit logs.
