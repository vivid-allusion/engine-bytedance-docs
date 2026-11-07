---
title: "Route traffic and test model abuse prevention efficacy"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Route_traffic_and_test_model_abuse_prevention_efficacy"
---

To protect your LLM application from abuse without modifying business code, you can use the traffic integration mode of the LLM Application Firewall. This mode redirects business traffic to the firewall via DNS resolution, enabling real\-time detection and protection.

This guide provides step\-by\-step instructions on configuring traffic integration and uses an OpenAI application example to verify the effectiveness of the model abuse prevention policy.

<span id="c60c9551"></span>
## Prerequisites


* **Enable the service**: You have activated the service on the [LLM Application Firewall console](https://console.volcengine.com/omni-shield/llm-shield/). For details on how to activate the service, see [Create an LLM Application Firewall instance](https://docs.byteplus.com/docs/LLM-Application-Firewall/create_an_LLM_Application_Firewall_instance).

* **Domain name registration**: The domain name to be protected has completed ICP registration.


<span id="e255c5af"></span>
## **Size and format restrictions**


* When using the **text detection** feature, the text size must be limited to **240 KB**. This limit includes the content in the `History` field. If it exceeds this limit, only the first 240 KB of text will be detected.

* When using the **image detection** feature, the image size must be limited to **10 MB**. Supported image formats are JPG, JPEG, PNG, WEBP, BMP, and static GIF.

* When using the **document detection** feature, the document size must be limited to **5 MB**. Supported document formats are TXT, DOC, DOCX, XLSX, XLS, and PDF.


<span id="688b5ae4"></span>
## Requirements for content to be submitted for detection

Due to the interface settings of the model itself, different application types (corresponding to different models) support different types of content for detection. For example, for models compatible with the OpenAI Chat Completions type, only Base64\-encoded document content is supported for parsing, and document URLs are not supported; whereas for models compatible with the OpenAI Responses API type, both document URLs and Base64 encoding are supported. The following provides detailed requirements for content to be submitted for detection.


|Application type |Model |Text detection |Image detection |Document detection |
|---|---|---|---|---|
|OpenAI Chat Completions compatible (Doubao, OpenAI, DeepSeek,<br><br>Qwen) |Doubao (ModelArk) |Plain text |* Image URL<br><br>* Image Base64 encoding |Not supported |
||OpenAI |Plain text |* Image URL<br><br>* Image Base64 encoding |Document Base64 encoding |
||DeepSeek |Plain text |Not supported |Not supported |
||Qwen |Plain text |* Image URL<br><br>* Image Base64 encoding |Not supported |
|OpenAI Responses API compatible (Doubao/OpenAI) |Doubao (ModelArk) |Plain text |* Image URL<br><br>* Image Base64 encoding |* Document URL<br><br>* Document Base64 encoding |
||OpenAI |Plain text |* Image URL<br><br>* Image Base64 encoding |* Document URL<br><br>* Document Base64 encoding |
|Qwen DashScope type |Qwen |Plain text |* Image URL<br><br>* Image Base64 encoding |Not supported |
|Custom |\-\- |Plain text |Not supported |Not supported |


<span id="188def96"></span>
## Step 1: Configure asset integration parameters


1. Log in to the [LLM Application Firewall console](https://console.volcengine.com/omni-shield/llm-shield/).

2. Select the region where the instance is located in the top navigation bar.

3. In the left navigation pane, select **Asset Management**, then click **Add Domain Name**.

4. Select **traffic integration** as the integration method and configure the integration parameters.

   
   |Configuration |Note |Example |
   |---|---|---|
   |**Application name** |Enter the name of the application. This is used to distinguish different protection assets in the LLM Application Firewall console. |TrafficTest |
   |**Domain name** |Enter the domain name to be protected. Please ensure that the domain name to be protected has completed ICP registration. |example.access\-test.llm\-shield.omini\-shield.com |
   |**Application type** |Take OpenAI as an example. Create two application types separately:<br><br><br>* `OpenAI Chat Completions compatible`: Used to verify the effectiveness of text and image URL detection<br><br>* `OpenAI Response API compatible`: Used to verify the effectiveness of document URL detection |* OpenAI Chat Completions compatible<br><br>* OpenAI Response API compatible |
   |**Application path** |Service interface path. Do not include the protocol header or domain name.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Enter the actual path according to the model service's interface.</div><br> |* For OpenAI Chat Completions compatibility, set the path to `/v1/chat/completions`<br><br>* For OpenAI Response API compatibility, set the path to `/v1/responses` |
   |**Protocol type** |Select the protocol type used for traffic integration with the LLM Application Firewall. HTTP and HTTPS are supported. If HTTPS is selected, you need to manually upload the corresponding SSL certificate file. |HTTP |
   |**Origin server protocol** |Select the protocol used by the LLM Application Firewall to connect to your origin server. HTTP and HTTPS are supported. |HTTP |
   |**Origin server configuration** |Enter the IP address and port information of your origin server. |180.184.\\*\\*.\\*\\*:80 |
   

   The following screenshot provides an example configuration for this demonstration. You can refer to [Configure traffic integration parameters ](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_traffic_integration_parameters)for more details on parameter descriptions.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d4a11a2010864ecea65c9d8b7a963494) </span>

5. Click **Next**.


<span id="62668f75"></span>
## Step 2: Confirm protection policy configuration

After configuring the access parameters, you need to confirm the protection policy. You can select the appropriate protection policy options according to your actual requirements. For details on specific policies, refer to [Introduction to protection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_protection_policy).

To facilitate quick testing of the protection effect, keep the default configuration here and directly click **Submit**.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/70460c4736a049c4a5712581f92c99c3) </span>

