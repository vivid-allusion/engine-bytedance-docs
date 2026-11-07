---
title: "Milvus CLI user guide"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Milvus_CLI_user_guide"
---

Milvus CLI is the command\-line tool for Milvus for VectorDB. It supports resource management and operations for both control plane and data plane. With Milvus CLI, you can perform instance management, network configuration, database management, collection management, index management, vector search, and permission management to quickly complete resource configuration and data management tasks.

<span id="Ld3nMTBh"></span>
## Supported platforms


|**Operating system** |**Supported architectures** |**Installation package format** |
|---|---|---|
|Linux |amd64, arm64 |tar.gz |
|macOS |amd64, arm64 |tar.gz |
|Windows |amd64, arm64 |zip |


<span id="Jklurhig"></span>
## Install CLI

Milvus CLI supports Linux, macOS, and Windows operating systems. You can install it via installation scripts, npm, or by manually downloading the binary files.

<span id="DMtLxDBG"></span>
### Install using installation script


<Tabs>
<Tab zoneid="EgZEhmHe7I" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

Run the following command to install.

```Bash
curl -fsSL https://raw.githubusercontent.com/volcengine/milvus-cli/main/install.sh | sh
```


After installation, add the CLI directory to the system environment variables as prompted by the terminal.

```Bash
export PATH="$HOME/.milvus-cli/bin:$PATH"
```



</Tab>
<Tab zoneid="QR8FsbNoXC" title="Windows">
<TabTitle>Windows</TabTitle>

Run the following command to install.

```PowerShell
irm https://raw.githubusercontent.com/volcengine/milvus-cli/main/install.ps1 | iex
```



</Tab>
</Tabs>


<span id="PUloZN5r"></span>
### Install using npm

Execute the following command to install.

```Bash
npm install -g @volcengine/milvus-cli
```


<span id="d6NnfwxL"></span>
### Manually download and install

Go to the [GitHub Releases](https://github.com/volcengine/milvus-cli/releases) page to download the precompiled binary for your operating system and architecture. After downloading, extract the installation package and add the `milvus-cli` executable to the system `PATH` environment variable.

<span id="9DAXhNFm"></span>
### Verify installation

After installation, run the following command to verify the installation.

```Bash
milvus-cli version
```


Or

```Bash
milvus-cli --help
```


Successful output of version or help information indicates that the installation succeeded.

<span id="l9U96hat"></span>
## Quick start


1. Create profile.

   Run the following command to create the CLI runtime configuration.

   ```Bash
   milvus-cli profile create \
     --name default \
     --site volcengine \
     --region ap-johor \
     --project default \
     --credential volcengine \
     --language EN
   ```
   

2. Complete identity authentication.

   Execute the following command to log in using your BytePlus account's Access Key (AK) and Secret Key (SK).

   ```Bash
   milvus-cli auth login --name volcengine --ak <AK> --sk <SK>
   ```
   

3. Manage instances.

   Execute the following command to view the instance list.

   ```Bash
   milvus-cli instance list
   ```
   

   Execute the following command to view the instance details list.

   ```Bash
   milvus-cli instance describe --instance-id <instance-id>
   ```
   

4. Create a data plane connection.

   Execute the following command to create a data connection to the Milvus instance.

   ```Bash
   milvus-cli data connection create \
     --from-instance <instance-id> \
     --password <milvus-password>
   ```
   

5. Perform data operations.

   Execute the following command to view the database list.

   ```Bash
   milvus-cli data database list
   ```
   

   Execute the following command to view the collection list.

   ```Bash
   milvus-cli data collection list
   ```
   

   Execute the following command to perform vector search.

   ```Bash
   milvus-cli data vector search \
     --collection <collection-name> \
     --vector '[1.0, 2.0, 3.0]' \
     --limit 10
   ```
   


<span id="T0qBxfGZ"></span>
## CLI commands

Milvus CLI provides the following command groups. For more information, see [command overview](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/README.en.md).


|**Command group** |**Description** |**Documentation** |
|---|---|---|
|auth |Log on, log off, view authentication status |[control/auth.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/control/auth.en.md) |
|profile |Manage site/region/project/language contexts |[control/profile.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/control/profile.en.md) |
|spec |View version, region, specification, price, VPC/subnet/EIP information |[control/spec.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/control/spec.en.md) |
|instance |Manage dedicated instances |[control/instance.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/control/instance.en.md) |
|network |Manage dedicated endpoint deployment and allowlists |[control/network.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/control/network.en.md) |
|version |View CLI build information |[control/version.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/control/version.en.md) |
|completion |Generate shell auto\-completion scripts |[control/completion.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/control/completion.en.md) |
|data connection |Manage data plane connection configurations |[data/connection.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/data/connection.en.md) |
|data database |Manage databases |[data/database.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/data/database.en.md) |
|data collection |Manage collections |[data/collection.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/data/collection.en.md) |
|data partition |Manage partitions |[data/partition.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/data/partition.en.md) |
|data alias |Manage aliases |[data/alias.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/data/alias.en.md) |
|data index |Manage indexes |[data/index.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/data/index.en.md) |
|data vector |Vector search and operations |[data/vector.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/data/vector.en.md) |
|data user |Manage users |[data/user.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/data/user.en.md) |
|data role |Manage roles |[data/role.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/data/role.en.md) |
|serverless instance |Manage serverless instances |[serverless/instance.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/serverless/instance.en.md) |
|serverless network |Manage serverless network configuration |[serverless/network.md](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/references/serverless/network.en.md) |


<span id="pH3h7URv"></span>
## Agent integration

Milvus CLI provides the [Agent Skills](https://agentskills.io/) skill pack, which integrates with AI coding assistants, including:


* TRAE

* Claude Code

* Cursor

* Codex

* OpenCode

* GitHub Copilot


By integrating Agent Skills, the AI assistant can directly call the Milvus CLI to manage instances and perform data operations. For installation methods of each Agent, refer to [milvus-cli Agent Skill](https://github.com/volcengine/milvus-cli/blob/main/skills/milvus-cli/README.md#installation).
