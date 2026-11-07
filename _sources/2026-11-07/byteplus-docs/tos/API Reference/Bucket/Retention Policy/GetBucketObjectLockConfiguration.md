---
title: "GetBucketObjectLockConfiguration"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getbucketobjectlockconfiguration"
---

<span id="9bc1b2bd"></span>
## **Function Description**

This interface is used to obtain the retention policy of a bucket.

<span id="0fbebb72"></span>
## **Request syntax**

```JSON
GET /?object-lock HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="6059dade"></span>
## **Request parameters and headers**

The public message header used by this request; see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** | ** Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|object\-lock |Query |String |Yes |\- |Represents a special identifier for the GetBucketObjectLockConfiguration request. |


<span id="9b6d044c"></span>
## **Request body elements**

This request does not use message elements.

<span id="1e1aaa41"></span>
## **Response headers**

This request returns public response message headers.

<span id="2ba91dee"></span>
## **Response body elements**


|**Name** | ** Type** |**Sample Value** |**Description** |
|---|---|---|---|
|ObjectLockEnabled |String |Enabled |Whether to enable the retention policy; the only valid value is `Enabled`, which indicates that the retention policy is enabled. |
|Rule |Object |\- |Bucket retention strategy rules. |
|DefaultRetention |Object |\- |The default retention policy for the bucket.<br><br>Parent node: Rule. |
|Days |Integer |1 |Object lock duration (days): During the specified period, the object cannot be deleted or overwritten. The duration is measured in days.<br><br>Parent Node: DefaultRetention |
|Years |Integer |1 |Object lock duration (in years): During the specified number of years, the object cannot be deleted or overwritten. The unit is years, and one year equals 365 days.<br><br>Parent Node: DefaultRetention |
|Mode |String |COMPLIANCE |Retention policy mode, with the value limited to `COMPLIANCE`, indicates compliance mode, in which no user can delete or overwrite locked objects during the retention period.<br><br>Parent Node: DefaultRetention |


<span id="a2bbfbe0"></span>
## **Sample request  1**

```JSON
GET /?object-lock HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:59:18 GMT
Authorization: authorization string
```


<span id="a94aca18"></span>
## **Sample response 1**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0
x-tos-request-id: f91b0c03a01300c1-a444ed0
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 31

{   
    "ObjectLockEnabled": "Enabled"
}
```


<span id="4e2731e4"></span>
## **Sample request  2**

```JSON
GET /?object-lock HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:59:18 GMT
Authorization: authorization string
```


<span id="a969ff4b"></span>
## **Sample response2**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0
x-tos-request-id: f91b0c03a01300c1-a444ed0
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 92

{   
    "ObjectLockEnabled": "Enabled",
    "Rule": {
        "DefaultRetention": {
            "Days": 100,
            "Mode": "COMPLIANCE"
        }
    } 
}
```
