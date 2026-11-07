---
title: "Product Features"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Features"
---

This article describes the core features of API Gateway.

<span id=".QVBJIOWFqOeUn-WRveWRqOacn-euoeeQhg=="></span>
## Authentication

The API gateway supports multiple types of authentication and authorization methods, providing comprehensive protection for the security of API calls and preventing access by malicious users.


|Feature |Descriptions |
|---|---|
|HTTPS protocol |Supports the HTTPS communication protocol, supports uploading single, multiple, or wildcard domain name certificates, and uses HTTPS certificates to ensure secure data transmission. |
|IP allowlist and blocklist |Provides IP\-based blocklist and allowlist. You can configure the blocklist and allowlist to deny or allow access requests from specific IP addresses. The API gateway supports configuring IP blocklists and allowlists at the instance, service, and route levels to meet fine\-grained access control requirements. |
|JWT authentication |Provides the lightweight authentication specification, JSON Web Token (JWT), which allows secure and reliable information to be transmitted between users and servers. After JWT authentication is enabled for the Service, only requests that include a JWT token can successfully access resources under the Service's domain name. |
|HMAC authentication |Generate a tamper\-proof AK/SK signature for HTTP requests using the HmacSHA256 algorithm. After this feature is enabled, you must include the required request headers, signature, and other relevant information to access backend resources. |
|API key authentication |Key Auth is a simple and widely used user authentication mechanism. The client adds a unique API key in the request header or request parameter. After the server or proxy obtains the API key, it checks whether a corresponding Consumer or Client identity exists, after which the corresponding authentication can be completed. |


<span id=".57K-56Gu55qE5rWB6YeP566h5o6n"></span>
## AI gateway

The API gateway can act as an AI gateway, connecting to popular large language models such as OpenAI, Doubao, Moonshot, and Tongyi Qianwen, among others. It provides unified and highly available cloud\-native gateway features.


|Feature |Descriptions |
|---|---|
|AI multi\-model agent |Can be used as an AI gateway, providing managed cloud\-native gateway features for common large language models and a unified proxy for multi\-model access. and allow customization of access points and semantics to improve the user experience when using large AI models. |
|AI\-powered routing |Requests are scheduled to the backend inference instance with the lowest load, based on factors such as the number of queued requests and other relevant metrics, to ensure that requests are distributed as evenly as possible among backend inference instances. |
|Token monitoring |Monitor token usage across different departments and teams to help users effectively track model usage, for example, by identifying which projects or entities have the highest token consumption. |
|Token usage control |By monitoring the number of tokens used by large models, quotas can now be allocated for overall model token usage or for usage by different departments, enabling effective management of model resource usage. |


<span id=".57K-57uG55qE5pyN5Yqh5rK755CG"></span>
## Traffic management

The API gateway supports robust routing management, canary release by traffic proportion, and other features, allowing precise control and routing of traffic.


|Feature |Descriptions |
|---|---|
|Route management |Supports routing traffic based on Method, Path, or Query String, and distributes it to multiple target upstreams according to traffic weight, enabling scenarios such as application multi\-version management. |
|Timeout policy |Supports response timeout policies and allows you to configure the maximum wait time for a request's response as needed. If the API gateway does not receive a response from the backend Service within the specified time, the gateway will return a response with an HTTP status code of `504` to the client. |
|Cross\-domain policy |Supports the Cross\-Origin Resource Sharing (CORS) policy, allowing cross\-origin access and enabling secure cross\-origin data transmission. |
|Rewrite policy |Supports URL rewrite policies, allowing rewriting of the URL used to access the Service so that it can access backend Services at different paths. |
|Retry policy |Supports retry policy, allowing you to specify retry conditions and automatically retry failed requests. For example, failing to connect to the backend service or retrying a request using a specified HTTP status code. |


<span id=".5by65aSn55qE5a6J5YWo6Ziy5oqk"></span>
## Upstream type

The API gateway supports abstracting backend applications with the same feature into a single Upstream, decoupling routing and backend applications, and meeting requirements such as multi\-version management for backend applications.


|Feature |Descriptions |
|---|---|
|Vital Kubernetes Engine upstream type |This feature supports connecting to Vital Kubernetes Engine (VKE), abstracting the Kubernetes Services in a VKE cluster as Upstreams, which serve as the routing backend for the gateway. Applicable to scenarios where businesses use VKE deployment and want to publish services through a gateway. |
|Registry center type: Upstream |Supports connection to the BytePlus microservices engine (MSE), abstracts the services registered in MES Nacos as an Upstream, which serves as the gateway's routing backend. Applicable to scenarios where services use MSE Nacos for governance and need to be published through a gateway. |
|Upstream function as a Service type |This feature supports connecting to BytePlus Function Service (veFaaS), and abstracts a published function as an Upstream, which serves as the routing backend of the gateway. Applicable to scenarios where businesses adopt veFaaS deployment and wish to publish through a gateway. |
|Upstream Elastic Compute Service type |Supports connecting to BytePlus Elastic Compute Service (ECS), abstracting multiple Elastic Compute Service instances as a single Upstream to serve as the gateway routing backend. Applies to scenarios where the business is deployed on ECS and you want to publish it through a gateway. |
|Upstream fixed domain name type |Supports connecting to fixed domain names. Domain names that can communicate with the gateway network can be encapsulated as an Upstream and used as the routing backend for the gateway. |
|Upstreams with fixed IP type |Supports connecting to fixed IP addresses, allowing fixed IP addresses that can communicate with the gateway network to be encapsulated as an Upstream and used as the routing backend for the gateway. |


<span id=".5aSa5pa55L2N55uR5o6n"></span>
## Feature add\-ons

The API gateway supports multiple types of add\-ons, provides a wide range of product capabilities, and enhances gateway extensibility. Add\-ons support hot updates, enabling gateway configurations to take effect quickly without impacting live traffic.


|Feature |Descriptions |
|---|---|
|HMAC add\-on |Generate an unforgeable AK/SK signature for HTTP requests based on the HmacSHA256 algorithm. This signature is used to enable or disable the HMAC authentication feature. After enabling this feature, you must include the relevant request headers, signature, and other information to access the current resource. |
|Rate limiting add\-ons |Supports controlling access request thresholds at both the APIG instance level and the route level to ensure the stability of backend services. |
|IP allowlist and blocklist add\-on |Supports configuring IP blocklists and allowlists at the instance, service, and route levels to meet fine\-grained Identity and Access Management requirements. |
|Key Auth add\-on |The Key Auth user authentication mechanism is used to generate API Keys for authentication and authorization. The client adds the API key to the request header or request parameter. After the APIG instance obtains the API key, it checks whether the corresponding Consumer/Client identity exists, thus completing the corresponding authentication. |
