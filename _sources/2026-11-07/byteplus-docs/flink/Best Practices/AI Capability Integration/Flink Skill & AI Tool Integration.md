---
title: "Flink Skill & AI Tool Integration"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Flink_Skill_AI_Tool_Integration"
---

This document is intended for users who wish to use Serverless Flink within AI Agents such as Trae, Claude Code, OpenClaw, Codex, etc. It explains how to install the `volc-flink` CLI, install the `byted-serverlessflink-volc-flink` Skill, and leverage natural language to accomplish Flink SQL, JAR, CDC task development, task operations, anomaly diagnosis, and resource pool analysis.

<span id="02825f90"></span>
## **1. Overview**

`byted-serverlessflink-volc-flink` is an Agent Skill built around the `volc-flink` CLI. It does not replace the CLI, but enables the Agent to understand user intent, select appropriate sub\-skills, organize CLI commands, parse JSON output, and summarize results into actionable recommendations.

Typical capabilities include:


* CLI installation, version checking, command discovery, and schema queries.

* Context checks for login status, Profile, Project, Catalog, resource pool, etc.

* Draft creation, update, validation, publishing, and launching for Flink SQL, Flink JAR, Flink CDC, Batch SQL/JAR.

* Job querying, starting, stopping, restarting, scaling up/down, deletion, as well as Session cluster operations.

* Job Instance, event, log, Pod, and metric queries.

* Failure root cause diagnosis, performance analysis, and resource pool capacity observation.


The main entry point for the Skill is `byted-serverlessflink-volc-flink`, which routes to different sub\-skills based on intent:


|Scenario |Sub Skill |
|---|---|
|CLI Installation, Help, Schema |`byted-serverlessflink-volc-flink-cli` |
|Login and Credential Status |`byted-serverlessflink-volc-flink-auth` |
|Profile / Project |`byted-serverlessflink-volc-flink-config`<br><br>`byted-serverlessflink-volc-flink-projects` |
|Catalog Metadata |`byted-serverlessflink-volc-flink-catalog` |
|SQL Task Development |`byted-serverlessflink-volc-flink-sql` |
|JAR Task Development |`byted-serverlessflink-volc-flink-jar` |
|CDC Task Development |`byted-serverlessflink-volc-flink-cdc` |
|Batch Tasks |`byted-serverlessflink-volc-flink-batch` |
|Operations and Maintenance |`byted-serverlessflink-volc-flink-sre` |
|Monitoring Query |`byted-serverlessflink-volc-flink-monitor` |
|Exception Diagnosis |`byted-serverlessflink-volc-flink-diagnostic` |
|Performance Analysis |`byted-serverlessflink-volc-flink-performance` |
|Resource Pool Analysis |`byted-serverlessflink-volc-flink-resource-pool` |


<span id="efd375fc"></span>
### **Operating Principles**


* The Agent confirms current CLI capabilities via `volc-flink command list --output json` and `volc-flink schema < command.id> --output json`.

* By default, `--output json` is used for easier parsing; logs follow the scenario and use `--output ndjson`.

* For actions involving publishing, starting, stopping, restarting, deleting, scaling up/down, the Agent should first explain the objectives and impacts, then obtain confirmation.

* Login commands are executed locally by the user; the Agent should not request or display sensitive information such as AK/SK, Token, etc. in the conversation.


<span id="63ac822b"></span>
## **2. CLI Installation**

<span id="9fca6df8"></span>
### 2.1 Installing the Flink CLI Tool

Recommended method:

```Bash
npm install -g @volcflink/volc-flink
volc-flink --version
volc-flink --help
```


