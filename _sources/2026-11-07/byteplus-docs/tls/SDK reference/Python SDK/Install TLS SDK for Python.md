---
title: "Install TLS SDK for Python"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/install_tls_sdk_for_python"
---

Before you use a Torch Log Service (TLS) SDK to perform operations, install the SDK. This topic describes how to install TLS SDK for Python.

<span id="前提条件"></span>
## Before you begin


* Create and get a BytePlus AccessKey pair.

* The AccessKey pair has the permissions to access all API actions, resulting in high risks. We recommend that you create and use an IAM user to call API actions or perform routine O&M. Before you perform operations as an IAM user, make sure that the IAM user is granted the permissions to operate TLS resources.


<span id="准备开发环境"></span>
## Preparing a development environment

Visit the [Python official website](https://www.python.org/downloads) to download and install the Python development environment, or use Conda to create a virtual Python environment.

TLS SDK for Python supports Python 3.5 and later. Run the following command to view your Python version:

```bash
python -V
```


<span id="安装-sdk"></span>
## Installing the SDK

Run a pip command to install TLS SDK for Python.

Run the following command to install the SDK:

```bash
pip install volcengine
```


The following output indicates that the SDK is installed as expected.

```bash
Successfully installed volcengine
```
