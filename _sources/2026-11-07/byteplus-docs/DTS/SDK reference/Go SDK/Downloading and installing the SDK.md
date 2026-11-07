---
title: "Downloading and installing the SDK"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Downloading_and_installing_the_SDK"
---

This topic describes how to download and install the DTS Go SDK.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Go 1.5 or above is required, and Go 1.12 or above is recommended.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can execute the <code>go version</code> command to check the current Go version information.</div>


<span id=".c2RrLeS4i-i9veWcsOWdgA=="></span>
## SDK download address

Refer to [DTS Go SDK](https://github.com/volcengine/volc-sdk-golang) for the source code address of the DTS Go SDK.

<span id=".5a6J6KOFLXNkaw=="></span>
## Install the SDK

Run the following command in the target Go project to install the Go SDK.

```go
go get github.com/volcengine/volcengine-go-sdk/volcengine/credentials
go get github.com/volcengine/volcengine-go-sdk/volcengine/volcengineutil
```
