---
title: "GetBucketCustomDomain"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getbucketcustomdomain"
---

<span id="413ed146"></span>
## **Feature Description**

This interface is used to get the custom domain name configuration for the specified storage space (Bucket).

<span id="ba58b44f"></span>
## Precautions

To call this interface, you must be the owner of the bucket or be authorized with the GetBucketCustomDomain permission for the current bucket.

<span id="b1659979"></span>
## **Request syntax**

```JSON
GET /?customdomain HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="dbd56b15"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|customdomain |Query |String |Yes |\- |Represents a special identifier for the GetBucketCustomDomain request. |


<span id="b89139aa"></span>
## **Request body elements**

This request does not use message elements.

<span id="074690e8"></span>
## **Response headers**

The response contains a common response message header, please refer to [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="44795cb6"></span>
## **Response body elements**


|**Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|CustomDomainRules |Array |\- |Custom domain list. |
|Domain |String |example.com |Bound custom domain. |
|Cname |String |bucketname.tos\-ap\-southeast\-1.bytepluses.com |Value used to configure CNAME records. |
|Forbidden |Bool |false |Whether the domain is disabled. Value explanations are as follows:<br><br><br>* `false`: Not disabled.<br><br>* `true`: Disabled. |
|ForbiddenReason |String |DomainUnregistered |Reason for domain being banned. Value explanations are as follows:<br><br><br>* `Illegal`: Unauthorized use.<br><br>* `DomainUnregistered`: Domain not registered.<br><br>* `Other`: Other reasons. |
|CertId |String |cert\-9228928537e540f9a6a2fc844672\*\*\*\* |Certificate ID. |
|CertStatus |String |CertUnbound |Certificate status. Value explanations are as follows:<br><br><br>* `CertBound`: Certificate bound.<br><br>* `CertUnbound`: Certificate unbound.<br><br>* `CertExpired`: Certificate expired.<br><br>* `CertNotExist`: Certificate does not exist.<br><br>* `RoleNotExist`: Cross\-service authorization failed.<br><br>* `CertUnknown`: Certificate status unknown. |
|Protocol |String |tos |Explanation of the access protocol for custom domains is as follows:<br><br><br>* `tos`: tos protocol.<br><br>* `s3`: S3 protocol. |


<span id="eb9821f3"></span>
## **Sample request**

```JSON
GET /?customdomain HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="b9e63d9a"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 287

{
    "CustomDomainRules": [
        {
            "Domain": "examble.com",
            "Cname": "bucketname.tos-ap-southeast-1.bytepluses.com",
            "Forbidden": false,
            "ForbiddenReason": "",
            "CertId": "",
            "Protocol": "tos",
            "CertStatus": "CertUnbound"
        }
    ]
}
```
