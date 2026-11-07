---
title: "设置您的 Access Key ID 和 Secret Access Key"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-cli-login-cn"
---

本文档介绍如何使用边缘函数 CLI 设置您的 Access Key ID 和 Secret Access Key。

<span id="操作步骤"></span>
## 操作步骤

使用 `nest config set -g` 命令在全局项目配置文件中设置 Access Key ID 和 Secret Access Key。您可以从 [BytePlus 控制台](https://console.byteplus.com/iam/keymanage)获取 Access Key ID 和 Secret Access Key。

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


在全局项目配置文件中设置的 Access Key ID 和 Secret Access Key 适用于您当前设备上的所有函数项目。
