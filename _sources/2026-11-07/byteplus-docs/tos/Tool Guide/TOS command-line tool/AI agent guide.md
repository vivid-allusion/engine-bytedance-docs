---
title: "AI agent guide"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/AI_agent_guide"
---

You can add ve\-tos\-cli as a skill to AI agents to enable them to fully manage TOS operations based on standardized capability descriptions, command invocation, and result parsing. This topic explains how to do so.

<span id="f5e618a2"></span>
## Six design principles


* Discoverability (`help`/`capabilities`/`describe`): It exposes the command structure through standardized interfaces that support automatic discovery.

* Understandability: It provides clear parameter descriptions, risk prompts, examples, and API metadata.

* Safe execution (`dry-run` + confirmation): It supports preview mode and secondary confirmation mechanisms to reduce the risk of misoperation.

* Controlled output (structured output with four sections): The output follows a four\-section structure to ensure predictable, parsable results.

* Deterministic errors (stable `envelope` + exit codes): Error messages use a stable `envelope` format with standard exit codes for programmatic handling.

* Agent ecosystem (skills/MCP): It is compatible with skills and MCP for seamless integration into the agent ecosystem.


<span id="167801ff"></span>
## Recommended workflow

```Bash
ve-tos-cli capabilities --view compact --output json          # Discover
ve-tos-cli object upload --describe --output json             # Read contracts
ve-tos-cli rm tos://b/p/ --recursive --dry-run --output json  # Preview
ve-tos-cli ls tos://b/p/ --output json --query "data.objects[].key"  # Execute + retrieve values
```


<span id="9a368960"></span>
## Structured output (envelope)


|Field |Description |
|---|---|
|success/status |Indicates whether the request succeeded:<br><br><br>* `success`: Execution succeeded.<br><br>* `false`: Execution failed. |
|command |The canonical command path for this operation, such as `ve-tos object upload`. It can be copied and re\-executed directly. |
|request_id / status_code / ec |Request unique identifier/HTTP status code/error code for troubleshooting. |
|data |The result of executing the command. The structure varies by command type. |
|pagination |Pagination information, which includes `next_token`, `next_marker`, and `total_returned`. |
|error |Error details. The following subfields are provided:<br><br>`code`, `message`, `exit_code`, `kind`, `category`, `suggested_action`, `fix_command`, `doctor_hint`, and `docs_url`. |


<span id="4344fc4c"></span>
## Deterministic exit codes


|Exit code |Description |Category |Description |
|---|---|---|---|
|0 |Success |Success |Command executed successfully with no errors. |
|1 |Unknown |Unknown |Unknown error, usually caused by unexpected exceptions. |
|2 |AuthFailed |AuthError |Authentication failed. Your access key ID or secret access key may be invalid or expired. Please check your credential configuration. |
|3 |ConfigMissing |ConfigMissing |The configuration file does not exist, or the required configuration items are missing. This error is triggered when the `--config-path` flag is specified and the file does not exist. |
|4 |ResourceNotFound |NotFound |The resource does not exist. The path to the desired bucket or object may be incorrect. |
|5 |PermissionDenied |PermissionDenied |Your account does not have permission to perform this operation. Check your IAM policy configuration. |
|6 |ValidationError |InvalidParam |Parameter validation failed. Please verify that the command parameters are correct. |
|7 |RateLimited |QuotaExceeded |The request was rate\-limited or the quota was exceeded. Try again later or request a quota increase. |
|8 |TransferFailed |Retryable |Transfer failed. This is a retryable error that is usually caused by network issues or temporary anomalies. |
|9 |Conflict |Conflict |Conflicting resource states. This operation is incompatible with the current state of the resources, such as a concurrent write conflict. |


<span id="292ab3d1"></span>
## MCP integration

The Model Context Protocol (MCP) is an open\-source standard that enables AI agents to safely access and use external tools and data sources.

ve\-tos\-cli wraps CLI commands as MCP tools, allowing AI agents to access its functionality directly without manual terminal input.


* In `stdio` mode, which is the default, the service does not listen on any port. Instead, the client launches the MCP server as a subprocess.

* In `sse` mode, the service listens on `127.0.0.1:<port>` and exposes the `/sse` and `/message` endpoints.

* Tool names are derived from skill names using a simple conversion rule. For example, `ve-tos ls` becomes `ve_tos_ls`, and `ve-tos bucket create` becomes `ve_tos_bucket_create`.

* By default, `tools`/`call` runs in preview\-only mode, which means it does not execute the actual operation. Commands are only executed when the request explicitly includes `execute: true`.


<span id="0604f1f2"></span>
## Listing semantics

The default listing mode for `ve-tos` is `auto`:


* HNS buckets use hierarchical listing.

* FNS buckets use flat listing.


To enable prefix\-level concurrency, explicitly specify `--recursive-list-mode hierarchical`. This option also determines whether the `--list-concurrency` option takes effect.
