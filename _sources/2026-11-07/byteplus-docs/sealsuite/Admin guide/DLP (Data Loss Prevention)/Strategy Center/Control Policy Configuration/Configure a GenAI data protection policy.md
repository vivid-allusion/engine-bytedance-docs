---
title: "Configure a GenAI data protection policy"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-genai-data-protection-policy"
---

A GenAI data protection policy detects prompts that employees submit to AI applications or large language model APIs, identifies sensitive information in them, and audits or blocks the activity based on the configuration.

<span id="doxcnsUbBHuyU5InIxFi0wb2zlf"></span>
## Feature description

GenAI data protection prevents employees from submitting sensitive enterprise information when using AI. It checks prompts sent to AI, such as customer data pasted into a chat box, internal business text submitted for summarization, or text sent through large language model APIs by programs. It is suitable for auditing or blocking sensitive content while allowing employees to use AI.

The following two prompt types are currently supported:


* Prompts sent to **AI application**, such as the Cursor client, Doubao web version, ChatGPT web version, DeepSeek web version, and Kimi web version.

* Prompts sent to **large models** through APIs, such as DeepSeek, Claude, Volcengine Ark, and Alibaba Cloud Bailian. The supported objects are subject to the list on the configuration page.

   For large model service providers outside the built\-in model list, SealSuite also supports detection and identification. It can automatically discover unknown model brands accessed within the enterprise, generate assets, and apply protection.


The system currently checks the user prompt in the current turn. It does not detect files uploaded in requests, downloaded files, or model responses.

Within the preceding scope, the system identifies sensitive data in prompts, such as personal information or enterprise\-defined sensitive words, based on the **classification and grading rules** selected by the administrator. To use sensitive words, first prepare a built\-in or custom sensitive word library in **DLP \> Data Identification \> Sensitive Thesaurus**. Then reference the library in classification and grading rules, and add the rules to the policy.

After you configure rules, the following protections can be implemented:


* **Protect customer information**: For example, an enterprise prohibits sales employees from submitting customer mobile numbers to the Doubao web version. The administrator configures a classification and grading rule that identifies Chinese mainland mobile numbers, and sets the handling action to block in the GenAI data protection policy. When a sales employee submits "Please help me write a follow\-up SMS. Customer Zhang's mobile number is 13800000000", the system identifies the mobile number, blocks the current submission, and records a log.

* **Protect internal project content**: An enterprise configures the fictitious project code name "Sample Project\-A" as a custom sensitive word and configures the corresponding classification and grading rule. When an employee submits "Please summarize the implementation plan for Sample Project\-A", the system records or blocks the current submission based on the policy if the rule conditions are met.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For the Cursor client: When Cursor traffic passes through Secure Web Gateway (SWG), timeouts, slower responses, or errors may occur. If these issues occur, go to "Settings \> Browser & Network \> HTTP Compatibility Mode" in Cursor, switch to HTTP/1.1, and try again.</div>


<span id="doxcnP7i2jmYF6hcjqgiXruBSob"></span>
## Prerequisites


* SWG traffic diversion has been configured, and target HTTPS traffic can be decrypted. See [Configure a traffic diversion policy](https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies?lang=en) and [Configure an SSL decryption policy](https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies?lang=en).

