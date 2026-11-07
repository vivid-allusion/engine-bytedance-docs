---
title: "Voice Replication Management APIs"
product: "Seed Speech"
product_code: "byteplusvoice"
source: "https://docs.byteplus.com/en/docs/byteplusvoice/voicereplicationopenapi"
---

<span id="ERQWhBd4"></span>
# Overview

The following Byteplus Open API interfaces can be used to batch purchase, renew, or query sound replicas (Speaker_IDs), supporting large\-scale automated voice replication training and querying workflows. These APIs help streamline operations such as voice asset management, renewal, and resource allocation for customized voice synthesis.

<span id="ukJdWe8K"></span>
# Integration Guide


1. Detailed descirption of Byteplus OpenAPI can be found [here](https://docs.byteplus.com/zh-CN/docs/byteplus-platform/reference-common-parameters). The service address of BytePlus OpenAPI is: [open.byteplusapi.com](http://open.byteplusapi.com/)

2. Fixed Common Parameters:


```Python
Service = "speech_saas_prod"
Version = "2023-11-07"
Region = "ap-southeast-1"
```



3. Obtain the pair of AccessKey (AK) and secret AccessKey (SK) following this [guide](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). 

4. Invoke methods:

   1. SDK following this [guide](https://docs.byteplus.com/ja/docs/byteplus-platform/reference-how-to-calculate-a-signature) 

   2. Create a signature directly following this [guide](https://docs.byteplus.com/en/docs/byteplus-platform/reference-example)


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">Sample demos for both methods are provided at the end of this document. For additional examples in various programming languages, please refer to the <a href="https://github.com/byteplus-sdk?q=&type=all&language=&sort=">BytePlus GitHub repository</a>.</div>



5. Error code

   1. HTTP response codes not starting with 2xx are considered errors.

   2. The structure of an erroneous HTTP response is as follows:


```JSON
{
    "ResponseMetadata": 
    {
        "RequestId": "20220214145719010211209131054BC103", // "X-Top-Request-Id" param from the header
        "Action": "ListMegaTTSTrainStatus",
        "Version": "2023-11-07",
        "Service": "{Service}",// "X-Top-Service" param from the header
        "Region": "{Region}", // "X-Top-Region" param from the header
        "Error": 
        {
            "Code": "InternalError.NotCaptured",
            "Message": "xxx"
        }
    }
}
```



   3. The client can use the `"ResponseMetadata.Error.Code"` field to determine the type of error. The known types and their meanings are as follows:

      
      |**Code** |**Description** |
      |---|---|
      |OperationDenied.InvalidSpeakerID |The account or AppID does not have permission to perform the operation or cannot operate on one or more instances in the SpeakerID list. |
      |OperationDenied.InvalidParameter |The request body contains invalid fields (missing required fields, incorrect types, etc.). |
      |InternalError.NotCaptured |Unknown internal server error. |
      


<span id="SKUsJ3B2"></span>
## 

<span id="SKUsJ3B2"></span>
## API list

<span id="rjUj4um7"></span>
### Query SpeakerID Status Information `ListMegaTTSTrainStatus`


* **Interface Description**: Query the status information of purchased timbres, supporting filtering by SpeakerIDs and State. If the query conditions are empty, return all lists under the account's AppID or Project (if there are more than 1000 timbres, it is strongly recommended to use the pagination interface `BatchListMegaTTSTrainStatus`).

* **Request Method**: `POST`

* **Request Parameters**:



|**Parameter** |**Type** |**Required** |**Argument Type** |**Description** |
|---|---|---|---|---|
|Content\-Type |string |Y |header |Fixed string: `application/json; charset=utf-8` |
|Action |string |Y |query |ListMegaTTSTrainStatus |
|Version |string |Y |query |2023\-11\-07 |
|ProjectName |string |Y |body |Project name from the new console |
|SpeakerIDs |[]string |N |body |List of SpeakerIDs. <br><br>If ignoring SpeakerIDs to query data, it is strongly recommended to use the pagination interface: `BatchListMegaTTSTrainStatus` |
|State |string |N |body |Timbre status, supported values: <br><br><br>* Unknown<br><br>* Training<br><br>* Success<br><br>* Active<br><br>* Expired<br><br>* Reclaimed<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">See Appendix: State Enumeration Values</div><br> |
|OrderTimeStart |int64 |N |body |The upper bound for order time retrieval is a millisecond\-level timestamp. Due to instance delivery speed, it may be later than the actual payment completion time. |
|OrderTimeEnd |int64 |N |body |The lower bound for order time retrieval is a millisecond\-level timestamp. Due to instance delivery speed, it may be later than the actual payment completion time. |
|ExpireTimeStart |int64 |N |body |The upper bound for instance expiration time retrieval is a millisecond\-level timestamp. |
|ExpireTimeEnd |int64 |N |body |The lower bound for instance expiration time retrieval is a millisecond\-level timestamp. |



* **Return Data**:


```JSON
{
  "ResponseMetadata": {
    "RequestId": "20220214145719010211209131054BC103", // X-Top-Request-Id parameter in header
    "Action": "",
    "Version": "",
    "Service": "{Service}", // X-Top-Service parameter in header
    "Region": "{Region}" // X-Top-Region parameter in header
  },
  "Result": {
    "Statuses": [
      // Empty Slot Response Example
      {
        "SpeakerID": "S_9uxxxx72", // speakerID
        "InstanceNO": "Model_storage_xSV1Pll1xNLXkOCS",
        "InstanceStatus": "active",
        "IsActivatable": false,
        "State": "Unknown", // Status of speakerID
        "DemoAudio": null,
        "Version": null,
        "CreateTime": 0,
        "ExpireTime": 0, // The voice slots have been upgraded. No voice storage fees will be charged, and the voice slots will not expire.
        "OrderTime": 1782810654000, // Order time, unit: ms
        "Alias": "",
        "AvailableTrainingTimes": 15, // Remaining training times, 0 for activated SpeakerID
        "ResourceID": "seed-icl-2.0", // The voice slots for ICL 1.0 and ICL 2.0 have been unified. This field only indicates the product version associated with the slot purchase and does not affect the actual training performance.
        "Avatar": "",
        "Labels": null,
        "Description": "",
        "ModelTypeDetails": null,
        "CloneSource": 0,
        "EnableFormalized": false
      },
      // Trained Slot Response Example
      {
        "SpeakerID": "S_VIxxxx72",
        "InstanceNO": "Model_storage_ygVDaith0LR9tybY",
        "InstanceStatus": "active",
        "IsActivatable": true,
        "State": "Success",
        "DemoAudio": "https://sf16-vxxxx3EE%3D",
        "Version": "V1", // Number of training times for speakerID
        "CreateTime": 1783935649000,
        "ExpireTime": 0, // The voice slots have been upgraded. No voice storage fees will be charged, and the voice slots will not expire.
        "OrderTime": 1782810715000,
        "Alias": "",
        "AvailableTrainingTimes": 14, // Remaining training times, 0 for activated SpeakerID
        "ResourceID": "seed-icl-2.0", // The voice slots for ICL 1.0 and ICL 2.0 have been unified. This field only indicates the product version associated with the slot purchase and does not affect the actual training performance.
        "Avatar": "",
        "Labels": null,
        "Description": "",
        "ModelTypeDetails": [
          {
            "ModelType": 5,
            "DemoAudio": "https://sf19-vxxxx",
            "IclSpeakerId": "ICL_uranus_6a54b29d4645c125",
            "ResourceID": "seed-icl-2.0", // Use this resourceID when calling TTS endpoints.
            "SupportedModels": [
              {
                "Model": "seed-tts-2.0-standard",
                "SupportedLanguages": [
                  "zh-cn", "en", "ja", "es-mx", "id", "pt", "de", "fr",
                  "ko", "pt-br", "ar", "fil", "ms", "ru", "th", "vi",
                  "it", "pl", "sv", "tr"
                ]
              },
              {
                "Model": "seed-tts-2.0-omni",
                "SupportedLanguages": [
                  "es-mx"
                ]
              }
            ]
          }
        ],
        "CloneSource": 0,
        "EnableFormalized": false
      }
    ]
  }
}
```


&nbsp;

<span id="3kOHp7Bw"></span>
### Pagination Query for SpeakerID Status `BatchListMegaTTSTrainStatus`


* **Interface Description:**  Query the status of purchased timbres; compared with `ListMegaTTSTrainStatus`, it adds pagination\-related parameters and returns; supports two pagination methods: using token and declaring page number; among them, 

   * the pagination token is empty on the last page

   * the pagination token is encrypted with a private key

   * the pagination interface is a new interface and does not affect the behavior of existing interfaces.

* **Request Method:**  `POST`

* **Request Parameters:** 



|**Parameter** |**Type** |**Required** |**Argument type** |**Description** |
|---|---|---|---|---|
|Content\-Type |string |Y |header |Fixed string: `application/json; charset=utf-8` |
|Action |string |Y |query |BatchListMegaTTSTrainStatus |
|Version |string |Y |query |2023\-11\-07 |
|ProjectName |string |Y |body |Project name from the new console |
|SpeakerIDs |string |N |body |SpeakerID list; passing empty value returns all SpeakerIDs under the specified AppID or Project |
|State |string |N |body |Timbre status, supported values: <br><br><br>* Unknown<br><br>* Training<br><br>* Success<br><br>* Active<br><br>* Expired<br><br>* Reclaimed<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">See Appendix: State Enumeration Values</div><br> |
|PageNumber |int |N |body |Page number, must be greater than 0, default is 1 |
|PageSize |int |N |body |Number of items per page, must be in [1, 100], default is 10 |
|NextToken |string |N |body |String returned by the last request; if not empty, it will override the values of PageNumber and PageSize |
|MaxResults |int |N |body |Cooperates with NextToken to control the maximum number of returned results; if not empty, it must be in [1, 100], default is 10 |
|OrderTimeStart |int64 |N |body |The upper bound for order time retrieval is a millisecond\-level timestamp. Due to instance delivery speed, it may be later than the actual payment completion time. |
|OrderTimeEnd |int64 |N |body |The lower bound for order time retrieval is a millisecond\-level timestamp. Due to instance delivery speed, it may be later than the actual payment completion time. |
|ExpireTimeStart |int64 |N |body |The upper bound for instance expiration time retrieval is a millisecond\-level timestamp. |
|ExpireTimeEnd |int64 |N |body |The lower bound for instance expiration time retrieval is a millisecond\-level timestamp. |



* **Return Data:** 


```JSON
{
    "ResponseMetadata": 
    {
        "RequestId": "20220214145719010211209131054BC103", // X-Top-Request-Id parameter in header
        "Action": "BatchListMegaTTSTrainStatus",
        "Version": "2023-11-07",
        "Service": "{Service}",// X-Top-Service parameter in header
        "Region": "{Region}" // X-Top-Region parameter in header
    },
    "Result":
    {
        "AppID": "xxx",
        "TotalCount": 2, // Total number of speakerIDs
        "NextToken": "", // NextToken string, which can be used to send requests for subsequent results; empty if no more results
        "PageNumber": 1, // Current page number when using pagination parameters
        "PageSize": 2, // Number of items included in the current page when using pagination parameters
        "Statuses": 
        [
    {
        "SpeakerID": "S_9uxxxx72", // speakerID
        "InstanceNO": "Model_storage_xSV1Pll1xNLXkOCS",
        "InstanceStatus": "active",
        "IsActivatable": false,
        "State": "Unknown", // Status of speakerID
        "DemoAudio": null,
        "Version": null,
        "CreateTime": 0,
        "ExpireTime": 0, // The voice slots have been upgraded. No voice storage fees will be charged, and the voice slots will not expire.
        "OrderTime": 1782810654000, // Order time, unit: ms
        "Alias": "",
        "AvailableTrainingTimes": 15, // Remaining training times, 0 for activated SpeakerID
        "ResourceID": "seed-icl-2.0", // The voice slots for ICL 1.0 and ICL 2.0 have been unified. This field only indicates the product version associated with the slot purchase and does not affect the actual training performance.
        "Avatar": "",
        "Labels": null,
        "Description": "",
        "ModelTypeDetails": null,
        "CloneSource": 0,
        "EnableFormalized": false
      },
        ]
    }
}

```


<span id="qJdoWUGg"></span>
### Voice Order Placement `OrderAccessResourcePacks`


* **Interface Description**: Place an order for SpeakerIDs and pay for it in one step. 

   **Prerequisites: ** 

   * The AppID has enabled voice cloning; 

   * The account has sufficient balance (or vouchers) to automatically pay for the order. 

   * Frequency limit: A maximum of 2000 voices can be ordered within 2 minutes.

* **Request Method**: `POST`

* **Request Parameters**:



|**Parameter** |**Type** |**Required** |**Argument Type** |**Description** |
|---|---|---|---|---|
|Content\-Type |string |Y |header |Fixed string: `application/json; charset=utf-8` |
|Action |string |Y |query |OrderAccessResourcePacks |
|Version |string |Y |query |2023\-11\-07 |
|ProjectName |string |Y |body |Project name from the new console |
|ResourceID |string |Y |body |Platform's service type resource identifier, required:<br><br> `volc.seedicl.voiceclone` |
|Code |string |Y |body |Platform's billing item identifier, required and unique: `Model_storage` |
|Times |int |Y |body |Duration for ordering a single timbre, in months |
|Quantity |int |Y |body |Number of timbres to order, <br><br>e.g.100 means purchasing 100 timbres |
|AutoUseCoupon |bool |N |body |Whether to automatically use vouchers |
|CouponID |string |N |body |Voucher ID, obtained through Voucher Management |
|ResourceTag |object |N |body |Project & tag bill configuration |
|ResourceTag.CustomTags |string |N |body |Tags, obtained through Tag Management |
|ResourceTag.ProjectName |string |N |body |Project name, obtained through Project Management |



* **Request Example**:


```Python
{
    # "AppID": "100000000", #Use this appID if the legacy console is being used. 
    # "ResourceID": "volc.megatts.voiceclone", #Use this resource ID if only Voice Repilication 1.0 was enabled. 
    "ProjectName": "default",
    "ResourceID": "volc.seedicl.voiceclone",
    "Code": "Model_storage",
    "Times": 12,
    "Quantity": 2000
}
```



* **Return Data**:


```JSON
{
    "ResponseMetadata": 
    {
        "RequestId": "20220214145719010211209131054BC103", // X-Top-Request-Id parameter in header
        "Action": "OrderAccessResourcePacks",
        "Version": "2023-11-07",
        "Service": "{Service}",// X-Top-Service parameter in header
        "Region": "{Region}" // X-Top-Region parameter in header},
        "Result":
        {
            "OrderIDs": 
            [
                "Order20010000000000000001" // Order ID returned after successful purchase
            ]
        }
}
```


&nbsp;

<span id="ZKW4jyHk"></span>
### Query SpeakerID by Order ID `ListMegaTTSByOrderID`


* **Interface Description**: Query purchased SpeakerIDs by order ID 

* **Request Method**: `POST`

* **Request Parameters:** 



|**Parameter** |**Type** |**Required** |**Argument Type** |**Description** |
|---|---|---|---|---|
|Content\-Type |string |Y |header |Fixed string: `application/json; charset=utf-8` |
|Action |string |Y |query |ListMegaTTSByOrderID |
|Version |string |Y |query |2023\-11\-07 |
|ProjectName |string |Y |body |Project name from the new console |
|OrderID |string |Y |body |Order ID returned from `OrderAccessResourcePacks` (e.g. `Order20010000000000000001`) |
|PageNumber |int |N |body |Page number, must be greater than 0, default is 1 |
|PageSize |int |N |body |Number of items per page, must be in [1, 100], default is 10 |
|NextToken |string |N |body |String returned by the last request; if not empty, it will override the values of PageNumber and PageSize |
|MaxResults |int |N |body |Cooperates with NextToken to control the maximum number of returned results; must be used together with NextToken; if not empty, it must be in [1, 100], default is 10 |



* **Request Example**:


```Python
{
    # "AppID": "100000000", #Use this appID if the legacy console is being used. 
    "ProjectName": "default",
    "OrderID": "Order20010000000000000001",
    "PageNumber": 1,
    "PageSize": 10,
    "NextToken": "foobarfoobar",
    "MaxResults": 10
}
```



* **Return Data**:


```JSON

 
{
    "ResponseMetadata": 
    {
        "RequestId": "20220214145719010211209131054BC103", // X-Top-Request-Id parameter in header
        "Action": "OrderAccessResourcePacks",
        "Version": "2023-11-07",
        "Service": "{Service}",// X-Top-Service parameter in header
        "Region": "{Region}" // X-Top-Region parameter in header},
        "Result":
        {
            "OrderIDs": 
            [
                "Order20010000000000000001" // Order ID returned after successful purchase
            ]
        }
}

{
  "ResponseMetadata": {
    "RequestId": "20220214145719010211209131054BC103", // X-Top-Request-Id parameter in header
    "Action": "OrderAccessResourcePacks",
    "Version": "2023-11-07",
    "Service": "{Service}",// X-Top-Service parameter in header
    "Region": "{Region}" // X-Top-Region parameter in header},
  },
  "Result": {
  "OrderBuyQuantity": 1,
  "OrderBuyCurrentSuccessQuantity": 1,
  "OrderBuyCurrentFailedQuantity": 0,
  "IsAllProcessed": true,
  "Statuses": [
    {
      "SpeakerID": "S_pxxxxe2",
      "InstanceNO": "Model_storage_T1Jzz6-yloPBdqaD",
      "InstanceStatus": "active",
      "IsActivatable": false,
      "State": "Unknown",
      "DemoAudio": null,
      "Version": null,
      "CreateTime": 0,
      "ExpireTime": 0,
      "OrderTime": 1788491577000,
      "Alias": "",
      "AvailableTrainingTimes": 15,
      "ResourceID": "seed-icl-2.0",
      "Avatar": "",
      "Labels": null,
      "Description": "",
      "ModelTypeDetails": null,
      "CloneSource": 0,
      "EnableFormalized": false
    }
  ],
  "PageNumber": 1,
  "PageSize": 10,
  "TotalCount": 1
}
}
```


&nbsp;

<span id="UxX7stqM"></span>
### Voice Renewal `RenewAccessResourcePacks`

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note:</div>


<div data-tips="true" data-tips-type="default">Voice slots for ICL 1.0 and ICL 2.0 have been unified. The voice slots have also been upgraded and no longer incur storage fees or expire.</div>


<div data-tips="true" data-tips-type="default">So this <strong>Renew API is no longer required</strong>. </div>



* **Interface Description**: Renew voice and pay for it in one step. 

   **Prerequisites: ** 

   * The account has sufficient balance (or vouchers) to automatically pay for the order. 

   * Frequency limit: A maximum of 2000 voices can be renewed within 2 minutes.

* **Request Method**: `POST`

* **Request Parameters:** 



|**Parameter** |**Type** |**Required** |**Argument Type** |**Description** |
|---|---|---|---|---|
|Content\-Type |string |Y |header |Fixed string: `application/json; charset=utf-8` |
|Action |string |Y |query |RenewAccessResourcePacks |
|Version |string |Y |query |2023\-11\-07 |
|Times |int |Y |body |Renewal duration for timbre, in months |
|SpeakerIDs |string |N |body |List of SpeakerIDs to renew, which can be obtained by filtering through the `BatchListMegaTTSTrainStatus` interface |
|AutoUseCoupon |bool |N |body |Whether to automatically use vouchers |
|CouponID |string |N |body |Voucher ID, obtained through Voucher Management |



* **Return Data**:


```JSON
{
    "ResponseMetadata": 
    {
        "RequestId": "20220214145719010211209131054BC103", // X-Top-Request-Id parameter in header
        "Action": "OrderAccessResourcePacks",
        "Version": "2023-11-07",
        "Service": "{Service}",// X-Top-Service parameter in header
        "Region": "{Region}" // X-Top-Region parameter in header},
        "Result":
        {
            "OrderIDs": 
            [
                "Order20010000000000000001" // Order ID returned after successful purchase
            ]
        }
}
```


&nbsp;

<span id="hTCfQuW8"></span>
## Appendix

<span id="LBGviWMd"></span>
### State Enumeration Values


|**State** |**Description** |
|---|---|
|Unknown |SpeakerID has not been trained |
|Training |Voice cloning is in progress (contact support if it stays in this state for a long time) |
|Success |Voice cloning training is successful, TTS synthesis is available |
|Active |Activated (cannot be trained again) |
|Expired |Byteplus console instance has expired or the account is in arrears |
|Reclaimed |Byteplus console instance has been reclaimed |


<span id="glkqpxdk"></span>
### Common Error Values


|**Error** |**Description** |
|---|---|
|InvalidParameter |Incorrect request parameters |
|Forbidden.InvalidService |Voice cloning not enabled |
|Forbidden.ErrAccountNotPermission |Account has no permission |
|Forbidden.LimitedTradingFrequency |Order placement frequency limit error |
|InvalidParameter.AppID |AppID is incorrect or invalid |
|NotFound.ResourcePack |Timbre (or resource pack) does not exist |
|InvalidParameter.InstanceNumber |Invalid voice (or instance) |


<span id="gaJaKSIH"></span>
## Demo


<Tabs>
<Tab zoneid="IZgz4p2pFt" title="Python Example">
<TabTitle>Python Example</TabTitle>

<span id="wGNCB6Wy"></span>
### Precondition


* Detailed information on environment setup is available in the README.md file located in the sample package.


<span id="rGlkztHA"></span>
### **Download code example ** 

<Attachment link="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260630120246-429936714342.zip" name="byteplus_voicereplicationmanagementAPI_demo.zip">byteplus_voicereplicationmanagementAPI_demo.zip</Attachment>


<span id="6rXPJmnA"></span>
### **Invoke**

> Check the README.md files for usage instructions. 

> `sign_fullapilist.py` directly calls the API by manually implementing HMAC\-SHA256 signatures, providing complete signature visibility but with complex code; while `signwithsdk_fullapilist.py` uses the official BytePlus SDK, offering a cleaner object\-oriented interface but requiring additional dependency installation.


```Bash
python sign_fullapilist.py --help
#or
python signwithsdk_fullapilist.py --help
```





</Tab>
</Tabs>
