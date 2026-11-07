---
title: "安装 Python SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-python-sdk-zh-CN"
---

本主题介绍如何安装 Python SDK，并提供示例代码以帮助加快您的开发流程。

<span id="7005dd37"></span>
## **前提条件**


* 访问密钥：请参阅 [服务端 SDK 概述](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk-zh-CN)。

* 环境要求：需要 Python 3.5 或更高版本。如果您的系统尚未安装 Python，请访问 python.org 下载并安装适合的版本。

* 您还需要 pip，它是 Python 的包管理器。如果您的系统尚未安装 pip，请参阅 [pip 文档](https://pip.pypa.io/en/stable/getting-started/)获取安装说明。


<span id="f6bdf044"></span>
## 安装或升级 SDK

在终端中运行以下命令以安装最新版本的 Python SDK：

```Groovy
pip3 install --user byteplus-sdk
```


在终端中运行以下命令以升级到最新版本的 Python SDK：

```Python
pip3 install --upgrade byteplus-sdk
```


<span id="6215a314"></span>
## 设置访问密钥

要设置 **Access Key ID** 和 **Secret Access Key**，您可以采用以下任一方法：


* 将 `BYTEPLUS_ACCESSKEY` 环境变量设置为您的 **Access Key ID**，并将 `BYTEPLUS_SECRETKEY` 环境变量设置为您的 **Secret Access Key**。

* 调用 API 时传递 **Access Key ID** 和 **Secret Access Key**。示例代码如下。

   ```Python
   from byteplus_sdk.live.v20230101.live_service import LiveService
   service = LiveService()
       service.set_ak('Access Key ID')
       service.set_sk('Secret Access Key')
   ```
