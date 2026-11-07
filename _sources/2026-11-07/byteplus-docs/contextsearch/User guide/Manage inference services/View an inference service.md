---
title: "View an inference service"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/View_an_inference_service"
---

You can view information about prebuilt inference services and custom inference services, including basic information, monitoring information, and logs of the inference services. This topic describes how to view inference services.

<span id="k0hJ6GOQ"></span>
## Procedure


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. In the left navigation bar, select **Models and reasoning \> Inference service**, click the **Pre\-built inference service** or **Custom inference service** tab, then click the name of the target inference service.

4. In the inference service details panel, view information about the inference service in each tab.

   
   <Tabs>
   <Tab zoneid="F0U7GB2Pid" title="Basic information">
   <TabTitle>Basic information</TabTitle>
   
   On the **Basic information** tab, you can view the inference service's basic information, custom parameters, access information, associated models, and more.
   
   
   * Basic information
   
      Includes service name, availability zone, resource type, specification/number of nodes, access point throttling, creation time, startup time, stop time, description, and purchase method.
   
   * custom parameter
   
      Includes custom parameters added when creating an inference service, consisting of key and value.
   
   * Associated model
   
      You can view the model access address and call information.
   
      In the **Operation** column of the target model, select **Private network call information** or **Public network call information** to view the model's call information. Replace `$API_KEY` in the call information to call the model directly within ECS.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For instructions on obtaining an API Key, see <a href="https://docs.byteplus.com/en/docs/contextsearch/View_an_API_Key">View an API Key</a>.   </div>
      
   
   
   </Tab>
   <Tab zoneid="wgBSfq10vT" title="Monitoring">
   <TabTitle>Monitoring</TabTitle>
   
   Under the **Monitoring** tab, you can view monitoring information for the inference service. Filtering monitoring information by time range is supported.
   
   
   </Tab>
   <Tab zoneid="zRclZRw8Mg" title="Logs">
   <TabTitle>Logs</TabTitle>
   
   Under the **Logs** tab, you can view log content for the custom inference service. Filtering log content by time range, log level, file, and keyword is supported.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">Only inference services with <strong>Purchase method</strong> as <strong>Exclusive resource</strong> support viewing logs.</div>
   
   
   
   </Tab>
   <Tab zoneid="his6PpnCfR" title="Call example">
   <TabTitle>Call example</TabTitle>
   
   Under the **API Example** tab, you can view how to invoke the inference service. Currently, only API Key authorization is supported.
   
   After creating an API Key in ContextSearch, use the API Key to gain access to the custom inference service. You can obtain an API Key, set it in environment variables, and call the custom inference service following the example provided. For detailed instructions, see [View an API Key](https://docs.byteplus.com/en/docs/contextsearch/View_an_API_Key).
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">Inference services linked to certain models do not support call examples.</div>
   
   
   
   </Tab>
   </Tabs>