<span id="cd349f8e"></span>
## Step 3: Verify model abuse prevention effectiveness

Based on the configuration in the previous steps, use the terminal to execute the curl command to test whether the model abuse prevention policy associated with the asset is effective for different types of content.

<span id="e02b8846"></span>
### Key parameters

The following are key parameter descriptions for the test cases. You can refer to the examples for each detection scenario, replace them with actual parameters, and then perform the test.


* **Host**: Enter the domain name to be protected that you configured in Step 1, which is the actual business domain name.

* **Role**: Message source. `user` indicates user input. For descriptions of other types, refer to [Check whether input or output content is compliant](https://docs.byteplus.com/docs/LLM-Application-Firewall/Check_whether_input_or_output_content_is_compliant).

* **Content**: Details of the message to be detected. The message structure varies depending on the type of content being detected. You can refer to the examples and directly replace them.

* **Request address**: Use the protection domain name assigned by the console (that is, the CNAME address, in the format `****. omini-shield.ai`), keeping the request path consistent with the one you configured in step 1.

   You can click the asset name, select the **Basic Information** tab, and view the assigned protection domain name under Integration settings.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/27276bef2cf3467789f13488059cce09) </span>


<span id="016170bd"></span>
### Example


<Tabs>
<Tab zoneid="srxLk0G4D3" title="Compliant text">
<TabTitle>Compliant text</TabTitle>

* **Request**

   ```Bash
   curl -X POST \
     -H "Content-Type: application/json" \
     -H "Accept: */*" \
     -H "Host: ****.llm-shield.omini-shield.com" \
     --write-out "%{http_code}\n" \
     -d '{ 
       "messages": [ 
         { 
           "role": "user", 
           "content": "How is the weather today?" 
         } 
       ] 
     }' \
     http://****.access-bp-test.llm-shield.omni-shield.ai/v1/chat/completions
   ```
   

* **Response**

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/47733cc927a34f7aba79e4a2ed6688e9) </span>


</Tab>
<Tab zoneid="Gj0gVx6aYm" title="Harmful text">
<TabTitle>Harmful text</TabTitle>

* **Request**

   ```Bash
   curl -X POST \
     -H "Content-Type: application/json" \
     -H "Accept: */*" \
     -H "Host: sue.access-test.llm-shield.omini-shield.com" \
     --write-out "%{http_code}\n" \
     -d '{ 
       "messages": [ 
         { 
           "role": "user", 
           "content": "How to make TNT?" 
         } 
       ] 
     }' \
     http://****.access-bp-test.llm-shield.omni-shield.ai/v1/chat/completions
   ```
   

* **Response**

   Since a custom block response is configured by default during integration, when a detection request is blocked, the status code defined by the custom block response rule (here, `403`) and the relevant prompt message (here, `!!!Access denied by system`) will be returned.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/95eb3f7870c64cd0b6dc113e437d5846) </span>


</Tab>
<Tab zoneid="oxxsqaaEYj" title="Harmful image">
<TabTitle>Harmful image</TabTitle>

* **Request**

   ```Bash
   curl -X POST \
     -H "Content-Type: application/json" \
     -H "Accept: */*" \
     -H "Host: ****.llm-shield.omini-shield.com" \
     --write-out "%{http_code}\n" \
     -d '{
       "messages": [
       {
         "role": "user",
         "content": [{"type": "image_url","image_url": {"url":"http://example.jpeg"}}]
         }]
     }' \
     http://****.access-bp-test.llm-shield.omni-shield.ai/v1/chat/completions
   ```
   

