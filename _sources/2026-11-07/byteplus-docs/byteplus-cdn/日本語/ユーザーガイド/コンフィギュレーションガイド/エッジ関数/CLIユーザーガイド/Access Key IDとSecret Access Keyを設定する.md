---
title: "Access Key IDとSecret Access Keyを設定する"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-cli-login-jp"
---

このドキュメントでは、エッジ関数CLIを使用してAccess Key IDとSecret Access Keyを設定する方法について説明します。

<span id="手順"></span>
## 手順

`nest config set -g`コマンドを使用して、グローバルプロジェクト設定ファイルにAccess Key IDとSecret Access Keyを設定します。Access Key IDとSecret Access Keyは[BytePlus Console](https://console.byteplus.com/iam/keymanage)から取得できます。

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


グローバルプロジェクト設定ファイルに設定されたAccess Key IDとSecret Access Keyは、現在のデバイス上のすべての関数プロジェクトに適用されます。
