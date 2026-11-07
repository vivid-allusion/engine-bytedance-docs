---
title: "Limits"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Limits"
---

This topic introduces certain limits that you may encounter when using the AgentKit service.

<span id="gKvudVVi"></span>
## Agent runtime


|Limit item |Limit description |Changeable |
|---|---|---|
|Number of agent runtimes that a single account can create in a single region |20 |Yes. To increase the quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs). |
|Number of instances that can be created by a single agent runtime (that is, the maximum number of instances) |20 |No |
|Maximum size of an image file that can be imported |10 G |No |
|Execution timeout for synchronous requests |30 min |No |
|Max payload size |16 MB |No |


<span id="MbZfyFEY"></span>
## Sandbox templates


|Limit item |Limit description |Changeable |
|---|---|---|
|Number of sandbox templates that can be created by an account in a region |20 |Yes. To increase the quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs). |
|Maximum number of concurrent sandbox instances for a sandbox template |100 |Yes. To increase the quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs). |
|Maximum lifecycle duration of a sandbox instance |24 hours |No |


<span id="GmjYQPIx"></span>
## Gateway


|Limit item |Limit description |Changeable |
|---|---|---|
|**Dedicated gateway instance** |||
|Number of dedicated gateway instances that can be created by an account in a region |3 |No |
|Number of dedicated gateway instances of the **MCP type** that can be created by an account in a region |1 |No |
|Number of instances of the **model service type** that can be created by an account in a region |1 |No |
|Number of instances of the **agent runtime type** that can be created by an account in a region |1 |No |
|**MCP** |||
|Number of MCP services that can be created by an account in a region. |10 |Yes. To increase the quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs). |
|Number of API Key inbound authentication entries that can be configured for an MCP service/toolset |5 |No |
|Number of clients that can be associated with an MCP service/toolset OAuth JWT |5 |No |
|**Model service** |||
|Number of model services that can be created by an account in a region |1 |Yes. To increase the quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs). |
|Number of model providers that can be created under a model gateway |10 |Yes. To increase the quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs). |
|Number of API Keys that can be configured under a model provider |10 |Yes. To increase the quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs). |


<span id="ZUaiaIUp"></span>
## Skills Center


|Limit item |Limit description |Changeable |
|---|---|---|
|Number of skills that one account can create in a region |200 |Yes. To increase the quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs). |
|Number of Skills spaces that one account can create in a single region |200 |Yes. To increase the quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs). |
|Number of skills that can be registered in a skills space |20 |Yes. To increase the quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs). |
