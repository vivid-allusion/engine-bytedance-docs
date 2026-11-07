---
title: "MCP troubleshooting"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/MCP_troubleshooting"
---

This topic describes common issues, possible causes, and solutions for Model Context Protocol (MCP) services and MCP toolsets in AgentKit. It covers scenarios including creation, connection, invocation, private network access, quotas, billing, and protocol compatibility. You can refer to the relevant scenario to troubleshoot issues on your own.

## Failure to create an MCP service or an MCP toolset

### MCP service remains in the "**Creating**" state for an extended period

**Symptom description**

After an MCP service is created, the status remains at "**Creating**" for an extended period. Under normal conditions, creation may take approximately 7 to 8 minutes. If the process has not completed after 30 minutes, it should be treated as "**Abnormal**".

**Possible causes**

* Underlying resources are still being created, and initialization has not been completed.

* An error occurred during MCP service deployment.

**Troubleshooting steps**

1. After creating an MCP service, wait 7 to 8 minutes, then refresh the page to update the MCP service list. Check whether the service status has changed to "**Running**".

2. If the status changes to "**Unavailable**" after refreshing, you can view the failure logs. This method applies only to MCP services created using the "Deploy MCP service" method.

   1. If the MCP service status becomes "Unavailable" after the page refreshes, hover over the status and click "View log".

   2. Search for the keyword "error" in the logs to locate the issue.

   3. Resolve the issue based on the log error message and retry. If you cannot resolve it on your own, record the service name, creation time, and current status. Then contact BytePlus technical support.

3. Query failure logs via OpenAPI.

   Call [GetMCPService](https://docs.byteplus.com/en/docs/agentkit/GetMCPService_-_Queries_MCP_service_details?lang=en) to query the MCP service status. In some deployment failure scenarios, the failure log URL is returned in the FailedLogFileUrl field.

4. If the service remains in the "**Creating**" state after 30 minutes and none of the above steps resolve the issue, record the service name, creation time, and current status. Then contact BytePlus technical support.

### MCP service status shows "Unavailable" after creation

**Symptom description**

An MCP service fails to be created in the console, and the service status is displayed as "**Unavailable**".

**Possible causes**

During MCP deployment, GitHub\-related dependency packages need to be pulled over the public network. If the pull takes more than **2** minutes due to network issues, MCP service creation may fail.

**Troubleshooting steps**

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).  In the MCP service list, find the service with the "**Unavailable**" state. If the MCP service was created using the "Deploy MCP service" method, hover over the status and click "View log". In the logs, check whether there is a message indicating that the dependency package pull timed out.

2. Create the MCP service again. This step addresses intermittent failures, and the issue may be resolved after retrying.

3. If the issue persists after multiple retries, record the service name, creation time, and log information. Then contact BytePlus technical support.

### MCP tool API file parsed successfully, but "Internal error" appears after confirmation

**Symptom description**

When you create an MCP tool, the API file is parsed successfully, but an "Internal error" message appears after you confirm the creation.

**Possible causes**

The uploaded API file does not meet specifications or has formatting issues.

**Troubleshooting steps**

1. Confirm that the API file uploaded when creating the MCP tool is a valid Swagger 2.0 or OpenAPI 3.0 file. For detailed requirements, see [MCP service API file specifications and examples](https://docs.byteplus.com/en/docs/agentkit/MCP_service_API_file_specifications_and_examples?lang=en).

2. Confirm that the uploaded file is in the `.json`, `.yaml`, or `.yml` format, and that the file size does not exceed **5** MiB.

   > **warning**

   > Do not upload Word documents, PDFs, HTML files, or general Markdown files.

3. If the uploaded file meets all the above requirements but the "Internal error" message still appears, record the operation time, file format, file size, and error message. Then contact BytePlus technical support.

## Failed to connect to an external MCP server

### Connection fails after creating an MCP service using a third\-party address

**Symptom description**

When you create an MCP service using a third\-party address, the connection fails or the service is unavailable. Alternatively, the network is reachable but MCP calls cannot be completed.

**Possible causes**

* A third\-party regular REST API address was entered instead of a standard MCP server address.

* The configured protocol, domain name, port, or path does not match the actual server information.

* The MCP transport protocol is inconsistent with the protocol supported by the server.

* The public network backend has DNS resolution, TLS certificate, or network access issues.

* The backend requires an API key, token, or custom header, but outbound credentials are not configured correctly.

* The connection test in the console is blocked by the browser's Cross\-Origin Resource Sharing (CORS) policy.

* The service experienced a brief error and recovered on its own.

**Troubleshooting steps**

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).  In the MCP service list, check the service status. If the MCP service was created using the "Deploy MCP service" method, hover over the status and click "View log". Then check the logs and identify the cause.