For more CLI installation documentation, refer to [火山 Flink Cli 工具](https://docs.byteplus.com/docs/flink/104298).

<span id="1194d220"></span>
### **2.2 Initializing Login and Project Context**

After installation, first check CLI availability:

```Bash
volc-flink --version
volc-flink command list --output json
```


Login is performed locally by the user, who must follow the instructions to enter authentication information for Volcano Flink, including Region, AK, SK, Project, etc.:

```Bash
# Log in to the Volcengine Flink Platform
volc-flink auth login
# Check Login Status
volc-flink auth status --output json
```


<span id="33437578"></span>
## **3. Skill Installation**

On the Skill page, installation is supported via the [Volcano Find Skill Platform](https://findskill.com/volcengine/serverlessflink/byted-serverlessflink-volc-flink).

<span id="4934ddcc"></span>
### **3.1 Using in Trae**

It is recommended to use the installation script to install the Flink Skill:

```Bash
npx skills add https://skills.volces.com/skills/volcengine/serverlessflink -s byted-serverlessflink-volc-flink --agent trae
```


Additionally, when Trae supports Agent / Skill / MCP extensions, you can search for and download `byted-serverlessflink-volc-flink` via FindSkills MCP. After installation, ensure that `volc-flink` is accessible in the PATH of Trae's runtime environment.

<span id="dd031797"></span>
### **3.2 Using in Claude Code**

It is recommended to use the installation script to install the Flink Skill:

```Bash
npx skills add https://skills.volces.com/skills/volcengine/serverlessflink -s byted-serverlessflink-volc-flink --agent claude-code
```


Usage diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0b298c6be314e87ba34dfcb179ef233~tplv-goo7wpa0wc-image.image) </span>

<span id="d19f2691"></span>
### **3.3 Using in Codex**

It is recommended to use the installation script to install the Flink Skill:

```Bash
npx skills add https://skills.volces.com/skills/volcengine/serverlessflink -s byted-serverlessflink-volc-flink --agent codex
```


Usage diagram

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49b5746a2cfd4a32955765f36c6d6f90~tplv-goo7wpa0wc-image.image) </span>

<span id="df0af1e0"></span>
### **3.4 Using in OpenClaw**

It is recommended to use the installation script to install the Flink Skill:

```Bash
npx skills add https://skills.volces.com/skills/volcengine/serverlessflink -s byted-serverlessflink-volc-flink --agent openclaw
```


<span id="7c5ba137"></span>
### **3.5 Post\-installation Verification**

Execute or guide execution in any Agent:

```Bash
Help me use the byted‑serverlessflink‑volc‑flink skill to check the version of the volc‑flink tool and introduce its related functions. 
Help me check what projects are available on the Volcengine Flink platform. 
Help me check which Flink resource pools exist under the XXX project.
Help me check what Flink drafts are available. 
Help me check which Flink tasks are running.
```


If `command list` can return the command list, and `auth status` and `project current` correctly display the context, it indicates that the basic link between CLI and Skill is available.

<span id="3cd1fe9c"></span>
## **4. Use Cases**

<span id="9937ec50"></span>
### **4.1 Developing Flink Tasks**

<span id="b8156b2f"></span>
#### **4.1.1 Flink SQL Tasks**

Applicable Scenarios:


* Generate or modify Flink SQL.

* Create streaming or batch SQL drafts.

* Validate SQL drafts.

* Publish drafts and start Jobs.


Agent prompt examples:

```Plain
Create a Flink SQL task using the byted‑serverlessflink‑volc‑flink Skill. 
The task name is demo_sql_order_stat, the directory is /demo, and the Engine version is 1.17. 
Please first check the current profile, project, resource pool and draft directory. 
The SQL file is located at ./sql/order_stat.sql. 
Perform validation after creation, but do not publish unless I confirm.
```


Underlying command reference:

```Bash
volc-flink auth status --output json
volc-flink profile list --output json
volc-flink project current --output json
volc-flink draft directory list --output json
volc-flink draft create --name demo_sql_order_stat --directory-id <dir-id> --job-type FLINK_STREAMING_SQL --engine-version FLINK_VERSION_1_17 --sql-file ./sql/order_stat.sql --output json
volc-flink draft get --id <draft-id> --output json
volc-flink draft validate --id <draft-id> --output json
```


Publish and start:

```Bash
volc-flink resource-pool list --output json
volc-flink draft publish --id <draft-id> --resource-pool-id <pool-id> --yes --output json
volc-flink job start --id <job-id> --from new --yes --output json
```


<span id="f344f28d"></span>
#### **4.1.2 Flink JAR Tasks**

Applicable Scenarios:


* Upload or reference JAR files from local, TOS, or file resources.

* Specify Main Class and Main Args.

* Create, update, publish, and start JAR tasks.


Agent prompt examples:

```Plain
Create a JAR task using the byted‑serverlessflink‑volc‑flink Skill. 
The JAR path is ./target/order‑job.jar, and the Main Class is com.example.OrderJob. 
The task type is streaming JAR, the Engine version is 1.17, and the parameters are --env prod --topic order_events. 
Please confirm the resource directory and draft directory first, then create the draft. Only perform draft get verification after creation.
```


Underlying command reference:

```Bash
volc-flink draft create --name order_jar_job --directory-id <dir-id> --job-type FLINK_STREAMING_JAR --engine-version FLINK_VERSION_1_17 --jar ./target/order-job.jar --resource-dir-id <resource-dir-id> --main-class com.example.OrderJob --args "--env prod --topic order_events" --output json
volc-flink draft get --id <draft-id> --output json
```


