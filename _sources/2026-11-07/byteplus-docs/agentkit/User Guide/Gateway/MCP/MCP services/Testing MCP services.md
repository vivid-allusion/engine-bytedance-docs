---
title: "Testing MCP services"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Testing_MCP_service"
---

After an MCP service is created and started, you can use the testing feature to verify that the service is running properly and to test the parameters of specific MCP tools. Testing helps ensure that tool behavior meets expectations. This topic describes how to test an MCP service.

> **warning**

* > **Network information**: Public network domain name testing is available to all users. Private network domain name testing is currently in **Beta**and can be used only after it is enabled. To request access, contact your account manager.

* > **Billing note**: Operations on the Test tab, such as connection tests, tool retrieval, and tool calls, follow the same logic as calling an MCP service or MCP toolset through code. **All of these operations go through the gateway and count toward the usage of the corresponding billing items**. Control the testing frequency to avoid unexpected charges. For more information about billing rules, see [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items).

## Prerequisites

* An MCP service has been created. For more information, see [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

* (Optional) If you use a private network domain name for MCP testing, ensure that your local machine is connected to the target VPC through Direct Connect, VPN, or another method and can resolve the private network domain name. Otherwise, the connection test will fail. If your local machine is not configured to forward DNS requests to the BytePlus private DNS, you can enable public network resolution for the private network domain name.

   * **For private network connection configuration, see** [Direct Connect - Best practices](https://docs.byteplus.com/en/docs/directconnect/best-practices-overview?lang=en).

   * **Enable public network resolution for private domain names**: Configure based on the gateway mode to which the MCP service belongs. For more information, see [Enabling or disabling public network resolution for private domains](https://docs.byteplus.com/en/docs/agentkit/Enabling_or_disabling_public_network_resolution_for_private_domains).

## Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> MCP integration", and click the "MCP Service" tab.

3. In the service list, click the name of the target service, click the "Test" tab, and verify the tools in the MCP service as prompted.

   * **Step 1**: In the "Select a domain name and then access it for testing" step, click "Connection test". "Domain name" and "API Key" or "Access Token" are automatically populated. No input is required.

      * **Domain name**: Select the domain name for accessing the MCP service to be tested. If the MCP service supports both a public domain name and a private domain name, select either one.

      * **API Key/Access Token**: Inbound identity authentication for the MCP service.

      * **Identity authentication token**: If an MCP service uses only the Identity authentication plugin, configure the "Token Header" and "Token Value" fields during testing. The method for obtaining the Token Value is as follows:

         1. Go to the [User management](https://console.byteplus.com/agentkit/region:agentkit+cn-beijing/identity?pageSize=10&currentPage=1) page and click the name of the target user pool.

         2. On the "Client" tab, click a client name whose "Client type" is **Web application**.  and other client types do not currently support token retrieval.

         3. On the details page, click "Login test" in the upper\-right corner and log in using any authorized method.

         4. After a successful login, go to the **Token information** section on the login test result page and copy the `id_token` or `access_token` as the Token Value.

   * **Step 2:**  In the "Select the tool to be tested" step, select the tool to test. For details about the tools, see the tool descriptions in the console.

   * **Step 3:**  In the "Enter parameters for testing" step, enter the testing parameters as needed and click "Testing tool" to complete the operation.

4. View the test result.

   * If **Test succeeded** is displayed, the tools in the MCP service can be connected as expected.

   * If **Test failed** appears, the MCP service cannot connect to the tool. Follow the error message to troubleshoot and test again.
