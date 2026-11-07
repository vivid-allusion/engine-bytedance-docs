---
title: "Viewing MCP service startup failure logs"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_logs_for_MCP_service_startup_failures"
---

When an MCP service fails to be created or published, you can view the startup failure logs to obtain the failure reason and identify configuration issues. These logs are useful for troubleshooting issues related to images, startup commands, environment variables, network connectivity, or backend dependency anomalies. This topic describes how to view the startup failure logs of an MCP service.

> **warning**

> This topic applies only to MCP services of the **deployment** integration type. When an MCP service is in the **Unavailable** state, you can view the publication failure logs of the MCP service. [Submit a ticket](https://console.byteplus.com/workorder/create) if support is required.

### Scenarios

* The MCP service is in the **Unavailable** state.

* A service created by deploying an MCP service fails to start.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Service" tab.

3. In the MCP service list, hover over "Unavailable" in the "Status" column of the target MCP service and click "View log".

4. In the "MCP service log" dialog box, view the reasons for MCP service publication failure.