2. Confirm that the backend address of the MCP service is the complete MCP server address provided by the third party, not a regular REST API address.

3. Verify the protocol, domain name, port, and path in the backend address one by one to confirm the configuration is correct. If any configuration error is found, modify the backend service configuration on the details page.

4. Confirm whether the transport protocol selected for the MCP service is consistent with the protocol actually supported by the backend. An inconsistency may cause the MCP service to be unavailable. If any configuration error is found, modify the backend service configuration on the details page.

5. If the backend uses a public network address, check the following:

   * Whether DNS resolves correctly.

   * Whether the TLS certificate is valid and the certificate domain name matches the access domain name.

   * Whether the backend allows public network access.

6. If the backend requires authentication, configure the corresponding credentials in the backend outbound credentials of the MCP service.

7. If HTTP 401 or 403 is returned, check whether the outbound credentials are missing, incorrect, or expired. Then confirm that the header name and authentication prefix meet the backend requirements.

8. Initiate the call again and confirm that the backend returns an MCP protocol response rather than a regular REST API response. For more configuration details, see [MCP service documentation](https://docs.byteplus.com/en/docs/agentkit/MCP_services?lang=en).

9. If the issue still cannot be resolved, record the operation time, file format, file size, and error message. Then contact BytePlus technical support.

## Troubleshoot private network access issues

### Private network MCP service cannot access the target ECS instance

**Symptom description**

The MCP service is configured to use VPC access, but it cannot access an ECS instance in the same VPC. Alternatively, users may assume that enabling private network access automatically allows access to all ECS instances and ports within the VPC.

> **tip**

> If the gateway that the MCP service belongs to is a dedicated gateway, the MCP network configuration follows that dedicated gateway.

**Possible causes**

Enabling private network access only establishes the network conditions for accessing resources within the VPC. It does not automatically allow access to all ECS instances and ports. Actual connectivity also depends on security groups, network ACLs, system firewalls, and the service listening address and port configuration.

**Troubleshooting steps**

1. Confirm that the MCP service and the target ECS instance are in the same VPC, or that a usable network connection exists between them.

2. Check the inbound rules of the target ECS instance's security group. Allow the protocols and ports required for MCP service access as needed.

3. Check the subnet network ACL to confirm that the corresponding inbound or outbound traffic is not blocked.

4. Check the system firewall of the target ECS instance to confirm that the target port is allowed.

5. Check whether the backend service has started and is listening on an address and port accessible to other resources within the VPC.

6. Verify the backend configuration based on how the MCP service was created:

   * **Deploy MCP service**: The deployed code can access network\-reachable and allowed resources within the VPC.

   * **Import MCP service or HTTP to MCP**: You need to explicitly select a function, container, ECS instance, and port, or configure a fixed domain name as the backend.

7. Allow only the target ECS instances and ports required for your business, and verify whether the connection is restored.

8. If none of the above steps resolve the issue, record the error message, network configuration, and other relevant information. Then contact BytePlus technical support.

### Private domain name cannot be resolved

**Symptom description**

The MCP service cannot resolve or access an internal domain name.

**Possible causes**

Internal domain name resolution is only valid for resources within a BytePlus VPC. The client may not be in the corresponding VPC, or the domain resolution chain may not have taken effect.

**Troubleshooting steps**

1. Confirm that the client is in the corresponding BytePlus VPC or has access to it through an available network link.

2. First, use the target IP address and port to verify network connectivity.

3. If the network is reachable but the domain name still cannot be resolved, temporarily add a mapping between the domain name and the target IP address to the hosts file on the client.

4. Retry the connection and verify whether the service is available.

   > **warning**

   > Manually modifying the hosts file is only suitable for temporary verification. For domain resolution and maintenance in production environments, confirm the approach based on your actual network architecture.

5. If none of the above steps resolve the issue, contact BytePlus technical support.

###

## Troubleshoot MCP tools that are not loaded or unresponsive

### Harness Runtime shows tools: []

**Symptom description**

An MCP service and toolset have been created, and the MCP toolset has been associated with Harness Runtime via `--mcp-toolset-id`. However, the ADK agent in the runtime logs shows **tools: []**  , and MCP tools are not loaded.

**Possible causes**

The current public beta version of Harness does not yet support MCP tools. Running `agentkit runtime update --mcp-toolset-id` only establishes the association at the runtime level. It does not automatically inject MCP tools into the agent created inside Harness.

**Troubleshooting steps**

1. Check whether you are using the public beta version of Harness.

2. [Check the runtime logs](https://docs.byteplus.com/en/docs/agentkit/Viewing_runtime_instance_logs?lang=en). If the ADK agent continues to show **tools: []** , tool injection cannot be completed by running `agentkit runtime update --mcp-toolset-id` again.

3. If your application requires MCP tools, temporarily switch to an agent runtime mode that already supports MCP tool loading. Wait for the general availability release of Harness to provide MCP tool support.

## Handle insufficient quota

### MCP calls return a quota exceeded or insufficient quota error

**Symptom description**

The MCP service or MCP toolset can no longer be called. The page or logs indicate insufficient quota.

**Possible causes**

* **Shared gateway**: The MCP quota for the current account or project has been exhausted.

* **Dedicated gateway**: The quota supported by the current dedicated gateway specification has been exhausted. Upgrade the gateway specification.

**Troubleshooting steps**

* **Dedicated gateway quota exhausted**: Upgrade the gateway specification. For detailed instructions, see [Changing dedicated gateway instance specifications](https://docs.byteplus.com/en/docs/agentkit/Changing_gateway_instance_specifications).

* **Shared gateway quota exhausted**: The shared gateway is better suited for PoC and development testing. For production environments, we recommend using a dedicated gateway. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Gateway_modes_and_MCP_request_counting_rules?lang=en)

   1. Go to the BytePlus Quota Center to view the current usage and limits for MCP\-related quotas. For default quota values, see [Limits](https://docs.byteplus.com/en/docs/agentkit/Limits?lang=en).

   2. After confirming that you have reached the quota limit, submit a quota increase request. Wait for approval and confirm that the new quota has taken effect. Then retry the MCP call to verify that the service is restored.

   3. If you cannot increase the quota on your own, contact your account manager.

## MCP request counting and billing

### A single tool call generates request records on both the toolset and service sides

**Symptom description**

After you call an MCP toolset, request counts appear for both the MCP toolset and its associated MCP service. After connection to a dedicated gateway, the gateway records more requests than the tool call QPS.

**Possible causes**

When the MCP toolset receives a request, it accesses the associated MCP service to complete the tool call. As a result, a single business request is recorded once on the MCP toolset side and once on the MCP service side. Each count is included in the corresponding usage statistics separately.

For scenarios using a dedicated gateway, the actual number of requests handled by the gateway is **twice** the tool call QPS. For example, if the toolset accesses the MCP service at 10 QPS, the dedicated gateway handles 20 requests per second.

**Troubleshooting steps**

1. Check the request usage of the MCP toolset and the MCP service separately. Do not mistake the counts on both sides for a duplicate billing issue.

2. When evaluating the dedicated gateway specification, estimate the actual gateway request volume as **twice** the tool call QPS. For detailed information, see [MCP request counting rules](https://docs.byteplus.com/en/docs/agentkit/MCP_request_counting_rules?lang=en).

3. If the tool call QPS is 10, verify the dedicated gateway's capacity and monitoring data against 20 requests per second.

4. If the actual request volume significantly exceeds this figure, cross\-check by accounting for requests generated by periodic connections.

5. If the numbers still do not match expectations, contact BytePlus technical support.

> **warning**

> The request counting logic is the same for shared gateways and dedicated gateways. Dedicated gateways additionally provide gateway\-level monitoring data and QPS configuration for the gateway specification.
