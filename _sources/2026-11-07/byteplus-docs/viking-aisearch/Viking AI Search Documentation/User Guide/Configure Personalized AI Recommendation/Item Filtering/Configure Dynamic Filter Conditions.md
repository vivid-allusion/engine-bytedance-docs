---
title: "Configure Dynamic Filter Conditions"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Dynamic_recommendation_scope_configuration"
---

<span id="d16960e2"></span>
# Introduction

To allow your users to filter recommendation results in real\-time based on their immediate preferences, such as by brand or video type, you can use the dynamic filtering feature. This guide provides step\-by\-step instructions on how to configure dynamic filtering rules in the UI and then pass filter parameters in your API calls to deliver a more personalized and relevant user experience.

This also allows you to a single recommendation scenario to provide recommendation across multiple similar pages on your platform.

<span id="51ea5cd7"></span>
## Use Cases


|**Industry** |**Scenarios** |
|---|---|
|Video Platform |Filter by video type (Movies, TV Shows, Documentaries) or genre (e.g., North America, Asia) based on user selection. <br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/788cdac22b8e48b4854b479b5785c3bd) </span><br><br> |
|E\-Commerce |Filter by specific sub\-categories, by brand or price<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/42960b7af46d4c0f8ec318ec831d46ad) </span><br><br> |


<span id="1b2eff31"></span>
# Important Note

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>



1. <div data-tips="true" data-tips-type="warning">The platform does not perform mutual exclusion checks. Ensure the filtering logic is correct during configuration. If mutually exclusive conditions exist, the system returns empty results without reporting an error.</div>


2. <div data-tips="true" data-tips-type="warning">If an item is missing a specific field used in a filter, the system automatically ignores that filtering condition for that item. For more information, see <a href="https://docs.byteplus.com/docs/viking-aisearch/Static_Recommendation_Scope_Configuration#545109f8">Automatic Degradation</a>.</div>




---



<span id="55970b43"></span>
# Step 1: Create dynamic filters

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Dynamic filters and static filters can concurrently exist in the same filter rule.</div>



1. In the left navigation bar, select ** Scope** \> **Define Recommendable Items** to open the static recommendation scope configuration page


 &nbsp;

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/fb809e3b51954d9c8ae74167b39e77ce" width="500px" /></div>



&nbsp;

2. Click **Add Rule** and configure filter rules based on your business needs. Each filter rule supports condition groups to achieve compound logic, such as (A and B) or C, **with up to one level of nesting.** 



|**Configuration** |**Description** |
|---|---|
|Outer logical operator |In nested filters, it defines the top\-level logical relationship between condition groups (AND/OR). |
|Logical operator |Defines condition combination logic. AND requires all conditions to be met; OR requires any one condition to be met. |
|Filter field |Select an item field from the dropdown list. **Only fields marked as Filterable are supported.**  |
|Condition type |Select a matching rule, such as `found in`, `not found in`, or numerical range comparison. |
|Condition value |Enter the matching value. |



&nbsp;

3. Click on the gray "Dynamic Parameter" to configure a dynamic filter. Dynamic parameters act as "placeholders." You do not need to enter specific values here; the actual value is passed dynamically for each request. 

   **Names of dynamic parameters found in a filter rule must be unique. ** 

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">\*Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Values for the dynamic parameters must be passed in during the Recommend API request. We recommend ensuring that the dynamic parameter name is easy to understand.    </div>
   


&nbsp;

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/76a23af2b29e41a692f28f1156a3cda7" width="800px" /></div>




&nbsp;

4. If there exist conflicting names, the system will prompt you to rename the parameter. Rename the parameter by clicking the ** edit** icon and inputting the new name.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/86381b3fc271440f9be77832bcf5c231" width="800px" />   </div>
   



&nbsp;

5. Save rule configuration.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Dynamic filter configurations cannot be tested on the platform. </div>


<div data-tips="true" data-tips-type="default">To experience the filtering effects, you must deploy the rule to production and pass dynamic parameter values via the Recommend API </div>



