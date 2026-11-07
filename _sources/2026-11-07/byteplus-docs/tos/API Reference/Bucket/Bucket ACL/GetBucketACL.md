---
title: "GetBucketACL"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-getbucketacl"
---

<span id="8926cba1"></span>
## **Description**

This API is used to get the ACL of a specified bucket. Calling this API requires READ_ACP permission.

<span id="5c7fdb15"></span>
## **Request syntax**

```JSON
GET /?acl HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="b87b78f6"></span>
## **Request parameters and headers**

For common request headers, see [Common parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|acl |Query |String |Yes | |Identifies a GetBucketACL request. |


<span id="cef18dbc"></span>
## **Request body elements**

No elements are used.

<span id="50c07910"></span>
## **Response headers**

For common response headers, see [Common parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="a8fc77ed"></span>
## **Response body elements**


|**Name** |**Type** |**Description** |
|---|---|---|
|Grants |Array |The root node for object access control. |
|Grantee |Object |The authorized user. Parent node: Grants. |
|Type |String |The user type. Parent node: Grantee. |
|Canned |String |This property is returned when `Type` is `Group`. Valid values:<br><br><br>* `AllUsers`: All users.<br><br>* `AuthenticatedUsers`: Users that have been authorized based on the account ID.<br><br><br>Parent node: Grantee. |
|ID |String |This property is returned when `Type` is `CanonicalUser`, indicating the authorized user ID. Parent node: Grantee. |
|Permission |String |The permission type. The value descriptions are as follows:<br><br><br>* `READ`：Allow the authorized user to access bucket metadata, object metadata, download objects, list objects within a bucket, and view shard tasks.<br><br>* `READ_NON_LIST`：Allow authorized users to access bucket metadata, object metadata, and download objects.<br><br>* `WRITE`：Allow authorized users to create, overwrite, and delete any object in the bucket, initialize multipart tasks, upload parts, merge parts, and cancel multipart tasks.<br><br>* `READ_ACP`：Allow the authorized party to read the ACL of the bucket.<br><br>* `WRITE_ACP`：Allow the authorized user to modify or delete the ACL of the bucket.<br><br>* `FULL_CONTROL`：Allow the grantee to have READ, WRITE, READ_ACP, and WRITE_ACP permissions on the bucket.<br><br><br>Parent node: Grantee. |
|Owner |Object |The object owner. |
|ID |String |The account ID. Parent node: Owner. |
|BucketAclDelivered |Bool |Whether to enable default object inheritance bucket ACL function, the possible values are as follows:<br><br><br>* `true`：Enable object default inheritance of bucket ACL functionality.<br><br>* `false`：Disable object default inheritance of bucket ACL functionality. |


<span id="bfede759"></span>
## **Sample request**

```JSON
GET /?acl HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 06:45:39 GMT
Authorization: authorization string
```


<span id="6febb4fd"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0
x-tos-request-id: f91b0c03a01300c1-a444ed0
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 340

{
    "Owner": {
        "ID": "AccountID"
    },
    "Grants": [
        {
            "Grantee": {
                "ID": "AccountID",
                "Type": "CanonicalUser"
            },
            "Permission": "FULL_CONTROL"
        }
    ]
}
```
