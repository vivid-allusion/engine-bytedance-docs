---
title: "AI Model Fallbacks"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/AI_Model_Fallbacks"
---

The AI gateway supports the model Fallback feature. When the AI model configured in the system is unresponsive or encounters an error, the system can automatically switch to the Fallback model, effectively ensuring the stability and reliability of the application. This article describes how to configure the Fallback model.

<span id="NjgVztmJ"></span>
## Background information

AI Fallback refers to the mechanism in an AI gateway where, if the primary model Service becomes unavailable, the system automatically switches to a fallback model, thereby effectively ensuring the stability and reliability of the application and preventing request failures caused by exceptions or high load on any model Service. Typical scenarios are shown in the following figure.

<span id="cwnr01Wv"></span>
## trigger condition

When the Model Service is called, any HTTP status code in the `4xx` or `5xx` range triggers AI Fallback.

<span id="MgXBNbVH"></span>
## Prerequisites


* The target large language model service and Fallback model service have been activated, and the API Key has been obtained. 

* API gateway

   * An API Gateway instance has been created. For details, refer to [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

   * The gateway instance has been upgraded to version 3.4.0 or later. For details, refer to [Version Management](https://docs.byteplus.com/en/docs/apig/Version_Management).

   * Service created and custom domain name bound. For more information, refer to [Create a service](https://docs.byteplus.com/en/docs/apig/Creating_a_service) and [Bind a custom domain name](https://docs.byteplus.com/en/docs/apig/Adding_domain_name).

   * The target large language model and the Fallback model have been configured to use Upstream. For details, refer to [AI multi-model proxy](https://docs.byteplus.com/en/docs/apig/AI_Multi-Model_Proxy).


<span id="yVAeEb1i"></span>
## Procedure


1. In the left navigation bar, select **Route Management \> Service List (Domain Name)** .

2. Click **Create Route** and configure routing information. When configuring Upstream traffic distribution, enable Fallback, and configure the Fallback model.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Fallback |Enable the AI model Fallback feature. When this feature is enabled, if the backend AI model returns a `4xx` or `5xx` error code, the AI gateway will automatically switch to the fallback model.<br><br><br>* **Target Upstream**: Configure the Upstream for the Fallback model.<br><br>* **Target model**: Configure the Fallback target model. If not configured, pass\-through is used by default.<br><br>* **Target path**: The path of the model to be configured. If not configured, pass\-through is enabled by default. |
   

4. Click **Add** to complete the configuration.


<span id="qa2prZo4"></span>
## Result validation


1. When the main model is functioning normally, you can access the large model via its domain name in the local environment.


```bash
curl http://apig-example.com \
  -H "Content-Type: application/json" \
  -d '{
    "model": "ep-20***-***",
    "messages": [
      {"role": "system","content": "You are Doubao, an AI assistant developed by ByteDance."},
      {"role": "user","content": "What are the common cruciferous plants?"}
    ]
  }'
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When invoking a large model through the AI gateway, the <code>model</code> field is required, but it can be assigned any value. The AI gateway will replace this value with the configuration of the <strong>target model</strong> as defined in the routing configuration.</div>



2. When the main model fails, you can still obtain a response by calling the large model via domain name in the local environment. This indicates that the AI gateway has successfully switched to the Fallback model.
