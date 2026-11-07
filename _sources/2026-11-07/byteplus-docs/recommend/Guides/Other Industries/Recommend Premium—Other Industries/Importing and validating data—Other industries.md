---
title: "Importing and validating data—Other industries"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-other_premium_importing_and_validating_data"
---

Users have to define their schema and import their data for the BytePlus Recommend team. After the data is imported, the BytePlus Recommend team will validate the data to ensure quality standards are met. BytePlus Recommend generates a data report so clients can get an overview of the quality of their imported data. With the imported data, we will be able to train the models to provide accurate and timely recommendation results.

There are five main steps to importing data:


|**Step** |**Description** |
|---|---|
|Prepare for data import |Based on their preferred import method, users must prepare for data import, such as by creating a storage path or reformatting data. |
|Import trial data |Users can import trial data to evaluate the quality of their data. A minimum of two weeks of data is needed for quality validation. |
|Import historical data |Users can import historical data for the model. This full\-bulk upload requires a minimum of two months of historical data but is best with a year or more. |
|Import incremental data |Users can import incremental data for real\-time data synchronization. |


<span id="Preparing for data import"></span>
# Preparing for data import

Prior to the actual data import, users need to format the data and/or configure the path according to their preferred import method. Users can import their data using one of the following methods:


* Google Cloud Service (GCS)

* Amazon S3

* API


<span id="Importing data through Google Cloud Service (GCS)"></span>
## Importing data through Google Cloud Service (GCS)

Users can import trial and historical data through GCS. For BytePlus to successfully access the data, the following must be completed:


* Store data in either .csv or .json format.

* Grant the BytePlus Recommend Team access to the Bucket.

* Name the Bucket URL and files according to our requirements.


**To import data through GCS:** 


