---
title: "Download and installation"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Download_and_installation"
---

This topic describes how to download and install the Go SDK for RDS for SQL Server.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

Go 1.14 or a higher version is installed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can run the <code>go version</code> command to check your current Go version.</div>


<span id=".c2RrLeS4i-i9veWcsOWdgA=="></span>
## **SDK download address**

For the source code of the SQL Server Go SDK, see [SQL Server Go SDK](https://github.com/byteplus-sdk/byteplus-go-sdk-v2/tree/main/service/rdsmssql).

<span id=".5a6J6KOFLXNkaw=="></span>
## **Install the SDK**

In your target Go project, run the following command to install the Go SDK.

```Go
go get github.com/byteplus/byteplus-go-sdk-v2/byteplus/credentials
go get github.com/byteplus/byteplus-go-sdk-v2/byteplus/byteplusutil
```
