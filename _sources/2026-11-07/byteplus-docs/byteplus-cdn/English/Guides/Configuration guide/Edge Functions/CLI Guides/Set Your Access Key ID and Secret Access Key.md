---
title: "Set Your Access Key ID and Secret Access Key"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-cli-login-en"
---

This document describes how to use the Edge Functions CLI to set your access key ID and secret access key.

<span id="steps"></span>
## Steps

Use the `nest config set -g` command to set your access key ID and secret access key in the global project configuration file. You can obtain your access key ID and secret access key from the [BytePlus Console](https://console.byteplus.com/iam/keymanage).

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


The access key ID and secret access Key set in the global project configuration file apply to all function projects on your current device.
