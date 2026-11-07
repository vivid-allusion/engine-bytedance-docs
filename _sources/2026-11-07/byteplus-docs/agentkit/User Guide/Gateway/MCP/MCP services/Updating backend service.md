---
title: "Updating backend service"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_backend_service"
---

The backend service of an MCP service is responsible for processing business logic and executing specific functions. If an MCP service's backend service address, protocol, access method, or API configuration changes, you can update the backend service configuration in the console to point the MCP service to the correct business service. This topic describes how to update the backend service of an MCP service.

<span id="sVKZWafm"></span>
### Scenarios


* The backend service is migrated to a new address, port, or access path.

* After the backend API is upgraded, you need to update the associated MCP service configuration accordingly.

* The original backend service is unavailable, and you need to switch to a new service instance.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Modifying the backend service configuration triggers a rolling restart of related instances. <strong>Brief service unavailability or fluctuations in request processing may occur during the restart</strong>. We recommend performing this operation during off\-peak hours and notifying affected callers in advance.</div>


<span id="rgjN85z4"></span>
## Prerequisites


* An MCP service has been created. For more information, see [Creating an MCP service](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

* A new backend service configuration has been prepared, and the backend service has been confirmed accessible.

* If the MCP service uses private network access, make sure that the backend service, VPC, subnet, and access allowlist configurations match.


<span id="7508GDx7"></span>
## Procedure


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Service" tab.

3. In the MCP service list, click the name of the target service. On the "Basic information" tab, click "Edit" next to "Backend service".

4. On the "Edit backend service" page, update the service configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The method for modifying the backend configuration is similar to that for creating the backend configuration. For parameter details, see <strong>Backend configuration</strong> in <a href="https://docs.byteplus.com/en/docs/agentkit/MCP_services">Creating an MCP service</a>.   </div>
   

5. Click "Confirm". After the update is complete, view the inbound identity authentication information on the MCP service details page. The information is updated to the new configuration.
