---
title: "View attack logs"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/View_details_of_attack_events"
---

Attack logs record requests that trigger LLM Application Firewall protection policies. On the Attack Logs page, you can review request content, matched rules, detection categories, policy actions, and event times.

Use these logs to determine why a request was blocked or flagged, identify the detected risk, and locate events that require further investigation.

<span id="86c5ab4b"></span>
## Prerequisites

Before reviewing attack logs, confirm that:


* The assets you want to protect have been integrated with the LLM Application Firewall.

* You have configured protection policies, such as prompt injection protection, model abuse prevention, sensitive data leakage prevention, or deepfake detection.

* The protection policies are enabled and have processed requests that triggered the corresponding detection capabilities.


<span id="3535c9e1"></span>
## Log types

The Attack Logs page provides separate tabs for different types of security events:


|Tab |Description |Use cases |
|---|---|---|
|LLM Protection Logs |Displays logs generated when text, user prompts, or model responses trigger an LLM protection policy. |Investigate prompt attacks, model abuse, sensitive data leakage, topic manipulation, and other LLM\-related risks. |
|Deepfake Logs |Displays logs generated when an image or video triggers deepfake detection. |Review detection results for AI\-generated or manipulated images and videos. |


You can search logs by time range and apply advanced filters. The page provides quick time ranges of 1 hour, 24 hours, 7 days, and 30 days. You can also specify a custom time range.

<span id="b73b9a0c"></span>
## View LLM protection logs


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield).

2. In the left menu bar, select **Attack log**.

3. Click the **LLM protection logs** tab.

4. Set the query time range.

5. To precisely locate logs, click **Advanced filter** and filter by AppID, request ID, request content, detection category, and other criteria.

6. View the target record in the log list.

7. To further investigate, click **Log analysis** on the right side of the target record.


The LLM protection log list contains the following key information:


|Field |Description |
|---|---|
|AppID |ID of the application or asset that triggered the detection. Use this value to identify the integrated asset associated with the request. |
|Submission type |Source of the submitted content, such as a user prompt or model response. |
|Request content |Summary of the content that triggered the detection. Use it to understand the context in which the risk was identified. |
|Matched rule |Protection rule triggered by the request. Use this field to verify which policy configuration produced the result. |
|Detection category |Risk category detected in the content, such as role\-playing. |
|Action taken |Action applied by the triggered protection rule, such as blocking the request. |
|Time |Time when the attack log was generated. |
|Actions |Click **Log Analysis** to view detailed information about the request and detection result.<br><br><br>* If the request triggered a built\-in detection category, the details include the detection category, matched content, and decision reason.<br><br>* If the request triggered a custom detection category, the details include the detection category and matched content. |


<span id="05a9473a"></span>
## View deepfake logs


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield).

2. In the left menu bar, select **Attack log**.

3. Click the **Deepfake logs** tab.

4. Set the query time range.

5. To precisely locate logs, click **Advanced filter** and filter by AppID, request ID, detection category, and other criteria.

6. View the target record in the log list.


The deepfake log list contains the following key information:


|Field |Description |
|---|---|
|AppID |ID of the application or asset that triggered the detection. |
|Request content |Type and summary of the detected content, such as an image or video. |
|Detection result |Indicates whether the content was identified as manipulated. |
|Detection category |Manipulation categories detected in the content and their confidence scores. The score corresponds to the `Prob` field returned by the API and indicates the probability that the sample matches the category.<br><br>A sample can trigger multiple categories. When this occurs, the system displays a separate confidence score for each category.<br><br><br>* `10900000`: Default forgery<br><br>* `10901000`: PS forgery<br><br>* `10902000`: Forged entity<br><br>* `10903000`: Forged text<br><br>* `10904000`: Forged face |
|Time |Time when the attack log was generated. |


<span id="d68acea4"></span>
## Investigate an event

Review an attack log in the following order:


1. Verify that the `AppID` belongs to the expected asset. This prevents you from investigating an event generated by another application.

2. Review the request content and submission type to determine whether the detection was triggered by a user prompt, model response, image, or video.

3. Check the matched rule and detection category to identify the triggered policy and associated risk type.

4. Review the action or detection result to determine whether the request was blocked, allowed, or identified as manipulated content.

5. For LLM protection events, open **Log Analysis** to review the matched content and decision reason. Use this information to investigate potential false positives, false negatives, or policy configuration issues.


<span id="30afe030"></span>
## Frequently asked questions

<span id="070a4bad"></span>
### Why can’t I find the expected log?

Confirm that the selected time range includes the time when the request occurred. Also verify that the `AppID`, detection type, and protection policy are configured correctly.

A log is generated only when the corresponding protection or detection policy is enabled and the request triggers that policy.

<span id="a735a827"></span>
### What is the difference between the two log types?

**LLM Protection Logs** record content security events involving text, user prompts, and model responses. Use them to investigate risks such as prompt attacks, model abuse, and sensitive data leakage.

**Deepfake Logs** record detection results for images and videos that may contain AI\-generated or manipulated content.
