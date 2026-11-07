---
title: "Managing Predictions for Retail Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-managing_predictions_for_retail_industry"
---

Once models are created and trained, you can retrieve recommendation results through our BytePlus Recommend APIs. The following steps must be completed before integrating recommendation models into your production environment:


1. Integrate the Predict API

2. Integrate the AckServerImpressions API

3. Conduct allowlist testing

4. Conduct load testing


<span id="4e498c4e"></span>
# Integrating Predict API

Use the [Predict](https://docs.byteplus.com/recommend/reference/retail_saas_predict) API to retrieve your actual recommendation results.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">These Curl commands simply provide a general idea of how a testing account appears when using code samples.</div>



* <div data-tips="true" data-tips-type="tip">For real integrations, refer to our <a href="https://docs.byteplus.com/recommend/samples/retail_code_samples">Code samples</a>.</div>


* <div data-tips="true" data-tips-type="tip">For real API integrations, use PROTO instead of JSON.</div>


* <div data-tips="true" data-tips-type="tip">Use the right MODEL_ID shown in your model list.</div>



**EXAMPLE**

```text
curl --request POST \
      --url https://rec-api-sg1.recplusapi.com/RetailSaaS/Predict \
      --header 'Accept: application/json' \
      --header 'Content-Type: application/json' 
      --data '
{
      "scene": {
      "scene_name": "homepage recommended for you"
      },
      "user_id": "test_user",
      "size": 30,
      "model_id": "you_model_id",
}
'
```


<span id="6d717281"></span>
# Integrating AckServerImpressions API

The [AckServerImpressions](https://docs.byteplus.com/recommend/reference/retail_saas_ackserverimpressions) API provides accurate server impression information. It is vital in evaluating and improving recommendation performance. Post\-processing logics may be in place with each unique client, and this can create inaccurate recommendation results for the user. This API helps BytePlus Recommend identify what is shown.

```text
curl --request POST \
      --url https://rec-api-sg1.recplusapi.com/RetailSaaS/AckServerImpressions \
      --header 'Accept: application/json' \
      --header 'Content-Type: application/json' \
      --data '
{
      "scene": {
      "scene_name": "homepage recommended for you"
      },
      "altered_products": [
           {
                "product_id": "product_a",
                "altered_reason": "kept",
                "rank": 1
           },
           {
                "product_id": "product_c",
                "altered_reason": "inserted",
                "rank": 2
           },
           {
                "product_id": "product_b",
                "altered_reason": "filtered",
                "rank": 0
           }
      ],
      "predict_request_id": "predict_returned_request_id",
      "user_id": "test_user",
      "traffic_source": "byteplus"
}
'
```


<span id="fe34a80c"></span>
# Allowlist testing

Allowlist testing refers to model performance testing done by approved users. When code integration is complete, users are highly recommended to review the performance of BytePlus Recommend APIs using accounts from an approved list. These are usually your own developers' accounts.

If the chosen model is not ready when the user calls the Predict API, an error message "The Model ID is not ready for use" will be shown.

<span id="04a2a940"></span>
# Load testing

We want to ensure a stable and efficient production environment for our users. To assess the performance of the BytePlus API in collaborative scenarios, load testing involves subjecting the system to peak Query Per Second (QPS) conditions for a duration of 1\-2 hours. This test aims to evaluate how the API handles high\-demand situations during collaboration. Additionally, clients have the option to request BytePlus to generate a stress testing report. This report includes details such as sample requests and corresponding QPS values, offering a comprehensive overview of the API's performance under stress conditions.

For more information on QPS limits, refer to [BytePlus Recommend Standard quotas and limits](https://docs.byteplus.com/recommend/docs/retail_standard_getting_started).
