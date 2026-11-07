---
title: "Configure custom application types"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/configure_custom_application_types"
---

When connecting to the LLM Application Firewall using either the traffic\-based or model\-based approach, you can select a preconfigured model application. The LLM Application Firewall will automatically parse and adapt to the corresponding data. Additionally, you can also customize application types, allowing the firewall to read the business fields you specify and complete detection. To ensure that the LLM Application Firewall can accurately identify and detect target content, it is recommended to manually verify the parsed fields. This article uses a specific DeepSeek dialog interface Schema file as an example to explain how to add custom application types and specify the information about the location of paths, prompt positions, and response positions.

<span id="353a5795"></span>
## UI description

The following is an interface overview for matching parameters after parsing the Schema file:


* Parameter value (①): All parameters in the request body; you can set parameter matching conditions and specify the fields to be inspected.

* JQ expression (②): The JQ expression is automatically generated based on the filter criteria set in area ①. You can also modify it manually.

* Matching results (③): Set the position of the results to be submitted for inspection in the results queue, and preview the current matching results.

* Original JSON (④): The original request body data parsed from your Schema file.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8d1967f613cc44a39b5ae44f86c0a04a) </span>

<span id="38da4336"></span>
## Step 1: Obtain the Schema file

You can use the ApiFox tool to generate and export the Schema file for the interface.


1. Download the [ApiFox](https://apifox.com/) tool.

2. Launch ApiFox. On the homepage, click **Quick request**.

3. Create and send requests.

   Using DeepSeek Dialog API as an example:

   ```JSON
   curl https://api.deepseek.com/chat/completions \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer <DeepSeek API Key>" \
     -d '{
           "model": "deepseek-chat",
           "messages": [
             {"role": "system", "content": "You are a helpful assistant."},
             {"role": "user", "content": "Hello!"}
           ],
           "stream": false
         }'
   ```
   

4. Click **Send** to obtain the response result of a successful request.

5. After receiving a successful response, click  in the upper right corner.

6. Enter the interface name, then click **Save**.

7. Click the `···` on the right side of the interface and select `Export`.

8. Set the export parameters as shown in the figure below.

   * Data format: OpenAPI Spec

   * Export scope: Selected interfaces (only selected interfaces will be exported)

   * OpenAPI Spec version: OpenAPI 3.1

   * File format: JSON

9. Click **Export**, and the JSON schema file will be downloaded to your local machine.


<span id="795c5f3a"></span>
## Step 2: Import a Schema file


1. On the custom application type configuration page of the LLM Application Firewall, click **Import schema**.

2. Select the prepared JSON schema file and confirm the upload.

   After a successful upload, the platform will automatically parse the imported Schema file. Then:

   * Extract API path information

   * Identify request and response parameter structures

   * Generate initial parameter matching configurations

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Please verify that the path and request method are correct.   </div>
   

<span id="57bc943f"></span>
## Step 3: Confirm prompt position


1. Click **Matching parameter** to the right of **Prompt position**.

2. On the **Matching** ** parameter** screen, expand all fields and select the parameter fields for detection.

   * For prompt detection, you only need to detect the user's input prompt (corresponding to a `role` of `user` in this example).

   * In the current example schema, the content for detection corresponds to the `content` field.

   Based on the above, set the filter conditions as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6f2ace99044947a3933f82dc861b86ac) </span>

3. Preview the JQ expression.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">No modification is required in most cases.   </div>
   

4. Set conditions for multiple matching results.

   The request body may contain a multi\-turn conversation, so the generated JQ expression might produce multiple matches. In this case, prompt detection should focus on the user's most recent input. It is recommended to set the option to "Last item". If you have other custom requirements, such as detecting prompts from the entire conversation history, you can also modify this configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Detecting multiple matching results may consume more tokens.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/62024172b630435795c435fe9053e015) </span>

5. Verify that the matching results are as expected.

   As shown below, the matching results align with the content to be detected from the original JSON.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f28df7f632c44026a374c43719523d20) </span>

6. After confirming, click **OK**.

   The prompt position is automatically populated with the confirmed JQ expression.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/36e0d23a4bad4636987104a9d4dc29eb) </span>


<span id="b1fbb8da"></span>
## Step 4: Configure response position


1. Click **Matching parameter** to the right of **Response position**.

2. On the **Matching** ** parameter** screen, expand all fields and select the parameter fields to be detected.

   * For response detection, only the LLM's response content is required (in this example, where the role is "assistant").

   * In this example's schema, the content to be detected corresponds to the "content" field.

   Therefore, set the filter conditions as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/885b372d61184cf09389af34e5c67fd1) </span>

3. Preview the JQ expression.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">\*Description   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Usually, no changes are needed.   </div>
   

4. Set the condition for multiple matching results.

   The request body may contain a multi\-turn conversation, so the generated JQ expression might produce multiple matches. Response detection should focus on the latest response from the LLM. We recommend setting this to "Last item". If you have other custom requirements, such as detecting the model's output from the entire conversation history, you can also modify this configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">\*Description   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Detecting multiple matches may consume more tokens.   </div>
   

5. Confirm that the matching results meet your expectations.

   As shown below, the matching result corresponds to the content to be inspected in the original JSON.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c17cfefc3e6e437ca24906bc0d5fb7b2) </span>

6. After confirming, click **OK**.

   The response position is automatically populated with the confirmed JQ expression.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ea5c954abd5446e292c3b30c80a33a34) </span>

   You have now finished configuring the prompt and response positions for the custom application type.
