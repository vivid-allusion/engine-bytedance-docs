---
title: "PutFetchTask"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Putfetchtask"
---

## Introduction

Use the PutFetchTask API to create an asynchronous task that fetches resources from the specified URL and stores them in the specified bucket. Only one object is fetched each time; you can specify the bucket and the final object name during fetching.

## Server\-side encryption

With server\-side encryption enabled, TOS encrypts the data you upload at the object level and stores the encrypted data permanently. When you download an object, TOS automatically decrypts and returns the data to you. For more details about server\-side encryption, see [Server-side encryption overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).

## ACL

You can set the object's ACL through headers. All objects are private by default. You can grant specific permissions to an account or predefined group. For more details about ACL, see [ACL policy overview](https://docs.byteplus.com/docs/tos/docs-overview_4).

## Storage type

TOS stores objects in Standard Storage by default. This storage type features high availability, reliability, and performance. You can also choose another storage type according to the use case. For more information about storage types, see [Storage type](https://docs.byteplus.com/docs/tos/docs-storage-type).

## Callback

PutFetchTask supports callback functions. After setting the callback parameters, a callback will be executed based on the fetch result, described as follows:

* If fetching the object succeeds, the callback will be triggered according to the CallBack parameters set.

* If fetching the object fails, a special callback message format will be returned to the third\-party application service, including the parameters and error information from the request.

> **tip**

> The callback function of PutFetchTask does not currently support callback signatures.

## Notes

|**Category** |**Notes** |
|---|---|
|Number of objects |* Only one object can be fetched at a time.<br><br>* The maximum supported size is 500 GiB. Fetching objects larger than 500 GiB will fail. |
|URL |Only supports fetching publicly accessible URL resources. |
|Permission |Make sure the BytePlus account you use has permission to upload objects to the corresponding bucket; otherwise, asynchronous fetch tasks will fail. |
|Trigger mechanism |Uses an asynchronous triggering mechanism that does not execute tasks sequentially but allows multiple tasks to run simultaneously; task blocking does not prevent others from running. |
|Call result |After calling the PutFetchTask API, only the task ID will be returned. If you want to check the details of this task, such as whether it executed successfully, you can call the GetFetchTask API. For details, see [GetFetchTask](https://docs.byteplus.com/docs/tos/Getfetchtask). |
|QPS |When calling the PutFetchTask interface to submit tasks, a maximum of 100 QPS is supported. |
|Bucket type |HNS buckets do not support the PutFetchTask interface yet. |

## Request syntax

```JSON
POST /?fetchTask HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
<Optional Additional Header>

{
    "URL": "http://abc.123/",
    "Object": "objectName"
}
```

## Request parameters and headers

This request uses common request headers. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

|**Name** |**Location** |**Type** |**Required** | ** Sample value** |**Note** |
|---|---|---|---|---|---|
|fetchTask |Query |String |Yes |\- |Represents the special identifier for the PutFetchTask request. |
|x\-storage\-class |Header |String |No |STANDARD |Specifies the storage type of the destination object. If this parameter is unset, the object inherits the default storage type of its containing bucket. Valid values:<br><br><br>* `STANDARD`: Standard Storage.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `COLD_ARCHIVE`: Cold Archive.<br><br>   > **tip**<br>   <br><br>   > Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou).<br>   <br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive.<br><br>   > **tip**<br>   <br><br>   > Deep Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou). It is currently in closed beta. Please contact your account manager to use this storage type.<br>    |
|x\-tos\-acl |Header |String |No |private |Object ACL setting. Valid values:<br><br><br>* `private`: Private.<br><br>* `public-read`: Public read.<br><br>* `public-read-write`: Public read\-write.<br><br>* `authenticated-read`: Authenticated user read.<br><br>* `bucket-owner-read`: Bucket owner read.<br><br>* `bucket-owner-full-control`: Bucket owner full control.<br><br>* `default`: Inherits bucket ACL, meaning the object's ACL policy is consistent with the bucket's ACL policy. |
|x\-tos\-grant\-full\-control |Header |String |No |id=123,id=456 |Grants the grantees READ, READ_ACP, and WRITE_ACP permissions on the object during object creation. Format: id=account1,id=account2. |
|x\-tos\-grant\-read |Header |String |No |id=123,id=456 |Allows the grantee to read the object and its metadata. Format: id=account1,id=account2. |
|x\-tos\-grant\-read\-acp |Header |String |No |id=123,id=456 |Allows the grantees to read the object ACL. Format: id=account1,id=account2. |
|x\-tos\-grant\-write\-acp |Header |String |No |id=123,id=456 |Allows the grantees to modify the object ACL. Format: id=account1,id=account2. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |Header |String |No |AES256 |Specifies the algorithm for SSE\-C encrypting the object. Valid values are as follows:<br><br>`AES256`: Encrypt the object using AES256 algorithm. |
|x\-tos\-server\-side\-encryption\-customer\-key |Header |String |No |1234567890abcdefghijklmnopqrstuv |Specify the SSE\-C encrypted object's key. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |Header |String |No |0gYVWExOAz67jX5A6qY4+A== |Represents the MD5 value of the key used for the encrypted object. The value is derived by Base64\-encoding the 128\-bit MD5 of the key and is used for message integrity check to ensure error\-free transmission of the encryption key. |
|x\-tos\-meta\-\* |Header |String |No |x\-tos\-meta\-key: value |Used to add custom metadata for customized object management. Your custom metadata will appear in the response headers when others retrieve this object or query the object metadata. |