* Classification and grading rules for identifying sensitive content are ready. See [Manage classification and grading rules](https://docs.byteplus.com/en/docs/sealsuite/managing-classification-and-grading-rules?lang=en).


<span id="doxcnfrfcXdjA2kzNrdQITchJRf"></span>
## Add a GenAI data protection policy

<span id="doxcnBII2w40jN3gq98lDfSkhHc"></span>
### Step 1: Fill in basic information


1. Log in to the SealSuite Admin Console and choose **DLP** \> **Strategy Center**.

2. Under **Control Strategy**, switch to **GenAI Data Protection** and click **Create policy**.

3. Fill in the following basic information.



|Configuration item |Description |
|---|---|
|Policy name |Required. Identifies the policy and is used to find matching events in the logs. |
|Policy Description |Optional. Describes the purpose and scope. Up to 100 characters are allowed. |
|Priority |Defines the policy execution order (0\-100). **A higher value indicates a higher priority**. When policies with the same priority are hit, the latest created or updated policy is executed. |
|Manage labels |Select a tag to associate with the current policy. This field is optional. The drop\-down list only displays tags granted to the current administrator. Tags enable policy permission isolation between administrators in different regions or business lines.<br><br>To add or adjust visible tag options in the drop\-down list, a super administrator must modify the "Management tag scope" for your administrator role in **Enterprise Settings** \> **Administrator permissions**. For more information, see [Edit Administrator permissions](https://docs.byteplus.com/en/docs/sealsuite/docs-editing-or-deleting-administrator?lang=en). |


<span id="doxcnqESoeHg0HKB2WpJC4iHxkc"></span>
### Step 2: Select a handling action and control scope


1. In **Action**, select **Audit** or **Block**.

   Start with auditing to assess policy matches, then enable blocking as needed.

2. In the **Configure control scope** area, switch to the **AI application** or **Model Provider** tab, and select the objects to protect.

   Use **Search AI apps and models** to quickly find objects.

   * **AI application**: Select applications that employees use directly, such as "DeepSeek web version". To check prompts sent by employees in a web chat box, select the corresponding application here.

   * **Model Provider**: Select API service providers, such as "DeepSeek" or "Alibaba Cloud Bailian". To check prompts sent by programs through APIs, select the corresponding provider here.

3. Check the selected objects and ensure that all applications or API providers requiring control are covered.


<span id="doxcn5qSfz5QJ2Sl0x9fpEouC1f"></span>
### Step 3: Configure outbound behavior


1. In the **Control Action** area, confirm that **Sensitive Text** is enabled and expanded.

2. In the **Outgoing content** area, click **Add Data**.

3. Select and confirm classification and grading rules that contain the "File content" identification condition. Check the added **Categorized and graded data** and **Data sensitive level**.


GenAI data protection uses only the **File content** condition in classification and grading rules to identify outbound text. Even if a rule contains multiple identification conditions, only its file content condition is used. The selection window displays the complete list of classification and grading rules. View rule details and confirm that the selected rule contains the file content condition you need.

Classification and grading rules define the content to identify. When a rule uses sensitive words, it should reference a built\-in or custom sensitive word library in **DLP** \> **Data Identification** \> **Sensitive Thesaurus**, and then be added to this policy. For more information, see [Manage sensitive word libraries](https://docs.byteplus.com/en/docs/sealsuite/managing-sensitive-thesaurus?lang=en).

<span id="doxcnX3qjxVKMQZB5yfGz5JE77b"></span>
### Step 4: Set effective objects


1. In the **Scope** area, select **User** or **Device**. Select the objects to control by department, role, member, or device.

2. To configure exceptions, enable **Exclude object** and select the corresponding objects.

   You can exclude specified devices, device groups, departments, roles, or employees.

3. After confirming the control scope, sensitive content, handling action, and effective objects, click **Confirm** to save.

4. Return to the list, check the **Policy Status** of the policy, and enable the policy as needed.


<span id="doxcnHnU3vufCep8WAdpayRiHFd"></span>
## Manage the policy lifecycle

In the **GenAI Data Protection** list, you can view the number of enabled and disabled audit and block policies, and manage individual policies.


* **Locate policies**: Filter by audit or block type, policy name, employee, and device. Check the protection scope by viewing associated objects, classification and grading rule names, effective objects, and excluded objects in the list.

* **Enable or disable**: Use the **Policy Status** switch to control whether the policy participates in control. To temporarily pause a policy, disable it and retain its configuration.

* **Edit**: Click **Edit** to adjust the configuration and save it. Before changing the action to block, check logs to evaluate hit conditions and the impact scope.

* **Copy**: Click **Copy** to create a similar policy based on an existing policy. Check the name, associated objects, sensitive rules, and effective scope before saving.

* **Delete**: Click **Delete** and follow the prompts on the page to remove policies that are no longer needed.


<span id="doxcnbFVGPjFpn29BzAyXd0jf39"></span>
## View hit logs

After configuring a policy, use the following logs to trace policy changes and check whether sensitive content sent by employees was audited or blocked.


* **Administrator operation logs**: To trace policy management operations, go to **Audit Logs** \> **Admin Log**, set **Operation module** to **GenAI data protection policy**, and locate records by operator and operation time. Logs record policy creation, viewing, editing, deletion, and tag changes. Use **Operation type**, **Operation details**, and **Operation status** to verify specific operations and execution results. Operations in which an administrator unlocks and views sensitive content in AI conversations are also recorded in Administrator operation logs.

* **GenAI data outbound logs**: Go to **DLP** \> **Investigation Audit** \> **Audit Log** \> **GenAI Data Protection** to view hit employees, AI applications or model providers, sensitive data, and handling actions. For more information, see [View GenAI data outbound logs](https://docs.byteplus.com/en/docs/sealsuite/genai-data-outgoing-logs-view?lang=en).
