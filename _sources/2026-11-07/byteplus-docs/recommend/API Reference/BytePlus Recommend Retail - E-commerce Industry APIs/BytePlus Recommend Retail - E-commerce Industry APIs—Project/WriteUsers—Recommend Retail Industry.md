---
title: "WriteUsers—Recommend Retail Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-retail_writeusers"
---

The WriteUsers API, specifically designed for Recommend in the Retail/E\-commerce industry, allows you to efficiently upload new user data or update existing user information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on BytePlus Recommend token authentication, refer <a href="https://docs.byteplus.com/en/recommend/reference/api_token_authentication">here</a>.</div>


<span id="a1abe13f"></span>
# Limitations

The following requirements are applicable to WriteUsers API:


* Each request can upload a maximum of 2,000 user data records at a time. If you upload more than 2,000 user data records in a single request, you will encounter a rejection.

* The result obtained by multiplying QPS by the number of uploads per request must be less than 30,000.


<span id="36c7c3c1"></span>
# HTTP request


|**URL** |https://rec\-ap\-singapore\-1.byteplusapi.com/data/api/retail/${tenant}/user |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The following topics provide detailed information on the parameters required for the WriteUsers API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Not all request parameters are included in the following table. For a complete list, refer to <a href="https://docs.byteplus.com/recommend/reference/api_token_authentication">HTTP header parameters</a>.</div>


<span id="144f0eac"></span>
## Query

The following table details the query parameters required for the WriteUsers API:


|**Query String Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|method |String |Yes |Write |*  |


<span id="1dad2339"></span>
## Body

The following table details the body parameters required for the WriteUsers API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|users |Array of Objects |Yes |*  |This is a list of user data intended for upload on the platform. The user list can contain a maximum of 100 entries. Exceeding this limit will result in a standard 400 error being returned. |
|extra |Object |No |*  |This field is used to pack key\-value pairs. For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization) . |


<span id="3af2abb4"></span>
### Users

The field represents a list of user data to be uploaded onto the platform. The maximum allowed number of entries for the user list is 2000. If this quota is exceeded, a standard 400 error will be returned. The list comprises the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|user_id |String |Yes |1457789 |The unique identifier for the user. The user_id must remain consistent when used in other data imports like UserEvents or Predict.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you plan to encrypt the user_id and substitute it with a hashed value, ensure that you use the identical encrypted value in other parameters.</div><br><br><br>In cases where users frequently log in and log out of the web or mobile application, inconsistent IDs for the same user may arise. To ensure consistency, we recommend utilizing the device_ID or member_ID instead. For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|gender |String |No |Male |The user's gender. The accepted values are:<br><br><br>* Male<br><br>* Female<br><br>* Other |
|age |String |No |23 |The user's age. The accepted values can be an estimated value or a range. |
|tags |Array of Strings |No |new users |The tags for the user. You should include as many tags as possible for the user, even if it has low coverage or might be inaccurate. The accepted values include:<br><br><br>* new users<br><br>* low purchasing power<br><br>* bargain seeker<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|activation_channel |String |No |AppStore |The channel where the user was acquired.<br><br>The accepted values include:<br><br><br>* AppStore<br><br>* GoogleAds<br><br>* FacebookAds<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|membership_level |String |No |silver |The user's membership level.<br><br>The accepted values include:<br><br><br>* silver<br><br>* elite<br><br>* 4<br><br>* 5<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|registration_timestamp |Int64 |No |1623593487 |The timestamp when the user registered or activated an account. |
|location |Object |No |*  |The user's location information. |
|location_country |String |No |USA |The user's country. The accepted values include:<br><br><br>* USA<br><br>* UK<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|location_city |String |No |Kirkland |The user's city. The accepted values include:<br><br><br>* San Jose<br><br>* Chicago<br><br>* NYC<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|location_district_or_area |String |No |King County |The user's district or area. The accepted values include:<br><br><br>* King County<br><br>* Santa Monica County<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|location_postcode |String |No |98033 |The user's postal code.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Not all countries use or require a postal code.</div><br> |
|extra |Object |No |*  |This field is used to pack key\-value pairs. For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |


