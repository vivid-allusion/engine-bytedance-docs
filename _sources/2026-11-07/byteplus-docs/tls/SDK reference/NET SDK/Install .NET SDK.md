---
title: "Install .NET SDK"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Install_NET_SDK"
---

Before you use the BytePlus .NET SDK to call the TLS API and implement related features, you need to first install the .NET SDK. This article introduces the installation steps for the .NET SDK. 

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The access key (AccessKey) has been created and obtained.

* The access key (AccessKey) has full permissions for all APIs. It is recommended that you use IAM users to perform API\-related operations and daily maintenance. Before using IAM users, the main account must grant IAM users permissions for relevant TLS resources and operations.


<span id=".5YeG5aSH5byA5Y-R546v5aKD"></span>
## Prepare the development environment

.NET SDK is hosted on the NuGet platform. Please download and install it before beginning integration. 

<span id=".5a6J6KOFLXNkaw=="></span>
## Install the SDK

Go to the [NuGet](https://www.nuget.org/packages/VolcengineTls) official website, download the SDK, and install it.

```JSON
dotnet add package VolcengineTls --version 1.0.1
```
