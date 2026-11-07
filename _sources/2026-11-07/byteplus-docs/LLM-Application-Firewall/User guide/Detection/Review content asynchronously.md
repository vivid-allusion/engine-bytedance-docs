---
title: "Review content asynchronously"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Review_content_asynchronously"
---

Asynchronous Review provides professional content review capabilities for text, images, and files. It supports batch review, result verification, and policy optimization through manual uploads in the console or automated SDK calls.

Enterprises can use this feature to validate samples before deploying a model and continuously monitor content after deployment. It helps teams identify risks quickly, establish reusable review policies, reduce the effort required for manual investigation, and maintain consistent, traceable security governance across business units.

<span id="1b819ef8"></span>
## Use cases


* **Filtering LLM\-generated content**: Screen and block non\-compliant responses, recommendations, and other LLM\-generated content before it reaches end users. This helps maintain a consistent security baseline without compromising the user experience and reduces the risk of inappropriate content causing reputational damage.

* **Identifying sensitive information**: Detect sensitive content in text, images, and files, including politically sensitive, terrorism\-related, sexually explicit, and personal information. This enables enterprises to meet regulatory requirements and manage content risks more efficiently.


<span id="04d30a95"></span>
## Review methods

The service supports two review methods. Choose the appropriate method based on your business stage and integration requirements.

<span id="fb53a70f"></span>
### Manual review in the console

Upload samples directly in the console without writing code or completing a technical integration. This lightweight, ready\-to\-use method is suitable for routine sampling, batch reviews, and offline audits. It allows business teams to evaluate the review capabilities and obtain results with minimal setup.

Before deploying the service in a production environment, we recommend using the console to validate representative samples and confirm that the service meets your business requirements.

<span id="ef43d235"></span>
### Automated review through the SDK

Integrate the review capabilities into existing data upload, content moderation, or risk management workflows by using the SDK.

This method is suitable for stable, high\-frequency online services. After a user submits content, your application can automatically initiate a review and retrieve the result, reducing manual intervention and shortening the risk response process.

<span id="4aae1065"></span>
## Limits and recommendations

Review the following limits and recommendations before submitting content.

<span id="e8f3c088"></span>
### Sample limits


* **Number of samples**: A single batch can contain up to **100 samples**. If you have more than 100 samples, submit them in multiple batches.

* **Text samples**: Upload text samples in batches by using the provided Excel template. Each text sample should contain no more than 10,000 characters. For more accurate results, submit complete, semantically coherent passages.

* **Image samples**: Each image must be no larger than **5 MB**. Supported formats include `jpg`, `jpeg`, `png`, `gif`, `webp`, `bmp`, `tiff`, `ico`, `icns`, `sgi`, `jp2`, `heic`, and `heif`. We recommend standardizing the image format before uploading files.

* **File samples**: Each file must be no larger than **5 MB**. Only PDF files are supported.


<span id="50f6ebc0"></span>
### Recommended configurations


* **SDK policy management**: Before publishing the review assistant, SDK calls use the default policy, which is suitable for initial validation. After publishing the assistant, specify its **policy ID** in SDK calls to keep production results consistent with the published configuration.

* **Input sanitization**: Submit only the content that needs to be reviewed. Remove unrelated instructions, explanatory text, and conversation history to improve the accuracy and interpretability of the results.

* **Feedback and optimization**: If a review result does not meet your expectations, provide the expected result and explain the reason for your assessment. This feedback helps the system refine the policy.

* **Request rate**: Each account can submit up to **3,000 samples per hour**. During peak traffic periods or large batch imports, stagger requests as needed to avoid exceeding this limit.


<span id="3a570cdd"></span>
## Procedure

<span id="104e38b1"></span>
### Step 1: Create a review assistant

Before using Asynchronous Review for the first time, create a review assistant. The assistant provides a workspace for uploading samples, reviewing results, submitting feedback, and publishing policies. It also serves as the basis for subsequent policy validation and SDK integration.


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield).

2. In the top bar, select the region for the instance.

