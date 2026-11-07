---
title: "Utilities"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Utilities"
---

Utilities provide auxiliary capabilities, including capability discovery, generic API invocation, configuration management, shell completion, Model Context Protocol (MCP) services, skill management, and self\-diagnostics. This topic explains how to use utilities commands.

<span id="bb757133"></span>
## Overview


|Command |Description |Example link |
|---|---|---|
|capabilities |Displays a list of the capabilities supported by ve\-tos\-cli. You can filter the list by hierarchy, group, or keyword. |[capabilities](https://docs.byteplus.com/docs/tos/Utilities#a9914d0c) |
|config |Initializes or manages tool configurations with multi\-`profile` support. |[config](https://docs.byteplus.com/docs/tos/Utilities#cb431551) |
| api |Sends requests directly to TOS server‑side APIs. This command is suitable for debugging or executing operations that are not yet encapsulated by the tool. |[api (raw API passthrough)](https://docs.byteplus.com/docs/tos/Utilities#9c61f5b1) |
|completion |Generates scripts that complete commands in the current shell. |[completion](https://docs.byteplus.com/docs/tos/Utilities#b571929f) |
|doctor |Diagnoses issues with the runtime environment, such as tool configuration, credentials, and network connectivity. |[doctor](https://docs.byteplus.com/docs/tos/Utilities#b328bf32) |
|serve (MCP) |Starts the MCP service, with support for both `stdio` and `SSE` transport modes. |[serve (MCP)](https://docs.byteplus.com/docs/tos/Utilities#d58ff088) |
|skill |Lists or exports skill definition files for AI agent integration. |[skill](https://docs.byteplus.com/docs/tos/Utilities#cd4e5cf8) |


<span id="9e87d103"></span>
## Utilities commands

<span id="a9914d0c"></span>
### Capabilities

Use the `capabilities` command to view a list of the capabilities supported by ve\-tos\-cli. You can filter the list by hierarchy, group, or keyword.


* Use the `--view` option to specify the desired output view, choosing from `groups` (default), `text`, `compact`, or `full`.

* Use `--group`, `--search`, or `--layer` to filter the results.


Code example:

```Bash
ve-tos-cli capabilities --view groups
ve-tos-cli capabilities --view compact --output json
ve-tos-cli capabilities --view full --search lifecycle --output json
ve-tos-cli capabilities --group low_level
```


<span id="cb431551"></span>
### config

Use the `config` command to initialize or manage tool configurations with multi\-`profile` support.


* The default configuration file path is `~/.tos/config.toml`. You can override this path using the `--config-path` flag or the `TOS_CONFIG_PATH` environment variable. TOS\-specific configurations are written to the `profile.ve-tos` file.

* The following fields are adjustable:

   `checkpoint_dir`, `batch_report_dir`, `batch_report_format`, `progress_enabled`, `max_retry_count`, `requesttimeout`, `connecttimeout`, and `maxconnections`.


Code example:

```Bash
ve-tos-cli config init --profile staging
ve-tos-cli config show --output json
ve-tos-cli config set region cn-beijing
ve-tos-cli config set endpoint https://tos-cn-beijing.volces.com
ve-tos-cli config set control_endpoint https://tos-control-cn-beijing.volces.com   # Control plane endpoint
ve-tos-cli config set account_id 2100000001
ve-tos-cli config set max_retry_count 3
ve-tos-cli config set staging.control_endpoint https://tos-control-cn-shanghai.volces.com
```


<span id="9c61f5b1"></span>
### api (raw API passthrough)

Use the `api` command to send requests directly to TOS server\-side APIs. This method is ideal for debugging or executing operations that are not yet encapsulated by the tool.


* The `--request` parameter supports inline JSON and file references using the `file://path` syntax. Configurable fields include:

   `method`, `endpoint_rule` (or `endpoint_kind`), `bucket`, `key`, `path`, `query`, `headers`, and `body`.

* The `--force` flag is required to execute non\-idempotent operations.


Code example:

```Bash
ve-tos-cli api object list --describe
ve-tos-cli api bucket lifecycle --dry-run --request '{"method":"GET","endpoint_rule":"bucket","bucket":"mybucket","query":{"lifecycle":""}}'
ve-tos-cli api object delete --force --request '{"method":"DELETE","endpoint_rule":"object","bucket":"mybucket","key":"old.txt"}'
```


<span id="b571929f"></span>
### completion

Use the `completion` command to generate scripts that complete commands in the current shell.

Code example:

```Bash
ve-tos-cli completion bash --output json | jq -r '.data.script' > ~/.ve-tos-completion.bash
echo 'source ~/.ve-tos-completion.bash' >> ~/.bashrc
ve-tos-cli completion zsh --output json | jq -r '.data.script' > ~/.zfunc/_ve-tos
ve-tos-cli completion fish --output json | jq -r '.data.script' > ~/.config/fish/completions/ve-tos.fish
ve-tos-cli completion powershell --output json | jq -r '.data.script' >> $PROFILE
```


<span id="b328bf32"></span>
### doctor

Use the `doctor` command to diagnose issues with the runtime environment, such as tool configuration, credentials, and network connectivity.


* Supported check items include `auth`, `config`, `registry`, `permissions`, `region`, `network`, `version`, `mcp`, `principles`, and `completion`.

* Use the `--live-network` and `--network-timeout-ms` flags to control the behavior of live network probing.


Code example:

```Bash
ve-tos-cli doctor --output json
ve-tos-cli doctor --check auth
ve-tos-cli doctor --check permissions --bucket mybucket
ve-tos-cli doctor --check principles
```


<span id="d58ff088"></span>
### serve (MCP)

Use the `serve` command to start the MCP service, with support for both `stdio` and `SSE` transport modes.

Code example:

```Bash
ve-tos-cli serve --mcp --dry-run --output json
ve-tos-cli serve --mcp
ve-tos-cli serve --mcp --transport sse --port 9090
```


<span id="cd4e5cf8"></span>
### skill

Use the `skill` command to list or export skill definition files for AI agent integration.


* The results are written to the `dir/SKILL.md` and `dir/{domain}/{skill_name}/SKILL.md` files.

* The tool will refuse to overwrite an existing target path.


Code example:

```Bash
ve-tos-cli skill list --output json
ve-tos-cli skill export --dry-run --dir ./ve-tos-skills --output json
ve-tos-cli skill export --name "ve-tos bucket create" --dir ./ve-tos-skills
ve-tos-cli skill export --language zh --dir ./ve-tos-skills-zh
```
