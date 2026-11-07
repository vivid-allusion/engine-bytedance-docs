---
title: "Recommend"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Recommendation"
---

<span id="864da1f2"></span>
# Notes


* **Usage Limits:** 

   * Due to HTTP body size limits, the maximum body size for a single request cannot exceed 10 MB.


<span id="374ded73"></span>
# Request


* Request Method: POST

* Request URL:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/application/{application_id}/{scene_id}` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/{scene_id}` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/application/{application_id}/{scene_id}` |


`{application_id}`: The unique identifier for an application, assigned by the system after creation. It can be viewed in the console.

`{scene_id}`: The unique identifier for a recommendation scene, assigned by the system after creation. The format is scene{id} (e.g., sceneR01asDfs). You can copy the Scene ID by hovering over the scene name under 'Recommendation Experience' in the console. **The Scene ID starts with ** **`scene`** **.** 

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d3de33aa402a40d2a57b5d8e10df61b1) </span>

&nbsp;

<span id="3af69728"></span>
## Authentication Method

You can authenticate with an API Key or an Access Key. For details, see the [API Authentication documentation.](https://www.volcengine.com/docs/85296/1544950)

<span id="ad6eaefc"></span>
# Request Parameters

<span id="4fa39169"></span>
## Request Body


|**Parameter** |**Data Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|user |**User**<br><br> |<span data-api-tag="require\|a728pgbor">必选</span> |See: [User](https://docs.byteplus.com/docs/viking-aisearch/Recommendation#3032d22a) |**User Information**<br><br>Specifies the user who triggered this API call. |
|parent_items |Array<**Item**\> |**`Conditionally required`** |See: [Item](https://docs.byteplus.com/docs/viking-aisearch/Recommendation#47d0575d) |**Item on the details page (parent item)** <br><br>In the "Recommended on details page" scenario, the unique ID of the item on the current details page must be provided. The item ID must exist in the item dataset. |
|page_size |Integer |**`Optional`** |10 |**Configure maximum returned quantity**<br><br>If not provided, the return quantity configured in the console for the current scene is used. Pagination is not supported. The results are returned in a single batch.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Does the returned quantity not match the configured quantity?</div><br><br><br><div data-tips="true" data-tips-type="default">The returned count is not necessarily equal to the <code>pa</code><code>ge</code><code>_s</code><code>ize</code> parameter. If, after deduplication and filtering, the number of recommendable items is less than <code>p</code><code>age</code><code>_s</code><code>ize</code>, the returned count may be less than the configured count.</div><br> |
|disable_personalize<br><br><span data-api-tag="add\|aVKgucNEW">新增</span> |Boolean |**`Optional`** |`true` |**Disable personalized recommendations**<br><br>For compliance, the default is `false (enables personalized recommendations)`.<br><br>When personalized recommendations are disabled, recommendations will only be based on non\-personalized recalls, such as trending items and parent item similarity recalls. Recommended items will still adhere to your business configuration rules, including boosting, demotion, filtering, deduplication, and diversity rules.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Description</div><br><br><br><div data-tips="true" data-tips-type="default">Disabling personalized recommendations increases the probability of receiving empty results.</div><br> |
|session_id |String |**`Optional`** |`"session_123"` |**A unique identifier for a user session.** <br><br>Use a custom and unique value for each session, such as a UUID.<br><br>> Learn more: [Pinned Recommendation](https://docs.byteplus.com/docs/viking-aisearch/Pinned_Recommended_Items)<br><br><br>When pinned items are configured for a recommendation scene and 'Repeat recommendations on each refresh' is disabled, the platform uses the `session_id` to check if the pinned configuration has been applied to a visit within **24 hours**.<br><br><br>* If this parameter is not provided, repeated pinning will occur for the **same visit within 24 hours**. |
|filter |Object<**Filter**\> |**`Optional`** |See: [Filter](https://docs.byteplus.com/docs/viking-aisearch/Recommendation#db3f2d55) |**Dynamic filter parameter**<br><br>If 'Dynamic Parameter Filtering' is configured for the scene's recommendation scope, you must pass the parameter values through this field. The platform automatically uses the value to populate the parameter's filter conditions. The platform automatically ignores missing dynamic filter conditions. |
|output_fields |Array<String\> |**`Optional`** |`["title", "category"]`<br><br> |**Return Fields**<br><br>The fields returned by the recommended items API. All fields are returned by default. For nested object fields (Object, Array<Object\>), only passing the top\-level field name is supported.<br><br><br>* Incorrect field names and fields nested within an Object are automatically ignored.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Why aren't all fields returned?</div><br><br><br><div data-tips="true" data-tips-type="default">When an item has many fields, returning all of them increases the response speed of the recommendation API. Return only necessary fields to reduce latency, improve API response performance, and enhance log readability.</div><br> |
|context |Object<**Context**\> |**`Optional`** |See: [Context](https://docs.byteplus.com/docs/viking-aisearch/Recommendation#65900099) |**Request context**<br><br>Affects the recall processing logic for recommended items and the returned item results. |
|conditional_boost |Array<**Conds**\> |**`Optional`** |See: [Conds](https://docs.byteplus.com/docs/viking-aisearch/Recommendation_API_uplift_and_demotion_rule_configuration#ca81d523) |**API\-Level Promotion and Demotion Configuration**<br><br>> To learn more, see: [Boost and Bury via API (V2)](https://docs.byteplus.com/docs/viking-aisearch/Recommendation_API_uplift_and_demotion_rule_configuration)<br><br><br>The platform automatically merges and applies the promotion and demotion rules configured in both the console and the API. If omitted, only the promotion and demotion rules configured in the console will apply. |
|items |Object<**InputItems**\> |**`Optional`** |See: [InputItems](https://docs.byteplus.com/docs/undefined/689ca6076b8e61052657cef0#4823d19c) |**Custom candidate items**<br><br>Provided item list is merged into the recall candidate pool prior to ranking and re\-ranking. Custom merge weights are supported.<br><br>Typical use cases:<br><br><br>* **Ad blending:**  Inject sponsored items into the organic recall stream for unified ranking.<br><br>* **External candidate pool:**  Supply items recalled by the caller's own complex business logic. |
|debug |Boolean |**`Optional`** |true |Returns debug information associated with the API request. Defaults to false. |


<span id="54bbd814"></span>
## Data Structure

<span id="3032d22a"></span>
### User


|**Parameter** |**Data Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|_user_id |String |<span data-api-tag="require\|aBnAkpgoh">必选</span> |`"user_199432"` |**A unique identifier for the user.** <br><br>Identifies the user who triggered the API call. For users who are not logged in, you can use a globally unique identifier, such as a device ID, as a virtual user ID. |


<span id="47d0575d"></span>
### Item


|**Parameter** |**Data Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|_id |String |**`Conditionally required`** |`"item_1001"` |**The unique ID of the item.** <br><br>In "Recommended on Detail Page" scenarios, you must provide the unique ID of the item on the current detail page. The item ID must exist in the item dataset. |


<span id="db3f2d55"></span>
### Filter


|**Parameter** |**Example value** |**Description** |
|---|---|---|
|Parameter name |```JSON```<br>```{```<br>```    "category": ["shoes"],```<br>```    "max_price": 100.50```<br>```}```<br> |**Dynamic filter parameters**<br><br>> Depends on the platform configuration. See: [Configure Dynamic Filter Conditions](https://docs.byteplus.com/docs/viking-aisearch/Dynamic_recommendation_scope_configuration)<br><br><br>Used to pass dynamic filtering condition parameters that are consistent with the platform configuration. The parameter names must align with the platform configuration. **The platform automatically ignores missing dynamic filtering conditions.** <br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">The data type of the parameter value must be the same as the item field. Rules with misaligned data formats are invalid and will be automatically ignored.</div><br> |


<span id="65900099"></span>
### Context


|**Parameter** |**Example value** |**Description** |
|---|---|---|
|location |```JSON```<br>```{```<br>```    "latitude": "12.1243",```<br>```    "longitude": "-012.1223"```<br>```}```<br> |**Request user location**<br><br>> Depends on the platform configuration. See: [Boost and Demote by User Geo-location](https://docs.byteplus.com/docs/viking-aisearch/User_geographic_location-based_ranking_boost_and_demotion)<br><br><br>Supports passing the user's location to configure geolocation\-based item boosting and demotion. The input data must be a string. **If the input is invalid, the platform automatically ignores the configuration.**  |


<span id="3b41d1cd"></span>
### InputItems


|**Parameter** |**Data Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|items |Array<**Item**\> |<span data-api-tag="require\|aBj7w7y91">必选</span> |See：[Item](https://docs.byteplus.com/docs/viking-aisearch/Recommendation#47d0575d) |A list of custom candidate items, where each element is an Item object. **Maximum list length: 400.**  |
|weight |float |<span data-api-tag="require\|awLyB3oAq">必选</span> |0.3 |The merge weight controls the blending ratio between custom items and system\-recalled items.<br><br><br>* **weight ≤ 0:**  Custom items are excluded; only system\-recalled items are ranked.<br><br>* **0 < weight < 1:**  Custom items and system\-recalled items are blended according to the specified weight.<br><br>* **weight ≥ 1:**  Only custom items are ranked; system\-recalled items are discarded. |


&nbsp;


---



&nbsp;

<span id="65653637"></span>
# Response parameters

<span id="5d9f7a12"></span>
## Request response


|**Parameter** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|request_id |String |`"25ee998a-5462-9385-9f18-035f1da7a6e5"` |**Request ID**<br><br>The unique identifier for a request, which helps you to locate it quickly. |
|result |Object |Contains the content of the `rec_results` and `extra_info` parameters. |**Complete content response** |
|rec_results |Array<**RecommendResults**\> |See: [RecommendResults](https://docs.byteplus.com/docs/viking-aisearch/Recommendation#48767e7f) |**A list of recommended items, including their unique identifiers and detailed information.**  |
|extra_info |Object<**ExtraInfo**\> |See: [ExtraInfo](https://docs.byteplus.com/docs/viking-aisearch/Recommendation#09fcad10) |**Additional information about request processing**<br><br>Use this to check the recommendation request processing logic, which helps you understand and troubleshoot the validity of your configuration and whether the processing logic meets business requirements. |


<span id="fb011f8b"></span>
## Data structure

<span id="48767e7f"></span>
### RecommendResults


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|_id |String |"item_1003" |**Unique item key**<br><br>Item ID of the recommended item. |
|display_fields |Object |```JSON```<br>```{```<br>``` "item_count":  1234,```<br>``` "update_time": 1752238693295,```<br>``` "item_id": "item_1003"```<br>```}```<br> |**Item data content object**<br><br>The returned fields can be defined by the `output_fields` request parameter. By default, all fields are returned, and their content is consistent with the imported item dataset.<br><br> |


<span id="09fcad10"></span>
### ExtraInfo


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|forced_item_info |Object <**ForcedItems**\> |See below: [ForcedItems](https://docs.byteplus.com/docs/viking-aisearch/Recommendation#30f2849c) |**Pinned Item Processing Logic**<br><br>When the pinned item configuration is enabled for a recommendation scene, the parameter returns the pinned item ID and effective status, allowing you to check if it works as expected. |
|omitted_params |Array<String\> |`["category", "max_price"]` |**Automatically Ignored Dynamic Filtering Conditions**<br><br>The platform automatically ignores invalid or empty dynamic filtering conditions to ensure the recommendation API returns results. This parameter lists the names of ignored [Filter](https://docs.byteplus.com/docs/viking-aisearch/Recommendation#db3f2d55)parameters in the request. |
|boost_status |Array<String\> |`["success", "field not found", "invalid operator"]` |**API Promotion and Demotion Rule Status**<br><br>> To understand the meaning of each status, see: [Boost and Bury via API (V2)](https://docs.byteplus.com/docs/viking-aisearch/Recommendation_API_uplift_and_demotion_rule_configuration)<br><br><br>Returns the execution status of API rules when promotion and demotion rules are passed in a request.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Return Order Logic</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Strictly follow</strong><strong>s</strong><strong> parameter</strong><strong> </strong><strong>or</strong><strong>der.</strong></div><br><br><br><div data-tips="true" data-tips-type="default">If the first configuration runs successfully,<code>boost_status</code>'s first status will be <code>success</code>.</div><br> |
|diversity_rule |Object<**SuccessRules**\> |See below: [SuccessRules](https://docs.byteplus.com/docs/undefined/689ca6076b8e61052657cef0#d6dc0b38) |**Active diversity rules**<br><br>Returns the names of the diversity rules that are active on this current API request.  |


<span id="30f2849c"></span>
### ForcedItems


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|item_ids |Array<String\> |`["60493", "52937"]` |**Successfully pinned item IDs**<br><br>If an item ID is not in the item dataset, the platform automatically removes the item. |
|skipped |Boolean |`false` |**Pin status**<br><br>> For session_id parameter configuration, see: [Request Body](https://docs.byteplus.com/docs/viking-aisearch/Recommendation#4fa39169)<br><br><br><br>* `true`: The `session_id` has appeared within the last 24 hours, and the pin is inactive<br><br>* `false`: The `session_id` has not appeared within the last 24 hours, and the pin is active. |


<span id="d9ad900a"></span>
### SuccessRules


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|success_rules |Array<String\> |`["123", "423"]` |**Active diversity rules**<br><br>Returns the rule ID of the diversity rules that are active on this current API request.  |


&nbsp;


---



<span id="67772d58"></span>
# API Example

<span id="7b0a1920"></span>
## Sample Request


<Tabs>
<Tab zoneid="qtUP3cJeu3" title="Homepage recommendations">
<TabTitle>Homepage recommendations</TabTitle>

<span id="ce598f3b"></span>
### Home Page Recommendation

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/\${application_id}/\${scene_id}' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
      "user": {
        "_user_id": "user_199432"
      },
      "page_size": 10,
      "session_id": "GrrZCRhl",
      "filter": {
        "category": "shoes",
        "max_price": 100.5
      },
      "output_fields": ["item_count", "update_time","item_id"],
      "context": {
        "location": {
          "latitude": "+12.12",
          "longitude": "+012.12"
        }
      },
      "conditional_boost": [{
          "conds": [
            {
              "field": "brand",
              "op": "must",
              "conds": ["apple","samsung","huawei"]
            }
          ],
          "boost": 0.8
        }]
}'
```



