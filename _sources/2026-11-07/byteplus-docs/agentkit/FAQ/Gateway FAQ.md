---
title: "Gateway FAQ"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Gateway_FAQ"
---

<span id="cNGyMkZB"></span>
## How to access MCP service?

You can view examples of integrating the MCP service into typical IDEs/CLIs in the MCP service details. For details, refer to [MCP service calling examples](https://docs.byteplus.com/en/docs/agentkit/MCP_services#JSLkeDYY) or [MCP toolset calling examples](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset#gPrq71Pl).

<span id="cpvbBTnk"></span>
## How to handle the 403 Forbidden error returned with the response body "RBAC: access denied" when I call the MCP service?

Use requests with a valid API KEY to access the MCP service.

<span id="WYCpGW4R"></span>
## Is SSE protocol access to the MCP service supported?

Currently, the SSE protocol is not supported. Streamable HTTP is recommended, due to the limits of the SSE protocol in reliability and ease of use.

<span id="1FZulqvR"></span>
## Is STDIO\-type remote access to the MCP service supported?

Yes. When you create an MCP service, selecting MCP service creation of the STDIO type will automatically enable conversion to the remote MCP.
