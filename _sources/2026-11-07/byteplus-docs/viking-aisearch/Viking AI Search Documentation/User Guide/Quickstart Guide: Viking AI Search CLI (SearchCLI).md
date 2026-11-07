---
title: "Quickstart Guide: Viking AI Search CLI (SearchCLI)"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/search-cl"
---

Viking AI Search is a unified AI search, recommendation, and conversational search SaaS on BytePlus. This guide introduces **SearchCLI**, the official open\-source command\-line tool for Viking AI Search. SearchCLI lets you manage your search, recommendation, and conversational search services from a terminal or from inside an AI Agent.


---



<span id="c201e199"></span>
# Feature overview

SearchCLI covers the entire Viking AI Search workflow from a single command line: data ingestion, application setup, scene configuration, quality evaluation, strategy tuning, and runtime requests for search, recommendation, and conversational search.

**Core capabilities**


* **Data management:**  create datasets, define schemas, and ingest item data and user\-event data.

* **Application management:**  create applications, bind datasets, edit schema field indexes, and manage online configurations.

* **Search / recommendation / conversational search: ** run search queries, issue recommendation requests, and start conversational\-search sessions.

* **Scene configuration:**  create and manage search and recommendation scenes, and tune their strategy parameters.

* **Automated evaluation and tuning:**  run automated search\-quality evaluation and receive strategy recommendations.

* **Agent\-friendly:**  every command supports `--json` output, designed for AI Agent integration.


&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">The underlying binary and command prefix for SearchCLI are both <code>vs</code>, and all related environment variables are prefixed with <code>VIKING_</code>. Throughout this document, <code>vs</code> refers to the SearchCLI command.</div>



---



<span id="aa689bb0"></span>
# Prerequisites


* **BytePlus account: ** A registered BytePlus account with Viking AI Search enabled.

* **Access Key:**  An Access Key ID (AK) and Secret Access Key (SK) issued from the BytePlus console **Access Control** page.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f7b5c1f19ce74a5eb431d3d07d2a5afd) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Sub\-account users may not be able to create AK/SK directly — contact your enterprise administrator. Keep AK/SK confidential: never share them in chat, transmit them in plaintext, or commit them to source control. The account holder is solely responsible for any consequences of credential leakage.</div>



---



<span id="efee18fc"></span>
# Installation

SearchCLI supports two usage modes &mdash; pick the one that fits your scenario.


|**Usage mode** |**When to use** |**Characteristics** |
|---|---|---|
|**AI Agent (Recommended)**  |Operate via an AI agent such as OpenClaw, Trae, Claude Code, or Codex |Natural\-language driven; the agent runs commands for you |
|**Developer terminal** |Run commands manually in a terminal |Precise control; suitable for development, debugging, and CI/CD |


<span id="f8455b73"></span>
## Step 1: Download the SearchCLI installer

