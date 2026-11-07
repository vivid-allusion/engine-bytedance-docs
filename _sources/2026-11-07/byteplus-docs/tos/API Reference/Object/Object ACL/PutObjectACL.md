---
title: "PutObjectACL"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-putobjectacl"
---

<span id="4c64b67a"></span>
## **Introduction**

This API is used to set object ACL permissions. You can set the ACL during object upload and modify the ACL after object upload using this API. This API sets the ACL for the current version of an object by default. Include a `versionId` to set the ACL for a specific version of the object.

<span id="52a2fa7f"></span>
## **Request syntax**

```JSON
PUT /ObjectName?acl HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string

{   
    "Owner": { "ID": "test-cid" },
    "Grants": [{
        "Grantee": {
          "Type": "CanonicalUser",
          "ID": "test-cid"
        },
        "Permission": "FULL_CONTROL"
      }]
}
```


<span id="9397645a"></span>
## **Request parameters and headers**

For common request headers, see [Common parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|acl |Query |String |Yes |\- |Identifies a PutObjectACL request. |
|x\-tos\-acl |Header |String |No |private |Object ACL setting. Valid values:<br><br><br>* `private`: Private permission.<br><br>* `public-read`: Publicly readable.<br><br>* `public-read-write`: Publicly readable and writable.<br><br>* `authenticated-read`: Authenticated users have read access.<br><br>* `bucket-owner-read`: The bucket owner has read access.<br><br>* `bucket-owner-full-control`: The bucket owner has full control.<br><br>* `bucket-owner-entrusted`: Controlled by the bucket policy, with the bucket owner having full control.<br><br>* `default`: Inherit bucket ACL, that is, the ACL policy of the object remains consistent with the bucket ACL policy. |
|versionId |Query |String |No |57AF1A32CECB56721267 |Version ID of the object. Use this to modify the ACL of a specific version of the object. |


<span id="3c09759d"></span>
## **Request body elements**


|**Name** |**Type** |**Description** |
|---|---|---|
|Grants |Array |Root node for object access control permissions. |
|Grantee |Object |Authorized user. Parent node: Grants. |
|Type |String |User type. Parent node: Grantee. |
|Canned |String |Use this property when Type is Group. Valid values:<br><br><br>* AllUsers: All users.<br><br>* AuthenticatedUsers: Some users that have been authorized based on the account ID.<br><br><br>Parent node: Grantee. |
|ID |String |Specifies the account ID of the authorized user when Type is CanonicalUser. Parent node: Grantee. |
|Permission |String |Permission type. Parent node: Grants. |
|Owner |Object |Object owner. |
|ID |String |Account ID. Parent node: Owner. |
|IsDefault |Bool |Whether to set the ACL of the object to inherit the bucket's ACL, meaning the ACL policies of the object and the bucket remain consistent.<br><br><br>* `true`: Set the ACL of the object to inherit the bucket's ACL.<br><br>* `false`: If no ACL is set for an object to inherit the bucket ACL, the object's ACL defaults to private.<br><br><br>The default value is `false`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Owner and BucketAclDelivered parameters must be set together and do not support setting the Grantee parameter simultaneously.</div><br> |


<span id="27c3b17f"></span>
## **Response headers**

The response contains only common headers.

<span id="1689a573"></span>
## **Response body elements**

No elements are used.

<span id="bddbe0d8"></span>
## **Sample request**

```JSON
PUT /ObjectName?acl HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:59:18 GMT
Authorization: authorization string

{
    "Owner": {
        "ID": "AccountID"
    },
    "Grants": [
        {
            "Grantee": {
                "ID": "test-cid",
                "Type": "CanonicalUser"
            },
            "Permission": "FULL_CONTROL"
        }
    ]
}
```


<span id="5f5c2281"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 4fac130beeb50032-a444ed0
x-tos-request-id: 4fac130beeb50032-a444ed0
Date: Fri, 30 Jul 2021 13:59:18 GMT
server: TosServer
Content-Length: 0
```
