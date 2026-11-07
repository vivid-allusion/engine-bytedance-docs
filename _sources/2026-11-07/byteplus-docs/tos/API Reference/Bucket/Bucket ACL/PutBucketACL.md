---
title: "PutBucketACL"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-putbucketacl"
---

<span id="00db0e05"></span>
## **Introduction**

This API is used to set bucket ACLs. Setting bucket ACLs requires WRITE_ACP permission. A bucket ACL can have up to 100 grants. This API operates in an overwriting manner, which means a new bucket ACL overwrites the old one.

You can set a bucket ACL in either way:


* Set an ACL in the request body.

* Specify permissions in headers.


<span id="b2bcc353"></span>
## Specifying permissions in headers

Specify an ACL in either way:


* Designate a predefined ACL using the x\-tos\-acl request header. Predefined ACLs have preconfigured grantees and permissions. Using this header indicates that you cannot use other headers to specify permissions in the request.

   Below are the predefined ACLs:

   
   |**Predefined ACL** |**Description** |
   |---|---|
   |private |Sets private permission that rejects access from other accounts. |
   |public\-read |Grants read permission to all users. |
   |public\-read\-write |Grants read and write permissions to all users. |
   |authenticated\-read |Grants read permission to authenticated users only. |
   

* Use the x\-tos\-grant\-read, x\-tos\-grant\-write, x\-tos\-grant\-read\-acp, x\-tos\-grant\-write\-acp, and x\-tos\-grant\-full\-control headers to explicitly specify access permissions. If you use these headers, you cannot use the x\-tos\-acl request header to specify a predefined ACL. The header values adhere to the format of `type=value`, where the type can be one of the following:

   * id: The value is an account ID.

   * canned: The value of a predefined group.

      Below are the predefined groups:

      
      |**Predefined group** |**Description** |
      |---|---|
      |AllUsers |All users |
      |AuthenticatedUsers |Authenticated users |
      


<span id="bcd0beca"></span>
## **Request syntax**

```JSON
PUT /?acl HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
x-tos-acl: ACL
x-tos-grant-full-control: GrantFullControl
x-tos-grant-read: GrantRead
x-tos-grant-read-acp: GrantReadACP
x-tos-grant-write: GrantWrite
x-tos-grant-write-acp: GranteWriteACP

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


<span id="73072904"></span>
## **Request parameters and headers**

For common request headers, see [Common parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|acl |Query |String |Yes | |Identifies a PutBucketACL request. |
|x\-tos\-acl |Header |String |No |private |Bucket ACL setting. Valid values:<br><br><br>* `private`: Private permission.<br><br>* `public-read`: Publicly readable.<br><br>* `public-read-write`: Publicly readable and writable.<br><br>* `authenticated-read`: Authenticated users have read access. |
|x\-tos\-grant\-full\-control |Header |String |No |id: test\-cid |Grants all permissions to specified users. |
|x\-tos\-grant\-read |Header |String |No |id: test\-cid |Grants READ permission to specified users. |
|x\-tos\-grant\-read\-non\-list |Header |String |No |id: test\-cid |Revoke the permission to list objects and multipart tasks within the bucket.<br><br>x\-tos\-grant\-read\-non\-list must be used in conjunction with x\-tos\-grant\-read\-acp, meaningless when used alone. When used in conjunction with x\-tos\-grant\-read\-acp, it indicates that the grantee is authorized to access bucket metadata, object metadata, and download objects. |
|x\-tos\-grant\-read\-acp |Header |String |No |id: test\-cid |Grants READ_ACP permission to specified users. |
|x\-tos\-grant\-write |Header |String |No |id: test\-cid |Grants WRITE permission to specified users. |
|x\-tos\-grant\-write\-acp |Header |String |No |id: test\-cid |Grants WRITE_ACP permission to specified users. |


<span id="1f567ccf"></span>
## **Request body elements**


|**Name** |**Type** |**Description** |
|---|---|---|
|Grants |Array |The root node for object access control. |
|Grantee |Object |The authorized user. Parent node: Grants. |
|Type |String |The user type. Parent node: Grantee. |
|Canned |String |Use this property when `Type` is `Group`. Valid values:<br><br><br>* `AllUsers`: All users.<br><br>* `AuthenticatedUsers`: Some users that have been authorized based on the account ID.<br><br><br>Parent node: Grantee. |
|ID |String |Use this property to specify the account ID of the authorized user when `Type` is `CanonicalUser`. Parent node: Grantee. |
|Permission |String |The permission type,the value descriptions are as follows:<br><br><br>* `READ`：Allow the authorized user to access bucket metadata, object metadata, download objects, list objects within a bucket, and view shard tasks.<br><br>* `READ_NON_LIST`：Allow authorized users to access bucket metadata, object metadata, and download objects.<br><br>* `WRITE`：Allow authorized users to create, overwrite, and delete any object in the bucket, initialize multipart tasks, upload parts, merge parts, and cancel multipart tasks.<br><br>* `READ_ACP`：Allow the authorized party to read the ACL of the bucket.<br><br>* `WRITE_ACP`：Allow the authorized user to modify or delete the ACL of the bucket.<br><br>* `FULL_CONTROL`：Allow the grantee to have READ, WRITE, READ_ACP, and WRITE_ACP permissions on the bucket.<br><br><br>Parent node: Grants. |
|Owner |Object |The object owner. |
|ID |String |The account ID. Parent node: Owner. |
|BucketAclDelivered |Bool |Whether to enable default object inheritance bucket ACL function, the possible values are as follows:<br><br><br>* `true`：Enable object default inheritance of bucket ACL functionality.<br><br>* `false`：Disable object default inheritance of bucket ACL functionality.<br><br><br>The default value is `false`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Owner and BucketAclDelivered parameters must be set together, otherwise the default object inheritance bucket ACL feature cannot be enabled.</div><br> |


<span id="2f1a7be8"></span>
## **Response headers**

The response contains only common headers.

<span id="d1ba0b68"></span>
## **Response body elements**

No elements are used.

<span id="d13d24f8"></span>
## **Sample request 1**

```JSON
PUT /?acl HTTP/1.1
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


<span id="7d8ed932"></span>
## **Sample request 2**

```JSON
PUT /?acl HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:59:18 GMT
Authorization: authorization string
x-tos-acl: public-read
```


<span id="97b4914d"></span>
## **Sample request 3**

```JSON
PUT /?acl HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:59:18 GMT
Authorization: authorization string
x-tos-grant-read: canned=everyone
x-tos-grant-write: canned=AuthenticatedUsers,id=test-cid
```


<span id="cb9bfec0"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 4fac130beeb50032-a444ed0
x-tos-request-id: 4fac130beeb50032-a444ed0
Date: Fri, 30 Jul 2021 13:59:18 GMT
server: TosServer
Content-Length: 0
```
