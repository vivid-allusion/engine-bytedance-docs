---
title: "Introduction to protection policies"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/introduction_to_protection_policy"
---

Protection policies are the core security rules within the LLM Application Firewall that safeguard your AI applications against various threats. This document provides a comprehensive overview of the available policy types, such as access control, prompt injection protection, and sensitive data prevention. It also compares their features and explains their execution priority, helping you choose and configure the right security measures for your specific business scenarios.

<span id="463364e7"></span>
## Policy types


|Policy types |Description |Related documentation |
|---|---|---|
|Access control |An access control policy controls and restricts access from IP addresses that match specified rules. You can manually add IPv4 addresses or IPv4 CIDR ranges to specify the source of access, allowing or blocking requests from specific IP addresses. |[Configure access control policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_access_control_policies) |
|Resource exhaustion mitigation |After you configure a resource exhaustion mitigation policy, the LLM Application Firewall automatically identifies malicious compute consumption targeting LLM services and takes protective action to improve service stability. |[Configure resource exhaustion mitigation policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_resource_exhaustion_mitigation_policies) |
|Prompt injection protection |The LLM Application Firewall can identify attack instructions in user input prompts based on the protection policy you configure. It replaces the response from the large model to the user with a trained answer to prevent your model from being attacked. |[Configure prompt injection protection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_prompt_injection_protection_policies) |
|Model abuse prevention |A model abuse prevention policy can be used to identify and handle prompts that induce hallucinations in the model, preventing the model from being manipulated into generating inaccurate, offensive, or completely off\-topic responses. Supports classification detection for sensitive content such as drugs, fraud, gambling, discrimination, and more. |[Configure model abuse prevention policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_model_abuse_prevention_policies) |
|Sensitive data disclosure prevention |The sensitive data disclosure prevention policy uses a robust detection mechanism to identify personal data in real time. It then intercepts or handles this data in input and output content according to your predefined policies. This ensures that sensitive user data, such as personal identification information and contact details, are not leaked or misused when using large model services, thereby protecting user privacy and security. |[Configure sensitive data disclosure prevention policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_sensitive_data_disclosure_prevention_policies) |
|Custom watch list |The LLM Application Firewall's built\-in word bank matches sensitive or non\-compliant content in both input and output. In addition, the LLM Application Firewall also supports a custom watch list to better meet the content detection needs of your actual business scenarios. |[Configure custom watch lists](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_watch_lists) |
|Topic control |Topic control is a customizable protection feature of the LLM Application Firewall. It can be intelligently trained based on the sensitive topic content you provide—including sensitive words, blocklist and allowlist samples—and can automatically generate a detection corpus. By analyzing the correlation between user input and corpus in real time, the LLM Application Firewall can effectively intercept sensitive input and prevent large language models from being misused to generate non\-compliant content or content that may pose reputational risks. |[Configure topic control policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_topic_control_policies) |
|Custom block response |The custom block response policy supports configuring response codes and response page information, returning specific content for requests that match the policy and for which the action is `Block`, and displaying custom information to the client.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">The protection policy takes effect when the execution action is set to <code>Block</code>.</div><br> |[Configure custom block response policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_block_response_policies) |


<span id="2987bfd1"></span>
## Comparison of LLM protection policies

The following table compares the policies of prompt injection protection, model abuse prevention, and sensitive data disclosure prevention to help you quickly understand their differences.


|Features |Prompt injection protection |Model abuse prevention |Sensitive data disclosure prevention |
|---|---|---|---|
|**Main features** |Identify attack commands in user input prompts to prevent the model from being attacked |Identify and handle prompts that cause the model to hallucinate, and prevent the model from generating inaccurate or inappropriate responses |Real\-time identification of privacy data in input and output content to protect users' privacy and security |
|**Application scenarios** |Prevent attackers from controlling or compromising large models through carefully crafted prompts |Prevent large models from generating harmful, inappropriate, or non\-compliant content |Prevent users' sensitive information from being leaked during interactions with large models |
|**Protection target** |Model security |Model output quality and compliance |User privacy data |
|**Detection classification** |* Role\-playing<br><br>* Incomplete inputs<br><br>* Codified description<br><br>* Prompt stealing<br><br>* Default tags of prompt injection<br><br><br> |* Sensitive content<br><br>* Insult<br><br>* Porn and vulgarity |* ID number<br><br>* Bank card number<br><br>* Mobile phone number<br><br>* Other types of sensitive data vary by country/region |
|**Action** |* Observe<br><br>* Block<br><br>* Secure reply |* Observe<br><br>* Block<br><br>* Secure reply |* Observe<br><br>* Block<br><br>* Data masking<br><br>* Secure reply |
|**Effective method** |Detect input prompt |You can choose to detect both input and output simultaneously, or configure them separately. |You can choose to detect both input and output simultaneously, or configure them separately. |


<span id="4eefc9a9"></span>
## LLM policy priority

When using the LLM Application Firewall, you may configure multiple protection policies. If a request triggers several policies simultaneously, the system determines the final action according to the following logic:


1. Allowlist: Has the highest priority. If the allowlist rules are matched, the request is allowed immediately.

2. Blocklist: If a request does not match the allowlist but matches the blocklist, the request is directly intercepted.

3. Other large model protection policies include synchronous detection. When multiple policies are triggered simultaneously, actions are executed according to the priority order of `Block > Data masking > Secure reply > Observe`, with the strictest action given precedence.


The following scenarios illustrate the priority and execution logic of different protection policies.


|Policy combinations triggered |Final action |Decision logic |
|---|---|---|
|* Allowlist: pass<br><br>* Prompt injection protection: block |Pass |The allowlist has the highest priority, and its "pass" action overrides the actions of all other policies. |
|* Blocklist: block<br><br>* Model abuse prevention: observe |Block |When the allowlist is not matched, the blocklist has higher priority than other security policies. |
|* Prompt injection protection: block<br><br>* Sensitive data disclosure prevention: data masking |Block |The priority of the two security policies is the same, so the system selects the stricter "block" action. |
|* Sensitive data disclosure prevention: data masking<br><br>* Model abuse prevention: observe |Data masking |When two security policies have the same priority, the system selects the stricter "data masking" action. |
