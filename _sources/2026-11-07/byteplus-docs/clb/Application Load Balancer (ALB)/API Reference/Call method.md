---
title: "Call method"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-Signature-method"
---

## Request structure

To call BytePlus ALB OpenAPI, you send a request to the specified service address, which must include BytePlus signature information and the business information required by the specific API. The structure of an API request for BytePlus ALB includes the following:

* Service address.

* Communication protocol.

* Request method.

* Request parameters.

* Character encoding.

### Service endpoint

The table below lists the service endpoints for the ALB OpenAPI.

|**Region** |**Region ID** |**Service access address** |
|---|---|---|
|China (Beijing) |cn\-beijing |alb.cn\-beijing.byteplusapi.com.cn |
|China (Shanghai) |cn\-shanghai |alb.cn\-shanghai.byteplusapi.com.cn |
|China (Guangzhou) |cn\-guangzhou |alb.cn\-guangzhou.byteplusapi.com.cn |
|China (Hongkong) |cn\-hongkong |alb.cn\-hongkong.byteplusapi.com |
|Asia Pacific (Johor) |ap\-southeast\-1 |alb.ap\-southeast\-1.byteplusapi.com |
|Asia Pacific (Jakarta) |ap\-southeast\-3 |alb.ap\-southeast\-3.byteplusapi.com |

> **warning**

> In the request examples provided in each API documentation, alb.cn\-beijing.byteplusapi.com.cn is used uniformly. When calling the API, please replace the service endpoint with the one corresponding to the actual region where your resources reside.

### Communication protocols

Requests must be sent using the `HTTPS` protocol.

### Request method

See the specific requirements of each API for request methods. The OpenAPI for BytePlus ALB only supports GET requests.

**Precautions**

* When using the GET method, the common request parameters `Action` and `Version` must be included in the Query String.

* For GET requests, all parameters must be URL\-encoded.

### Request parameters

ALB OpenAPI requests contain two types of parameters: **Common request parameters** and **API request parameters**.

* Common request parameters, included in every API call. For details, see [Common parameters](https://docs.byteplus.com/en/docs/42/65787#.5YWs5YWx5Y-C5pWw).

* API request parameters are unique to each API. See the specific API descriptions for details.

### Character encoding

Requests and responses are encoded using the `UTF-8` character set.

## Common parameters

* Common request parameters are parameters that must be included in every API request. If an API request lacks a common request parameter, the request fails.

* The first letter of each common request parameter is capitalized to distinguish it from other request parameters. Common request parameters are divided into URI parameters and signature parameters.

### **URI parameters**

URI parameters must be included in the query string.

|**Name** |**Type** |**Required** |**Format** |**Notes** |**Example** |
|---|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |API name, which is interface\-specific and indicates the operation to be performed. |CreateLoadBalancer |
|Version |String |Yes |YYYY\-MM\-DD |API version information. |2020\-04\-01 |
|X\-Expires |Integer |No |900 |Indicates the validity period of the signature, in seconds. The default value is 900. |300 |

### **Signature parameters**

Every API request must include signature parameters. Signature parameters can be included in the query string as URI parameters or in the request headers.

#### Use case for Request Headers

If signature parameters are included in the request headers, the following parameters must be included.

|Name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |Indicates the UTC time of the signature, accurate to the second. For example, `20201103T104027Z` |
|Authorization |String |Yes |Indicates the signature value.<br><br>```json```<br>```HMAC-SHA256 Credential = {AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}```<br> |

The meaning of the information in the Authorization example is as follows:

|**Name** |**Type** |**Description** |**Example** |
|---|---|---|---|
|AccessKey |string |The AccessKey ID of your BytePlus account, which can be obtained from the [Secret management](https://console.byteplus.com/iam/keymanage/) page. |`AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZkYzE` |
|ShortDate |String |The time of the request, in UTC, accurate to the day. |20210913 |
|Region |String |Request region. |`cn-beijing` |
|Service |String |The name of the service being requested. |alb |
|SignedHeaders |String |The request headers involved in the signature. Separate request headers with semicolons. |`host;x-content-sha256;x-date` |
|Signature |String |A computed signature. |For more information about signatures, see [Signature mechanism](https://docs.byteplus.com/en/docs/42/65787#.562-5ZCN5py65Yi2). |

#### **Including signature parameters in query string**

If signature parameters are included in the query string, the following parameters must be included.

|Name |Type |Required |Description |Example |
|---|---|---|---|---|
|X\-Date |String |Yes |Indicates the UTC time of the signature, accurate to the second. |`20210913T081805Z` |
|X\-Algorithm |String |Yes |Indicates the signature algorithm. This parameter has a fixed value. |`HMAC-SHA256` |
|X\-Credential |String |Yes |Consist of {AccessKey}/{ShortDate}/{Region}/{Service}/request. |\- |
|X\-SignedHeaders |String |Yes |The request headers involved in the signature. Separate request headers with semicolons. |`host;x-content-sha256;x-date` |
|X\-Signature |String |Yes |A computed signature. |For more information about signatures, see [Signature mechanism](https://docs.byteplus.com/en/docs/42/65787#.562-5ZCN5py65Yi2). |

## Signature mechanism

To ensure the legitimacy of the requester's identity and protect the request from being maliciously tampered with during transmission, the BytePlus signature mechanism requires the requester to compute a hash value of the request parameters, encrypt it, and send it together with the API request to the server. The server will perform the same signature calculation on the received request and compare it with the signature provided by the requester. If the signature fails verification, the request will be rejected. For more information, see [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature).

## Response structure

A successful API request returns an HTTP status code of 200. When an API request fails, any of the following situations may occur:

* An HTTP status code of 4xx​ or 5xx.

* The response body's ResponseMetadata structure containing an Error field.

### Successful API request response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "CreateLoadBalancer",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    }, 
    "Result": {
        "RequestId": "20210811152539010225146063030****",
        "LoadBalancerId": "alb-bp1o94dp5i6ea****"
    }
}
```

### API **failed request response example**

```json
{
    "ResponseMetadata": {
        "RequestId": "20220420160740010225243081041DFBF1",
        "Action": "CreateLoadBalancer",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing",
        "Error": {
            "Code": "InvalidParameter.LoadBalancerName",
            "Message": "The ALB name is invalid"
        }
    }
}
```

Compared with the response of a successful request, the response of a failed request no longer contains the `Result` section, and an Error field additionally appears in `ResponseMetadata`. The field is explained as follows:

|Field |Notes |
|---|---|
|Error |Error indicates that this request failed. |
|Code |Code contains the specific error code. You can use the error code to search the documentation and resolve the issue yourself. |
|CodeN |CodeN is a numeric ID identifying the error code, which helps with troubleshooting. Only some interfaces provide CodeN. |
|Message |Message describes the specific cause of the error to assist your troubleshooting. |
|RequestId |RequestId is the unique identifier of each API request. If you encounter a problem that cannot be resolved on your own, you can contact us through the ticket system and provide the request ID. We will assist with troubleshooting. |
