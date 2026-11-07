---
title: "GetObjectACL"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-getobjectacl"
---

<span id="eaeaae4a"></span>
## **Description**

This API is used to get the ACL of a specified object.

Calling this API requires the READ_ACP permission. The ACL of the current object version is returned by default. Use the `versionId` parameter to get the ACL of a specific version of the object.

<span id="58cf1327"></span>
## **Request syntax**

```JSON
GET /objectname?acl HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="6a79658e"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|acl |Query |String |Yes | |Identifies a GetObjectACL request. |
|versionId |Query |String |No |123 |Version ID of the object. Use this to get the ACL of a specific version of the object. |


<span id="d5515791"></span>
## **Request body elements**

No elements are used.

<span id="cdba4380"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Type** |**Description** |
|---|---|---|
|x\-tos\-version\-id |String |Version ID of the object. |


<span id="f1b399ad"></span>
## **Response body elements**


|**Name** |**Type** |**Description** |
|---|---|---|
|Grants |Array |Root node for object access control permissions. |
|Grantee |Object |Authorized user. Parent node: Grants. |
|Type |String |User type. Parent node: Grantee. |
|Canned |String |This property is returned when Type is Group. Valid values:<br><br><br>* AllUsers: all users.<br><br>* AuthenticatedUsers: some users that have been authorized based on the account ID.<br><br><br>Parent node: Grantee. |
|ID |String |This property is returned when Type is CanonicalUser, indicating the authorized user ID. Parent node: Grantee. |
|Permission |String |Permission type. Parent node: Grants. |
|Owner |Object |Object owner. |
|ID |String |Account ID. Parent node: Owner. |
|IsDefault |Boolean |The ACL of the object is inherited from the bucket ACL, meaning the ACL policy of the object remains consistent with the bucket ACL policy. Only true will be returned, indicating that the object's ACL is inherited from the bucket ACL. |


<span id="6fb406fd"></span>
## **Sample request**

```JSON
GET /?acl HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 06:45:39 GMT
Authorization: authorization string
```


<span id="c2c667c9"></span>
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
