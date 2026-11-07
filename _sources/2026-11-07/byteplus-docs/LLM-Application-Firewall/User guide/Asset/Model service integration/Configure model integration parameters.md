---
title: "Configure model integration parameters"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_model_integration_parameters"
---

To protect your large language model (LLM) applications, you must configure them as assets within the LLM Application Firewall. This guide provides step\-by\-step instructions on how to add your model service, configure its access parameters such as API keys and domains for different platforms, and ultimately route its traffic through the firewall for security inspection.

<span id="048c0ed8"></span>
## Prerequisites

You have obtained the domain name and API Key for the relevant model service. For related operations, please refer to the [Obtain the model service domain name and API Key](https://docs.byteplus.com/docs/LLM-Application-Firewall/Obtain_the_model_service_domain_name_and_API_Key).

<span id="0fc272f7"></span>
## Important note

The API Key must follow the `Authorization: Bearer <API Key>` format; otherwise, authentication will fail and traffic cannot pass through.

<span id="1cb62202"></span>
## Steps


1. Log in to the [LLM Application Firewall Console](https://console.byteplus.com/omni-shield/llm-shield/).

2. In the top bar, select the region of the instance.

3. Select **Asset management** in the left navigation, and then click **Add asset**.

4. Select **model service access** as the access method, and configure the relevant parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1a59f195cc7c4916b2b5e84948d9463e) </span>

* **Application information**: Basic application information is used to identify the specific service that integrates with the LLM Application Firewall.

   
   |Parameter |Description |
   |---|---|
   |Application name |Your custom business application name is used to distinguish different access applications in the firewall console.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Must start with a letter or a number.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only letters, numbers, periods(.), underscores(_), and hyphens are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Length should be between 1 and 128 characters.</div><br> |
   |Description |Additional information about this application. |
   

* **Model configuration**: Model configuration parameters define how the firewall identifies and extracts prompts from requests and outputs from responses. This is essential for deep content security inspection. The specific configuration of these parameters may vary depending on the model type. Details are as follows:

   
   <Tabs>
   <Tab zoneid="NXYSnQBDDS" title="Machine learning platform">
   <TabTitle>Machine learning platform</TabTitle>
   
   * **Model service domain name**: Enter the machine learning platform service domain name you obtained in advance. For example, the public access address of the machine learning platform may be `https://scv8****.com/mlp/s-20250311190045-rbjcf/`; then enter `scv8****.com`. For details, refer to [Get the domain name of MLP](https://docs.byteplus.com/docs/LLM-Application-Firewall/Obtain_the_model_service_domain_name_and_API_Key#f35eef19).
   
   * **Protected domain name**: The platform automatically generates a protected domain name. Business requests are redirected to this domain name for inspection, and the inspected data is forwarded to the machine learning platform for processing. To replace the original access domain name with the protection domain name provided by the LLM Application Firewall and redirect business traffic to the LLM Application Firewall for protection.
   
   * **Custom protection path**: Configure the protection path to ensure requests are routed to the correct protection mechanism.
   
      * **Type**: The JSON structure, parameter names, data types, and other aspects may differ among mainstream large models when receiving user input and returning responses. For example, OpenAI's API may use the `messages` array to encapsulate conversation content, while other models may use the `prompt` field directly. The LLM Application Firewall supports data parsing and adaptation for several mainstream LLM applications (including OpenAI, Qwen, DeepSeek R1, DeepSeek V3, and Doubao). By selecting the appropriate application type, the firewall can automatically identify and parse the locations of the Prompt in the request body and the large model output in the response body, thereby simplifying your configuration process.
   
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
         
   
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If your large model business does not fall under the above supported application types, or if you need to perform more advanced custom parsing, you need to select the custom application type and import the schema to complete the integration. For relevant instructions on custom application configuration, please refer to <a href="https://docs.byteplus.com/docs/LLM-Application-Firewall/configure_custom_application_types">Configure custom application types</a>.      </div>
         
   
      * **Path**: Enter the full request path by combining the path from the public access address with the API request path. For example, if the public access address is `https://scv8****com/mlp/s-20250311190045-rbjcf` and the API request path is `/v1/chat/completions`, then enter `/mlp/s-20250311190045-rbjcf/v1/chat/completions`. A large model application may provide multiple API endpoints (for example, `/v1/chat/completions` for conversation, `/v1/embeddings` for generating vectors). The firewall can configure different protection policies for API endpoints based on their paths to meet diverse security requirements.
   
   
   </Tab>
   <Tab zoneid="b0sW6y3PhE" title="Ark platform">
   <TabTitle>Ark platform</TabTitle>
   
   * **Ark application API key**: Enter the Ark Application API Key you obtained in advance. For instructions on how to obtain it, refer to [Obtain an API key for ModelArk](https://docs.byteplus.com/docs/LLM-Application-Firewall/Obtain_the_model_service_domain_name_and_API_Key#a0f3291d).
   
   * **Ark domain name**: The unified domain name through which the Ark platform provides external services.
   
   * **Protection domain name**: The platform automatically generates a protection domain name. Business requests are redirected to this domain for inspection before being forwarded to the Ark platform. You must replace the original access domain name in your application with this protected domain name to route traffic through the LLM Application Firewall.
   
   
   </Tab>
   <Tab zoneid="dl3mGYIU3U" title="Other model services">
   <TabTitle>Other model services</TabTitle>
   
   * **Model application API key**: Enter the model application API key you obtained in advance. For information on how to obtain it, refer to the official documentation of the corresponding model service.
   
   * **Model service domain name**: The unified domain name through which the model service platform provides external services.
   
   * **Protection domain name**: The platform automatically generates a protection domain name. Business requests are redirected to this domain for inspection, and the inspected data is forwarded to your model service for processing. You need to replace the original access domain name with the protection domain name provided by the LLM Application Firewall, and redirect business traffic to the LLM Application Firewall for protection.
   
   * **Custom protection path**: Configure the corresponding protection path based on the model type to ensure that requests are accurately routed to the appropriate protection mechanism for processing.
   
      * **Type**: Different mainstream large models may differ in their JSON structure, parameter names, and data types when receiving user input and returning responses. For example, OpenAI's API may use the `messages` array to encapsulate conversation content, while other models may use the `prompt` field directly. LLM Application Firewall has performed data parsing and adaptation for some mainstream LLM applications, including OpenAI, Qwen, DeepSeek R1, DeepSeek V3, and Doubao. By selecting the corresponding application type, the firewall can automatically identify and parse the Prompt location in the request body and the large model output location in the response body, thereby simplifying your configuration process.
   
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
         
   
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If your large model business does not fall under the above supported application types, or if you require more advanced custom parsing, you need to select the custom application type and import a schema to complete the integration. For relevant instructions on custom application configuration, please refer to <a href="https://docs.byteplus.com/docs/LLM-Application-Firewall/configure_custom_application_types">Configure custom application types</a>.      </div>
         
   
      * **Path**: When the client sends a request to the large model application API, this refers to the exact path in the URL, excluding the domain name and port. A large model application may provide multiple API endpoints (for example: `/v1/chat/completions` for conversation, `/v1/embeddings` for generating vectors). The firewall can configure different protection policies for API endpoints on different paths to meet diverse security requirements.
   
   
   </Tab>
   </Tabs>
   

* **Origin server configuration:**  Origin server configuration parameters control the connection behavior between the LLM Application Firewall and the backend machine learning platform. Unless otherwise required, keep the default values.

   
   |Parameter name |Description |Default value |Configurable range |
   |---|---|---|---|
   |Connection timeout |The timeout period for establishing a connection between the LLM Application Firewall and the backend server. |4 |4 to 120 seconds |
   |Write timeout |The timeout period for the LLM Application Firewall to transmit requests to the backend server. |60 |30 to 3600 seconds |
   |Read timeout |The timeout period for the LLM Application Firewall to read a response from the backend server. |60 |30 to 3600 seconds |
   |Maximum origin retry attempts |The number of retry attempts allowed after an origin fetch failure in the LLM Application Firewall. |3 |1 to 10 times |
   |Reusable persistent connection |The number of reusable persistent connections that the LLM Application Firewall can maintain for fetching from the origin. |100 |60 to 1000 items |
   |Idle connection timeout |Idle time of the long connection established for requests between the LLM Application Firewall and the backend server. |15 |1 to 3600 seconds |
   

5. Click **Next**.

   The next page displays the default protection policy settings for the protected domain name. You can quickly configure here, or go directly to the policy configuration page for detailed configuration.

   For details on policy configuration, see [Introduction to protection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_protection_policy).


<span id="48e7c8db"></span>
## What to do next

After completing the configuration, you need to replace the original access domain name with the protection domain name provided by the LLM Application Firewall, and route business traffic to the LLM Application Firewall for protection.

For example, if your service uses the Ark Python SDK, you need to set the `base_url` in the following initialization configuration to ` /api/v3`.

```Python
client = Ark(
    api_key=os.environ.get("ARK_API_KEY"), # Ark's API key, for example: 5b25f2d5-466d-4017-a864-304d99cf****
    base_url="4b60****.access-bp.llm-shield.omni-shield.ai/api/v3"  # Set the Ark access path to <Protected domain name from LLM Application Firewall>/api/v3
```


After you update the domain name, applications deployed on Ark are automatically protected by the LLM Application Firewall. The LLM Application Firewall performs real\-time inspection on all relevant requests based on configured policies and returns the results.
