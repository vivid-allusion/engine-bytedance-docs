---
title: "Managing Predictions for Content Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-content_standard_getting_predictions"
---

Once models are created and trained, you can retrieve recommendation results through our BytePlus Recommend APIs. The following steps must be completed before integrating recommendation models into your production environment:


1. Integrate the Predict API

2. Integrate the AckServerImpressions API

3. Conduct allowlist testing

4. Conduct load testing


<span id="4a7813c3"></span>
# Integrating Predict API

Use the [Predict ](https://docs.byteplus.com/recommend/reference/content_saas_predict)API to retrieve your actual recommendation results.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">These Curl commands provide a general idea of how a testing account appears when using code samples.</div>



* <div data-tips="true" data-tips-type="tip">For real integrations, refer to our <a href="https://docs.byteplus.com/recommend/samples/content_code_samples">Code samples</a>.</div>


* <div data-tips="true" data-tips-type="tip">For real API integrations, use PROTO instead of JSON.</div>


* <div data-tips="true" data-tips-type="tip">Use the right MODEL_ID shown in your model list.</div>



**EXAMPLE**

```text
curl --request POST \
     --url https://rec-api-sg1.recplusapi.com/ContentSaaS/Predict \
     --header 'Tenant-Id: 3000001813' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
     "project_id": "804206547",
     "model_id": "100000",
     "scene": {
          "scene_name": "SearchPage"
     },
     "content_context": {
          "root_content": {
               "content_id": "1234456",
               "is_recommendable": 1,
               "categories": "[{\"category_depth\":1,   \"category_nodes\": [{\"id_or_name\":\"Movie\"}] },  {\"category_depth\":2,   \"category_nodes\": [{\"id_or_name\":\"Comedy\"}] } ]",
               "content_type": "gif",
               "video_duration": 1234555
          },
          "device": {
               "platform": "web"
          }
     },
     "user_id": "12345",
     "size": 20000
}
'
```


<span id="Integrating AckServerImpressions API"></span>
# Integrating AckServerImpressions API

The [AckServerImpressions](https://docs.byteplus.com/recommend/reference/content_saas_ackserverimpressions) API provides accurate server impression information. It is vital in evaluating and improving recommendation performance. Post\-processing logic may be in place with each unique client, and this can create inaccurate recommendation results for the user. This API helps BytePlus Recommend identify what is shown.

```text
curl --request POST \
     --url https://rec-api-sg1.recplusapi.com/ContentSaaS/AckServerImpressions \
     --header 'Tenant-Id: 3000001813' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
     "project_id": "804206547",
     "model_id": "100000",
     "scene": {
          "scene_name": "HomePage",
          "page_number": 33
     },
     "altered_contents": [
          {
               "content_id": "1234556",
               "altered_reason": "kept",
               "rank": 3
          }
     ],
     "predict_request_id": "asdfkk",
     "user_id": "sdfsss",
     "traffic_source": "self"
}
'
```


<span id="Approved list testing"></span>
# Allowlist testing

Approved list testing refers to model performance testing done by approved users. When code integration is complete, users are highly recommended to review the performance of BytePlus Recommend APIs using accounts from an approved list. These are usually your own developers' accounts.

If the chosen model is not ready when the user calls the Predict API, an error message "The Model ID is not ready for use" will be shown.

<span id="Load testing"></span>
# Load testing

We want to ensure a stable and efficient production environment for our users. To assess the performance of the BytePlus API in collaborative scenarios, load testing involves subjecting the system to peak Query Per Second (QPS) conditions for a duration of 1\-2 hours. This test aims to evaluate how the API handles high\-demand situations during collaboration. Additionally, clients have the option to request BytePlus to generate a stress testing report. This report includes details such as sample requests and corresponding QPS values, offering a comprehensive overview of the API's performance under stress conditions.

For more information on QPS limits, refer to [BytePlus Recommend Standard quotas and limits](https://docs.byteplus.com/recommend/docs/content_standard_getting_started).