Visit the SearchCLI [GitHub](https://github.com/volcengine/SearchCLI) repository and download the installer that matches your operating system, or clone the repo directly:

```Bash
git clone git@github.com:volcengine/SearchCLI.git vs
cd vs
bash ./scripts/install.sh
```


&nbsp;

<span id="36d502b5"></span>
## Step 2: Install SearchCLI

<span id="9ffd42e1"></span>
### Option 1: Install via AI Agent (Recommended)

When using SearchCLI through an AI Agent, send the installation prompt below to the agent. The agent will install the binary and walk you through authorization.

&nbsp;

**Steps**


1. Download the binary for your OS as described in **Step 1**.

2. Open an AI Agent that can execute commands in your local terminal (OpenClaw, Trae, Claude Code, Codex, etc.).

3. Paste the installation prompt provided in the Viking AI Search console into the agent.

4. Follow the agent's prompts to enter your AK and SK **in the terminal** when asked.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Do <strong>not</strong> paste AK/SK into the agent chat box. Always enter them via interactive terminal input or environment variables when the agent prompts you.</div>


&nbsp;

**Agent installation prompt**

```Bash
Run Search CLI installation and Configuration commands only in the real terminal on my computer's host machine.
Note: the underlying binary name and command prefix for Search CLI both use viking (for example, viking-macos-arm64), and the related environment variables also start with VIKING_.

Do not run any underlying binary commands in your sandbox, including --help, skill install, environment variable checks, auth, and doctor. If you do not currently have access to the real terminal on the host machine, stop and explain first. Do not continue trying.

Requirements:

1. Assume that Search CLI has not been installed on this computer before.
2. I have already downloaded the underlying binary for the current operating system, and its name includes 'vs'. If you do not know the path to this binary, you must ask me first. Do not guess or search the entire disk.
3. After you obtain the binary path, you must always use this absolute path to run commands before proceeding to the globalization suggestion step in step 9. Do not clone the repository, change PATH, copy or rename the binary, or try to install it as a global command.
4. If it is Windows PowerShell, always execute the command in this form:
  - & "<Binary absolute path>" --help
  - & "<Binary absolute path>" skill install all
5. If it is macOS or Linux, execute the command directly using the binary's absolute path. Before running any command for the first time, first try running chmod +x <binary absolute path> to ensure execute permission.
6. First perform the following steps:
  - <Binary absolute path> --help
    - Note: on macOS, if this command appears stuck for a long time with no output, it may be blocked by the system's Gatekeeper. Stop waiting immediately and prompt me to go to "System Settings -> Privacy & Security" to allow it to run.
  - <Binary absolute path> skill install all --json
    - Note: this command requires downloading over the network and may take a long time. Wait for it to complete, and do not interrupt it forcefully.
7. Handle authorization in this priority order:
  - First check whether VIKING_AK and VIKING_SK already exist in the current host's real terminal environment; if they do, execute:
  - If both are present, execute:
    - <Binary absolute path> auth import-env
  - If not, first determine whether the current host's real terminal is an interactive TTY
  - Only execute this after confirming that the current terminal is an interactive TTY:
    - <Binary absolute path> auth login
    , then stop at the input prompt and wait for me to enter the AK/SK in that real terminal
  - If the current terminal is not an interactive TTY, or you cannot maintain interaction, do not run auth login. Tell me directly which commands I should enter in the current real terminal to set VIKING_AK and VIKING_SK, then wait for me to reply “Setup complete” before continuing:
    - <Binary absolute path> auth import-env
  - If you find that your execution environment cannot read the environment variables that I set manually, instruct me to manually run
    - <Binary absolute path> auth import-env
    and then let you take over the remaining process.
  - Never ask me to send AK/SK in the chat.
8. After authorization is complete, execute and show the key results:
  - <Binary absolute path> auth status --json
  - <Binary absolute path> doctor --json
  - <Binary absolute path> skill list --json
9. Global installation recommendation (very important):
  After all validations in step 8 pass successfully, you must proactively give me the following recommendation: “Currently, 'vs' can only be called by using an absolute path. To make the 'vs' command directly available in other terminals or new AI sessions later, we recommend moving it to a system PATH directory (for example, /usr/local/bin/vs on macOS/Linux). Would you like me to perform this global installation for you?”
  - If I answer “Yes”, provide and execute the corresponding rename and move operations, or the command to modify environment variables.
  - If I answer “No”, this task ends.
10. If any step fails, stop immediately and tell me:
- Failed command
- Full error output
- Your assessment
- Next step recommendations
```


&nbsp;

<span id="247ce7ad"></span>
### Option 2: Install via the command line

If Node.js is not installed, you need to install it in your terminal first. Run the following commands in the terminal to install and configure the Node.js LTS version using nvm:

```Bash
# Install nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# Load nvm
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"

# Install and use the Node.js LTS version
nvm install --lts
nvm use --lts
nvm alias default 'lts/*'

# Verify the installation
node -v
npm -v
```



1. Run the following in a terminal to download and install:


```Bash
git clone git@github.com:volcengine/SearchCLI.git vs
cd vs
bash ./scripts/install.sh
```



2. Configure your BytePlus AK/SK using one of two methods.



<Tabs>
<Tab zoneid="ql6fuZTZ27" title="Interactive Login">
<TabTitle>Interactive Login</TabTitle>

**Interactive login** (Recommended for personal machines)

```Bash
vs auth login
```


Paste your AK and SK at the prompts.


</Tab>
<Tab zoneid="MuXyU4Covf" title="Import Environment Variables">
<TabTitle>Import Environment Variables</TabTitle>

**Import from environment variables** (recommended for CI/CD or servers)

```Bash
# Configure environment variables
export VIKING_AK="&lt;your AK&gt;"
export VIKING_SK="&lt;your SK&gt;"

# Import into SearchCLI
vs auth import-env
```



</Tab>
</Tabs>


<span id="6f23fcef"></span>
## Step 3: Verify installation

Check installation and authorization status:

```Bash
vs auth status
```


&nbsp;

**Expected result:**  the active AK is displayed and the login status shows `Active`.

&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Resolving macOS security block</div>


<div data-tips="true" data-tips-type="default">On macOS, an unsigned binary may be blocked the first time it runs.</div>



1. <div data-tips="true" data-tips-type="default">Run <code>vs --help</code> in the terminal.</div>


2. <div data-tips="true" data-tips-type="default">If a "cannot open" alert appears, or the command produces no output for a long time, press <strong>Ctrl + C</strong>.</div>


3. <div data-tips="true" data-tips-type="default">Open <strong>System Settings → Privacy & Security</strong>, scroll down to the security prompt about <code>vs</code>, and click <strong>Open Anyway</strong> (or <strong>Allow</strong>).</div>


4. <div data-tips="true" data-tips-type="default">Run <code>vs --help</code> again and click <strong>Open</strong> in the confirmation dialog. Seeing the full help output means Gatekeeper has been cleared.</div>



&nbsp;


---



<span id="e1eba38a"></span>
# Get started

The examples below illustrate common operations after installation. Inside an AI Agent, describe your intent in natural language and the agent will translate it into the corresponding CLI commands — the agent assists you, while you remain in control of every action.

<span id="482e2f4e"></span>
## Through an AI Agent (natural language)


|**Goal** |**Say to the agent** |
|---|---|
|List all features |What can SearchCLI do? |
|List installed skills |What capabilities does SearchCLI have? |
|Create an application and import data |Help me create an application with this data: <attached data file\> |
|Set a field index |Set `title` as a searchable (text) field |
|Try out search |Run a few searches and show me the results |
|Try out recommendation |Create a recommendation scene and sample\-test recommendations for a few users |
|Try out conversational search |Test conversational search on this application |
|Modify strategy configuration |Set the search recall limit to 50, then enable semantic rerank |
|Inspect current configuration |Show me the current item dataset, search strategy, and recommendation strategy |


<span id="a046bf84"></span>
## Through the command line

<span id="aeb7a15b"></span>
### **Create a dataset and ingest data**

```Bash
# Create a dataset
vs dataset create \
  --name "My_Item_Dataset" \
  --type "multi_modal" \
  --theme general \
  --schema @./schema.json

# Ingest data
# Replace "<Dataset ID>" with the actual dataset ID returned by the `dataset create` command
vs dataset ingest \
  --dataset-id <Dataset ID> \
  --fields @./items.json
```


<span id="16029cf6"></span>
## schema.json Generation and Format Requirements

schema.json is the field configuration file required for dataset creation. You need to define it manually based on your business data structure and save it in the current working directory where the command is executed.

Requirements:


1. **Basic structure**: The file must be a JSON array. Each element represents a field definition, and a dataset can contain up to 200 fields.

2. **Required properties**:

   * The entire file must be a JSON array.

   * Each item in the array must be an object.

   * Each field object must include at least:

      * field_name: The field name. It must start with a letter, and may contain letters, numbers, and underscores. Length: 1 to 128 bytes.

      * field_type: The field type. Supported values include int64, float, string, bool, list<string\>, list<int64\>, vector, sparse_vector, text, and image.


<span id="S8WTrHzf"></span>
## items.json Generation and Format Requirements

items.json is the dataset file to be imported. It must be manually written according to the field structure defined in schema.json, in array format. Each element corresponds to one data record, and a single import supports up to 100 records.

<span id="SuGjoFh0"></span>
### **Create an application and bind a dataset**

```Bash
# Create an application
vs app create \
  --name "My_Search_App" \
  --industry "ecommerce" \
  --description "E-commerce search test application"

# Bind the dataset and configure fields
# Replace "<app_id>" with the actual ID returned by the `create` command
vs app dataset bind \
  --application-id <app_id> \
  --dataset-id <dataset_id>
```


<span id="e2e4db5a"></span>
### **Run search / recommendation / conversational search**

```Bash
# Search
vs search run \
  --application-id <app_id> \
  --query "<keyword>"

# Recommend
vs recommend run \
  --application-id <app_id> \
  --scene-id <scene_id> \
  --user-id <user_id>

# Conversational search
vs chat run \
  --application-id <app_id> \
  --message "<your message>" \
  --pretty
```


<span id="529540da"></span>
### **Manage search\-scene configuration**

```Bash
# Inspect a search scene
vs search scene get \
  --application-id <app_id> \
  --scene-id <scene_id> \
  --format json

# Update a search scene
vs search scene update \
  --application-id <app_id> \
  --scene-id <scene_id> \
  --config @./search-config.json
```


**search\-config.json example：** 

```JSON
{
  "SearchConfig": {
    "RetrieveConfigs": [
      {
        "DatasetID": "107191177",
        "DatasetType": 1,
        "MaxRecallNum": 100,
        "Mode": 1,
        "RerankEnabled": true,
        "RerankTopK": 50
      }
    ]
  }
}
```


<span id="6796da1a"></span>
# Command reference

SearchCLI exposes the following command groups.


|**Command group** |**Description** |**Common subcommands** |
|---|---|---|
|`vs auth` |Credential management |`login`, `import-env`, `status`, `logout` |
|`vs doctor` |Environment health check |Verifies dependencies, authorization, and configuration |
|`vs skill` |Skill\-package management |`list`, `install`, `search`, `show` |
|`vs app` |Application management |`create`, `get`, `update`, `delete`, `activate`, `status` |
|`vs dataset` |Dataset management |`create`, `get`, `ingest`, `schema get` |
|`vs data` |Data operations |`write`, `import` |
|`vs search` |Search execution and scene management |`run`, `scene create / get / update / delete` |
|`vs recommend` |Recommendation execution and scene management |`run`, `scene create / get / update / delete` |
|`vs chat` |Conversational search |`run` (supports multi\-turn dialog and session management) |
|`vs item` |Item\-onboarding workflow |`profile` (analyze data), `plan` (generate plan), `apply` (execute plan) |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Run <code>vs --help</code> for the full command list, or <code>vs <group> --help</code> (for example, <code>vs search --help</code>) for subcommand details.</div>


<div data-tips="true" data-tips-type="default">All commands support <code>--json</code> to emit machine\-readable output for scripting and AI Agent integration.</div>



---



<span id="fd99be10"></span>
# Skill system

SearchCLI ships with a built\-in **skill\-package** system designed for AI Agents. A skill package is a set of Markdown instruction files; the agent loads them to operate the CLI correctly when completing complex tasks.

**Install all skill packages**

```Bash
vs skill install all --json
```


&nbsp;

**Available skill packages**


|**Skill package** |**Purpose** |
|---|---|
|`vs-shared` |Shared initialization and environment checks: install, auth, `doctor`, profile switching |
|`vs-item-onboarding` |Item\-dataset ingestion and application bootstrap, with review and confirmation gates |
|`vs-search` |Search execution and search\-scene management |
|`vs-search-tuning` |Automated search\-quality evaluation and strategy recommendations |
|`vs-chat` |Conversational\-search execution |
|`vs-recommend` |Recommendation execution and recommendation\-scene management |
|`vs-app-dataset-bind` |Application\-to\-dataset binding |


<span id="61049e54"></span>
###
