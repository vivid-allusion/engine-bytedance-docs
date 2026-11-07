---
title: "Configure hallucination content protection policies"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_hallucination_content_protection_policies"
---

Hallucination detection identifies content in LLM responses that conflicts with established facts, the conversation context, or provided reference materials. It helps enterprises detect inaccurate or unsupported answers in scenarios such as knowledge\-based Q&A, intelligent customer service, and business assistants, reducing the risk of misleading users, spreading false information, or influencing business decisions.

When an LLM uses an enterprise knowledge base, business documents, or approved answers, model\-generated responses may not always remain faithful to the provided information. You can configure hallucination detection rules in the LLM Application Firewall to identify and record potentially unreliable responses for auditing and further review.

<span id="dce57940"></span>
## How detection works

In Retrieval\-Augmented Generation (RAG) scenarios, hallucination detection evaluates whether an LLM response is supported by the provided reference materials. It does not assess whether the response is merely fluent or well written.

The system compares the following inputs:


* The user’s question

* The retrieved reference content

* The LLM’s final response


If the response contains claims that clearly conflict with or are not supported by the reference content, the system may classify it as a consistency anomaly.

<span id="34104fa3"></span>
## Input requirements

Consider the following requirements when using hallucination detection:


* **Reference content length**: The reference content must not exceed 4,096 characters.

* **Supported content type**: Only text content is supported.

* **Input quality**: Detection accuracy depends on the quality of the reference content. Incomplete, irrelevant, or noisy retrieved content may reduce the reliability of the detection results.


<span id="8fe47e8b"></span>
## Configure a policy


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield).

2. Select the region where the instance is located in the top bar.

3. In the left navigation, select **Protection\>LLM Protection\>** **Hallucination content protection**.

4. Enable the policy. Turn on this switch to activate the hallucination content protection feature; otherwise, subsequently added rules will not take effect.

5. Click **Add rule** and configure the relevant parameters.

   
   |Parameters |Description |
   |---|---|
   |**Rule Name** |Enter a name that identifies the rule.<br><br>The name must begin with a letter or digit. It can contain letters, digits, periods (`.`), underscores (`_`), and hyphens (`-`). The length must be between 1 and 128 characters. |
   |**Asset** |Select the asset or request path to which the rule applies. If you select an asset, the matching scope includes all paths configured for that asset.<br><br>Path\-based matching is not currently supported for assets integrated through the SDK. |
   |**Detection Category** |Select the type of hallucination to detect. Currently, only consistency anomaly detection is supported. |
   |**Action** |Select the action taken when the rule is triggered. Currently, only **Observe** is supported. The request is allowed to continue, and the event is recorded in the attack logs for auditing. |
   |**Rule Toggle** |Enable or disable the rule. |
