---
title: "MCP protocol version compatibility"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/MCP_protocol_version_compatibility"
---

The MCP protocol version defines how clients and servers communicate, including message format, capability declaration, initialization method, and invocation behavior. When calling an MCP service or MCP toolset, you need to select a protocol version supported by both sides to establish communication.

<span id="0VQGArT3"></span>
## Supported MCP protocol versions

Different protocol versions may differ in their interaction pattern. For example, compared to earlier versions, `MCP 2026-07-28` has evolved to adopt a stateless invocation model better suited for gateway and serverless scenarios. Therefore, it differs from earlier versions in initialization, session persistence, and multi\-turn interaction. The MCP protocol version defines message format, capability declaration, initialization method, and invocation behavior. Streamable HTTP is a message transport mechanism. The two are distinct concepts. When access is currently provided over Streamable HTTP, clients still need to select the appropriate MCP protocol version based on what they support.


|**MCP service** |**MCP toolset** |
|---|---|
|* **`2026-07-28`**<br><br>* **`2025-11-25`**<br><br>* **`2025-06-18`**<br><br>* **`2025-03-26`** |* **`2026-07-28`**<br><br>* **`2025-11-25`**<br><br>* **`2025-06-18`**<br><br>* **`2025-03-26`** |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Full return, semantic retrieval, and tag retrieval are the tool matching methods of MCP toolsets and do not represent different MCP protocol versions.</div>


<span id="xmbXVU66"></span>
## MCP 2026\-07\-28 protocol compatibility

AgentKit MCP now supports MCP protocol version `2026-07-28`. You can still use earlier protocol versions to call MCP services and MCP toolsets.

**For existing MCP services and MCP toolsets, the following minimal\-effort compatibility approach is available**: No changes are required to existing MCP services. Simply add them to an MCP toolset to access new protocol capabilities through the toolset.

<span id="kcWxBnDS"></span>
### **New protocol compatibility rules for existing MCP toolsets**

**Compatibility logic for existing MCP toolsets**


* **No impact on existing toolsets**: When calling an MCP toolset using the MCP `2026-07-28` stateless protocol, you can access tools already in the toolset without needing to consider the protocol each tool actually uses. Existing call methods remain available.

* **Downstream tool compatibility**: MCP toolsets support adding downstream tools that use either stateful or stateless invocation. When calling an MCP toolset, the client does not need to be aware of the protocol or session mechanism used by the downstream tools.

* **Client adaptation requirements**: Clients can access an MCP toolset using either stateful or stateless invocation. To switch to the MCP 2026\-07\-28 protocol, only the client's invocation logic needs to be adjusted based on the protocol. No changes are required to the protocols used by existing tools in the MCP toolset.

* **MRTR tool invocation requirements**: To call a tool that supports Multi\-Round\-Trip Requests (MRTR), the client must use the MCP 2026\-07\-28 protocol to send requests to the MCP toolset.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Whether MRTR is supported depends on the capabilities of the target tool.   </div>
   

<span id="8w0C7Bbr"></span>
### **Adaptation requirements for MCP services in different scenarios**

**Compatibility logic for existing MCP services**

Existing MCP services are not automatically updated to a new protocol version. Protocol support is determined by the backend logic you implement. To call an existing MCP service using the MCP 2026\-07\-28 protocol, choose one of the following methods:


* **Method 1**: Call the existing MCP service directly. Adapt the service based on how it was created.

* **Method 2**: No adaptation is required. Simply add the MCP service to an MCP toolset and call tools in the existing MCP service through the toolset using the new protocol. MCP toolsets provide broader compatibility with the new protocol than direct calls to MCP services.


**Adaptation requirements by creation method**


* **Deployed MCP service**

   1. To call an existing MCP service deployed using an image with the new protocol, you need to first adapt the image to support the new protocol and publish it.

   2. In the AgentKit console, go to the MCP service list and click the name of the target MCP service. On the **Basic information** tab, click "Edit" in the "Backend service" section.

   3. Click the image input field, select the adapted and published image, and click "Confirm". The image is updated, and a rolling restart is triggered to apply the changes.

* **Imported MCP service**: To call an imported MCP service using the new protocol, you need to adapt the backend service to support the new protocol yourself. Once the adaptation is complete, you can call tools in the MCP service using the new protocol.

* **HTTP\-to\-MCP service**: To call an existing HTTP\-to\-MCP service using the new protocol, no additional adaptation is required. You can call it directly.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>The protocol plugin update mechanism is as follows:</strong>   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Existing HTTP\-to\-MCP services</strong>: Protocol plugins are not updated automatically. The system automatically updates the plugin only when you add, delete, or modify an MCP conversion rule on the MCP\-type dedicated gateway. If no changes are made, the plugin version remains unchanged.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Newly created HTTP\-to\-MCP services</strong>: The latest plugin version is used by default, with built\-in support for both old and new protocols.   </div>
   


