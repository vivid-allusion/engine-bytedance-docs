---
title: "Installing the Go SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Install-the-go-sdk"
---

This article provides the download link and installation instructions for the TOS Go SDK.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before installing the SDK, you must first install Golang version 1.13 or later. You can visit [the Golang official website](https://go.dev/) to download the installation package.

After installation is complete, you can use the `go version` command to view the version information.

<span id=".c2RrLeS4i-i9veWcsOWdgA=="></span>
## SDK Download Link


* Latest source code address: [Source code address](https://github.com/volcengine/ve-tos-golang-sdk)

* Revision History: [Version Record](https://github.com/volcengine/ve-tos-golang-sdk/blob/main/CHANGELOG.md)

* Historical Version Address: [Historical Version](https://github.com/volcengine/ve-tos-golang-sdk/releases)


<span id=".5a6J6KOF5pa55byP"></span>
## Installation Method

The TOS Go SDK is managed using go mod. If go mod has not been initialized in your local project, you can run the following command to initialize it.

```go
go mod init example
```


After initializing go mod locally, run the following command to install the latest version of the SDK.

```go
go get -u github.com/volcengine/ve-tos-golang-sdk/v2
```


After installation is complete, run the following command to check the SDK version.

```go
package main

import (
   "fmt"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
   fmt.Println("TOS GO SDK Version: ", tos.Version)
}
```