&nbsp;

6. To test dynamic filtering, select the dynamic filter rule and click "Sync changes to API" to activate it. You can then test the feature by calling the API. 

   For more details on deploying configurations to production, refer to [Deploy Scenario](https://docs.byteplus.com/docs/viking-aisearch/Recommendation_Scene#36be5bc4).


&nbsp;

<span id="ba86e114"></span>
## Supported Operators


|**Operators / Data Type** |<div style="text-align: center"><br><strong>String</strong></div><br> |<div style="text-align: center"><br><strong>Integer</strong></div><br> |<div style="text-align: center"><br><strong>Float</strong></div><br> |<div style="text-align: center"><br><strong>Array<X\></strong></div><br> |<div style="text-align: center"><br><strong>Boolean</strong></div><br> |<div style="text-align: center"><br><strong>Publish time</strong></div><br> |<div style="text-align: center"><br><strong>Timestamp</strong></div><br> |<div style="text-align: center"><br><strong>Object</strong></div><br> |
|---|---|---|---|---|---|---|---|---|
|Contains (in) |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>Not suppotted</div><br> |
|Does not contain (not in) |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> ||
|In range |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>❌</div><br> |<div style="text-align: center"><br>❌</div><br> ||
|Less than / earlier than |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> ||
|Less than or equal to |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> ||
|Greater than / later than |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> ||
|Greater than or equal to |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> ||
|Equals |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> ||
|Not equal to |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> ||



---



<span id="49a9ca25"></span>
# Step 2: API request

Dynamic filtering depends on passing dynamic parameter values when calling the Recommend API. You must include the `filter` field in the request body to pass dynamic parameters.


* Dynamic filter conditions where values are not found in API requests will be automatically ignored. 

* Illegal parameters keys will be automatically ignored.


&nbsp;

When multiple dynamic parameters are configured, you can pass a parameter value for each item attribute in the request. 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">API Reference</div>


<div data-tips="true" data-tips-type="default">To learn how to pass parameter values in online requests to the Recommend API, refer to <a href="https://docs.byteplus.com/docs/viking-aisearch/Recommendation#db3f2d55">Filter</a>.</div>


&nbsp;

<span id="7890956d"></span>
## Sample API Request

Here is a complete example of sending a dynamic filtering request using cURL.

> In this sample, `brand` is the name of your configured dynamic parameter, and `selected_brand` is the actual brand value to filter.


```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/{scene_id}' \
-H 'Authorization: Bearer <YOUR_ACCESS_TOKEN>' \
-H 'Content-Type: application/json' \
-d '{
  "user_id": "12345",
  "scene": "homepage_feed",
  "filter": {
    "brand": "selected_brand"
  }
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Replace `<your_access_token\>` with your actual access token. For information on how to obtain it, see  <a href="https://docs.byteplus.com/docs/viking-aisearch/API_Authentication">API Authentication</a>.</div>


&nbsp;


---



<span id="fa9319b8"></span>
## Frequently asked questions

When illegal parameters are present, the platform will automatically gracefully degrade to limit the scope of impact, ensuring that item recommendations can be returned as much as possible. 

The detailed degradation logic is as follows:


|**Scenario** |**Degradation** **logic** |
|---|---|
|API request is missing dynamic parameters |Ignore affected dynamic filters. Other filters (static and dynamic) remain effective.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Example</div><br><br><br><div data-tips="true" data-tips-type="default">The platform is configured with the dynamic  filter rule (A IN B) AND (A NOT IN C) . Parameter B is not found in the API request. </div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>A in B</strong>: Dynamic filter condition does not take effect.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>A not in C</strong><strong>:</strong> Dynamic filter condition remains active and valid.</div><br> |
|Dynamic parameters present in API request but are missing values |Same as above |
|Retrieved item is missing fields |Filter conditions will **automatically ignore** related filters; see [Automatic Degradation](https://docs.byteplus.com/docs/viking-aisearch/Static_Recommendation_Scope_Configuration#545109f8) for details. |