3. In the left navigation, select **Detection \> Async Review** to enter the assistant management page.

4. Click **Create review assistant**, and then click **Get started**. Create a separate assistant for each business scenario so that you can manage samples and policy versions independently.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/224393fa5b294b0d8ee8a9e7f5769946) </span>

5. In the data upload panel on the right, upload the content that you want to review.

   You can upload different types of samples in the same review task. This allows you to review multimodal results in one place without creating separate tasks for each content type.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/44110a87e7cf4d499d11634c1a57d128) </span>

6. Optional: Enter a prompt describing your review criteria, business context, or risk categories that require special attention. This information helps the LLM Application Firewall assess the submitted content according to your business requirements.

   If you do not enter a prompt, the system uses the default policy. If your industry has specific requirements or your scenario requires customized decisions, provide a concise description of the applicable rules and expected outcomes.

7. Verify the uploaded samples and prompt, and then click the send icon in the lower\-right corner to submit the review task.

   The system reviews the submitted samples and displays the results when processing is complete. For batch submissions, examine both the risk classification and the explanation provided for each result to identify recurring issues.


<span id="b97fa40e"></span>
### Step 2: Verify results and optimize the policy

After the system completes the review, verify the results and submit feedback where necessary.


1. The system reviews each sample individually. When processing is complete, the review page displays the risk status and the reason for each decision.

2. If a result does not meet your expectations, click **Review result does not meet expectations** below the result and explain your assessment.

   Describe the relevant business context, the content that triggered the result, and the outcome you expected. Clear and specific feedback helps the system understand your requirements and improves subsequent results.

3. After verifying all results and submitting your feedback, run the review again. The system reevaluates the samples based on the updated feedback so that you can confirm whether the policy produces the expected results.


<span id="89e9aa4f"></span>
### Step 3: Publish the review assistant

When the review results meet your requirements, publish the review assistant. After publishing it, you can use its policy ID to invoke the review service through the SDK as part of your business workflow.

<span id="cdb28678"></span>
### Step 4: View review logs

On the Asynchronous Review page, click **Log** to view records from the current and previous review tasks. The logs include both risky and non\-risky content.

Each log retains key information about the review process, allowing teams to trace samples, investigate anomalies, and verify SDK calls. For periodic audits, filter the logs by time range or business scenario to locate relevant records more efficiently.

<span id="035df67d"></span>
## Related operations

<span id="241fe1de"></span>
### Download review results

On the review result details page, click the download icon in the upper\-right corner to export all results from the current review task as an `.xlsx` file. You can use the exported file for archiving, secondary review, or cross\-team collaboration.

The exported file contains the following fields:


|Attribute |Description |
|---|---|
|type |Type of content reviewed. Possible values are `image`, `text`, and `file`. |
|tosKey |Resource identifier for an uploaded image or file. You can use this identifier to locate the original content. |
|data |Original content information. For text samples, this field contains the submitted text. For image and file samples, it contains the corresponding file name. |
|taskId |Unique ID of the review task associated with the sample. Use this ID to track and investigate individual review items. |
|isRisk |Indicates whether the content poses a risk. <br><br>`TRUE`indicates that a risk was detected, and `FALSE`indicates that no risk was detected. |
|riskScore |Estimated probability that the content poses a risk. The value ranges from `0` to `1.0`. A higher score indicates a higher estimated risk. |
|riskReason |Primary reason the content was classified as risky. Use this information for manual verification and policy adjustment. |


<span id="30bc67d2"></span>
### Rename a review assistant


1. On the assistant list or details page, locate the assistant and click the edit icon next to its name.

2. Enter a new name and save the change.


Use descriptive names to distinguish assistants created for different business scenarios or policy versions. This reduces the likelihood of selecting the wrong assistant or creating duplicate configurations.

<span id="e609c3a5"></span>
### Disable a review assistant

If a review assistant is no longer needed for production calls or must be temporarily taken offline, locate it in the assistant list and select **Disable**. SDK calls can no longer use the assistant while it is disabled.
