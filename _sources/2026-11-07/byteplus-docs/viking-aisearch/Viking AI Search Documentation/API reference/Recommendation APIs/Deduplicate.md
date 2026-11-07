---
title: "Deduplicate"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Deduplicate_API"
---

<span id="8a733dde"></span>
# Deduplication API

The **Deduplication API** enables clients to proactively report item IDs for real\-time filtering. It addresses two common issues with server\-side deduplication: items that are cached on the client but never actually displayed to users being incorrectly filtered out, and cross\-scenario impression data not being tracked.

<span id="dea31744"></span>
## Key Capabilities

Data submitted through this API powers the recommendation engine's impression\-based deduplication feature. Unlike traditional server\-side deduplication, impression\-based deduplication only filters items that users have actually seen, preventing high\-quality content from being permanently excluded due to missed impressions.

&nbsp;

Using this API, you can manually manage the deduplication item list for each recommendation scenario. Key benefits include:


* **Cross\-channel impression tracking:**  Prevents duplicate recommendations caused by impressions occurring across different channels.

* **Client\-side control:**  Puts deduplication management in the hands of the client, enabling full\-scene coverage.


&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">\*Prerequisite</div>


<div data-tips="true" data-tips-type="warning">Before calling this API, you must configure the <strong>Associated Pages/Modules</strong> in the corresponding recommendation scenario. For configuration details, see  <a href="https://docs.byteplus.com/docs/viking-aisearch/Remove_items_exposed_to_users">Exposure Deduplication</a> for configuration details. <strong>If this is not configured, the API will return an error.</strong></div>



---



<span id="7354ae5a"></span>
# Request


* **Method:**  **POST**

* **Endpoints:** 



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/application/{application_id}/deduplicate` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/deduplicate` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/application/{application_id}/deduplicate` |


`{application_id}`: The unique application identifier assigned when you create an application in the console. You can find this value in the console.


* **Authentication:**  Supports API Key or Access Key authentication. For details, see [API Authentication](https://www.volcengine.com/docs/85296/1544950).


<span id="2394b0b1"></span>
# Request Parameters

<span id="6053a101"></span>
## Request Body


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|`event_scene` |String |<span data-api-tag="require\|aW8jis7uY">必选</span> |`"homepage"` |**Event scene**<br><br>The scene where the user interaction occurs. Must match a value from the **Event Scene** field in your user event dataset. <br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">\*Note</div><br><br><br><div data-tips="true" data-tips-type="warning">The scene must also be configured as a <strong>Linked Page</strong> in the recommendation scenario, otherwise the API will return an error.</div><br> |
|`user` |**User** |<span data-api-tag="require\|aiFo66sGs">必选</span> |See below |**User information**<br><br>User information that associates the deduplication list with a specific user. Supports logged\-in user IDs. <br><br>For anonymous users, a device ID or other globally unique identifier can be used as a virtual user ID. |
|`items` |Array<**Item**\> |<span data-api-tag="require\|ahEYp1R6i">必选</span> |See below |**Exposed items**<br><br>The list of exposed items to deduplicate. See the Item object definition below. |


<span id="0690c0ef"></span>
## Data Structure

<span id="3e78cd92"></span>
### User


|**Parameter** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|`_user_id` |String |<span data-api-tag="require\|abEnq6oL4">必选</span> |`"user_id_123"` |The unique identifier for the user. <br><br>For anonymous users, use a globally unique identifier such as a device ID. |


<span id="431bbd71"></span>
### Items


|**Parameter** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|`_id` |String |<span data-api-tag="require\|azwTxPf3U">必选</span> |`"item_id_123"` |The unique identifier for the item to deduplicate. The item ID must already exist in the item dataset. |



---



<span id="3e791adc"></span>
# Response Parameters

<span id="f6003f13"></span>
## Request Response


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|`request_id` |String |`"25ee998a-5462-9385-9f18-035f1da7a6e5"` |A unique identifier for the request, used to trace and diagnose individual API calls. |


<span id="d5615818"></span>
# API Example

```JSON
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/\${application_id}/deduplicate' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
      "event_scene": "hompage",
        "user": {
            "_user_id": "user_id_12"
        },
        "items": [
            {"_id": "item_id_1"},
            {"_id": "item_id_2"}
        ]
}'
```


&nbsp;


---



<span id="1a011777"></span>
## Error Handling

If you receive an `InternalServiceError`, check the following:


1. Confirm that the **Associated Pages/Modules** have been configured in the corresponding recommendation scenario before calling this API. For details, see [Exposure Deduplication](https://docs.byteplus.com/docs/viking-aisearch/Remove_items_exposed_to_users).

2. Verify that the value of `event_scene` matches a value present in the **Event Scene** field of the corresponding user event dataset.


```JSON
{
    "error": {
        "code": "InternalServiceError",
        "message": "Service has some internal Error. Pls Contact With Admin."
    },
    "request_id": "5166-63e6460e6774"
}

```


<span id="b7672004"></span>
### Error Codes

For a full list of error codes, see the [Common Error Codes](https://docs.byteplus.com/docs/viking-aisearch/Common_Error_Codes) documentation.

&nbsp;
