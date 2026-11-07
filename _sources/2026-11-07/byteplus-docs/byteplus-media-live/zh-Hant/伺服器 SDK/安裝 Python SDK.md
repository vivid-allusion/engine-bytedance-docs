---
title: "安裝 Python SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-python-sdk-zh-TW"
---

本主題介紹如何安裝 Python SDK，並提供範例程式碼以協助加速您的開發流程。

<span id="7005dd37"></span>
## **先決條件**


* Access Key：請參閱[Server SDK 概述](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk-zh-TW)。

* 環境需求：需安裝 Python 3.5 或更高版本。若尚未安裝 Python，請前往 python.org 下載並安裝適用的版本。

* 您還需要 pip，這是一個 Python 的套件管理工具。若尚未安裝 pip，請參閱[pip 文件](https://pip.pypa.io/en/stable/getting-started/)以取得安裝說明。


<span id="f6bdf044"></span>
## 安裝或升級 SDK

請在終端機中執行以下指令，以安裝最新版的 Python SDK：

```Groovy
pip3 install --user byteplus-sdk
```


請在終端機中執行以下指令，以升級至最新版的 Python SDK：

```Python
pip3 install --upgrade byteplus-sdk
```


<span id="6215a314"></span>
## 設定 Access Key

若要設定**Access Key ID**與**Secret Access Key**，可採用以下任一方法：


* 將`BYTEPLUS_ACCESSKEY`環境變數設為您的**Access Key ID**，並將`BYTEPLUS_SECRETKEY`環境變數設為您的**Secret Access Key**。

* 呼叫 API 時傳入**Access Key ID**與**Secret Access Key**。範例程式碼如下。

   ```Python
   from byteplus_sdk.live.v20230101.live_service import LiveService
   service = LiveService()
       service.set_ak('Access Key ID')
       service.set_sk('Secret Access Key')
   ```