<span id="CdqI7G9n"></span>
## MCP 2026\-07\-28 stateless mechanism

Under the MCP **`2026-07-28`** protocol, the protocol layer adopts a stateless invocation model:


* The initialization handshake using initialize and notifications/initialized is no longer used.

* Mcp\-Session\-Id is no longer used to maintain protocol\-level sessions.

* Each request must independently carry the protocol version, client capabilities, and the context information required for the current call. The server cannot rely on the same connection or previous requests to recover the client's protocol version, capabilities, or business context.


<span id="0PyvQXxK"></span>
### How stateless invocation works for MCP services

MCP **`2026-07-28`** adopts a stateless invocation model at the protocol layer. Clients no longer perform the initialization handshake using initialize and notifications/initialized or use Mcp\-Session\-Id to maintain protocol\-level sessions.

Each request must independently carry the protocol version, client capabilities, and the context information required for the current call. The server cannot rely on the same connection or previous requests to recover the client's protocol version, capabilities, or business context.


* #### Send stateless requests <span id="UBBxoW7I"></span>

   When an MCP service is called over Streamable HTTP, each JSON\-RPC request must be handled as an independent request.

   * The request header must carry the following:

      * `MCP-Protocol-Version`: The MCP protocol version.

      * `Mcp-Method`: The method to call.

      * `Mcp-Name`: The target name or URI. Required when calling methods that include a target name or URI, such as `tools/call`, `resources/read`, or `prompts/get`.

   * The `params._meta` field in the request body must carry the following:

      * `io.modelcontextprotocol/protocolVersion`

      * `io.modelcontextprotocol/clientCapabilities`

      We recommend that you also include `io.modelcontextprotocol/clientInfo`. The protocol version, method name, and target name in the request header must be consistent with the corresponding fields in the request body.

* #### Discover service capabilities <span id="f7BKqDPl"></span>

   Clients can call `server/discover` to obtain the protocol versions, capability declaration, server information, and cache hints supported by the server. `server/discover` is used only for discovering service capabilities. It is not an initialization handshake and does not create a protocol\-level session.

* #### Preserve business state across requests <span id="MVCVz3b4"></span>

   If an MCP service needs to preserve business process context, external system operation progress, or temporary task state across multiple calls, the tool should return an explicit handle, task ID, or state identifier, and the client should pass it in subsequent requests as a regular parameter.

   In MRTR scenarios, the server can return the following:

   * `resultType` set to `input_required`: A status flag indicating that the server sets `resultType` to `input_required` to tell the client that the current task is not complete and requires more information. When `resultType` is set to `complete`, the task is complete.

   * `inputRequests`: A list of instructions telling the client what is needed, such as asking the user to fill in a parameter, confirm an action, or provide the result of a certain capability.

   * Optional `requestState`: A context checkpoint. The server packages the current processing progress into an opaque string for the client to include in the next retry, so the server knows where it left off. Not all tools have intermediate state that needs to be saved.

   After collecting the required input, the client resends the original request with the results carried in `inputResponses` and passes back `requestState as-is`. The server must re\-verify on each call whether the current caller has permission to access the relevant state, and must avoid implicitly binding business state to an HTTP connection or protocol session.

   For earlier MCP protocol versions, clients must still follow the initialization and session mechanisms of the corresponding version. The platform can handle requests of different protocol versions within its compatibility range, but clients must not mix message formats from different versions.


<span id="K8fP4IsO"></span>
### How stateless invocation works for MCP toolsets

Under the MCP **`2026-07-28`** protocol, MCP toolsets use a per\-request self\-describing stateless model for tool discovery and tool invocation. Clients do not need to perform an initialization handshake using `initialize` and `notifications/initialized`, and do not rely on `Mcp-Session-Id` to maintain protocol\-level sessions.

Each tools/list or tools/call request must independently carry the protocol version, client capabilities, authentication information, and business parameters required for the current call. Authentication information typically comes from the HTTP authentication context, such as the Authorization request header, rather than from clientInfo.


* #### Send stateless requests <span id="u4ugKbqQ"></span>

   When an MCP toolset is called over Streamable HTTP, each JSON\-RPC request must be handled as an independent request.

   * The request header must carry the following:

      * `MCP-Protocol-Version`: The MCP protocol version.

      * `Mcp-Method`: The method to call.

      * `Mcp-Name`: The name of the tool to call. Required only when a specific tool is invoked.

   * The `params._meta` field in the request body must carry the following:

      * `io.modelcontextprotocol/protocolVersion`

      * `io.modelcontextprotocol/clientCapabilities`

   We recommend that you also include `io.modelcontextprotocol/clientInfo`. The protocol version, method name, and tool name in the request header must be consistent with the corresponding fields in the request body.

