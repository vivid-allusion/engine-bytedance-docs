---
title: "Release notes"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Release_notes"
---

This article introduces the latest updates to API Gateway (APIG) features. New features will be available regionally in the coming future for trials.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the release notes, <strong>region</strong> records the region where the feature was first released. The actual supported regions are as shown in the console.</div>


<span id="ud5wwxrX"></span>
## April 2026


|Feature name |Description |Region |Related documentation |
|---|---|---|---|
|External authentication and authorization |The external authentication and authorization add\-on adds configuration options to ignore preflight requests (Options), allow anonymous access, hide credentials, and more, supporting richer authentication and authorization scenarios. |All |[External authentication and authorization](https://docs.byteplus.com/en/docs/apig/Custom_authentication_and_authorization) |
|HTTP routing supports configuration of fallback capability |When the backend service pointed to by the route returns an abnormal response, requests can be automatically forwarded to a preset fallback backend, ensuring high availability and continuity of business. |All |[Creating routes](https://docs.byteplus.com/en/docs/apig/Creating_a_route) |


<span id="NKg4ZUAB"></span>
## November 2025


|Feature name |Description |Region |Related documentation |
|---|---|---|---|
|GEOIP add\-on |The GEOIP add\-on supports obtaining the user's country code based on the user's source IP address and adding it to the header for subsequent business use. |All |[GEOIP add-on](https://docs.byteplus.com/en/docs/apig/GEOIP_plugin) |
|ID generation plugin for LLM session persistence |LLM session persistence ID generation add\-on generates a session persistence ID based on backend instance information or the prompt in the request, and implements session persistence using a consistent hash policy. |All |[ID generation plugin for LLM session persistence](https://docs.byteplus.com/en/docs/apig/LLM_session_persistence_ID_generation_plugin) |
|Consistent Hash supports overload protection |After enabling instance overload protection, if the number of active requests for an instance exceeds the threshold of average active requests, even if the hash value matches the instance, the instance will not be selected. |All |* [Creating VKE type Upstreams](https://docs.byteplus.com/en/docs/apig/Creating_a_Vital_Kubernetes_Engine_type_Upstream)<br><br>* [ECS type Upstream](https://docs.byteplus.com/en/docs/apig/Elastic_Compute_Service_type_Upstream)<br><br>* [Static domain name type Upstream](https://docs.byteplus.com/en/docs/apig/Fixed_domain_name_type_Upstream)<br><br>* [Static IP type Upstream](https://docs.byteplus.com/en/docs/apig/Fixed_IP_type_Upstream) |
|MCP Service supports OpenAPI 3.0 |Supports converting RESTful APIs described according to the OpenAPI 3.0 specification to MCP protocol. |All |[MCP service](https://docs.byteplus.com/en/docs/apig/MCP_Service) |


<span id="vIROpg56"></span>
## October 2025


|Feature name |Description |Region |Related documentation |
|---|---|---|---|
|Global rate limiting add\-on |Global rate limiting add\-on manages traffic access through metrics such as token count, bandwidth, and connection count, ensuring stable and efficient system performance. |All |[Global rate limiting add-on](https://docs.byteplus.com/en/docs/apig/Global_rate_limiting_plugin?lang=en) |
|instance version Update |Gateway instance adds version 4.0.0. Version 4.0.0 and above require enabling the NAT gateway in the VPC. |All |[Version management](https://docs.byteplus.com/en/docs/apig/Version_Management) |


<span id="1k8epnF4"></span>
## September 2025


|Feature name |Description |Region |Related documentation |
|---|---|---|---|
|AI gateway service |[**beta · apply for trial**] New AI Gateway Service, provides rapid creation of AI Gateway functionality for large AI models deployed in Vital Kubernetes Engine cluster. |All |[AI gateway service](https://docs.byteplus.com/en/docs/apig/AI_gateway_service) |
|MCP service |New MCP Service,provides seamless migration capability from RESTful API to MCP Protocol. |All |[MCP service](https://docs.byteplus.com/en/docs/apig/MCP_Service) |
|CORS policy |Supports flexible configuration of cross\-origin headers when configuring cross\-origin policy. |All |[Configuring CORS policies](https://docs.byteplus.com/en/docs/apig/Configuring_a_cross-origin_policy) |


<span id="Tu2JWiuc"></span>
## August 2025


|Feature name |Description |Region |Related documentation |
|---|---|---|---|
|Importing registered clusters |Based on the Registered cluster feature of VKE, now supports importing multi\-cloud clusters into APIG instance, using them as the upstream source for the gateway, so that the gateway can obtain the service list in the cluster. and implement multi\-cloud and multi\-cluster management. |All |[Importing registered clusters](https://docs.byteplus.com/en/docs/apig/Import_a_registered_cluster) |
|Self\-built Authentication |Adds support for connecting to user self\-built authentication and authorization services, facilitating unified authentication methods for users. |All |[Self-built Authentication](https://docs.byteplus.com/en/docs/apig/Custom_authentication_and_authorization) |
|AI model fallback |Adds support for model fallback feature. When the configured AI model in the system cannot respond or encounters an error, the system can automatically switch to the fallback model, effectively ensuring application stability and reliability. |All |[AI model fallback](https://docs.byteplus.com/en/docs/apig/AI_Model_Fallbacks) |
|Gateway instance |When creating a Gateway instance, new support for VPC subnet verification is added, displaying the remaining IP addresses of the current subnet. For subnets with fewer than 2 IP addresses, creating API Gateway instances is prohibited. |All |[Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance) |


<span id="l0QCzXIu"></span>
## May 2025


|Feature name |Description |Region |Related documentation |
|---|---|---|---|
|instance version management |Gateway instance supports instance version display. Differentversions support different gateway features. |All |[Version management](https://docs.byteplus.com/en/docs/apig/Version_Management) |
|LLM load\-aware routing |New LLM load\-aware routing add\-on,supports load balancing based on model inference scenarios. According to the load of the LLM backend GPU (for example: number of queued requests, KV\-Cache usage, and so on), provides load balancing capabilities that better fit inference scenarios. |All |[LLM load-aware routing](https://docs.byteplus.com/en/docs/apig/LLM_load-aware_routing) |
|LLM Session affinity routing |A new LLM session affinity routing add\-onprovides the capability to forward requests with the same session ID in multi\-turn sessions to the same instance, and to distribute requests with different session IDs as much as possible. |All |[LLM session affinity routing](https://docs.byteplus.com/en/docs/apig/LLM_Session_Affinity_Routing) |
|MCP Session persistence |Added the MCP session persistence plugin to support multi\-instance session persistence based on the MCP protocol. |All |[MCP session persistence](https://docs.byteplus.com/en/docs/apig/MCP_session_persistence) |


<span id=".MjAyNOW5tDEy5pyI"></span>
## March 2025


|Feature name |Description |Region |Related documentation |
|---|---|---|---|
|API Key authentication |* New Key Auth add\-on, supports authentication and authorization for the gateway based on API Key.<br><br>* Consumer now supports API Key management, allowing automatic generation or upload of API Key. |China (Beijing)<br><br>China (Shanghai)<br><br>China (Guangzhou)<br><br>Asia Pacific (Johor) |* [Create Key Auth add-on](https://docs.byteplus.com/en/docs/apig/Creating_Key_Auth_plugin)<br><br>* [Generating credentials](https://docs.byteplus.com/en/docs/apig/Generating_credentials)<br><br>* [Use API Key for gateway Authentication](https://docs.byteplus.com/en/docs/apig/Using_API_Key_to_Implement_Gateway_Authentication_and_Authorization) |
|Routing policy |Added support for retry policy, allowing automatic retry of failed requests based on specified retry conditions or status codes. |China (Beijing)<br><br>China (Shanghai)<br><br>China (Guangzhou)<br><br>Asia Pacific (Johor) |[Configuring retry policy](https://docs.byteplus.com/en/docs/apig/Configuring_a_retry_policy) |
|Upstream |New Upstream of fixed IP address type. Allows packaging fixed IP addresses that are interconnected with the gateway network as an Upstream, serving as the routing backend for the gateway. |China (Beijing)<br><br>China (Shanghai)<br><br>China (Guangzhou)<br><br>Asia Pacific (Johor) |[Static IP type Upstream](https://docs.byteplus.com/en/docs/apig/Fixed_IP_type_Upstream) |


<span id=".MjAyNOW5tDEy5pyI"></span>
##
