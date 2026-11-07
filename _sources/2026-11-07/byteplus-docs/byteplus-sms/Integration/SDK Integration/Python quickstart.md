---
title: "Python quickstart"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-python-quickstarts"
---

Use BytePlus SDK for Python to call SendSms API so that you can send a text message to a group of recipients by using an example file.

<span id="56a52d5d"></span>
## Prerequisites


* Python 3.0 or later.

* Pip is installed.

   Pip is a package manager for Python that makes it easier to install the libraries you need.

* Have generated AK (Access Key) and SK (Secret Key).

   If you haven't generated AK/SK yet, go to [BytePlus Console](https://console.byteplus.com/auth/login/) \> **User Profile** \> **IAM** \> **Key Management** \> **Create New Access Key**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each BytePlus account can have maximum 2 pairs of AK/SK at the same time.   </div>
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/c6a93e2-AKSK.png) </span>


<span id="ca450b84"></span>
## Downloading SDK for Python

The SDK for Python provides an example project file called [example_send_sms.py](https://github.com/byteplus-sdk/byteplus-sdk-python/tree/master/byteplus_sdk/example/sms) for you to quickly call SendSms API.

To download the SDK, follow the steps:


1. Go to [BytePlus SDK for Python](https://github.com/byteplus-sdk/byteplus-sdk-python).

2. In the upper right corner, click **Code** \> **Download ZIP**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/da1604a-Py.png) </span>


<span id="14918746"></span>
## Installing the SDK

In the terminal window, run the following command to install BytePlus SDK for Python.

```python
pip3 install --user byteplus_sdk
```


Setting up authentication

Open the example file [example_send_sms.py](https://github.com/byteplus-sdk/byteplus-sdk-python/tree/master/byteplus_sdk/example/sms).

To set up authentication by AK/SK, fulfill your AK and SK in the example file as shown below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This is the recommended way to set up authentication.</div>


```python
iam_service.set_ak('your ak')
iam_service.set_sk('your sk')
```


Alternatively, you can also fulfill your AK and SK in the environment variable setting as shown below.

```python
BYTEPLUS_ACCESSKEY="your ak"  
BYTEPLUS_SECRETKEY="your sk"
```


Otherwise, you can fulfill your AK and SK by creating a JSON file under ～/.byteplus/config as shown below.

```python
{"ak":"your ak","sk":"your sk"}
```


<span id="3f6ba323"></span>
## Sending text messages using SendSms API


1. Fulfill the parameters in the body section of the example file **example_send_sms.py** as shown below. To understand the parameters, refer to [SendSms](https://docs.byteplus.com/byteplus-sms/docs/sendsms).


```python
# coding:utf-8
from __future__ import print_function

import json

from byteplus_sdk.sms.SmsService import SmsService
from byteplus_sdk.const.Const import *

if __name__ == '__main__':
    # oversea
    sms_service = SmsService(REGION_AP_SINGAPORE1)

    # cn
    # sms_service = SmsService()

    # call below method if you don't set ak and sk in $HOME/.volc/config
    sms_service.set_ak('AK0000')
    sms_service.set_sk('SK0000==')

    body = {
        "SmsAccount": "19cb0000",
        "From": "BytePlus",
        "TemplateID": "SPT_1ba0000",
        "TemplateParam": "{\"code\": \"43133\",\"time\": \"10\"}",
        "PhoneNumbers": "+6500000000",
        "Tag": "tag",
    }
    resp = sms_service.send_sms(body)
    print(resp)
```



2. In the terminal window, run the following command.


```python
python3 example_send_sms.py
```


<span id="a1d9509f"></span>
## Result

After the text message is sent, you will receive a success message containing a MessageID in the response.
