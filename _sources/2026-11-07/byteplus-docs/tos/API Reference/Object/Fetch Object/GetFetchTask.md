---
title: "GetFetchTask"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getfetchtask"
---

<span id="04f2ce86"></span>
## **Feature description**

Call the GetFetchTask API to query detailed information about asynchronous tasks, including task status and callback information.

<span id="9e7c16f5"></span>
## Notes


* The GetFetchTask API only supports querying asynchronous tasks within 72 hours. Tasks older than 72 hours cannot be queried.

* HNS buckets are currently not supported by the GetFetchTask API.


<span id="2a421e83"></span>
## **Request syntax**

```JSON
GET /?fetchTask&taskId=da62d05e-e6e4-4bad-924a-ed4ab98ae17a HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="f2d2206a"></span>
## **Request parameters and headers**


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|fetchTask |Query |String |Yes |\- |A special identifier representing the GetFetchTask request. |
|taskId |Query |String |Yes |fac10613\-4cfa\-4689\-bffd\-8360b7dd0d38 |asynchronous task ID |


<span id="1d475142"></span>
## **Request body elements**

No elements are used.

<span id="ddcea231"></span>
## **Response headers**

This request returns common response headers. See [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="f870cab3"></span>
## **Response body elements**

This request returns the current status of the asynchronous task.


|**Name** |**Type** |**Sample Value** |**Note** |
|---|---|---|---|
|State |String |Success |Task status, the value description is as follows:<br><br><br>* `Running`: in progress,<br><br>* `Succeed`: succeeded,<br><br>* `FetchSuccessCallBackError`: fetch succeeded, callback failed,<br><br>* `Failed`: failed |
|Err |String |fetch failed reason:back\-to\-source failed. the reason is mirror\-back: unexpected status code 404 |Reason for task failure.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>Err</code> parameter returns the reason for task failure only when <code>Status</code> is in <code>Failed</code> or <code>FetchSuccessCallBackError</code> state.</div><br> |
|Task |Array |\- |Task details. See the table below for details **Task structure**. |


**Task structure**


|**Name** |**Parameter type** |**Sample value** |**Note** |
|---|---|---|---|
|URL |String |http://abc.123/ |URL to be fetched. |
|IgnoreSameKey |String |true |Fetch policy when a file with the same name exists in the bucket. The values are described as follows:<br><br><br>* `true`: abandon the fetch if a file with the same name already exists in the bucket.<br><br>* `false`: fetch the object even if a file with the same name exists in the bucket, overwriting the original object when uploading. |
|ContentMD5 |String |XrY7u+Ae7tCTyyK7j1rNww== |The base64 value of the uploaded file's MD5. |
|Bucket |String |test |The name of the bucket. |
|Object |String |data.jpg |Object name. |
|CallbackURL |String |http://domainname.com/callback |Callback request URL. |
|CallbackHost |String |alternative\-domainname.com |Host header when sending a callback request. |
|CallbackBody |String |{"bucket" : ${bucket}, "object" : ${object}, "key1" : ${x:key1}, "key2" : ${x:key2}} |The message body sent with the callback request. |
|CallbackBodyType |String |application/json |Callback request message body type. |
|StorageClass |String |STANDARD |The storage type of the destination object. |
|Acl |String |private |Object access permissions. |
|GrantFullControl |String |id=account1 |Grants the grantees READ, READ_ACP, and WRITE_ACP permissions on the object during object creation. Format: id=account1,id=account2. |
|GrantRead |String |id=Account1 |Allows the grantees to read the object and its metadata. Format: id=account1,id=account2. |
|GrantReadAcp |String |id=account1 |Allows the grantees to read the object ACL. Format: id=account1,id=account2. |
|GrantWriteAcp |String |id=account1 |Allows the grantees to modify the object ACL. Format: id=account1,id=account2. |
|SSECAlgorithm |String |AES256 |The algorithm used for SSE\-C encrypted objects. |
|SSECKey |String |YWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWE= |SSE\-C encrypted object key. |
|SSECKeyMd5 |String |0gYVWExOAz67jX5A6qY4+A== |The MD5 value of the key used for SSE\-C encrypted objects. |
|UserMeta |Array |\- |Added custom metadata. For details, see the table below **UserMeta structure**. |


**UserMeta structure**


|**Name** |**Type** |**Sample value** |**Note** |
|---|---|---|---|
|Key |String |key |Custom metadata key. |
|Value |String |value |Custom metadata value. |


<span id="a8f4b4e4"></span>
## **Sample request**

```JSON
GET /?fetchTask&taskId=da62d05e-e6e4-4bad-924a-ed4ab98ae17a HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:53:55 +0000
Authorization: authorization string
```


<span id="9ad84385"></span>
## **Sample response**


* Response example of task success

   ```JSON
   HTTP/1.1 200 OK
   Date: Fri, 30 Jul 2021 13:53:55 GMT
   Server: TosServer
   x-tos-id-2: 1e89f203jld00006-a444fd0
   x-tos-request-id: 1e89f203b2d00006-a444ed0
   Content-Length: 143
   {
       "State": "Success",
       "Task":{
           "URL": "http://abc.123/",
           "IgnoreSameKey": false,
           "Bucket": "bucketname",
           "Object": "objectName"
       }
   }
   ```
   

* Response example of task failure

   ```JSON
   HTTP/1.1 200 OK
   Date: Fri, 30 Jul 2021 13:53:55 GMT
   Server: TosServer
   x-tos-id-2: 1e89f203jld00006-a444fd0
   x-tos-request-id: 1e89f203b2d00006-a444ed0
   Content-Length: 143
   {
       "State": "Failed",
       "Err": "fetch failed reason:back-to-source failed. the reason is mirror-back: unexpected status code 404",
       "Task":{
           "URL": "http://abc.123/",
           "IgnoreSameKey": false,
           "Bucket": "bucketname",
           "Object": "objectName"
       }
   }
   ```
