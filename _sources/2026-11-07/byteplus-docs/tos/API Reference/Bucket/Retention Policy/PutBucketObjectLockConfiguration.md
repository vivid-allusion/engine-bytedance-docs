---
title: "PutBucketObjectLockConfiguration"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Putbucketobjectlockconfiguration"
---

<span id="212e7606"></span>
## **Function Description**

This interface is used to configure the bucket retention policy. After configuring the bucket retention policy, if no retention period is specified when uploading an object, the newly uploaded object will inherit the bucket's retention period by default.

<span id="97dab14f"></span>
## Precautions


* Once a retention period is set for an object, it cannot be canceled and will only expire automatically when the retention period ends.

* After the bucket retention policy is configured, if a newly uploaded object does not have an individual retention period set, it will inherit the bucket retention period by default and automatically enter the locked state. Objects uploaded before the bucket retention period is set will not automatically inherit that retention period.

* If only the object lock feature is enabled without setting either the bucket retention period or the object retention period, objects will not enter the locked state and cannot obtain protection against deletion or overwriting.


<span id="79f68b97"></span>
## **Request syntax**

```JSON
PUT /?object-lock HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string

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


<span id="884be11d"></span>
## **Request parameters and headers**

The public message header used by this request. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** | ** Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|object\-lock |Query |String |Yes |\- |A special identifier representing the PutBucketObjectLockConfiguration request. |


<span id="77e43010"></span>
## **Request body elements**


|**Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ObjectLockEnabled |String |Yes |Enabled |Whether to enable the retention policy; the only valid value is `Enabled`, which indicates that the retention policy is enabled. |
|Rule |Object |No |\- |Bucket retention policy rules. |
|DefaultRetention |Object |No |\- |Default retention policy for buckets.<br><br>Parent Node: Rule. |
|Days |Integer |No |1 |Object lock duration: During the specified number of days, the object cannot be deleted or overwritten. The unit is days, with a valid range of 1 to 36,500 days.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only one of the <code>Days</code> or <code>Years</code> parameters needs to be set.</div><br><br><br>Parent Node: DefaultRetention |
|Years |Integer |No |1 |Object lock duration: During the specified number of years, the object cannot be deleted or overwritten. The unit is years, with a valid range of 1 to 100 years. One year is defined as 365 days.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only one of the <code>Days</code> or <code>Years</code> parameters needs to be set.</div><br><br><br>Parent Node: DefaultRetention |
|Mode |String |No |COMPLIANCE |Retention policy mode, with the only valid value being `COMPLIANCE`, indicates compliance mode, in which no user can delete or overwrite locked objects during the retention period.<br><br>Parent Node: DefaultRetention |


<span id="4ff0215a"></span>
## **Response headers**

This request returns public response message headers.

<span id="acf3a77a"></span>
## **Response body elements**

There is no message element in this request response.

<span id="77348b38"></span>
## **Sample request  1**

Enable the object lock feature and set the retention period to 100 days.

```JSON
PUT /?object-lock HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:59:18 GMT
Authorization: authorization string

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


<span id="6aa02b1b"></span>
## **Sample response** 1

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444cd0        
x-tos-request-id: f91b0c03a01300c1-a444cd0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 0
```


<span id="92642f68"></span>
## **Sample request  2**

Enable only the object lock function without setting a retention period.

```JSON
PUT /?object-lock HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:59:18 GMT
Authorization: authorization string

{   
    "ObjectLockEnabled": "Enabled" 
}
```


<span id="e1b4a0e4"></span>
## **Sample response** 2

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 0
```