## Request body elements

|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|URL |Body |String |Yes |http://abc.123/ |URL to be captured.<br><br>> **tip**<br><br><br>> Currently supports only a single URL.<br> |
|Object |Body |String |Yes |objectName |Specify the object name stored in TOS. |
|IgnoreSameKey |Body |Bool |No |true |Fetch strategy when an object with the same name exists in the bucket, with the following options:<br><br><br>* `true`: If an object with the same name already exists in the bucket, the current fetch will be abandoned.<br><br>* `false`: If an object with the same name exists in the bucket, the object will still be fetched, and uploading it will overwrite the original object in the bucket.<br><br><br>The default is `false`.<br><br>> **tip**<br><br><br>> The key of the object is used to determine if it has the same name; object content is not compared.<br> |
|ContentMD5 |Body |String |No |XrY7u+Ae7tCTyyK7j1rNww== |The base64 value of the MD5 of the object to be uploaded. After setting, TOS calculates the MD5 of the uploaded object and verifies it against the MD5 carried by PutFetchTask. If verification fails, the object fetch will fail. |
|CallbackUrl |Body |String |No |http://domainname.com/callback |The callback request URL specifies the address of the third\-party application service. After a successful upload, the TOS service sends an HTTP/HTTPS request to this address. The details are as follows:<br><br><br>* The path and query parts of the URL must be URL\-encoded.<br><br>* The URL must follow the HTTP/HTTPS protocol; if the protocol is not specified, it defaults to `https://`.<br><br>* Supports up to five URLs, separated by semicolons (`;`). When the TOS server sends callback requests, it attempts them in order until the first URL returns a successful response.<br><br><br>> **warning**<br><br><br><br>* > Callback parameter variables are not supported.<br><br><br>* > If `CallbackUrl` is empty, other upload callback parameters will be ignored, indicating no upload callback parameter is set for this request.<br><br><br>* > The domain or IP included in `CallbackUrl` cannot be special domains or IPs: 127.0.0.1, 0.0.0.0, 0:0:0:0:0:0:0:1, 0:0:0:0:0:0:0:0, localhost.<br> |
|CallbackHost |Body |String |No |alternative\-domainname.com |The HOST header used when sending callback requests to replace the HOST parsed from `callbackUrl`.<br><br>> **warning**<br><br><br><br>* > Callback parameter variables are not supported.<br><br><br>* > `CallbackHost` parameter can be empty.<br><br><br>* > `CallbackHost` must conform to domain or IP format rules; the domain or IP cannot be special values such as 127.0.0.1, 0.0.0.0, 0:0:0:0:0:0:0:1, 0:0:0:0:0:0:0:0, or localhost.<br> |
|CallbackBody |Body |String |No |{"bucket" : ${bucket}, "object" : ${object},"fetchTaskId":${fetchTaskId}} |The message body sent during the callback request must match the type specified by `callbackBodyType`.<br><br>> **tip**<br><br><br><br>* > Supports callback parameter variables. For details, see [Callback parameter variables](https://docs.byteplus.com/docs/tos/Upload-callback#.5Zue6LCD5Y-C5pWw5Y-Y6YeP).<br><br><br>* > The callback parameter supports configuring the variable `"fetchTaskId": ${fetchTaskId}`, and it only applies to the `PutFetchTask` interface. Regardless of whether the fetch is successful or not, as long as this variable is configured, the corresponding `TaskId` will be carried in the client callback `body`.<br><br><br>* > When `CallbackBodyType` is `application/json`, it must be valid JSON; TOS server strictly validates this field. When `callbackBodyType` is `application/x-www-form-urlencoded`, it can be empty.<br><br><br>* > If the callback fails, the CallbackBody parameter will be ignored.<br> |
|CallbackBodyType |Body |String |No |application/json |The message body type of callback request (Content\-Type), used together with `callbackBody`. Only values of `application/x-www-form-urlencoded` and `application/json` are supported; other values are invalid.<br><br>The default value is `application/x-www-form-urlencoded`.<br><br>> **tip**<br><br><br>> Callback parameter variables are not supported.<br> |

## Response headers

This request returns common response headers. See [common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

## Response body elements

This request returns the ID of the asynchronous task.

|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TaskID |String |da62d05e\-e6e4\-4bad\-924a\-ed4ab98ae17a |Asynchronous task ID. |

## Sample request

```JSON
POST /?fetchTask HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
<Optional Additional Header>

{
    "URL": "http://abc.123/",
    "Object": "objectName"
}
```

## Sample response

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 143
{
    "taskid": "da62d05e-e6e4-4bad-924a-ed4ab98ae17a"
}
```
