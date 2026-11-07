---
title: "AI multi-model proxy"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/AI_Multi-Model_Proxy"
---

AI gateway supports connecting to common large language models (OpenAI, Doubao, Kimi, Tongyi Qianwen, etc.), providing unified and highly available AI gateway features for large language models. This article describes how to access a large language model through an AI gateway.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>[Beta · apply for trial] </strong>: This feature is currently in beta, please contact your account manager to use it.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

API Gateway (APIG) is an AI gateway, providing managed cloud native gateway features for common large language models, and realizing unified multi\-model access proxy features. At the same time, the API Gateway supports connecting to [Vital Managed Service for Prometheus ](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus)Product for instance\-level and service\-level observation and alert.

<span id=".5aSa5qih5Z6L5Luj55CG6K6_6Zeu"></span>
### Multi\-model proxy access

In the process of AI application development and construction, it is especially necessary to connect to multiple different model vendors. Because different vendors or models have their own unique interfaces and call methods. In order to adapt to different large models, developers must adapt call information from multiple vendors or models in their application code. This makes the integration process particularly complex and time\-consuming.

By using AI gateways to implement multi\-model proxies, unify protocols and call methods between different vendors and models. Developers no longer need to adapt each model vendor's API individually.


* For the AI application that has been developed, since the AI gateway realizes the hosting of the model type and API\-Key, the system will automatically rewrite the relevant information in the access request. Therefore, existing applications can access multiple model vendors directly through the AI gateway without modification, which can help users migrate to new models (such as bean bags, dark side of the moon, etc.) more quickly and smoothly.

* For newly developed AI applications, all models can be accessed by simply following the unified interface specification of the AI gateway, which greatly simplifies the difficulty and effort of integration. At the same time, when new vendors or models are added later, developers only need to make one modification on the gateway to adapt to all models using the protocol, without modifying the application itself, reducing maintenance costs.


<span id=".6Ieq5a6a5LmJ5o6l5YWl54K55ZKM6K-t5LmJ"></span>
### Custom access points and semantics

When using the AI gateway to access the large model, it allows users to use a custom Domain name, and can use more practical access point semantics to improve the user experience when using the AI large model. E.g., for many large models, `/chat/completions `access points are primarily used to generate conversations. After using the AI gateway proxy large model, you can use a more practical access point name and use `/chatbot `instead of `/chat/completions `, which is convenient for users to quickly identify the meaning of the access point and mask the differences between access points of different manufacturers.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The target large language model service has been opened and the API Key has been obtained. 

* A VMP workspace has been created, details refer to [Creating a workspace ](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* Domain name registers have obtained the domain name to be bound. 

* API Gateway

   * An API Gateway instance has been created, details refer to [Creating an instance ](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

   * A service has been created and bounded to custom domain name. details refer to [Creating a service ](https://docs.byteplus.com/en/docs/apig/Creating_a_service), [Adding domain name](https://docs.byteplus.com/en/docs/apig/Adding_domain_name).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu6IFVwc3RyZWFt"></span>
### Step 1: Create a upstream


1. In the left navigation bar select **Backend Management \> Upstream List ** .

2. On the Upstream list page, click **Create Upstream ** .

3. On the create Upstream page, fill in the parameter information as required.

   * **Basic information ** : name and instance of configuration Upstream.

   * **Backend configuration ** : Backend Service select **AI model proxy ** .

      
      |parameter |Description |
      |---|---|
      |Model type |In the drop\-down menu, select the large language model type that needs to be represented. Currently, OpenAPI, Doubao, Dark Side of the Moon, Tongyi Qianwen are supported. |
      |model address |After selecting the large language model, the system will automatically fill in the address corresponding to the large language model. Please confirm that the address is correct. If necessary, modify the model address. |
      |Model API Key |API Key configuration large language model, used to complete authorization authentication. |
      |Advanced settings |Click **add ** to add the special field of the model service provider in the Header or Body of the HTTP access message. |
      

4. Click **Confirm ** to create Upstream.


<span id=".5q2l6aqk5LqM77ya5Yib5bu66Lev55Sx"></span>
### Step 2: Creat a route

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The system supports a single route for the specified Service configuration, and also supports adding routes for multiple Service batches. This article specifies Service configuration single route as an example.</div>


* <div data-tips="true" data-tips-type="tip">The actions method to add route for multiple service batches, refer to <a href="https://docs.byteplus.com/en/docs/apig/Creating_a_route">Creating a route</a>.</div>


1. In the left navigation bar select **Route Management \> Service List (Domain name) ** .

2. On the Service List page, click the target Service name to enter the current Service Overview page.

3. Click **add route ** to configure route list.

   * **Basic information ** : name of configuration route, request method method, and path path.

   * **Upstream traffic delivery ** : configuration Upstream and traffic weight connected to the routing backend.

      
      |parameter |Description |
      |---|---|
      |upstream type |Select the access Upstream type, in this case select the **AI model agent ** . |
      |Select Upstream |In the dropdown menu select configuration AI model type Upstream. |
      |weight |Configuration of the current Upstream traffic weight. Integer form, with values ranging from 1 to 1000.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The system will display the traffic division proportionally according to the total weight of the Upstream configuration and the proportion of the full stack of each Upstrem, and the percentage number is accurate to two decimal places.</div><br> |
      |target model |Configuration target model. |
      |Target path |Configure the path of the model. |
      

4. Click **confirm ** to create the route.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

In the local environment, use a custom access point to invoke the large model and obtain a response.

```bash
curl http://apig-example.com \
  -H "Content-Type: application/json" \
  -d '{
    "model": "ep-20***-***",
    "messages": [
      {"role": "system","content": "You are Doubao, an AI assistant developed by ByteDance"},
      {"role": "user","content": "What are the common cruciferous plants?"}
    ]
  }'
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When calling a large model through the AI gateway, the <code>model </code>is a required field, but can take any value, and the AI gateway will replace its value with the configuration of the <strong>target model </strong>in the route.</div>
