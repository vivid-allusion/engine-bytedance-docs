---
title: "Data Plane API Calling Process"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Data_Plane_API_Calling_Process"
---

<span id="b1b40194"></span>
# Overview

This document provides an overview of the data plane API request process. Before using the API interface, you need to complete the following preparations.

It also introduces the public parameters of the response body for your reference when making API calls.

<span id="e9b09a74"></span>
# Calling Process

<span id="46bc82b8"></span>
## 1. Account Registration and Service Activation

Follow the [Account Registration and Service Activation](https://docs.byteplus.com/en/docs/VikingDB/Registering_an_account_and_activating_the_service) page to complete account registration and service activation.

<span id="246b6da6"></span>
## 2. AK/SK Key Acquisition

Before calling the various capabilities of the VikingDB vector database, ensure you have generated the Access Key.

Access Key includes Access Key ID (abbreviated as AK) and Access Key Secret (abbreviated as SK). Among them, AK is used to identify the user, and SK is used to verify the user's key. Please keep them secure.

AK/SK key acquisition methods are as follows. For more details, please refer to [Access Key (Key) Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).


1. Click [Key Management] in the dropdown box under the account name in the upper right corner to go to the corresponding page.

2. Click the [New Key] button to obtain AK/SK, which can be used as credentials to call the API.

3. 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38797f929fcc428d8e22264edea065ea~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For security reasons, it is recommended to create a sub\-account and use the sub\-account's AK/SK.</div>


<span id="70d5e739"></span>
## 3. Signature Generation

<span id="c560c854"></span>
### **What is a Signature?** 

A signature is an encoded string calculated in the API request, used for authentication and preventing data tampering.

<span id="f4ffa9f5"></span>
### **Can a signature be used permanently once obtained?** 

Unlike AK and SK, each request's signature is independent and temporary. A signature can only be used for one specific request and cannot be used permanently.

In the calling example below, **prepare_request** is the authentication function.

<span id="a526d21d"></span>
## 4. Calling Example (Using Python as an Example)

Example of calling the interface to point query in the dataset

```Python
      
"""
pip3 install volcengine
"""
import os

from volcengine.auth.SignerV4 import SignerV4
from volcengine.Credentials import Credentials
from volcengine.base.Request import Request
import requests, json

class ClientForDataApi:
    def __init__(self, ak, sk, host):
        self.ak = ak
        self.sk = sk
        self.host = host

    def prepare_request(self, method, path, params=None, data=None):
        r = Request()
        r.set_shema("https")
        r.set_method(method)
        r.set_connection_timeout(10)
        r.set_socket_timeout(10)
        mheaders = {
            'Accept': 'application/json',
            'Content-Type': 'application/json',
            'Host': self.host,
        }
        r.set_headers(mheaders)
        if params:
            r.set_query(params)
        r.set_host(self.host)
        r.set_path(path)
        if data is not None:
            r.set_body(json.dumps(data))
        credentials = Credentials(self.ak, self.sk, 'vikingdb', 'cn-beijing')
        SignerV4.sign(r, credentials)
        return r
        
    def do_req(self, req_method, req_path, req_params, req_body):
        req = self.prepare_request(method=req_method, path=req_path, params=req_params, data=req_body)
        return requests.request(method=req.method, url="http://{}{}".format(self.host, req.path),
                                  headers=req.headers, data=req.body, timeout=10000)

if __name__ == '__main__':
    client = ClientForDataApi(
        ak = "*",#Replace with your ak
        sk = "*",#Replace with your sk
        host = "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com",
    )
    req_method = "POST"
    req_params = None
    req_path = "/api/vikingdb/data/fetch_in_collection"
    req_body = {
        "collection_name": "my_collection",
        'ids': [1, 2, -1]
    }
    result = client.do_req(req_method=req_method, req_path=req_path, req_params=req_params, req_body=req_body)
    print("req http status code: ", result.status_code)
    print("req result: \n", result.text)
```


<span id="127e6f51"></span>
# Supported Domains and Regions

[Region and Endpoint](https://docs.byteplus.com/docs/undefined/68aecf6f817cd302c85e8ef4)


|**Region Name** |**Region ID** |**Public Network Domain Name** |**Private Network Connection Service Name (Non\-domain)**  |
|---|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |[api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com](http://api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com/) |com.bytepluses.privatelink.ap\-southeast\-1.vikingdb\-ann |


<span id="81aa6f1c"></span>
# Public Response Parameters


|Parameter Name |Type |Description |
|---|---|---|
|request_id |string |Request ID |
|code |string |Operation status code. A value of "Success" indicates a successful operation; otherwise, the value is an error code phrase in the format "Xxx" or "Xxx.Yyy". |
|message |string |Operation execution information. If the operation is successful, the message is "The API call was executed successfully."; otherwise, it contains error information. The message is a complete English sentence. |
|result |map |If the operation has no result or does not require a result, this field is null. |
