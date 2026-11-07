---
title: "PutObjectTagging"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-putobjecttagging-"
---

<span id="ef028546"></span>
## **Description**

This API is used to set the tagging of an object. Object tags are a set of key\-value pairs.

<span id="f32b8dfc"></span>
## **Versioning**

If your bucket has versioning enabled, note the following restrictions when using PutObjectTagging:


* By default, the API sets tagging for the current version of the object. Use the `versionId` parameter to specify the target version of action.

* You cannot set tags for a delete marker if that is what the request URL resolves to. If you try to do so, TOS returns `404 Not Found`.


<span id="e36d8d7c"></span>
## **Note**


|**Category** |**Note** |
|---|---|
|API |Note the following two scenarios when using the PutObjectTagging API to set tags:<br><br><br>* If the object has no tags, PutObjectTagging adds a set of tags (key\-value pairs) to that object.<br><br>* If the object already has tags, PutObjectTagging overwrites them. |
|Tag |* You can set up to 10 tags for a single object. When using multiple tags, make sure the keys are unique.<br><br>* Altering object tags does not affect the last modified time of the object. |
|Key\-value pair |* The keys and values are case\-sensitive.<br><br>* The keys and values of tags can only consist of uppercase and lowercase letters, digits, spaces, and the following symbols: colon ( : ), plus sign ( + ), hyphen ( \- ), equal sign ( = ), period ( . ), underscore ( _ ), and forward slash ( / ).<br><br>* The maximum length is 128 characters for keys and 256 characters for values.<br><br>* To set object tags that contain arbitrary characters through HTTP headers, you need to URL\-encode the tag keys and values. |


<span id="fe8ca60c"></span>
## **Request syntax**

```JSON
PUT /objectname?tagging
Content‐Length: 114
Host: Host: examplebucket.tos-ap-southeast-1.bytepluses.com
Date: Mon, 18 Mar 2019 08:25:17 GMT
Authorization: SignatureValue
{
    "TagSet": {
        "Tags": [
            {
                "Key": "aa", 
                "Value": "bb"
            },
         {
                "Key": "bb", 
                "Value": "cc"
            }
        ]
    }
}
```


<span id="d5e9666d"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|tagging |Query |String |Yes | |Identifies a PutObjectTagging request. |
|versionId |Query |String |No |/ |Version ID of the object. Use this to set the tags of a specific version of the object. |


<span id="89084ca2"></span>
## **Request body elements**

The request body specifies the desired tagging of the object.


|**Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|TagSet |Container |Yes |/ |A set of tags. |
|Tags |Container |Yes |/ |Tag information. |
|Key |String |Yes |aa |Tag key. |
|Value |String |No |bb |Tag value. |


<span id="c266c659"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="485b6e35"></span>
## **Response body elements**

No elements are used.

<span id="a55a7679"></span>
## **Sample request**


* Setting tags for an object

   ```JSON
   PUT /objectname?tagging
   Content‐Length: 114
   Host: bucketname.tos-ap-southeast-1.bytepluses.com
   Date: Mon, 18 Mar 2019 08:25:17 GMT
   Authorization: SignatureValue
   {
       "TagSet": {
           "Tags": [
               {
                   "Key": "aa", 
                   "Value": "bb"
               },
            {
                   "Key": "bb", 
                   "Value": "cc"
               }
           ]
       }
   }
   ```
   

* Setting tags for a specific version of an object

   ```JSON
   PUT /objectname?tagging&versionId=57894830D7822B2ACB78
   Content‐Length: 114
   Host: bucketname.tos-ap-southeast-1.bytepluses.com
   Date: Mon, 18 Mar 2019 08:25:17 GMT
   Authorization: SignatureValue
   {
       "TagSet": {
           "Tags": [
               {
                   "Key": "aa", 
                   "Value": "bb"
               },
            {
                   "Key": "bb", 
                   "Value": "cc"
               }
           ]
       }
   }
   ```
   


<span id="ef306962"></span>
## Sample **response**


* Sample response to setting tags for an object

   ```JSON
   HTTP/1.1 200 OK
   content-length: 0
   server: TosServer
   date: Wed, 24 Jun 2020 08:57:15 GMT
   x-tos-id-2: 4fac130bedb6002c-a444ed0
   x-tos-request-id: 4fac130bee03002e-a444ed0
   json
   ```
   

* Sample response to setting tags for a specific version of an object

   ```JSON
   HTTP/1.1 200 OK
   content-length: 0
   server: TosServer
   date: Wed, 24 Jun 2020 08:58:15 GMT
   x-tos-id-2: ea2ceb08a4e30021-a444ed0
   x-tos-request-id: 5726ce090a2d002d-a444ed0
   x-tos-version-id: 57894830D7822B2ACB78
   json
   ```
