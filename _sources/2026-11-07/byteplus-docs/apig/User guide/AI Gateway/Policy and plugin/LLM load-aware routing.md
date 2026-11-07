---
title: "LLM load-aware routing"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/LLM_load-aware_routing"
---

LLM load\-aware routing supports model inference scenariosby providing load balancing capabilities that are better suited to inference scenarios, based on the load of the LLM backend GPU (such as the number of queued requests, KV\-Cache usage, and more). This article describes how to configure LLM load\-aware routing.

<span id="sFYcCGzd"></span>
## Background Information

In traditional traffic gateways or LoadBalancer systems, load balancing algorithms, such as round robin, random, least connections or requests, consistent hashing, and many other algorithms, are often used to forward incoming traffic to different backend instances. However, in the field of AI large language models, the amount of resources used by a single request, such as GPU resources, is uncertain due to user requests, differences between models, and the randomness of prompt\-generated responses. However, traditional LoadBalancer algorithms cannot detect changes in the load status of backend instances in real time, which may result in unbalanced backend loads and affect the overall system throughput and response latency. Therefore, in AI model inference scenarios, it is necessary to schedule requests to the instance with the lowest load based on the backend GPU load conditions, including GPU KV\-Cache usage, the number of queued requests, and other factors. This ensures that backend inference instances handle requests as evenly as possible and prevents uneven GPU request distribution.

<span id="h8JQYQqH"></span>
## Prerequisites


* The APIG instance has been created. For details, refer to [Create an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* The APIG instance has been upgraded to version 3.3.0 or above. For details, refer to [Version Management](https://docs.byteplus.com/en/docs/apig/Version_Management).

* Service has been created. For details, refer to [Create service](https://docs.byteplus.com/en/docs/apig/Creating_a_service#.5Yib5bu65pyN5Yqh).

* Routes have been created. For details, refer to [Creating a route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).


<span id="CgRHtGtb"></span>
## Limit


* The same Plugin can only be bound once to the same resource.

* Within the same route, the LLM load\-aware routing Plugin, the LLM Session affinity routing Plugin, and the MCP session persistence Plugin are mutually exclusive and cannot be enabled at the same time.


<span id="A0uRPLWo"></span>
## Procedure


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the left navigation bar, select **Plugin management \> ** **LLM Load Aware Routing Plugin**, click **Create Plugin**, and configure Plugin parameters.

   
   |**Parameter** |Description |
   |---|---|
   |Effective level |Select the activation level for the LLM load\-aware routing Plugin. Currently, only the **Routing level** is supported. |
   |Instance |Select the APIG instance to which the Plugin belongs from the drop\-down menu. |
   |Service |In the dropdown menu, select the Plugin and its associated service. |
   |owning route |In the dropdown menu, select the Plugin, and then select its associated route. |
   |Notes/comments |You can choose whether to edit the notes/comments section based on your business needs. For example, you can specify the purpose of the Plugin to facilitate later identification. |
   |Inference engine |Select the inference engine used by the LLM, including **vllm, sglang**, and **others**.<br><br><br>* **Metric interface**: Configure the URI path where the inference engine exposes metrics, for example `/metrics`.<br><br>* **Metric port**: Configure the port number used to expose inference engine metrics, for example, `8000`.<br><br>* **Metric name**: Configure a metric for load awareness. The API gateway selects the optimal backend instance based on this metric. For example`vllm:num_requests_waiting`. |
   |minimum load difference |Configure the minimum difference based on the load scheduling metric |
   

3. Click **OK** to complete the configuration.


<span id="hL2AGJUA"></span>
## View configuration

After completing the configuration, check the Plugins you have configured in the Plugin list. If the Plugin status is **Enabled**, it means the Plugin is enabled.

&nbsp;
