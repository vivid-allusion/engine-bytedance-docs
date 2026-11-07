---
title: "Deleting MCP services"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Deleting_MCP_services"
---

If an MCP service is no longer used, you can delete it in the AgentKit console. Before deletion, confirm that no agents, CLIs, or external systems are still calling the service to avoid service call failures after deletion. This topic describes how to delete an MCP service.

## Scenarios

* An MCP service created for testing has been verified and no longer needs to be retained.

* A service has been migrated to a new MCP service instance, and the old service can be retired.

* An MCP service created by mistake needs to be cleaned up.

> **danger**

* > A deleted MCP service cannot be recovered. After deletion, agents, IDEs, CLIs, or external systems that depend on the service will no longer be able to call the associated tools. Before proceeding, confirm that all callers have switched away from the service or stopped using it.

* > An MCP service may be associated with a dedicated gateway and configured as an effective resource for a gateway credential transformation plugin rule. If you delete such an MCP service, the system automatically removes it from "Effective resource" in all associated plugin rules.

## Prerequisites

* An MCP service has been created. For more information, see [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

* You have confirmed that the MCP service is no longer used by any business process, agent, or external client.

* If you need to retain the configuration, record the service name, network configuration, inbound authentication method, backend service configuration, and tool list before deleting the service.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Service" tab.

3. In the MCP service list, find the target service and click "Delete" in the "Actions" column.

4. In the dialog box, confirm that the operation is correct, and then click "Delete". The system indicates "Deleted successfully," meaning the target MCP service has been deleted.
