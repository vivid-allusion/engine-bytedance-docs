---
title: "Install TLS SDK for Go"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/install_tls_for_go"
---

Before you use Torch Log Service (TLS) SDK for Go to perform operations, install the SDK. This topic describes how to install TLS SDK for Go.

<span id="前提条件"></span>
## Before you begin


* Create and get a BytePlus AccessKey pair.

* The AccessKey pair has the permissions to access all API actions. We recommend that you use an IAM user to call API actions or perform routine O&M. Before you use an IAM user, use a BytePlus account to grant the IAM user the permissions to operate TLS resources.


<span id="准备开发环境"></span>
## Preparing a development environment

To download and install the Go development environment, visit the [Go official website](https://golang.org/doc/install/source).


* After you install the environment, create the GOPATH environment variable and set it to point to your code directory. For more information on GOPATH, run the `go help gopath` command.

* TLS SDK for Go supports Go 1.14 and later. Run the `go version` command to view your Go version.


<span id="安装sdk"></span>
## Installing TLS SDK for Go


1. Download TLS SDK for Go.

   ```go
   go get -u github.com/volcengine/volc-sdk-golang
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For Go 1.16 and later, we recommend that you run the <code>go install</code> command to download TLS SDK for Go.   </div>
   

2. Load TLS SDK for Go.

   ```go
   import (
           sdk "github.com/volcengine/volc-sdk-golang/service/tls"
           "github.com/volcengine/volc-sdk-golang/service/tls/pb"
   )
   ```
