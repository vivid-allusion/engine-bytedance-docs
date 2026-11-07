---
title: "Python SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-python-sdk"
---

This article introduces how to install the Python SDK and provides code examples to help you accelerate your development process.

<span id="7005dd37"></span>
## **Prerequisites**


* Access key, refer to [Server SDK overview](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk#get-access-key).

* Environmental requirements: Python 3.5 or a higher version required. If you don't have Python installed, visit python.org to download and install the appropriate version.

* You also need pip, which is a package manager for Python. If you don't have pip installed, visit the [pip documentation](https://pip.pypa.io/en/stable/getting-started/) for instructions on how to install it.


<span id="f6bdf044"></span>
## Installing or Upgrade the SDK

In terminal, run the following command to install the latest version of the Golang SDK:

```Groovy
pip3 install --user byteplus-sdk
```


In terminal, run the following command to upgrade the current version to the latest version of the Golang SDK:

```Python
pip3 install --upgrade byteplus-sdk
```


<span id="6215a314"></span>
### Setting the Access key

To set the **Access Key ID** and **Secret Access Key**, you can use either of the following methods:


* Set the environment variables `BYTEPLUS_ACCESSKEY` as **Access Key ID** and `BYTEPLUS_SECRETKEY` as **Secret Access Key**.

* Pass the **Access Key ID** and **Secret Access Key** when calling the API. The code sample is as follows:

   ```Python
   from byteplus_sdk.live.v20230101.live_service import LiveService
   service = LiveService()
       service.set_ak('Access Key ID')
       service.set_sk('Secret Access Key')
   ```
