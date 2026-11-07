---
title: "Release notes"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Release_notes"
---

This article introduces the feature release and documentation dynamics of various versions of the LLM Application Firewall. Welcome to experience the new features of the product. 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Some product capabilities are available by allowlist only. If your account does not currently have access, contact technical support to request access.</div>


<span id="a51934c5"></span>
## August 2026


|Release date |Feature |Description |Related documentation |
|---|---|---|---|
|2026\-08\-10 |Protection |**Enhanced deepfake detection**: Deepfake Detection can now distinguish between general manipulated content, image editing, manipulated entities, manipulated text, and manipulated faces. These detailed labels help you identify the type of manipulation associated with each detection result. |[Detect deepfakes with the SDK](https://docs.byteplus.com/docs/LLM-Application-Firewall/Detect_deepfakes_with_the_SDK)<br><br>[Check whether input or output content is compliant](https://docs.byteplus.com/docs/LLM-Application-Firewall/Check_whether_input_or_output_content_is_compliant) |
||Logs |**New attack log analysis view**: You can now view the detection category, matched content, and decision reason for a request, helping you determine why it was classified as risky. Structured risk details have also been added to the logs, including risk labels, trigger sources, and matches for custom sensitive keywords. |[View attack logs](https://docs.byteplus.com/docs/LLM-Application-Firewall/View_details_of_attack_events) |
||Operations |**Optimization sample review**: You can review samples identified by the system as suspected false positives or false negatives. If the original detection result is correct, mark individual samples or multiple samples as **As Expected**. These samples are excluded from subsequent policy optimization. |[Review content asynchronously](https://docs.byteplus.com/docs/LLM-Application-Firewall/Review_content_asynchronously) |


<span id="f079a527"></span>
## July 2026


|Release date |Feature |Description |Related documentation |
|---|---|---|---|
|2026\-07\-08 |Protection |**Custom block responses for streaming clients**: The `text/event-stream` page type is now supported. You can return blocked content to clients in Server\-Sent Events (SSE) format, improving compatibility with applications that use streaming responses. |[Configure custom block response policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_block_response_policies) |


<span id="5d57672a"></span>
## June 2026


|Release date |Feature |Description |Related documentation |
|---|---|---|---|
|2026\-06\-28 |Protection |**Hallucination Detection**: Compares the user’s question, reference content, and model response to identify answers that conflict with the provided context or reference materials.<br><br>This capability is suitable for knowledge\-based Q&A, intelligent customer service, and business assistants. You can use it for pre\-release testing, production response monitoring, knowledge retrieval optimization, and prompt refinement.<br><br>Hallucination Detection is currently available in invite\-only preview. Contact your sales representative to request access. |[Configure hallucination content protection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_hallucination_content_protection_policies) |
||Detection |**Deepfake Detection**: Analyzes images and videos for signs of AI generation, deepfakes, compositing, and other forms of manipulation.<br><br>This capability is suitable for scenarios such as insurance claims and logistics damage claims, helping businesses reduce the operational and financial risks associated with fraudulent materials. |[Test deepfake detection](https://docs.byteplus.com/docs/LLM-Application-Firewall/Create_online_test_tasks#6990cc37)<br><br>&nbsp;<br><br> |
||Detection |**Asynchronous Review**: Provides an interactive workflow for uploading samples, detecting risks, submitting manual feedback, and publishing review policies. You can review detection results, provide feedback on incorrect decisions, and run the review again to validate an updated policy.<br><br>&nbsp;<br><br>Asynchronous Review supports batch processing of mixed text, image, and document samples. It is suitable for pre\-release compliance testing, ongoing content inspections, and iterative review policy optimization. |[Review content asynchronously](https://docs.byteplus.com/docs/LLM-Application-Firewall/Review_content_asynchronously) |
||Operations |**Adaptive Policy Optimization**: Analyzes historical logs to identify suspected false positives and false negatives and then generates policy optimization recommendations. After confirming the identified samples, you can run regression testing and publish the optimized policy.<br><br>This capability is suitable for reducing excessive false positives, identifying potential false negatives, and stabilizing policy performance as business traffic changes. |[Optimize your policies adaptively](https://docs.byteplus.com/docs/LLM-Application-Firewall/Optimize_your_policies_adaptively) |


<span id="232aa335"></span>
## April 2026


|Release date |Feature |Description |Document |
|---|---|---|---|
|2026\-04\-08 |Asset |For assets connected through a traffic gateway, a new feature allows you to customize the content for inspection. You can configure prefix and suffix matching rules to precisely define the inspection scope and filter out data that does not require detection (for example, fixed system prompts or templated text). This ensures that only core business data undergoes security inspection, thereby improving detection efficiency and accuracy. |[Integrate LLM Application Firewall using a traffic-based approach](https://docs.byteplus.com/docs/LLM-Application-Firewall/Integrate_LLM_Application_Firewall_using_a_traffic-based_approach) |
|2026\-04\-08 |Protection |Supports content security detection for video files in mainstream formats such as MP4 and AVI. |[Configure model abuse prevention policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_model_abuse_prevention_policies) |
|2026\-04\-08 |Development |Added parameter descriptions and SDK call examples for video file detection. |[SDK overview](https://docs.byteplus.com/docs/LLM-Application-Firewall/SDK_overview) |


<span id="91a04a56"></span>
## January 2026


|Release date |Feature |Description |Document |
|---|---|---|---|
|2026\-01\-27 |Protection |**Custom protection**: You can train a dedicated protection model by providing sample content. You can then associate the model with a custom detection category and link that category to your protected assets in a rule. This customized model adapts better to your business scenarios, providing more precise and effective protection. |[Configure custom watch lists](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_custom_watch_lists) |
|2026\-01\-27 |Protection |**Custom responses**: You can set one or more customized responses for different detection categories. When a user prompt triggers a category, the system returns the preset response, which your application can then use to reply to the end user. This helps improve service response speed and user experience. |[Configure custom response policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_a_custom_response_rule) |
|2026\-01\-08 |Protection |**Upgraded multimodal detection**: You can configure model abuse protection policies for asset integrated through any method to detect undesirable content, such as gore, violence, and pornography, in images and documents. This ensures your business remains compliant and secure, and prevents model abuse. |[Configure model abuse prevention policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_model_abuse_prevention_policies) |
|2026\-01\-08 |Development |* **API: Enhanced content moderation**<br><br>   * **Document content detection**: Detects inappropriate content, such as violence, gore, and pornography, within documents to ensure compliance and prevent model abuse.<br><br>   * **Hybrid multimodal detection**: Processes text, images, and documents simultaneously within a single request to significantly improve inspection efficiency.<br><br>* **SDK Updates**<br><br>   * **Proxy service support**: Supports proxy configuration during SDK initialization, enabling seamless data forwarding through proxy servers.<br><br>   * **New code samples**: Added reference implementations for document detection and hybrid multimodal detection. |[Check whether input or output content is compliant](https://docs.byteplus.com/docs/LLM-Application-Firewall/Check_whether_input_or_output_content_is_compliant)<br><br>[SDK overview](https://docs.byteplus.com/docs/LLM-Application-Firewall/SDK_overview) |


<span id="f8631ab2"></span>
## October 2025


|Release date |Feature |Description |Document |
|---|---|---|---|
|2025\-10\-31 |Instance |Purchase LLM Application Firewall instances with flexible billing options, including subscription (monthly/yearly) or pay\-as\-you\-go, to suit your specific business needs and scaling requirements. |[Create an LLM Application Firewall instance](https://docs.byteplus.com/docs/LLM-Application-Firewall/create_an_LLM_Application_Firewall_instance) |
|2025\-10\-31 |Asset |Choose from three integration methods that best fit your business architecture:<br><br><br>* **SDK integration**: Integrate the SDK in your server\-side application. Business traffic flows directly from clients to your origin server. Your server calls the SDK and then decides how to handle the request based on the result.<br><br>* **Traffic integration**: Point your domain's DNS record to the firewall instance's CNAME address. All traffic will first pass through the firewall, which blocks attacks and forwards legitimate requests to your origin server.<br><br>* **Model service integration**: Replace your original model access domain with the endpoint provided by the firewall. Traffic is inspected by the firewall before being forwarded to your model service, ensuring the security and stability of your operations. |[Introduction to assets integration](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_assets_integration) |
|2025\-10\-31 |Protection |* **Access control**: Configure access sources by adding IPv4 addresses or CIDR blocks to allow or block requests from specific IPs.<br><br>* **LLM protection**: Defend against a variety of large language model (LLM) attacks, including resource exhaustion, prompt injection, model abuse, and sensitive data leakage.<br><br>* **Custom block response**: Customize the content returned to the client when a request is blocked, such as setting a specific response code or displaying a custom page. |[Introduction to protection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_protection_policy) |
|2025\-10\-31 |Attack log |When a request triggers a protection policy, the Attack Log feature records comprehensive information about the request. You can use these logs to assess your security posture and to identify and respond to abnormal traffic in a timely manner. |[View attack logs](https://docs.byteplus.com/docs/LLM-Application-Firewall/View_details_of_attack_events) |
|2025\-10\-31 |Log details |The logging feature collects access logs for your protected resources. It integrates with Torch Log Service, providing tools for search, analysis, monitoring, alerting, and data visualization to help you quickly understand your operational status and the effectiveness of your security policies. |[View and analyze logs](https://docs.byteplus.com/docs/LLM-Application-Firewall/View_and_analyze_logs) |
|2025\-10\-31 |Development |We provide code samples in Python, Java, and Go to help you quickly implement features like content moderation and safe response generation. |[SDK overview](https://docs.byteplus.com/docs/LLM-Application-Firewall/SDK_overview) |
