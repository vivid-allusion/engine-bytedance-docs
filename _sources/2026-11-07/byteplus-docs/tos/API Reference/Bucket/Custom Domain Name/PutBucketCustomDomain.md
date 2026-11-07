---
title: "PutBucketCustomDomain"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Putbucketcustomdomain"
---

<span id="3f55122a"></span>
## **Feature Description**

You can bind a custom domain to a bucket using PutBucketCustomDomain. Once bound, you can access resources within the bucket through this domain.

<span id="5af819b4"></span>
## Precautions


* To call this API, you must be the owner of the bucket or be authorized with PutBucketCustomDomain permission for the current bucket.

* A maximum of 20 domain names can be set.

* After binding a custom domain, you need to add DNS resolution to your domain, setting the CNAME to the bucket's external access domain name for the custom domain to take effect.


<span id="5388f529"></span>
## **Request syntax**

```JSON
PUT /?customdomain HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: 89
{
   "CustomDomainRule": {
      "Domain": "example.com",
      "CertId": "certID"
   }
}
```


<span id="a6a32656"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|customdomain |Query |String |Yes |\- |Represents a special identifier for the PutBucketCustomDomain request. |


<span id="955bb5eb"></span>
## **Request body elements**


|**Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|CustomDomainRule |Container |Yes |\- |Set custom domain name information. |
|Domain |String |Yes |example.com |The custom domain name needing binding.<br><br>Parent node: CustomDomainRule |
|CertId |String |No |cert\-9228928537e540f9a6a2fc844672\*\*\*\* |Certificate ID.<br><br>Parent Node: CustomDomainRule |
|Protocol |String |No |tos |Access protocol for the custom domain, with the following values:<br><br><br>* `tos`: TOS protocol.<br><br>* `s3`: S3 protocol. |


<span id="5ce1fc71"></span>
## Response headers

This request returns the common response message headers, please see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="8a5a000b"></span>
## **Response body elements**

There is no message element in this request response.

<span id="8cc927d6"></span>
## **Sample request 1**

```JSON
PUT /?customdomain HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: 64

{
   "CustomDomainRule": {
      "Domain": "example.com",
      "Protocol": "tos"
   }
}
```


<span id="ef7b3ecb"></span>
## **Sample response1**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
```


<span id="8b52dcd0"></span>
## **Sample request 2**

```JSON
PUT /?customdomain HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: 89

{
   "CustomDomainRule": {
      "Domain": "example.com",
      "CertId": "certID"
   }
}
```


<span id="9a6cd340"></span>
## **Sample response 2**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
```
