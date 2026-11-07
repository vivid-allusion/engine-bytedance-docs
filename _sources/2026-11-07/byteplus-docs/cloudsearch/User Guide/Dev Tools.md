---
title: "Dev Tools"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/dev_tools"
---

Cloud Search provides the Dev Tools feature, allowing you to send REST API requests to clusters through Dev Tools for quick query debugging or to verify if data indexing succeeded. This topic describes how to use Dev Tools.

<span id="9af33f25"></span>
## Prerequisites


* Before using Cloud Search service, register a Volcengine account and complete enterprise verification.

* When using Cloud Search for the first time, complete cross\-service authorization so Cloud Search can access resources from other cloud products. For authorization details, see [Cross-service authorization](https://docs.byteplus.com/en/docs/cloudsearch/cross-service-authorization).

* Before using Dev Tools, create an Elasticsearch or OpenSearch instance first. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).


<span id="8b91d3af"></span>
## Precautions

Dev Tools does not support Elasticsearch 6 instances.

<span id="OkbwfpP3"></span>
## Procedure


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the project and region where you want to create an instance.

3. In the left navigation bar, select **PaaS model** \> **Dev Tools**.

4. On the Dev Tools authorization page, select the instance you want to use Dev Tools with from the dropdown list, enter the instance's username and password, check **15\-day authorization exemption** if needed, then click **Authorize to view Dev Tools**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you select an authorized instance, you do not need to enter the instance's username and password; just click <strong>Authorize to view Dev Tools</strong> directly.   </div>
   

5. In the Dev Tools Console debug panel, enter the API request you want to call, then click the run icon to the left of the first line of the current API request to call the API.

   For example, you can enter the following code in the debug panel to call the GET type `_search` interface.

   ```JSON
   GET _search
   {
       "query": {
        "match_all": {}
       }   
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the API call succeeds, you can view the API call results on the right side of the debug panel.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view recent debug records in the Dev Tools debug panel, where the system automatically saves the latest 0.5 MB of content. If this limit is exceeded, earlier records will be automatically cleared to ensure a smooth debugging experience.   </div>
