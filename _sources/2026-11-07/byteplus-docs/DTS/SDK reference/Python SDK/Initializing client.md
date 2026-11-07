---
title: "Initializing client"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/client_initialization"
---

The DTS Python client provides a series of interfaces to interact with the Database Transmission Service (DTS) service and manage DTS Database resources. You need to initialize the DTS Python client before you can send HTTP/HTTPS requests to the Database Transmission Service (DTS). This topic describes how to initialize the DTS Python client.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* The DTS Python SDK has been downloaded and installed. Refer to [Download and install SDK](https://docs.byteplus.com/en/docs/DTS/downloading_and_installing_an_sdk) for specific steps.

* The following information has been obtained:

   * The Access Key ID (AK) and Secret Access Key (SK) information of the account. For instructions on how to obtain AKSK information, refer to [Viewing AKSK information](https://docs.byteplus.com/en/docs/byteplus-platform/reference-access-key).

   * Region information. For the Regions supported by DTS, refer to [Service address](https://docs.byteplus.com/en/docs/DTS/request_structure#.5pyN5Yqh5Zyw5Z2A).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## **Initialize client**

Initialize the client with the following code.

```python
import json

from volcengine.dts.dts_service import DtsService
if __name__ == '__main__':
    access_key = 'your_ak_here'
    secret_key = 'your_sk_here'
    region_str = 'region_str_here'

    dts_service = DtsService(region=region_str)
    dts_service.set_ak(access_key)
    dts_service.set_sk(secret_key)
```