* #### Retrieve accessible tools <span id="sxCiOaw8"></span>

   The MCP toolset determines the set of tools accessible for the current request based on the request's authentication information, project permissions, toolset configuration, and routing context. The tool list may change based on authorization scope, toolset configuration, backend MCP service status, or tool sync results, but must not depend on previous requests in the same HTTP connection.

   When the underlying tools have not changed, the tool list should remain stable. Clients can cache the tool list and reuse it in model context based on caching hints such as `ttlMs` and `cacheScope`.

   The following describes how different tool invocation patterns work:

   * **Full return**: The client calls `tools/list` to retrieve the list of tools that can be invoked directly in the MCP toolset. When the toolset aggregates tools from multiple MCP services, tool names may be disambiguated to avoid naming conflicts across services.

   * **Semantic retrieval**: `tools/list` may return entry tools such as `mcp_search_tool` and `mcp_use_tool`. The client first calls `mcp_search_tool` to retrieve candidate tools' `server_id`, `server_name`, `tool_id`, `tool_name`, and parameter structures based on the task description, then calls `mcp_use_tool` with the target tool information explicitly provided to complete the invocation.

   * **Tag retrieval**: `tools/list` may return entry tools such as `mcp_list_tools_by_tags` and `mcp_use_tool`. The client first filters candidate tools by tag, then calls `mcp_use_tool` with the target tool information explicitly provided to complete the invocation.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Semantic retrieval</strong> and <strong>tag retrieval</strong> are tool\-matching mechanisms of MCP toolsets, not protocol session state defined by MCP <code>2026-07-28</code>. Clients must re\-include the target tool information as regular parameters in subsequent <code>tools/call</code> requests.   </div>
   

* #### Preserve business state across requests <span id="0YC372hT"></span>

   If a tool invocation needs to preserve business process context, external system operation progress, or temporary task state across multiple requests, the tool should return an explicit handle, task ID, or state identifier, and the client should pass it in subsequent requests as a regular parameter.

   In MRTR scenarios, use `resultType`, `inputRequests`, `inputResponses`, and the optional `requestState` to complete multi\-turn interactions. The server must re\-verify on each call whether the current caller has permission to access the relevant state.


<span id="4O24769F"></span>
## MCP 2026\-07\-28 MRTR flow

MRTR handles scenarios where a single request cannot be completed immediately, and the server needs user input, user confirmation, or additional information from the client. In MCP `2026-07-28`, MRTR replaces the interaction pattern in earlier protocol versions where the server sent independent requests over an SSE connection. The core signal of MRTR is `resultType`, which indicates the processing status of a tool invocation result:


* `complete`: The tool invocation has completed.

* `input_required`: The tool has not finished executing and requires user input, user confirmation, or additional information from the client.


<span id="AAKZmS9L"></span>
### How MRTR works

The MRTR flow is as follows:


1. The client sends a `tools/call`, `resources/read`, or `prompts/get` request.

2. The server returns `resultType` with a value of `input_required` and uses `inputRequests` to describe the input or actions the client needs to complete.

3. After completing the required input or actions, the client resends the original request with a new JSON\-RPC `id` and includes the results in `inputResponses`.

4. If the server returned `requestState`, the client must pass it back as\-is in the retry request.

5. The server continues processing after receiving the required information:

   * When processing is complete, it returns `resultType` with a value of `complete`.

   * If additional information is still required, it can return `input_required` again, and the client repeats the flow above.


`requestState` is an opaque string generated by the server to recover request context. The client must not parse, modify, or guess its content, or use it for other requests. The server must validate the integrity, ownership, expiry, and original request information of `requestState` to prevent state tampering and cross\-user or cross\-request replay attacks.

The server can only request capabilities that the client has declared support for via `clientCapabilities`. For example, if the client has not declared the `Elicitation` capability, the server must not require the client to perform `elicitation/create`.

<span id="f1u9EuTE"></span>
### Additional notes on MCP toolsets

In **semantic retrieval** and **tag retrieval** modes, `mcp_use_tool` supports invoking one or more backend tools in a single request:


* If a backend tool returns `input_required`, the MCP toolset returns the corresponding `inputRequests` and `requestState` to the client.

* If multiple backend tools require input at the same time, the MCP toolset merges the pending input requests and ensures that request identifiers do not conflict.

* After providing the required input, the client must send a new, independent `tools/call` request with the original `requestState` unchanged and the corresponding `inputResponses`.
