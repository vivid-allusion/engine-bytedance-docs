---
title: "AI gateway service"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/AI_gateway_service"
---

API Gateway supports the feature for quickly creating AI gateways for AI large models deployed in Vital Kubernetes Engine clusters. This article introduces how to create an AI gateway for AI large models deployed in a cluster.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Beta · Apply for trial</strong>: This feature is currently in beta. To use it, please contact your account manager.</div>


<span id="uqh3TnnW"></span>
## Background information

When your large AI model is deployed in a Vital Kubernetes Engine cluster, you can use the AI Gateway Service to quickly create a gateway for your large AI model. Based on your configuration, the system automatically creates services, routes, and Upstream, enabling a one\-stop configuration process for the AI gateway. In the AI gateway service, each route corresponds to a backend model. 

<span id="uqh3TnnW"></span>
## Prerequisites


* Vital Kubernetes Engine

   * The Vital Kubernetes Engine cluster has been created, and the deployment of AI large models and services has been completed. For details, refer to [AI Cloud-Native Inference Suite](https://docs.byteplus.com/en/docs/vke/AI_cloud-native_inference_suite).

* API Gateway

   * The API Gateway instance has been created. For details, refer to [Create an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

   * The target cluster has been added as an Upstream source. For details, refer to [Import container clusters](https://docs.byteplus.com/en/docs/apig/Import_container_cluster).

   * (Optional) The service has been created, and a custom domain name has been bound. For details, refer to [Create service](https://docs.byteplus.com/en/docs/apig/Creating_a_service) and [Bind custom domain name](https://docs.byteplus.com/en/docs/apig/Adding_domain_name).


<span id="6F2txgvC"></span>
## Procedure


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, select **AI Gateway Service**, click **Create** **AI Gateway Service**.

   * **Basic Information**

   
   |Configuration Item |Descriptions |
   |---|---|
   |Instance |Select the API Gateway instance to which the AI Gateway belongs from the dropdown menu. |
   |Domain name |Configure domain names used by the AI gateway, including:<br><br><br>* **Use existing**: Use the domain name of the service that has already been created. When you select this option, you need to choose an existing service from the dropdown menu that appears.<br><br>* **Create a domain name**: Create a new domain name. When you select this option, the system automatically generates a new domain name, which is named `ai-service-xxxx`, where `xxxx` is a random string. |
   |AI Service Name |Configure the name of the AI service. The system will use this name to create the corresponding route. |
   |Access path |Configure the access path for the AI service. Configuration is currently not supported; by default, it matches the AI server name. For example, when the AI service name is configured as `seed`, after configuration is complete, the format of the access path for the large model is `domain/seed`. |
   

   * **Backend service**

   
   |Configuration Item |Descriptions |
   |---|---|
   |Backend Service |Select the backend service type to connect to Upstream. The default is **AI model proxy**. Configuration is currently not supported. |
   |Model type |Select the type of large language model to proxy in the dropdown menu. configuration is currently not supported.<br><br>The API gateway automatically aggregates all namespaces, services, and ports with the same name under all clusters from the Upstream source and treats them as a single application.<br><br><br>* **Namespace**: Select the namespace of the target Kubernetes service.<br><br>* **Service name**: Select the target Kubernetes service name.<br><br>* **Port**: Select the port exposed by the target Kubernetes service.<br><br>* **BaseUrl**: Configure the URL address for the backend model; corresponds to base_url in the OpenAI\-format SDK. For example `/v1`. |
   |Agreement |Select protocol type, supporting **HTTP1.1**, **HTTP2**, and **HTTP2/GRPC**. |
   |Cloud Load Balancer Algorithms |Configure the Cloud Load Balancer algorithm.<br><br><br>* **Round robin**: (default) Distributes all requests sequentially to Pods associated with the Kubernetes service. Suitable for scenarios where Pod specifications are identical.<br><br>* **Random**: Request random assignment among the Pods.<br><br>* **Least connections**: Assigns requests to the Pod currently handling the fewest requests.<br><br>* **Consistent hashing**: Performs load balancing based on header or query string information using Cloud Load Balancer. When the number of backend services remains unchanged, users carrying the same information are consistently routed to the same Pod. |
   

4. Click OK to complete the configuration.


<span id="5z1gNwSm"></span>
## Other configurations

<span id="hO91cSNI"></span>
### Obtain the access address

Select the target service from the service list. Click **Access method** in the **Actions** column to obtain the access address for the AI gateway service, including the **public network default domain name** and the **custom domain name**.

<span id="1eqY3NBl"></span>
### Enable authentication and authorization


1. After the AI Gateway Service is created, select the target service from the service list, click the service name, and enter the service details page.

2. Enable the authentication and authorization feature, and on the pop\-up configuration page, use the Key Auth plugin to configure API Key authentication and authorization. For more configuration details, refer to [API Key authentication and authorization](https://docs.byteplus.com/en/docs/apig/Creating_Key_Auth_plugin).


<span id="5z1gNwSm"></span>
## Result validation

<span id="RnCagvtI"></span>
### View configuration


1. After the AI gateway service is created, you can view the corresponding service in the service list.

   AI Gateway Service supports the following operation and maintenance actions

   * Click the **Edit** in the **Actions** column to edit the specified AI gateway service.

   * Click **delete** in the **Actions** column to delete the specified AI gateway service.

2. When an AI gateway service is created, the system simultaneously creates the corresponding Service, Route, and Upstream.

   * In the left navigation bar, select **Route Management \> Service List (Domain Name)** . It supports viewing services synchronously created by the system. Only when you create an AI gateway service and select **create domain name** will the service be created and a new domain bound simultaneously.

   * In the left navigation bar, select **Route Management \> Route List**. You can view routes created by system synchronization.

   * In the left navigation bar, select **Backend Management \> Upstream List** to view synchronized Upstreams.


<span id="EQkPzToO"></span>
### Access verification

In the local environment, you can use the domain name of the AI gateway service to invoke large models and obtain responses normally.

```bash
curl apig-example.com/seed/ -X POST  \
  -H "Content-Type: application/json"  \
  -H "Authorization: Bearer eyJhbGciOiJSUzI******" \
  -d '{
    "model": "seed_oss",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Who won the world series in 2020?"}
        ]
    }'
```


<span id="VYgrFTmR"></span>
## Related Documentation


* In addition to AI large models deployed in Vital Kubernetes Engine clusters, if you want to use the AI Gateway to proxy large models deployed by other methods, you can directly use the AI multi\-model proxy feature. For more information, refer to [AI multi-model agent](https://docs.byteplus.com/en/docs/apig/AI_Multi-Model_Proxy).

* For methods of deploying AI large models in Vital Kubernetes Engine, refer to [AI cloud-native inference suite](https://docs.byteplus.com/en/docs/vke/AI_cloud-native_inference_suite).


&nbsp;

&nbsp;
