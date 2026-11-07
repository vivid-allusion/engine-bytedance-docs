---
title: "Quick start with ve-tos-cli"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Quick_start_with_ve-tos-cli"
---

This topic describes how to quickly get started with ve\-tos\-cli.

<span id="8b26e41e"></span>
## Installation


<Tabs>
<Tab zoneid="bPnwL1euGU" title="Install via package manager">
<TabTitle>Install via package manager</TabTitle>

* Install via npm:

   ```Shell
   npm install -g ve-tos-cli
   ```
   

* Install via pip:

   ```Shell
   pip install ve-tos-cli
   ```
   

* To install on macOS using Homebrew, run the following commands in sequence:

   ```Plain Text
   brew tap volcengine/ve-storage-uni-cli https://github.com/volcengine/ve-storage-uni-cli
   brew trust volcengine/ve-storage-uni-cli
   brew install ve-tos-cli
   ```
   

* Install via cargo:

   ```Shell
   cargo install ve-tos-cli
   ```
   


</Tab>
<Tab zoneid="Zu74bnjNDP" title="Install with a shell script">
<TabTitle>Install with a shell script</TabTitle>

Install ve\-tos\-cli with a shell script.

```Shell
curl -fsSL https://github.com/volcengine/ve-storage-uni-cli/releases/latest/download/install.sh | sh -s -- ve-tos-cli
```



</Tab>
<Tab zoneid="sMMPblpMgw" title="Build from source">
<TabTitle>Build from source</TabTitle>

Build ve\-tos\-cli from the source code and install it.

```Shell
git clone git@github.com:volcengine/ve-storage-uni-cli.git
cd ve-storage-uni-cli
cargo build --release --manifest-path packaging/cargo/ve-tos-cli/Cargo.toml
./packaging/cargo/ve-tos-cli/target/release/ve-tos-cli --help
```



</Tab>
<Tab zoneid="CAt394sXqd" title="Integrate into an AI agent as a skill">
<TabTitle>Integrate into an AI agent as a skill</TabTitle>

Integrate ve\-tos\-cli into an AI agent as a skill. For more information, see [AI agent guide](https://docs.byteplus.com/docs/tos/AI_agent_guide).

```Shell
# Skill address
https://github.com/volcengine/ve-storage-uni-cli/tree/main/skills/ve-tos-cli
```



</Tab>
</Tabs>


<span id="61d8644b"></span>
## Quick start

After installation, complete the following steps to perform initialization, credential injection, and the first invocation.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The tool uses the <code>tos://bucket/key</code> format to reference TOS resources.</div>



1. Initialize the tool.

   ```Bash
   ve-tos-cli config init
   ve-tos-cli config set region cn-beijing
   ve-tos-cli config set endpoint https://tos-cn-beijing.volces.com
   ve-tos-cli config show --output json
   ```
   

2. Inject access credentials.

   ```Bash
   export TOS_ACCESS_KEY=<your-access-key-id>
   export TOS_SECRET_KEY=<your-secret-access-key>
   export TOS_SECURITY_TOKEN=<optional-sts-token>
   ```
   

3. Run the first command.

   ```Bash
   ve-tos-cli mb tos://my-bucket --region cn-beijing
   ve-tos-cli cp ./local.txt tos://my-bucket/local.txt --dry-run
   ve-tos-cli cp ./local.txt tos://my-bucket/local.txt
   ve-tos-cli ls tos://my-bucket/prefix/ --output table
   ve-tos-cli stat tos://my-bucket/local.txt --output json
   ```
   


<span id="365f1973"></span>
## Global parameters


|Parameter |Environment variable |Description |
|---|---|---|
|\-P, \-\-profile <PROFILE\> |TOS_PROFILE |Sets the `profile` name in the configuration file. The default name is `default`. |
|\-\-config\-path <PATH\> |TOS_CONFIG_PATH |Specifies the `TOML` path. The default location is `$HOME/.tos/config.toml`.<br><br>This directory also stores the local encryption `key` used to protect persisted secrets.<br><br>If the specified path does not exist, the command exits with an error (`exit 3`) and does not fall back (`env /`) to the default configuration. |
|\-r, \-\-region <REGION\> |\- |Overrides the current region setting. |
|\-e, \-\-endpoint <URL\> |\- |Overrides the current data plane `endpoint` setting. |
|\-\-control\-endpoint <URL\> |\- |Specifies the `endpoint` for control plane operations. This option only applies to TOS.<br><br>Use it with `--account-id` or configure it in advance via `config set`. |
|\-\-account\-id <ID\> |\- |Specifies the account ID for control plane operations. This option only applies to TOS.<br><br>Use it with `--control-endpoint` or configure it in advance via `config set`. |
|\-o, \-\-output <FORMAT\> |TOS_OUTPUT |Sets the output format. The possible values are `json`, `yaml`, `table`, `csv`, and `markdown`. |
|\-\-query <JMESPATH\> |\- |Filters the output using a `JMESPath` expression. |
|\-\-dry\-run |\- |Previews operations without executing them. |
|\-\-describe |\- |Prints the structured metadata for the command, including the definitions of parameters, descriptions of risks, and API mappings. |
|\-y, \-\-yes |\- |Skips interactive prompts and automatically confirms all operations. |
|\-\-confirm <RESOURCE\> |\- |Specifies `tos://...` to confirm critical delete operations with the exact target. |
|\-\-no\-color [<BOOL\>] |NO_COLOR |Disables colored output. The default value is `true`.<br><br>This is suitable for log collection or terminal environments that do not support ANSI. |
|`-v / -q` |\- |Sets the output verbosity:<br><br><br>* `-v` (\-\-verbose): Enables detailed logs.<br><br>* `-q` (\-\-quiet): Suppresses non\-error output. |
|\-\-language <en\|zh\> |\- |Sets the language for help information:<br><br><br>* `en`: English.<br><br>* `zh`: Chinese. |


<span id="110c801f"></span>
## Troubleshooting


* Common issues and their resolutions:

   
   |Issue |Resolution |
   |---|---|
   |Authentication failed (exit 2) |1. Verify that the `TOS_ACCESS_KEY` and `TOS_SECRET_KEY` that you provided are correct.<br><br>2. Run `ve-tos-cli doctor --check auth` for diagnosis. |
   |Configuration missing (exit 3) |If a configuration file that does not exist is specified via `--config-path` or `TOS_CONFIG_PATH`, the command exits with error `exit 3`.<br><br>Run `ve-tos-cli config init` and set the `region` and `endpoint`. |
   |Control plane command errors |Specify control plane information:<br><br><br>* via the `--control-endpoint` and `--account-id` options.<br><br>* using the environment variable `config set`. |
   |Deletion blocked |In non‑interactive mode, include `--force` and an exact target for `--confirm <RESOURCE>`. |
   |Recursive listing not working |Explicitly specify `--recursive-list-mode hierarchical`. |
   |Viewing lower\-level sub\-commands |Run `ve-tos-cli <group> --describe --output json` to view available sub\-commands. |
   

* To run a full diagnostic check:

   ```YAML
   ve-tos-cli doctor --output json
   ```