1. Create a [GCS Service Account](https://cloud.google.com/iam/docs/creating-managing-service-accounts).

2. Create a Bucket for BytePlus Recommend.

3. Store the User data into one or multiple JSON file(s) and into the following directory path: *gs://{prefix}/{created_bucket}/User/{filename.json}* .

4. Store the Product data into one or multiple JSON file(s) and into the following directory path: *gs://{prefix}/{created_bucket}/Product/{filename.json}* .

5. Store the UserEvent Data into one or multiple JSON file(s).

6. Store the UserEvent JSON file(s) into the following directory: *gs://{prefix}/{created_bucket}/UserEvent*.

7. Assign the Storage Object Viewer Role to the created Service Account.

8. Generate the [JSON keyfile](https://cloud.google.com/iam/docs/creating-managing-service-account-keys#creating) and share it with BytePlus.


<span id="Importing data through Amazon S3"></span>
## Importing data through Amazon S3

Users can import trial and historical data through Amazon S3. For BytePlus to successfully access the data, the following must be completed:


* Store data in a bucket in either .csv or .json format.

* Grant the BytePlus Recommend Team access to the Bucket.

* Name the Bucket URL and files according to our requirements.


**To import data through Amazon S3:** 


1. Create an [AWS account](https://docs.aws.amazon.com/AmazonS3/latest/userguide/setting-up-s3.html).

2. Create a Bucket for BytePlus Recommend.

3. Store the User data into one or multiple JSON or CSV file(s) and into the following directory path: *s3://{prefix}/{created_bucket}/User/{filename.json or csv}* .

4. Store the Product data into one or multiple JSON or CSV file(s) and into the following directory path: *s3://{prefix}/{created_bucket}/Product/{filename.json or csv}* .

5. Store the UserEvent data into one or multiple JSON or CSV file(s).

6. Store the UserEvent JSON or CSV file(s) into the following directory: *s3://{prefix}/{created_bucket}/UserEvent*.

7. Generate an [AWS](https://docs.aws.amazon.com/workspaces-web/latest/adminguide/getting-started-iam-user-access-keys.html) AccessKey ID and SecretAccess Key.

8. Upload the data to BytePlus console.


<span id="Importing data through API"></span>
## Importing data through API

Users can import data through [WriteUsers](https://docs.byteplus.com/recommend/reference/retail_writeusers), [WriteProducts](https://docs.byteplus.com/recommend/reference/retail_writeproducts), and [WriteUserEvents](https://docs.byteplus.com/recommend/reference/retail_writeuserevents) APIs. The data schema of the data sent through the API must match the schema defined in BytePlus Recommend.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">These Curl commands simply provide a general idea of how a testing account appears when using code samples.</div>



* <div data-tips="true" data-tips-type="tip">For actual integrations, refer to our <a href="https://docs.byteplus.com/recommend/samples/retail_code_samples">Code samples</a>.</div>


* <div data-tips="true" data-tips-type="tip">For actual API integrations, use PROTO instead of JSON.</div>


* <div data-tips="true" data-tips-type="tip">Users need to specify the PROJECT_ID and STAGE in the data.</div>



**EXAMPLE**


<Tabs>
<Tab zoneid="bgTmDBYDQT" title="WriteUsers">
<TabTitle>WriteUsers</TabTitle>

```curl
curl --request POST 'rec-api-sg1.recplusapi.com/RetailSaaS/WriteUsers' \
     --header 'Request-Id: e92e0969-8250-4bb0-9f57-7c6366835b62' \
     --header 'Content-Type: application/json' \
     -d @request.json
```



</Tab>
<Tab zoneid="K8CdPUhnzz" title="WriteProducts">
<TabTitle>WriteProducts</TabTitle>

```curl
curl --request POST 'rec-api-sg1.recplusapi.com/RetailSaaS/WriteProducts' \
     --header 'Request-Id: e92e0969-8250-4bb0-9f57-7c6366835b63' \
     --header 'Content-Type: application/json' \
     --d @request.json
```



</Tab>
<Tab zoneid="wRUI5ol7iT" title="WriteUserEvents">
<TabTitle>WriteUserEvents</TabTitle>

```curl
curl --request POST 'rec-api-sg1.recplusapi.com/RetailSaaS/WriteUserEvents' \
     --header 'Request-Id: e92e0969-8250-4bb0-9f57-7c6366835b62' \
     --header 'Content-Type: application/json' \
     -d @request.json
```



</Tab>
</Tabs>


For more information on handling data, refer to [Effective and efficient data synchronization](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization).

<span id="Resource provisioning"></span>
## Resource provisioning

A fair amount of resources are required to build a customized recommendation system for all our users. Once an import method is chosen, users have to wait approximately 30 minutes for resource provisioning before they can import the data. A callout message will appear to notify users of the current stage in the process.

<span id="Data import format (GCS / S3)"></span>
## Data import format (GCS / S3)

This section outlines the required format for the data you want to import through GCS or S3.

<span id="User data import format"></span>
### User data import format

In this section, the term "user" refers to your end\-users. If you are using Curl, the User data entries in your JSON file should look like the following example:

**EXAMPLE**

```JSON
{
  "user_id":"1457789",
  "gender":"male",
  "age":"23",
  "tags":[
    "new user",
    "low purchasing power",
    "bargain seeker"
  ],
  "activation_channel":"AppStore",
  "membership_level":"silver",
  "registration_time":"1623593487",
  "location":{
    "country":"USA",
    "city":"Kirkland",
    "district_or_area":"King County",
    "postcode":"98033"
  },
  "extra":{
    "device_id":"9C287922-EE26-4501-94B5-DDE6F83E1475"
  }
}
```


For more information on detailed data schemas in PROTO format, refer to [API PROTO definitions](https://docs.byteplus.com/recommend/samples/retail_api_proto_definitions).

Users should be aware of the following when creating their user_id:


* Users can encrypt User.user_id, but this must remain consistent.

* Users need to find stable user identifiers.

* Users should not include any personal information like the user's real name, mobile number, or exact address.


<span id="Product data import format"></span>
### Product data import format

In this section, the term "products" refers to the items in your catalog. If you are using Curl, the Product data entries in your JSON file should look like the following example:

**EXAMPLE**

```JSON
{
  "product_id":"632461",
  "categories":[
    {
      "category_depth":1,
      "category_nodes":[
        {
          "id_or_name":"Shoes"
        }
      ]
    },
    {
      "category_depth":2,
      "category_nodes":[
        {
          "id_or_name":"Men's Shoes"
        }
      ]
    }
  ],
  "brands":[
    {
      "brand_depth":1,
      "id_or_name":"Adidas"
    },
    {
      "brand_depth":2,
      "id_or_name":"Yeezy"
    }
  ],
  "price":{
    "current_price":49900,
    "origin_price":69900
  },
  "is_recommendable":true,
  "title":"adidas Men's Yeezy Boost 350 V2 Grey/Borang/Dgsogr",
  "quality_score":4.4,
  "tags":[
    "New Product",
    "Summer Product"
  ],
  "display":{
    "listing_page_display_tags":[
      "best seller",
      "hot sales"
    ],
    "detail_page_display_tags":[
      "FreeShipping",
      "Return in 7 days without any reasons"
    ],
    "listing_page_display_type":"image",
    "cover_multimedia_url":"https://images-na.ssl-images-amazon.com/images/I/81WmojBxvbL._AC_UL1500_.jpg"
  },
  "product_spec":{
    "product_group_id":"1356",
    "user_rating":0.25,
    "comment_count":100,
    "source":"self",
    "publish_time":"1623193487"
  },
  "seller":{
    "id":"43485",
    "seller_level":"1",
    "seller_rating":3.5
  },
  "extra":{
    "count":"20",
    "color":"white",
    "material":"fabric"
  }
}
```


For more information on detailed schemas in PROTO format, refer to [API PROTO definitions](https://docs.byteplus.com/recommend/samples/retail_api_proto_definitions).

<span id="UserEvent data import format"></span>
### UserEvent data import format

In this section, the term "user event" refers to the interaction between your users and the products on your platform. You must send the user_id, product_id, event_type, and timestamp according to the UserEvent PROTO format stated in [API PROTO definitions](https://docs.byteplus.com/recommend/samples/retail_api_proto_definitions). Users must insert pre\-defined acceptable values for their event_type.

Below is an example of importing an event on the product detail page. This is only applicable to events on the product detail page, so sending the root_product_id in the context object is mandatory here. You do not have to set this field for all other events.

**EXAMPLE**

```JSON
{
  "user_events":[
    {
      "user_id":"1457789",
      "event_type":"click",
      "event_timestamp":1623681888,
      "scene":{
        "scene_name":"product detail page",
        "page_number":2,
        "offset":10
      },
      "product_id":"632461",
      "device":{
        "platform":"android",
        "os_type":"phone",
        "app_version":"9.2.0",
        "device_model":"huawei-mate30",
        "device_brand":"huawei",
        "os_version":"10",
        "browser_type":"chrome",
        "user_agent":"Mozilla/5.0 (Linux; Android 10; TAS-AN00; HMSCore 5.3.0.312) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.106 HuaweiBrowser/11.0.8.303 Mobile Safari/537.36",
        "network":"3g"
      },
      "context":{
        "query":"",
        "root_product_id":"441356"
      },
      "attribution_token":"eyJpc3MiOiJuaW5naGFvLm5ldCIsImV4cCI6IjE0Mzg5NTU0NDUiLCJuYW1lIjoid2FuZ2hhbyIsImFkbWluIjp0cnVlfQ",
      "rec_info":"CiRiMjYyYjM1YS0xOTk1LTQ5YmMtOGNkNS1mZTVmYTczN2FkNDASJAobcmVjZW50X2hvdF9jbGlja3NfcmV0cmlldmVyFQAAAAAYDxoKCgNjdHIdog58PBoKCgNjdnIdANK2OCIHMjcyNTgwMg==",
      "traffic_source":"self",
      "extra":{
        "session_id":"sess_89j9ifuqrbplk0rti2va2k1ha0",
        "request_id":"860ae3f6-7e4d-43a9-8699-114cbd72c287"
      }
    }
  ]
}
```


Below is an example of sending a search event under the query "black shirt".

**EXAMPLE**

```JSON
{
  "user_events":[
    {
      "user_id":"1457789",
      "event_type":"search",
      "event_timestamp":1624681900,
      "scene":{
        "scene_name":"main search",
        "page_number":1,
        "offset":5
      },
      "product_id":"",
      "device":{
        "platform":"android",
        "os_type":"phone",
        "app_version":"9.2.0",
        "device_model":"huawei-mate30",
        "device_brand":"huawei",
        "os_version":"10",
        "browser_type":"chrome",
        "user_agent":"Mozilla/5.0 (Linux; Android 10; TAS-AN00; HMSCore 5.3.0.312) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.106 HuaweiBrowser/11.0.8.303 Mobile Safari/537.36",
        "network":"3g"
      },
      "context":{
        "query":"black shirt",
        "root_product_id":""
      },
      "attribution_token":"",
      "rec_info":"",
      "traffic_source":"byteplus",
      "extra":{
        "session_id":"sess_90j9ifuqrbplk0fda2va2k1ga0",
        "request_id":"900ae3f6-7e4d-43a9-8699-114cbd72c288"
      }
    }
  ]
}
```


<span id="Importing Recommend Premium data—trial, historical, incremental"></span>
# Importing Recommend Premium data—trial, historical, incremental

During data import, users are required to import data in three different stages:


* Trial data

* Historical data

* Incremental data


The table below is an overview of the data requirements for the three stages:


|**Stage** |**Trial Data** |**Historical Data** |**Incremental Data** |
|---|---|---|---|
|**Process** |Imports up to two weeks' worth of data. |Imports full historical data (one year and above). |Imports incremental data as close to real\-time as possible. |
|**Data Type** |User, Product, and UserEvent |User, Product, and UserEvent |User, Product, and UserEvent |
|**Frequency** |Once |Once |Real\-time / batch |
|**Import Method** |1. API<br><br>2. GCS<br><br>3. Amazon S3 |1. API<br><br>2. GCS<br><br>3. Amazon S3 |API only |


<span id="Importing trial data to Recommend Premium"></span>
## Importing trial data to Recommend Premium

After users have defined the data schema in the BytePlus Recommend console, they can start importing their trial data. We recommend uploading a small portion of the data set as trial data first. This allows users to better understand and evaluate the quality of their data before committing to the entire historical and incremental data import cycle which can take up to several days. The imported trial data will not be used for model training, and instead provides an opportunity to identify any errors.

Users must provide at least one day's worth of all User and Product data, and UserEvent data spanning at least 1.5 times the attribution window. For instance, if an attribution window is 7 days, users should upload about 11 days of UserEvent data.

<span id="Importing historical data to Recommend Premium"></span>
## Importing historical data to Recommend Premium

After the trial data has been imported in BytePlus Recommend, users can start importing their historical data.

Users have to upload data according to the following requirements:


* Consolidation of all historical User and Product Data

* Ideally the past year of UserEvent data (or minimally 2 months)

* Upload through GCS, S3, or API


**EXAMPLE**

Assuming that the current time is 2021/05/01 14:00:00 UTC, users should import the following data:


* User: consolidated data until 2021/04/30

* Product: consolidated data until 2021/04/30

* UserEvent: Event history from 2020/05/01 to 2021/04/30


<span id="Importing incremental data to Recommend Premium"></span>
## Importing incremental data to Recommend Premium

Users can only import incremental data after creating a model.

To get the most up\-to\-date recommendation, users should update their incremental data through the WriteUsers, WriteProducts, and WriteUserEvents APIs according to the following requirements:


* User: Real\-time or batch upload.

* Product: Real\-time or batch upload.

* UserEvent: As real\-time as possible.


**EXAMPLE**

Assuming that the current time is 2021/05/01 14:00:00 UTC, users should import the following data:


* User: real\-time data updates from 2021/05/01 14:00:00 UTC

* Product: real\-time data updates from 2021/05/01 14:00:00 UTC

* UserEvent: real\-time data updates from 2021/05/01 14:00:00 UTC


<span id="Data validation metrics"></span>
# Data validation metrics

This section details our team's metrics to determine whether there are possible issues with users' imported data.


|**Issues** |**Description** |
|---|---|
|Data volume |Data volume might be low.<br><br>Data volume sent and received might be different. |
|Duplication rate |Possibility of a high number of duplicated values. |
|Null/Missing/Abnormal value |Determines whether their occurrence is too frequent. |
|Join rate |The following types of connecting data rates are possible:<br><br><br>* UserEvent to User<br><br>   For example, you may want to check if the user_id in UserEvent can be found in the User table.<br><br>* UserEvent to Product<br><br>   For example, to check if the product_id in UserEvent can be found in the Product table.<br><br>* UserEvent to UserEvent<br><br>   For example, with the click\-to\-Impression Join Rate and Conversion\-to\-Click Join Rate, you can check if the relevant preceding events with the specific user_id and product_id can be found inside the UserEvent table. |
|Attribution rate |Verify whether the optimization metrics are aligned. |
|Event Tracking Test (Optional) |Verify whether UserEvents are logged properly (only applicable to incremental data). |


Misaligned metrics are common with BytePlus. We recommend the following steps to troubleshoot them:


|**Misaligned metric** |**Description** |**Troubleshooting** |
|---|---|---|
|Different sources for computation |You might normally use your own data storage to compute the metrics, but BytePlus Recommend uses the received data. |Make sure the data you send to the BytePlus Recommend team best represents the data in your storage system. |
|Different computation logic |For example, you might define a total order as a purchase event, while BytePlus Recommend does this with single products. |These discrepancies can be addressed by scheduling a meeting with the BytePlus Recommend team to ensure the metrics are aligned before model training starts. |
|Data loss during transmission |*  |Both parties should check the volume of data, statistics, and other areas to ensure there are no data transmission issues. |
|Other misalignments |*  |Contact the BytePlus Recommend team. |
