---
title: "安裝 Go SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-golang-sdk-zh-TW"
---

本主題介紹如何安裝 Go SDK，並提供範例程式碼以協助加速您的開發流程。

<span id="b4fa9856"></span>
## 先決條件


* Access Key：請參閱[Server SDK 概述](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk-zh-TW)。

* 環境需求：需安裝 Go 1.13 或更高版本。如需下載與安裝 Go 編譯器、工具及函式庫的說明，請參閱[安裝文件](https://go.dev/doc/install)。


<span id="9ee0aef8"></span>
## 安裝或升級 SDK

請在終端機中執行以下指令，以安裝最新版 Go SDK：

```Python
go get github.com/byteplus-sdk/byteplus-sdk-golang
```


請在終端機中執行以下指令，以升級至最新版 Go SDK：

```Groovy
go get -u github.com/byteplus-sdk/byteplus-sdk-golang
```


<span id="fe00307b"></span>
## 設定 Access Key

若要設定**Access Key ID**與**Secret Access Key**，您可以採用以下任一方法：


* 將`BYTEPLUS_ACCESSKEY`環境變數設為您的**Access Key ID**，並將`BYTEPLUS_SECRETKEY`環境變數設為您的**Secret Access Key**。

* 呼叫 API 時傳入**Access Key ID**與**Secret Access Key**。範例程式碼如下。

   ```Go
   instance := live_v20230101.NewInstance()
   instance.SetCredential(base.Credentials{
           AccessKeyID: "Access Key ID",
           SecretAccessKey: "Secret Access Key",
   })
   ```
