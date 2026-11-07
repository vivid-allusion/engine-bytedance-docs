---
title: "Configure traffic integration parameters "
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Configure_traffic_integration_parameters"
---

To protect your LLM application, this guide shows how to add a domain to the LLM Application Firewall using the traffic integration method. This method is ideal if your business is not configured with load balancing. This document provides step\-by\-step instructions for configuring all necessary parameters, including application information, network settings, and origin server details.

<span id="b71680bd"></span>
### Interface compatibility

Different LLMs often vary in their request and response structures, including JSON schemas, parameter naming, and data types. For instance, the OpenAI API utilizes a `messages` array to encapsulate dialogue history, while other models may employ a direct `prompt` field.

To ensure that the LLM Web Application Firewall correctly parses your traffic, you must select the appropriate **Application Type** based on your interface protocol.

MAWAF currently supports the following mainstream interface protocols:


* **OpenAI Chat Completions Compatible**: A stateless standard interface based on message streams. It is ideal for traditional chatbots, single\-turn text generation, and straightforward business integration scenarios.

   * **Supported Models**: Doubao, OpenAI, DeepSeek, and Qwen.

* **OpenAI Responses API Compatible**: A stateful interface specifically designed for AI Agents. It natively supports cloud\-based memory and tool\-calling loops (e.g., web search, file reading), making it ideal for building complex AI applications with autonomous task\-processing capabilities.

   * **Supported Models**: Doubao and OpenAI.

* **Qwen DashScope**: The native protocol for Alibaba Cloud’s Qwen DashScope service.