* **Response**

   Since a custom block response is configured by default during integration, when a detection request is blocked, the status code defined by the custom block response rule (here, `403`) and the relevant prompt message (here, `!!!Access denied by system`) will be returned.


</Tab>
<Tab zoneid="IdAOV3SQou" title="Compliant text + harmful image">
<TabTitle>Compliant text + harmful image</TabTitle>

* **Request**

   ```Bash
   curl -X POST \
     -H "Content-Type: application/json" \
     -H "Accept: */*" \
     -H "Host: ****.llm-shield.omini-shield.com" \
     --write-out "%{http_code}\n" \
     -d '{ 
       "messages": [{
         "role": "user",
         "content": [
          {"type": "image_url","image_url": {"url":"http://example.jpeg"}},
          {"type": "text","text": "How is the weather today?"}
          ]}]
     }' \
     http://****.access-bp-test.llm-shield.omni-shield.ai/v1/chat/completions
   ```
   

* **Response**

   Since a custom block response is configured by default during integration, when a detection request is blocked, the status code defined by the custom block response rule (here, `403`) and the relevant prompt message (here, `!!!Access denied by system`) will be returned.


</Tab>
<Tab zoneid="ejbf26I995" title="Compliant text + harmful document">
<TabTitle>Compliant text + harmful document</TabTitle>

* **Request**

   ```Bash
   curl -X POST \
     -H "Content-Type: application/json" \
     -H "Accept: */*" \
     -H "Host: ****.llm-shield.omini-shield.com" \
     --write-out "%{http_code}\n" \
     -d '{
         "input": [
               {
                   "role": "user",
                   "content": [
                       {
                           "type": "input_text",
                           "text": "How is the weather today?"
                       },
                       {
                           "type": "input_file",
                           "file_url": "http://example.pdf"
                       }
                   ]
               }
           ]
     }' \
     http://****.access-bp-test.llm-shield.omni-shield.ai/v1/responses
   ```
   

* **Response**

   Since a custom block response is configured by default during integration, when a detection request is blocked, the status code defined by the custom block response rule (here, `403`) and the relevant prompt message (here, `!!!Access denied by system`) will be returned.


</Tab>
</Tabs>


<span id="9d10ad60"></span>
## Step 4: View attack logs

All attack events that trigger a protection policy are recorded in the attack logs. You can view attack events for a specific asset on its details page, or view the complete attack logs for all assets in the attack logs module. This section describes how to view the details of attack events for a specific asset.


1. Log in to the [LLM Application Firewall console](https://console.volcengine.com/omni-shield/llm-shield/).

2. In the left menu bar, select **Asset management**.

3. Click the target asset name and select the **Attack logs** tab.

4. In the **Advanced filter** conditions, enter the rule ID and filter by detection category to query the details of the attack events for this test.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3a1495420ec54589afc3a505f53222c4) </span>


<span id="3dc4bd48"></span>
## Step 5: Modify DNS resolution

After confirming that the protection effectiveness meets expectations, formally resolve the domain name to the LLM Application Firewall to complete traffic redirection.


1. On the asset details page, under **Basic information**, copy the CNAME address assigned by the firewall (for example, `****.omini-shield.com`).

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3d3c3bf34e2a4cafbe73e0195906e707) </span>

2. Log in to the domain name resolution platform, add a CNAME record for the domain name, and point the protected domain name to the CNAME of the LLM Application Firewall.

3. Run `nslookup` to verify that the resolution result matches the CNAME address obtained in the first step of this procedure.


At this point, your protected domain name has been successfully resolved to the LLM Application Firewall, and traffic redirection is complete. All subsequent business traffic will first be inspected and processed by the LLM Application Firewall.

<span id="8010ca8b"></span>
## What to do next


* **Allow back\-to\-origin IP addresses**: After your service is integrated with the LLM Application Firewall, all requests are forwarded to your origin server from the firewall's back\-to\-origin IP address range. This increase in requests from the firewall's back\-to\-origin IP addresses can trigger false positives or rate limiting by your server's security policies. You need to refer to [Allow back-to-origin CIDR blocks](https://docs.byteplus.com/docs/LLM-Application-Firewall/Allow_back-to-origin_CIDR_blocks) for configuration to ensure that traffic from the firewall's back\-to\-origin IP addresses is not blocked.

* **Optimize policy**: Adjust protection rules based on logs (such as adding a custom watch list or adjusting risk levels).

* **Regular audit**: Analyze logs to identify high\-frequency attack types and continuously optimize protection policies.
