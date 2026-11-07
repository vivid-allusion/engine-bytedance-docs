---
title: "AI assistant"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ai-assistant"
---

BytePlus CDN provides an AI assistant that uses model capabilities from BytePlus ModelArk together with CDN product knowledge and console capabilities. You can describe a task in natural language to query configurations and data, analyze issues, or ask questions about CDN.

Consider using AI assistant when you want to:

* Search or compare configurations across one or more domains.

* Review bandwidth, traffic, status code, or other CDN metrics and obtain an analysis.

* Investigate an access, origin, or status code issue.

* Ask about CDN features, billing, caching behavior, or supported request methods.

AI assistant does not support adding domains or modifying domain configurations. It can upload or query certificates, but it cannot associate a certificate with a domain. To complete these operations, use the corresponding features in the CDN console.

## Page overview

You can open AI assistant in either of the following ways:

* In the left navigation pane of the BytePlus CDN console, click **AI assistant** to open the full page.

* On another CDN page, click the floating assistant icon to open the side panel. You can adjust the width of this panel.

After you submit a request, the welcome content and conversation remain on the same page. AI assistant may ask you for missing information and displays the progress and result of the task. Use the input box to add context or ask follow\-up questions.

To manage conversations:

* Click the **Historical conversation** icon to open an earlier conversation.

* Click the **New Dialogue** icon to start a conversation without the current context.

These controls are also available in the floating side panel.

## Supported tasks

### Configuration analysis

Use AI assistant to inspect, compare, and analyze the configuration of one or more domains. For example:

* "List the domains that have URL authentication enabled."

* "Check the configuration of `domain` and suggest optimizations."

* "Check the HTTPS security configuration of all domains."

* "Compare the configuration differences between `domain1` and `domain2`."

* "Analyze the domains under `example.com`, list their configurations, and identify identical configurations that are enabled."

### Data analysis

Use AI assistant to query bandwidth, traffic, status code, and other CDN metrics and obtain analysis results. For example:

* "Show the peak bandwidth for the last day."

* "Analyze CDN traffic distribution by ISP over the last 7 days."

* "Analyze CDN metrics for the last week and provide conclusions and recommendations."

* "List today's top five CDN domains by traffic and identify domains for which 5xx responses exceed 5%."

* "Query the 5xx status codes for `domain` over the last 3 hours at 5\-minute granularity and identify abnormal increases."

### Troubleshooting

Use AI assistant to investigate access, origin, or status code issues. For example:

* "Check whether the origin for `domain` is accessible."

* "Find out why the download from `url` fails."

* "Find out why accessing `url` returns a 403 response."

### Product consultation

You can also ask general questions about CDN features, billing rules, caching behavior, or supported request methods.

## Use AI assistant

1. Log in to the BytePlus CDN console.

2. Open AI assistant from the left navigation pane, or open the floating assistant on another CDN page.

3. Select a supported example question, or describe your request in the input box.

   * Replace placeholders such as `domain` and `url` with the resources that you want to analyze.

   * If AI assistant requests more information, provide the required context.

4. Review the task progress and result. Enter another message to add context or ask a follow\-up question.

To work without the current conversation context, click the **New Dialogue** icon. To return to an earlier conversation, click the **Historical conversation** icon.

## Service notes

AI assistant is intended to improve efficiency. Its responses might not always be accurate, complete, or applicable to your environment. Review generated content before using it.

Responses can be affected by:

* Model service errors, rate limits, or timeouts.

* Delayed or incomplete knowledge base updates.

* Incomplete, ambiguous, or insufficient input.

* Unavailable configuration query, data query, or diagnostic dependencies.

* Network errors, insufficient permissions, or security policies.

If AI assistant is unavailable or its response does not support your business decision, use the existing CDN console features, product documentation, or BytePlus support channels. Do not use AI assistant output as the only basis for an important business operation.

## Data security

* AI assistant uses model capabilities provided by BytePlus ModelArk. Customer data is not used for model training.

* CDN encrypts Agent logs, conversation records, and generated configuration records. It also protects this data through access control and access auditing.

* Use AI assistant only for CDN configuration queries, data queries, product consultation, and troubleshooting. Do not enter personal or sensitive information in a conversation.
