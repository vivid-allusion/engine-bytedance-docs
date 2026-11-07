---
title: "API release notes"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/API-change-records"
---

<span id=".MjAyNeW5tDAx5pyI"></span>
## September 2025


|API |Release note |Associated features |
|---|---|---|
|CreateDirectConnectHealthCheck |Added a new error code: `InvalidDirectConnectHealthCheck.SubnetAZNotSupported`. |Create a health check |
|ModifyDirectConnectHealthCheckProbeAttributes |Updated a request parameter: `DirectConnectHealthCheckProbeName`. |Modify a health check |
|DeleteDirectConnectHealthCheckProbes |Added a new error code: `InvalidDirectConnectHealthCheckProbe.InvalidProbe`. |Delete a health check |
|* CreateDirectConnectVirtualInterface<br><br>* ModifyDirectConnectVirtualInterfaceAttributes<br><br>* AllocateDirectConnectVirtualInterface |* Added a new request parameter: `EnableBfdEcho`.<br><br>* Modified the description of a request parameter (`EnableBfd`).<br><br>* Added new error codes: `InvalidDirectConnectVirtualInterface.BfdBfdEchoBothEnabled`, `InvalidDirectConnectVirtualInterface.NqaBfdEchoBothEnabled`, and `InvalidDirectConnectVirtualInterface.BfdEchoForbidden`. |* Create a DC Virtual Interface/Shared Virtual Interface<br><br>* Modify a DC Virtual Interface |
|* DescribeDirectConnectVirtualInterfaceAttributes<br><br>* DescribeDirectConnectVirtualInterfaces |* Added a new response parameter: `EnableBfdEcho`.<br><br>* Modified the description of a response parameter (`EnableBfd`). |Query a DC Virtual Interface |