* **Custom Type**: If your model service does not align with any of the pre\-defined types above, or if you require advanced custom parsing, we recommend connecting via **Schema Import**. For detailed instructions, please refer to [Configure custom application types](https://docs.byteplus.com/docs/LLM-Application-Firewall/configure_custom_application_types).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">\*Notice   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Custom application type is applicable to text detection only.   </div>
   

<span id="ba203192"></span>
## Prerequisites


* You have created a protection instance. For related operations, refer to [Create an LLM Application Firewall instance](https://docs.byteplus.com/docs/LLM-Application-Firewall/create_an_LLM_Application_Firewall_instance).

* The domain to be protected must have an ICP filing and must not have been previously added to the firewall.


<span id="2b8961ec"></span>
## Steps


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. Select the instance's region from the top bar.

3. In the left navigation, select **Asset management**, and then click **Add domain**.

4. Select **Traffic integration** as the integration method, and configure the integration parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cd593120d75445e8a651864b137b6535) </span>

   * **Application basic information**: This information is used to identify the specific business operation connected to the LLM Application Firewall.

      
      |Parameter |Description |
      |---|---|
      |App name |Your custom business application name, used to distinguish different access applications in the firewall console.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The name must start with a letter or a number.</div><br><br><br>* <div data-tips="true" data-tips-type="default">It can only contain letters, numbers, periods (.), underscores (_), and hyphens.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The length must be between 1 and 128 characters.</div><br> |
      |Description |Additional information about the access application. |
      

   * **Network configuration**: Used to configure parameters such as the domain name, application type, and path of assets to ensure that the LLM Application Firewall can accurately identify and process relevant traffic.

      
      |Parameter |Description |
      |---|---|
      |Domain name |Enter the domain names that require protection. Wildcard domains and exact domains are supported. Domain names must have ICP filing; domain names without ICP filing cannot be added.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">To configure both a wildcard domain and the main domain itself, configure them separately. For example: To configure both <code>*.</code><code>b.a.com</code> and <code>b.a.com</code>, each domain must be integrated separately and policies must be configured for each.</div><br> |
      |Application type |Select the interface protocol standard for the model service according to your model application's actual interface:<br><br><br>* **OpenAI Chat Completions compatible**: Supports models including Doubao, OpenAI, DeepSeek, and Qwen.<br><br>* **OpenAI Responses API compatible**: Supports models including Doubao and OpenAI.<br><br>* **Qwen DashScope model**: For the Alibaba Cloud Qwen DashScope native protocol.<br><br>* **Custom application type**: Integrate a custom application by importing a schema. For related configuration instructions, refer to the documentation.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Notice</div><br><br><br><div data-tips="true" data-tips-type="warning">Custom application type is applicable to text detection only.</div><br> |
      |Path |* This refers to the precise path in the URL, excluding the domain name and port, when the client sends a request to the LLM application API. An LLM application may provide multiple API endpoints (for example: /v1/chat/completions for conversation, /v1/embeddings for generating vectors).<br><br>* The firewall can configure different protection policies for API endpoints based on their paths to meet diverse security requirements. |
      |Protocol type |The communication protocols used by websites that need to integrate with the LLM Application Firewall can be either HTTP or HTTPS.<br><br><br>* Protocol selection: When the HTTPS protocol is selected, the corresponding certificate must be selected.<br><br>* Port number configuration: The HTTP protocol supports port 80 by default, and the HTTPS protocol supports port 443 by default.<br><br>* More settings:<br><br>   * HTTP 2.0: Before enabling, you must select the HTTPS protocol type. After enabling, HTTP 2.0 protocol is supported for access protection, and traffic is forwarded to the origin using the HTTP 1.0/1.1 protocol. |
      |Certificate selection |When selecting the HTTPS protocol, you must associate the corresponding certificate. You can upload a certificate directly to the LLM Application Firewall console, or associate an existing certificate by selecting it from the certificate list in the BytePlus Certificate Center. |
      

   * **Origin server configuration**: This configuration specifies the origin server address and other related information for traffic integration. It must be entered accurately based on your business requirements.

      
      |Parameter |Description |
      |---|---|
      |Origin server protocol |The protocol for traffic between the LLM Application Firewall and the origin server can be HTTP or HTTPS.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">This protocol setting applies to all origin servers in the same region.</div><br> |
      |Custom host header |* You can specify the value of the Host field in the HTTP request header when the firewall sends requests to the backend LLM application.<br><br>* Configure this option if your backend application uses the `Host` header to distinguish services or route requests. You also need this option if you access the firewall by IP but want the firewall to use a specific domain for requests to the origin. |
      |Origin server configuration |* Origin server address: The origin server IP address of the website that requires integration with the LLM Application Firewall.<br><br>* Origin server port: The port corresponding to the origin server address.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Each asset supports configuration of up to 20 origin servers.</div><br> |
      

   * **Advanced settings**: These parameters control the connection behavior between the LLM Application Firewall and the backend machine learning platform. Unless there is a specific need, keep the default values.

      
      |Parameter |Description |Default value |Configurable ranges |
      |---|---|---|---|
      |Connection timeout |The timeout period for establishing a connection between the LLM Application Firewall and the backend server. |4 |4 to 120 seconds |
      |Write timeout |The timeout period for the LLM Application Firewall to transmit requests to the backend server. |60 |30 to 3600 seconds |
      |Read timeout |The timeout period for the LLM Application Firewall to wait for a response from the backend server. |60 |30 to 3600 seconds |
      |Maximum origin retry attempts |The number of retry attempts allowed after an origin fetch failure in the LLM Application Firewall. |3 |1 to 10 |
      |Reusable persistent connection |The number of reusable persistent connections for traffic to the origin server. |100 |60 to 1000 connections |
      |Idle connection timeout |The idle timeout for persistent connections between the LLM Application Firewall and the backend server. |15 |1 to 3600 seconds |
      

5. Click **Next**.

   The page displays the default configuration options for the protection policy applied to the protected domain. You can perform a quick configuration here, or go directly to the policy configuration page to configure in detail.

   Refer to [Introduction to protection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_protection_policy) for a detailed introduction and configuration instructions for the corresponding policies.


<span id="db0e2426"></span>
## What to do next

To ensure that domains integrated via CNAME can be accessed properly, you need to perform the following actions:


1. **Allow back\-to\-origin CIDRs**: If the origin server is configured with a firewall or has security software installed, add the LLM Application Firewall's back\-to\-origin CIDRs to the allowlist to avoid affecting business traffic forwarding to the origin server. For more details, see [Allow back-to-origin CIDR blocks](https://docs.byteplus.com/docs/LLM-Application-Firewall/Allow_back-to-origin_CIDR_blocks).

2. **Verify that forwarding is working correctly**: Confirm whether the forwarding rules are effective to ensure that business traffic can be properly forwarded through the LLM Application Firewall. For more details, see[Verify forwarding configuration](https://docs.byteplus.com/docs/LLM-Application-Firewall/Verify_forwarding_configuration).

3. **Modify DNS resolution**: Point the domain to be protected to the CNAME address (recommended) provided by the LLM Application Firewall to redirect traffic to our service. For more information, see [Modify DNS resolution](https://docs.byteplus.com/docs/LLM-Application-Firewall/Modify_DNS_resolution).