Publish and start:

```Bash
volc-flink draft publish --id <draft-id> --resource-pool-id <pool-id> --yes --output json
volc-flink job start --id <job-id> --from new --yes --output json
```


<span id="5eaa0ef8"></span>
#### **4.1.3 Flink CDC Tasks**

Applicable Scenarios:


* Generate CDC YAML templates for MySQL, Kafka, Paimon, Doris, StarRocks, ByteHouse CDW, etc.

* Create or update CDC drafts.

* Publish and start CDC Jobs.


Agent prompt examples:

```Plain
Generate CDC YAML using the byted‑serverlessflink‑volc‑flink Skill. 
The source is MySQL and the target is Paimon. Keep credential placeholders and do not perform any CLI changes. 
After generation, explain what I need to supplement for each section of sources, sink, pipeline, route and transform.
```


Create CDC draft:

```Bash
volc-flink draft create --name mysql_to_paimon_cdc --directory-id <dir-id> --job-type FLINK_CDC_JAR --engine-version FLINK_VERSION_1_17 --cdc-version v3.4 --cdc-file ./cdc/mysql-to-paimon.yml --output json
volc-flink draft get --id <draft-id> --output json
```


Update CDC draft:

```Bash
volc-flink draft update --id <draft-id> --cdc-version v3.4 --cdc-file ./cdc/mysql-to-paimon.yml --output json
volc-flink draft get --id <draft-id> --output json
```


<span id="75e6326a"></span>
### **4.2 Operating Flink Tasks**

Applicable Scenarios:


* Query Job lists and details.

* Start, stop, and restart Jobs.

* Restore from the latest checkpoint or savepoint.

* Scale up or down running tasks.

* Operate Session clusters.


Read\-only query prompts:

```Plain
Use the byted‑serverlessflink‑volc‑flink Skill to query the Job status. 
List the Jobs under the current project, locate tasks whose names contain order, and display status, version, resource pool, parallelism, recent events and current instances. 
Do not perform any modification operations.
```


Underlying command reference:

```Bash
volc-flink job list --output json
volc-flink job get --id <job-id> --output json
volc-flink job events --id <job-id> --output json
volc-flink job instance list --job-id <job-id> --output json
```


Start task:

```Bash
volc-flink job start --id <job-id> --from new --yes --output json
```


Restart from latest checkpoint:

```Bash
volc-flink job restart --id <job-id> --from latest --yes --output json
```


Restart from savepoint:

```Bash
volc-flink job restart --id <job-id> --from savepoint --savepoint-id <savepoint-id> --yes --output json
```


Stop task and create savepoint:

```Bash
volc-flink job stop --id <job-id> --with-savepoint --yes --output json
```


Scale up/down while running:

```Bash
volc-flink job rescale --id <job-id> --parallelism 10 --tm-vcore 2 --tm-memory 8192 --slots-per-tm 4 --jm-vcore 1 --jm-memory 4096 --yes --output json
```


Note:


* The `s-...` provided by the user is usually a running instance ID, not necessarily a stable Job ID. The Agent should first use `job instance get` to map to `job_id`.

* Scaling running tasks should use `job rescale`; do not scale by modifying draft parameters and republishing.

* `job restart` does not accept runtime resource parameters; use `job rescale` for resource changes.


<span id="f89d039e"></span>
### **4.3 Diagnosing Flink Tasks**

Applicable Scenarios:


* Job failures, repeated restarts, or prolonged abnormal states.

* ERROR / WARN appears in logs.

* TaskManager, JobManager, or Pod exceptions.

* Performance issues such as backpressure, increased latency, reduced throughput, or insufficient resources.


Diagnostic prompts:

```Plain
Diagnose job <job‑id> using the byted‑serverlessflink‑volc‑flink Skill. 
Execute read‑only commands only. 
Query job get, job events, the latest instance, ERROR logs, Pod, and health metrics in sequence.
Output root cause, evidence, confidence level and next‑step suggestions.
```


Underlying command reference:

```Bash
volc-flink job get --id <job-id> --output json
volc-flink job events --id <job-id> --output json
volc-flink job instance list --job-id <job-id> --output json
volc-flink job instance get --id <instance-id> --output json
volc-flink job instance logs --id <instance-id> --level ERROR --limit 200 --output json
volc-flink job instance pods --id <instance-id> --output json
volc-flink job instance metrics --id <instance-id> --preset health --output json
```


Performance analysis prompts:

```Plain
Use the byted‑serverlessflink‑volc‑flink Skill to analyze the performance issues of job <job‑id> over the last 2 hours. 
Align metrics, WARN/ERROR logs and event timelines. 
Focus on throughput, latency, backpressure, checkpoint, CPU, memory and restart events. 
Do not perform scaling or restarts; provide recommendations only.
```


Log time ranges can use RFC3339 or Unix seconds:

```Bash
volc-flink job instance logs --id <instance-id> --since 2026-05-22T10:00:00+08:00 --until 2026-05-22T12:00:00+08:00 --level WARN --limit 200 --output json
```


Log follow:

```Bash
volc-flink job instance logs --id <instance-id> --follow --output ndjson
```


<span id="ae0a7a11"></span>
### **4.4 Resource Pool Analysis**

Applicable Scenarios:


* Select resource pool before publishing tasks.

* View resource pool status, capacity, and usage.

* Analyze whether the resource pool may cause task startup failures or performance bottlenecks.


Agent prompts:

```Plain
Analyze the resource pools of the current project using the byted‑serverlessflink‑volc‑flink Skill. 
Execute read‑only commands only. 
List resource pool ID, name, type, billing type, status, capacity, used resources, and creation time. 
For on‑demand resource pools, pay attention to the used CU count and total CU count. 
For monthly‑subscribed or hybrid resource pools, focus on the CPU and memory fields. 
Finally, recommend candidate resource pools suitable for deploying new tasks.
```


Underlying command reference:

```Bash
volc-flink resource-pool list --output json
volc-flink resource-pool get --id <pool-id> --output json
```


Select resource pool before publishing tasks

```Bash
volc-flink resource-pool list --output json
volc-flink draft publish --id <draft-id> --resource-pool-id <pool-id> --yes --output json
```


Recommended outputs for resource pool analysis include:


|Field |Description |
|---|---|
|ID / Name |Commands such as publish and session creation require precise referencing |
|Type |Distinguishes different resource pool types |
|Billing Type |`POST`, `PRE`, `MIX`, etc. |
|Status |Whether it can be used for publishing or starting |
|Capacity |Capacity fields such as CU, CPU, memory |
|Used Resources |Used to determine available quota |
|Risk |Insufficient capacity, abnormal status, resource fragmentation, etc. |


<span id="4f70c036"></span>
## **5. Common Agent Prompt Templates**

<span id="a389e84d"></span>
### **5.1 Read\-Only Pre\-Check**

```Plain
Use the byted‑serverlessflink‑volc‑flink Skill. 
Please execute read‑only commands only, and check the current auth, profile, project, and command list. 
Output the current context and a summary of available commands. Do not perform any create, update, publish, start, stop or delete operations.
```


<span id="b7cc9c2b"></span>
### **5.2 Create Task Without Publishing**

```Plain
Create a draft using the byted‑serverlessflink‑volc‑flink Skill, but do not publish it. 
First parse the target directory and project context, then run draft get and draft validate after creation. 
If you need to create directories or upload files, state the plan first and wait for my confirmation.
```


<span id="d12bcc8d"></span>
### **5.3 Publish and Start**

```Plain
Use the byted-serverlessflink-volc-flink Skill to publish and start draft <draft-id>. 
Please list candidate resource pools for me to select. 
Display the draft id, resource pool id and startup mode before publishing. 
Execute draft publish and job start only after my confirmation.
```


<span id="8461300f"></span>
### **5.4 Fault Diagnosis**

```Plain
Use the byted‑serverlessflink‑volc‑flink Skill to diagnose <job‑id>. 
Perform read‑only queries for job details, events, latest instances, ERROR logs, Pods and health metrics. 
Output: Phenomenon, Evidence, Possible Causes, Confidence Level, Recommended Next Steps.
```


<span id="e20b137a"></span>
## **6. Security and Best Practices**


* Strictly control login AK permissions. Avoid granting excessive permissions to prevent unexpected losses.

* The hallucination issue of large models cannot be completely avoided. All critical parameter configurations and execution commands must be carefully checked and confirmed.

* Do not paste AK/SK, Token, database passwords, or plaintext connection strings in chat.

* Sensitive fields in Connector YAML and SQL WITH parameters should use placeholders.

* All change operations should first confirm the target ID. Prefer using IDs and avoid relying on ambiguous names.

* For publish, start, stop, restart, scale up/down, and delete commands, it is recommended to always retain `--output json` to facilitate Agent result verification.

* Task diagnosis and performance analysis are read\-only by default; only when explicitly requested by the user should the SRE change process be initiated.

* Use `volc-flink schema <command.id> --output json` to validate the parameters currently supported by the CLI, avoiding outdated commands or old parameters.
