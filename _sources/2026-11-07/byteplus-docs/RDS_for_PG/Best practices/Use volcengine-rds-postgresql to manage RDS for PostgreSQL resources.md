---
title: "Use volcengine-rds-postgresql to manage RDS for PostgreSQL resources."
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Use_volcengine_rds_postgresql_to_manage_RDS_for_PostgreSQL_resources"
---

This topic will guide you through all configuration steps for integrating OpenClaw with BytePlus RDS for PostgreSQL.

<span id="AK6dDC6P"></span>
## Background information

[OpenClaw](https://clawd.bot/) is an open\-source lightweight AI agent tool. The code and data are deployed locally without uploading to the cloud, allowing users to **run it easily on their local machine.**  The tool extends practical business capabilities relying on various **Skills**, supports integration with mainstream large language models and a variety of feature extensions. Users only need to configure the corresponding skills to issue commands through natural language for automatic task completion. It can handle file processing, script execution, and office automation, as well as unify management of cloud resources such as servers and databases through cloud management and operations Skills, completing resource queries, batch maintenance, and routine inspections.

<span id="5mBSVGl2"></span>
## Preparations

Before you start Actions, ensure you have completed the following preparations:


* You have a BytePlus account and the RDS for PostgreSQL service is enabled. If not enabled, visit the [BytePlus RDS for PostgreSQL service enablement page](https://console.byteplus.com/db/rds-pg).

* You have obtained the access key of the BytePlus account, allowing OpenClaw to interact with BytePlus service via API.

   1. Log in to the BytePlus management console.

   1. Go to the **Access Control** \> **Access Key Management**  page.

   1. Create or retrieve a valid pair of Access Key ID and Secret Access Key on the **Access Key Management** page.

* You already have the related permissions for the RDS for PostgreSQL instance and have [created a database account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account?lang=en) for the instance.


If you need to manage tables in the instance, the database account should also be granted the corresponding permissions (such as SELECT, INSERT, SHOW, etc.).

<span id="jiWqLIoL"></span>
## Install OpenClaw

You can choose one of two methods to install and deploy OpenClaw.

<span id="HvvV370k"></span>
### Method one: one\-click deployment (recommended)

BytePlus provides an official one\-click deployment solution to help you quickly complete the installation and basic configuration of OpenClaw on a cloud server (ECS).


* **Operation entry**: [Quickly deploying OpenClaw and integrating Feishu AI assistant](https://docs.byteplus.com/en/docs/6396/2189942?lang=en#kY7J5nzc)


<span id="Dv1UNlqR"></span>
### Method two: local manual installation

if you want to install on a local computer (macOS, Windows, Linux), follow these steps.


1. Install OpenClaw: open your terminal or command prompt, then select and run the corresponding command based on your operating system.

   * **For macOS and linux systems**


```Plain Text
curl -fsSL https://openclaw.ai/install.sh | bash
```



* **For windows systems (using powershell)** 


```Plain Text
iwr -useb https://openclaw.ai/install.ps1 | iex
```



2. **Complete Initial Configuration**: After the installation script runs, it will guide you through basic configurations such as setting the API Key for the large language model. Follow the prompts in the terminal to complete these steps. After successful installation, the core service of OpenClaw runs on your device.


<span id="NteMtgHl"></span>
## Configure OpenClaw

After successfully installing OpenClaw, some key configurations are required for it to connect and manage RDS for PostgreSQL resources.


1. **Prepare the Python environment and uv**


Ensure Python and the uv tool (a fast Python package installer) are installed in the environment where OpenClaw resides.

```Plain Text
pip install uv
```



2. **Install the BytePlus RDS for PostgreSQL Skill**


Run the following command to download the RDS PostgreSQL Skill and copy it to OpenClaw's Skill directory.

```Plain Text
npx skills add https://skills.volces.com/skills/volcengine/agentkit-samples -s volcengine-rds-postgresql --agent openclaw
```



3. **Verify that the Skill is loaded in the Console**


After completing the above steps, open the OpenClaw web console. In the Skill management or extensions page, you should see the Skill named volcengine\-rds\-postgresql has loaded successfully.


4. **Set up environmental variables.** 


Configure OpenClaw with the Access Key required to access BytePlus. Environment variables are normally stored in ~/.openclaw/.env (the path may be /root/.openclaw/.env if you deployed via one\-click deployment). Edit this file and append the two lines below:

```Plain Text
VOLCENGINE_ACCESS_KEY=<Access_Key_ID>
VOLCENGINE_SECRET_KEY=<Secret_Access_Key>
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Replace the placeholder with the real key information obtained during preparation.</div>



5. **Restart OpenClaw service**


To apply the new environment variables, restart the OpenClaw service. The specific restart method depends on your installation mode (e.g., via systemctl, docker restart or the built\-in management commands). After restarting, the Skill will use the configured key for authentication.

<span id="Ad4TDXPx"></span>
## Get started

After configuration, you can start interacting with OpenClaw through natural language to manage your RDS for PostgreSQL instance.


* **Query database tables**: you can directly instruct OpenClaw to query the database. For example: "help me check how many tables are in the demo database" or "help me query the user information with ID 4 in the sys_user table."

* **Scheduled tasks**: with OpenClaw's task scheduling capability, you can set scheduled tasks to automatically perform data backup or monitor performance at specified times.