</Tab>
<Tab zoneid="UZl9UuTQca" title="Detail Page Recommendation">
<TabTitle>Detail Page Recommendation</TabTitle>

<span id="04727fc9"></span>
### Details Page Recommendation

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/\${application_id}/\${scene_id}' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
      "user": {
        "_user_id": "user_199432"
      },
      "parent_items": [{
          "_id": "item_id_1002"
        }],
      "page_size": 10,
      "session_id": "GrrZCRhl",
      "filter": {
        "category": "shoes",
        "max_price": 100.5
      },
      "output_fields": ["item_count", "update_time","item_id"],
      "context": {
        "location": {
          "latitude": "+12.12",
          "longitude": "+012.12"
        }
      },
      "conditional_boost": [{
          "conds": [
            {
              "field": "brand",
              "op": "must",
              "conds": ["apple","samsung","huawei"]
            }
          ],
          "boost": 0.8
        }]
}'
```


<span id="a242d842"></span>
## 


</Tab>
</Tabs>


&nbsp;

<span id="36a75d27"></span>
## Sample Response

```JSON
{
    "request_id": "25ee998a-5462-9385-9f18-035f1da7a6e5",
    "result": {
        "rec_results": [
          {
            "_id": "688932914577129760",
            "display_fields": {
                 "item_count":  1234,
                 "update_time": 1752238692193,
                 "item_id": "item_1004"
            }
          },
          {
            "_id": "528424731470549718",
            "display_fields": {
                 "item_count":  1234,
                 "update_time": 1752238693295,
                 "item_id": "item_1003"
            }
          }
        ],
        "extra_info": {
            "forced_item_info": {
                "item_ids": ["60493","52937"],
                "skipped": false
            },
            "omitted_params": ["max_price"],
            "boost_status":["success"]
        }
    }
}        
```


&nbsp;

<span id="5644c8a7"></span>
# Error Handling

<span id="c7af5f2b"></span>
## Error Code

For this API's error codes, refer to [Common Error Codes](https://docs.byteplus.com/docs/viking-aisearch/Common_Error_Codes) documentation.
