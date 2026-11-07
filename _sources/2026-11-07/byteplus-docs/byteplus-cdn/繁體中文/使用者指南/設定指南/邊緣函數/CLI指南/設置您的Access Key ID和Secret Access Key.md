---
title: "設置您的Access Key ID和Secret Access Key"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-cli-login-cn-zh-tw"
---

本文檔介紹如何使用邊緣函數 CLI 設定您的 Access Key ID 和 Secret Access Key。

<span id="操作步驟"></span>
## 操作步驟

使用 `nest config set -g` 指令在全域專案設定檔中設定 Access Key ID 和 Secret Access Key。您可以從 [BytePlus 控制台](https://console.byteplus.com/iam/keymanage)獲取 Access Key ID 和 Secret Access Key。

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


在全域專案設定檔中設定的 Access Key ID 和 Secret Access Key 適用於您當前裝置上的所有函數專案。
