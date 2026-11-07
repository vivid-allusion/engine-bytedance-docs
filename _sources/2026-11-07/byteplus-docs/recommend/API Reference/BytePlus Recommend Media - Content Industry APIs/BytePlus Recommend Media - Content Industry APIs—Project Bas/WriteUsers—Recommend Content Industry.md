---
title: "WriteUsers—Recommend Content Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-content_writeusers"
---

The WriteUsers API for BytePlus Recommend facilitates the uploading of new user data or updating existing user data in the Media/Content industry.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on BytePlus Recommend token authentication, refer <a href="https://docs.byteplus.com/en/recommend/reference/api_token_authentication">here</a>.</div>


<span id="58e88dac"></span>
# Limitations

The following limitations apply to WriteUsers API:


* Each request can upload no more than 2,000 user data records at a time. If you upload more than 2,000 user data records in a single request, you will encounter a rejection.

* The result obtained by multiplying QPS by the number of uploads per request must be less than 30,000.


<span id="36c7c3c1"></span>
# HTTP request

This is the URL and HTTP request method for the WriteUsers API.


|**URL** |https://rec\-us\-east\-1.byteplusapi.com/data/api/media/${tenant}/user |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the WriteUsers API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Not all request parameters are included in the following table. For a complete list, refer to <a href="https://docs.byteplus.com/recommend/reference/api_token_authentication">HTTP header parameters</a>.</div>


<span id="a40418e6"></span>
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
|user_id |String |Yes |1457789 |The unique user identifier. The user_id must remain consistent when used in other data imports like UserEvents or Predict.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you want to encrypt the user_id and use the hashed value instead, ensure that the same value is used in other parameters.</div><br><br><br>If users often log in and log out of the web or mobile application, you might get inconsistent IDs for the same user. To ensure consistency, we recommend using the device_ID or member_ID.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|gender |String |No |Male |The gender of a user. The accepted values are:<br><br><br>* Male<br><br>* Female<br><br>* Other |
|age |String |No |18\-25 |The age of a user. The accepted values can be an estimated value or a range. |
|tags |Array of Strings |No |new users, high purchasing power |The tags for a user. You should include as many tags as possible for the user, even if it has low coverage or might be inaccurate.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|device_id |String |No |abc123, 1 |The user's most used device's ID. |
|device_type |String |No |app |The user's most used device type. The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|subscriber_type |String |No |free |The subscription plan the user is on. The accepted values are:<br><br><br>* free<br><br>* paid<br><br>* other |
|language |String |No |English |The user's primary language. |
|view_history |String |No |123, 124 |The content consumed by the user. |
|activation_channel |String |No |AppStore |The channel where the user was acquired.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|membership_level |String |No |silver |The user's membership level.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|registration_timestamp |Int64 |No |1623593487 |The timestamp when the user registered and their account was activated. |
|country |String |No |USA |The user's country.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|city |String |No |San Jose |The user's city.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|district_or_area |String |No |Santa Monica County |The user's district or area.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|postcode |String |No |98033 |The user's postal code.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Not all countries use or require a postal code.</div><br> |
|extra |Object |No |*  |A field for additional information. You should provide as much information as possible by using this field. |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the WriteUsers API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |The `status` defines an error model. Each `status` message contains two types of data: error code and error message. |
|errors |Array of Objects |*  |This field is populated when the `status`is an error code: 1001. |


<span id="57d9bc60"></span>
## **Status**

The `status` defines an error model. Each `status` message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful or not.<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |


<span id="103325ea"></span>
### **User**

