---
title: "Client initialization"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Python_Client_initialization"
---

The Cloud Search Service Python client provides a series of APIs for interacting with the Cloud Search Service and managing resources. You need to initialize the Python client before sending HTTP/HTTPS requests to the Cloud Search service. This topic describes how to initialize the Cloud Search Python client.

<span id="OEeNaIJ3"></span>
## Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* You have obtained the Access Key ID (AK) and Secret Access Key (SK) for your account. For details, refer to [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).

* You have obtained the regions supported by Cloud Search. For details, refer to [Service endpoints](https://docs.byteplus.com/en/docs/cloudsearch/request-structure#request-method).

* You have downloaded and installed the Cloud Search Python SDK. For details, refer to [Download and installation](https://docs.byteplus.com/en/docs/cloudsearch/Python_Download_and_installation).


<span id="LCiBK12O"></span>
## Initialize the client

Initialize the client with the following code.

```Python
import byteplussdkcore
import byteplussdkescloud as escloud_sdk
from byteplussdkcore.rest import ApiException

if __name__ == "__main__":
    config = byteplussdkcore.Configuration()
    config.ak = "Your AK"
    config.sk = "Your SK"
    config.region = "Your Region"
    try:
        escloud_api = byteplussdkescloud.ESCLOUDApi(byteplussdkcore.ApiClient(config))
    except ApiException as e:
        print("Exception: %s\n" % e)
```
