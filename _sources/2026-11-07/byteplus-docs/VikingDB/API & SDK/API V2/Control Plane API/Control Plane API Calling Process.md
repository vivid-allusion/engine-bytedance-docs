---
title: "Control Plane API Calling Process"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Control_Plane_API_V2"
---

<span id="005a63fe"></span>
# Overview

This document introduces the control plane API calling process. Before using the API interface, you need to complete the following preparations.

It also includes a complete Python code example to help you make your first successful API call.

<span id="25825a04"></span>
# Calling Process

<span id="b39b9eb3"></span>
## 1. Account Registration and Service Activation

Follow the [Account Registration and Service Activation](https://docs.byteplus.com/en/docs/VikingDB/Registering_an_account_and_activating_the_service) page to complete account registration and service activation.

<span id="2b97c982"></span>
## 2. AK/SK Key Acquisition

Before calling the various capabilities of the VikingDB vector database, ensure you have generated the Access Key.

Access Key includes Access Key ID (abbreviated as AK) and Access Key Secret (abbreviated as SK). Among them, AK is used to identify the user, and SK is used to sign requests to verify the user's identity. Store them securely.

AK/SK key acquisition methods are as follows. For more details, please refer to [Access Key (Key) Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).


1. Click [Key Management] in the dropdown box under the account name in the upper right corner to enter the corresponding page.

2. Click the [New Key] button to obtain AK/SK, which can be used as credentials to call the API.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38797f929fcc428d8e22264edea065ea~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For security reasons, it is recommended to create a sub\-account and use the sub\-account's AK/SK.</div>


<span id="c2a46713"></span>
## 3. Signature Generation

<span id="8f229a10"></span>
### **What is a Signature?** 

Signature is an encoded string calculated by the client for an API request, used for authentication and preventing data tampering.

<span id="e0777216"></span>
### **Can a signature be used permanently once obtained?** 

Unlike ak and sk, each request's signature is independent and temporary. A signature can only be used for one specific request and cannot be used permanently.

The following example shows the complete process, from authentication to making a request.

<span id="b8c4332f"></span>
## 4. Calling Example (Using Python as an Example)

Example: Viewing dataset details

```Python
import os
import datetime
import hashlib
import hmac
from urllib.parse import quote

import requests, json

def norm_query(params):
    query = ""
    for key in sorted(params.keys()):
        if type(params[key]) == list:
            for k in params[key]:
                query = (
                        query + quote(key, safe="-_.~") + "=" + quote(k, safe="-_.~") + "&"
                )
        else:
            query = (query + quote(key, safe="-_.~") + "=" + quote(params[key], safe="-_.~") + "&")
    query = query[:-1]
    return query.replace("+", "%20")

def hmac_sha256(key: bytes, content: str):
    return hmac.new(key, content.encode("utf-8"), hashlib.sha256).digest()

def hash_sha256(content: str):
    return hashlib.sha256(content.encode("utf-8")).hexdigest()

class ClientForConsoleApi:
    def __init__(self, ak, sk, host, region):
        self.ak = ak
        self.sk = sk
        self.host = host
        self.region = region
        self.service_code = "vikingdb"
        self.version = "2025-06-09"

    def request(self, method, action, body, query=None, header=None):
        if query is None:
            query = {}
        if header is None:
            header = {}
        credential = {
            "access_key_id": self.ak,
            "secret_access_key": self.sk,
            "service": self.service_code,
            "region": self.region,
        }
        request_param = {
            "body": json.dumps(body),
            "host": self.host,
            "path": "/",
            "method": method,
            "content_type": 'application/json',
            "date": datetime.datetime.utcnow(),
            "query": {"Action": action, "Version": self.version, **query},
        }
        if body is None:
            request_param["body"] = ""
        x_date = request_param["date"].strftime("%Y%m%dT%H%M%SZ")
        short_x_date = x_date[:8]
        x_content_sha256 = hash_sha256(request_param["body"])
        sign_result = {
            "Host": request_param["host"],
            "X-Content-Sha256": x_content_sha256,
            "X-Date": x_date,
            "Content-Type": request_param["content_type"],
        }
        signed_headers_str = ";".join(
            ["content-type", "host", "x-content-sha256", "x-date"]
        )
        canonical_request_str = "\n".join(
            [request_param["method"].upper(),
             request_param["path"],
             norm_query(request_param["query"]),
             "\n".join(
                 [
                     "content-type:" + request_param["content_type"],
                     "host:" + request_param["host"],
                     "x-content-sha256:" + x_content_sha256,
                     "x-date:" + x_date,
                 ]
             ),
             "",
             signed_headers_str,
             x_content_sha256,
             ]
        )

        hashed_canonical_request = hash_sha256(canonical_request_str)
        credential_scope = "/".join([short_x_date, credential["region"], credential["service"], "request"])
        string_to_sign = "\n".join(["HMAC-SHA256", x_date, credential_scope, hashed_canonical_request])

        k_date = hmac_sha256(credential["secret_access_key"].encode("utf-8"), short_x_date)
        k_region = hmac_sha256(k_date, credential["region"])
        k_service = hmac_sha256(k_region, credential["service"])
        k_signing = hmac_sha256(k_service, "request")
        signature = hmac_sha256(k_signing, string_to_sign).hex()

        sign_result["Authorization"] = "HMAC-SHA256 Credential={}, SignedHeaders={}, Signature={}".format(
            credential["access_key_id"] + "/" + credential_scope,
            signed_headers_str,
            signature,
        )
        header = {**header, **sign_result}
        r = requests.request(method=method,
                             url="https://{}{}".format(request_param["host"], request_param["path"]),
                             headers=header,
                             params=request_param["query"],
                             data=request_param["body"],
                             )
        return r.status_code, r.headers, r.json()

if __name__ == '__main__':
    client = ClientForConsoleApi(
        ak = "*",#Replace with your ak
        sk ="*" ,#Replace with your sk
        host="vikingdb.ap-southeast-1.byteplusapi.com",
        region="cn-hongkong"
    )
    http_code, _, result_json = client.request(
        method="POST",
        action="GetVikingdbCollection",
        body={
            "CollectionName": "my_collection",
        }
    )
    print("req http status code: ", http_code)
    print("req result: \n", result_json)


    
```


<span id="63a141f1"></span>
# Supported Domains and Regions

[Region and Endpoint](https://docs.byteplus.com/docs/undefined/68aecf6f817cd302c85e8ef4)


|**Region Name** |**Region ID** |**Public Network Domain Name** |**Private Network Connection Service Name (Non\-domain)**  |
|---|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |[vikingdb.ap-southeast-1.byteplusapi.com](http://vikingdb.ap-southeast-1.byteplusapi.com/) |com.bytepluses.privatelink.ap\-southeast\-1.api.vikingdb |


Public Request Parameters


|Parameter |Type |Required |Location |Description |
|---|---|---|---|---|
|Action |String |Yes |Request parameter query |The operation to be performed, such as CreateVikingdbCollection. See the documentation for the specific operation for details. |
|Version |String |Yes |Request parameter query |API version, fixed value: 2025\-06\-09. |


<span id="a4468924"></span>
# Public Response Body Parameters

A successful response includes the ResponseMetadata and Result objects.


|Parameter Name |First\-level Sub\-parameter |Type |Description |
|---|---|---|---|
|ResponseMetadata | |Map |Response metadata |
||RequestId |String |Request ID |
||Action |String |Requested operation, example: CreateVikingdbCollection. |
||Version |String |API version, fixed value 2025\-06\-09. |
||Service |String |Target service identifier, fixed value vikingdb |
||Region |String |Service region, such as cn\-beijing |
|Result | |Map |If the operation does not return a result, this field is null. |


An error response only returns ResponseMetadata, which includes an Error object containing error information.


|Parameter Name |First\-level Sub\-parameter |Second\-level Sub\-parameter |Type |Description |
|---|---|---|---|---|
|ResponseMetadata | | |Map |Response metadata |
||RequestId | |String |Request ID |
||Action | |String |Requested operation, example: CreateVikingdbCollection. |
||Version | |String |API version, fixed value 2025\-06\-09. |
||Service | |String |Target service identifier, fixed value vikingdb |
||Region | |String |Service region, such as cn\-beijing |
||Error | |Map |Error information |
|||Code |String |The value of this parameter is the specific error code. You can look up this error code in the documentation to find a solution. |
|||Message |String |The message describes the specific reason for the error and can be used for troubleshooting. |