The user proto details. It contains the following fields:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|user_id |String |1457789 |The unique user identifier. The user_id must remain consistent when used in other data imports like UserEvents or Predict.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you want to encrypt the user_id and use the hashed value instead, ensure that the same value is used in other parameters.</div><br><br><br>If users often log in and log out of the web or mobile application, you might get inconsistent IDs for the same user. To ensure consistency, we recommend using the device_ID or member_ID.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|gender |String |Male |The gender of a user. The accepted values are:<br><br><br>* Male<br><br>* Female<br><br>* Other |
|age |String |18\-25 |The age of a user. The accepted values can be an estimated value or a range. |
|tags |Array of Strings |new users, high purchasing power |The tags for a user. You should include as many tags as possible for the user, even if it has low coverage or might be inaccurate.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|device_id |String |abc123, 1 |The user's most used device's ID. |
|device_type |String |app |The user's most used device type. The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|subscriber_type |String |free |The subscription plan the user is on. The accepted values are:<br><br><br>* free<br><br>* paid<br><br>* other |
|language |String |English |The user's primary language. |
|view_history |String |123, 124 |The content consumed by the user. |
|activation_channel |String |AppStore |The channel where the user was acquired.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|membership_level |String |silver |The user's membership level.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|registration_timestamp |Int64 |1623593487 |The timestamp when the user registered and their account was activated. |
|country |String |USA |The user's country.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|city |String |San Jose |The user's city.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|district_or_area |String |Santa Monica County |The user's district or area.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|postcode |String |98033 |The user's postal code.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Not all countries use or require a postal code.</div><br> |
|extra |Object |*  |A field for additional information. You should provide as much information as possible by using this field. |


<span id="ed90ff97"></span>
# Samples

The following section details the sample codes for the WriteUsers API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url 'https://rec-us-east-1.byteplusapi.com/data/api/media/media_demo/user?method=write' \
     --header 'Accept: application/json' \
     --header 'Content-Type: application/json' \
     --header 'Request-Id:12313208' \
     --header 'Tenant-Id:d7c5963593798b5263858b028f589' \
     --header 'Tenant-Nonce:1683633812' \
     --header 'Tenant-Ts:1683633812' \
     --header 'Tenant-Signature:8ef90c193048fb6d392c33fa848484a05338d446403075d98bd5006b36f247eb' \
     --data '{
     "users": [
          {
               "user_id": "1457789",
               "gender": "male",
               "age": "18-25",
               "tags": ["new user", "low purchasing power"],
               "device_id": "abc123",
               "device_type": "app",
               "subscriber_type": "free",
               "language": "English",
               "view_history": ["632461", "632462", "632463"],
               "activation_channel": "AppStore",
               "membership_level": "silver",
               "registration_timestamp": 1647570563,
               "country": "USA",
               "city": "Kirkland",
               "district_or_area": "King County",
               "postcode": "98033",
               "extra": {
                   "username": "demo"
               }
          },
          {
               "user_id": "1457799",
               "gender": "female",
               "age": "20",
               "tags": ["new user"],
               "device_id": "abc222",
               "device_type": "app",
               "subscriber_type": "paid",
               "language": "Chinese",
               "view_history": ["632461", "632462", "632463", "632464"],
               "activation_channel": "AppStore",
               "membership_level": "silver",
               "registration_timestamp": 1647570563,
               "country": "China",
               "city": "Beijin",
               "district_or_area": "HaiDian",
               "postcode": "014030",
               "extra": {
                   "username": "demo2"
               }
          }
     ],
     "extra": {
         "extra_key": "extra_value"
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


The following is **failed** sample response if the data entries exceed 2000.

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
        "user_id": "1457779",
        "gender": "unknown",
        "age": "18-25",
        "tags": [
          "new user",
          "low purchasing power"
        ],
        "device_id": "abc123",
        "device_type": "app",
        "subscriber_type": "free",
        "language": "English",
        "view_history": [
          "632461",
          "632462"
        ],
        "activation_channel": "AppStore",
        "membership_level": "silver",
        "registration_timestamp": "1623593487",
        "country": "USA",
        "city": "Kirkland",
        "district_or_area": "King County",
        "postcode": "98033",
        "extra": {
          "extra_key1": "extra_value1"
        }
      }
    }
  ]
}
```


<span id="9398e94b"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).
