---
title: "Downloading and installing SDK"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Downloading_and_installing_SDK_go"
---

This article describes how to download and install the Go SDK.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Go 1.5 or above is required, and Go 1.12 or above is recommended.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can execute the <code>go version</code> command to check the current Go version information.</div>


<span id=".c2RrLeS4i-i9veWcsOWdgA=="></span>
## SDK download address

For the source code address of the Go SDK, see [BytePlus SDK for Go](https://github.com/byteplus-sdk/byteplus-go-sdk-v2/tree/main/service/vedbm).

<span id=".5a6J6KOFLXNkaw=="></span>
## Install the SDK

In the target Go project, execute the following command to install the Go SDK.

```shell
go get github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/credentials
go get github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/byteplusutil
```
