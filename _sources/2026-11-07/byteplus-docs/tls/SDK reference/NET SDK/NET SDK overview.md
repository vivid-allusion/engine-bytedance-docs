---
title: ".NET SDK overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DotNET_SDK_overview"
---

The BytePlus TLS .NET SDK encapsulates common interfaces of TLS, allowing you to call server\-side APIs through the TLS .NET SDK to implement log collection and log query functionality. 

<span id=".54mI5pys6K-05piO"></span>
## Description

For the update log and version notes of the TLS .NET SDK, please refer to [GitHub](https://github.com/volcengine/ve-tls-dotnet-sdk). We recommend that you choose the latest version of the SDK to experience updated product capabilities and more stable service. 

<span id=".56S65L6L6aG555uu"></span>
## Example project

.NET SDK provides a wide range of sample projects for your reference, including common log sending scenarios. For detailed information, please refer to the GitHub source code.


|GitHub source code |Description |
|---|---|
|[ProducerExample.cs](https://github.com/volcengine/ve-tls-dotnet-sdk/blob/master/VolcengineTls.Examples/ProducerExample.cs) |Example code for the implementation class that sends logs using the Producer pattern. |
|[Program.cs](https://github.com/volcengine/ve-tls-dotnet-sdk/blob/master/VolcengineTls.Examples/Program.cs) |Example code for the entry class for sending logs in Producer mode. |
|[PutLogExample.cs](https://github.com/volcengine/ve-tls-dotnet-sdk/blob/master/VolcengineTls.Examples/PutLogExample.cs) |Example code for sending logs by calling the PutLogs API. |
|[PutLogV2Example.cs](https://github.com/volcengine/ve-tls-dotnet-sdk/blob/master/VolcengineTls.Examples/PutLogV2Example.cs) |Example code for sending logs using an API call to the PutLogsV2 interface |