<span id="e5aec494"></span>
### Extra

This field is used to pack key\-value pairs. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|newKey |String |*  |*  |*  |
|New Value |String |*  |*  |*  |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the WriteUsers API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |This field defines an error model. It contains two types of data: error code and error message. |
|errors |Array of Objects |*  |This field is populated when the status is an error code: 1001. |


<span id="f5baba9e"></span>
## **Status**

The `status` defines an error model. Each `status` message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful or not. The accepted values include:<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |


<span id="8a5ba3c8"></span>
# Samples

The following section details the sample codes for the WriteUsers API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON

curl --request POST \
     --url 'https://rec-ap-singapore-1.byteplusapi.com/data/api/retail/retail_demo/user?method=write' \
     --header 'Accept: application/json' \
     --header 'Content-Type: application/json' \
     --header 'Request-Id:12313208' \
     --header 'Tenant-Id:d7c5963593798b5263858b028f589' \
     --header 'Tenant-Nonce:1683628296' \
     --header 'Tenant-Ts:1683628296' \
     --header 'Tenant-Signature:81de52fa785b6552a2d3cca5382e62f7abb5829c3c7a3458f73cc303a701af64' \
     --data '{
     "users": [
          {
               "tags": [
                    "new user",
                    "low purchasing power",
                    "bargain seeker"
               ],
               "location": {
                    "city": "Kirkland",
                    "country": "USA",
                    "district_or_area": "King County",
                    "postcode": "98033"
               },
               "user_id": "1457789",
               "gender": "male",
               "age": "18-25",
               "activation_channel": "AppStore",
               "membership_level": "silver",
               "registration_timestamp": 1623593487,
               "extra": {
                    "user_name": "demo"
               }
          },
          {
               "tags": [
                    "new user"
               ],
               "location": {
                    "city": "Kirkland",
                    "country": "USA",
                    "district_or_area": "King County",
                    "postcode": "98033"
               },
               "user_id": "1457790",
               "gender": "female",
               "age": "25",
               "activation_channel": "AppStore",
               "membership_level": "silver",
               "registration_timestamp": 1623593499,
               "extra": {
                    "user_name": "demo2"
               }
          }
     ],
     "extra": {
          "additionalProp": "additionalVal"
     }
}'
```


<span id="de55caff"></span>
## Sample response

The following is a **successful** sample response.

```JSON
{ 
  "status": { 
    "message": "OK", 
    "success": true 
  }
}
```


The following is a **failed** sample response.

```JSON
{ 
  "status": { 
    "code": 400, 
    "message": "data is empty; errID:840491090 logID:2023040410191442531CEBDBB7FC46D5F4" 
  } 
}
```


The following is **failed** sample response if the data entries exceed 2,000.

```JSON
{
  "status": {
    "code": 413,
    "message": "The count of write items max to 2000; errID:840491090 logID:2023032311430332A733A4EA5CBF7B0926"
  }
}
```


The following is a **failed** sample response if the data is incomplete or inaccurate.

```JSON
{
  "status": {
    "code": 1001,
    "message": "Occur error, partial or all data handle fail"
  },
  "errors": [
    {
      "message": "in the 'gender' field, an unexpected value 'unknown' is included, only '[male female other]' can be accepted",
      "user": {
        "user_id": "1457789",
        "gender": "unknown",
        "age": "18-25",
        "tags": [
          "new user",
          "low purchasing power",
          "bargain seeker"
        ],
        "activation_channel": "AppStore",
        "membership_level": "silver",
        "registration_timestamp": "1623593487",
        "location": {
          "country": "USA",
          "city": "Kirkland",
          "district_or_area": "King County",
          "postcode": "98033"
        },
        "extra": {
          "user_name": "demo"
        }
      }
    }
  ]
}
```


<span id="9398e94b"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).
