---
title: "Getting predictions—Other industries"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-other_premium_getting_predictions"
---

Once the models are created and trained, users can retrieve the recommendation results through our BytePlus Recommend APIs. The following steps must be completed before integrating recommendation models into your production environment:


1. Integrate the Predict API

2. Integrate the AckServerImpressions API

3. Conduct approved list testing

4. Conduct load testing


<span id="Integrating Predict API"></span>
# Integrating Predict API

Use the [Predict ](https://docs.byteplus.com/recommend/reference/retail_predict)API to retrieve the actual recommendation results.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">These Curl commands simply provide a general idea of how a testing account appears when using code samples.</div>



* <div data-tips="true" data-tips-type="tip">For real integrations, refer to our <a href="https://docs.byteplus.com/recommend/samples/retail_code_samples">Code samples</a>.</div>


* <div data-tips="true" data-tips-type="tip">For real API integrations, use PROTO instead of JSON.</div>


* <div data-tips="true" data-tips-type="tip">Use the right MODEL_ID shown in your model list.</div>



**EXAMPLE**

```JSON
{
  "user_id": "1457789",
  "size": 20,
  "scene": {
    "scene_name": "product detail page",
    "page_number": 2,
    "offset": 10
  },
  "context": {
    "root_product": {
      "product_id": "632461",
      "categories": [
        {
          "category_depth": 1,
          "category_nodes": [
            {
              "id_or_name": "Shoes"
            }
          ]
        },
        {
          "category_depth": 2,
          "category_nodes": [
            {
              "id_or_name": "Men's Shoes"
            }
          ]
        }
      ],
      "brands": [
        {
          "brand_depth": 1,
          "id_or_name": "Adidas"
        },
        {
          "brand_depth": 2,
          "id_or_name": "Yeezy"
        }
      ],
      "price": {
        "current_price": 49900,
        "origin_price": 69900
      },
      "is_recommendable": true,
      "title": "adidas Men's Yeezy Boost 350 V2 Grey/Borang/Dgsogr",
      "quality_score": 3.4,
      "tags": [
        "New Product",
        "Summer Product"
      ],
      "display": {
        "listing_page_display_tags": [
          "best seller",
          "hot sales"
        ],
        "detail_page_display_tags": [
          "FreeShipping",
          "Return in 7 days without any reasons"
        ],
        "listing_page_display_type": "image",
        "cover_multimedia_url": "https://images-na.ssl-images-amazon.com/images/I/81WmojBxvbL._AC_UL1500_.jpg"
      },
      "product_spec": {
        "product_group_id": "1356",
        "user_rating": 0.25,
        "comment_count": 100,
        "source": "self",
        "publish_timestamp": 1623593487
      },
      "seller": {
        "id": "43485",
        "seller_level": "1",
        "seller_rating": 3.5
      },
      "extra": {
        "count": "20",
        "color":"white",
        "material":"fabric"
      }
    },
    "device": {
      "platform": "android",
      "os_type": "phone",
      "app_version": "9.2.0",
      "device_model": "huawei-mate30",
      "device_brand": "huawei",
      "os_version": "10",
      "browser_type": "chrome",
      "user_agent": "Mozilla/5.0 (Linux; Android 10; TAS-AN00; HMSCore 5.3.0.312) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.106 HuaweiBrowser/11.0.8.303 Mobile Safari/537.36",
      "network": "3g"
    },
    "candidate_product_ids": [
      "1111111",
      "2222222"
    ]
  },
  "extra": {
    "clean_impr": "true"
  }
}
```


<span id="Request_IDs"></span>
# Request_IDs

Request_id is a unique identifier of API requests. Users need to generate the request_id and include it in their directory when calling Predict and AckServerImpression APIs.

Request_ids can be used to compare Predict API requests and AckServerImpressions API requests (BytePlus Recommended Products compared to AckServerImpressions Products). The differences between the two will be used to finetune the recommendation models and improve their performance.

Aside from that, request_ids can be included when generating user behavior data to facilitate performance evaluation and model tuning. It is a good practice to have request_id added to all the user behavior types like click, add\-to\-cart, purchase, and many others. This ensures that the data received is more accurate. However, it is a good start to incorporate the request_id into the user impression data if it is challenging to integrate it into the generation process.

**EXAMPLE**

User A goes to a specific recommendation scene. You will send a Predict API request with the request_id of BD_1631520669720, and a list of products will be received.

After User A sees Product B from the BytePlus Recommendation results, she might find it interesting and engage with the product. From here, you can add a request_id to the first impression event and then the second and create two separate UserEvent records as follows:


* User A, impression, Product B, Request BD_1631520669720

* User A, click, Product B, BD_1631520669720.


With the request_id, the BytePlus Recommend team can track the original Predict API and algorithm used. We will also analyze the Callback API, and the algorithm's impact on user A will be evaluated. In this scenario, the product has a positive effect. Thus the system will turn up the algorithm for this specific user.

<span id="ee8ca566"></span>
# Generating Request_IDs

Users can generate unique request_ids for their API requests.

**To request for a request_id:** 


1. Identify the date.

2. Identify the time.

3. Identify the IP address.

4. Identify a random string.

5. String the four components together for a unique request_id.


<span id="Integrating AckServerImpressions API"></span>
# Integrating AckServerImpressions API

The [AckServerImpressions](https://docs.byteplus.com/recommend/reference/retail_ackserverimpressions) API provides accurate server impression information. It is vital in evaluating and improving recommendation performance. Post\-processing logics may be in place with each unique client, and this can create inaccurate recommendation results for the user. This API helps BytePlus Recommend identify what is shown.

```JSON
{
  "predict_request_id":"3c9d7f56-82d3-405d-a0a7-62b04fb8f800",
  "user_id":"user_id",
  "scene":{
    "scene_name":"home"
  },
  "altered_products":[
    {
      "product_id":"product_id_1",
      "altered_reason":"kept",
      "rank":1
    },
    {
      "product_id":"product_id_2",
      "altered_reason":"inserted",
      "rank":2
    },
    {
      "product_id":"product_id_3",
      "altered_reason":"filtered"
    }
  ]
}
```


<span id="Approved list testing"></span>
# Approved list testing

Approved list testing refers to model performance testing done by approved users. When code integration is complete, users are highly recommended to review the performance of BytePlus Recommend APIs using accounts from an approved list. These are usually your own developers' accounts.

If the chosen model is not ready when the user calls the Predict API, an error message "The Model ID is not ready for use" will be shown.

<span id="Load testing"></span>
# Load testing

We want to ensure a stable and efficient production environment for our users. Your project will have a default QPS (Query Per Second) limit defined. If you need to exceed the default QPS limit or have additional requirements for load testing, contact the BytePlus Recommend team for assistance.
