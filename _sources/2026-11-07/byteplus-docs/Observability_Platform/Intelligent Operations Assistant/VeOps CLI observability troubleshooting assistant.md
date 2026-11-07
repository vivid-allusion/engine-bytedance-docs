---
title: "VeOps CLI observability troubleshooting assistant"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/VeOps_CLI_observability_troubleshooting_assistant"
---

VeOps CLI is an observability troubleshooting tool designed for AI agents. It wraps the capabilities of Server\-side Monitoring, VMP, Cloud Monitor, TLS, and VKE, as well as local log and metric analysis, into commands that general\-purpose agents can reliably call. After installation, lots of repetitive queries and evidence organization involved in troubleshooting can be directly handed off to AI, improving troubleshooting efficiency. For example, you can use agents such as Claude Code, Codex, Cursor, Trae, OpenClaw, and Hermes to query metrics, logs, and traces, as well as troubleshoot alerts and inspect clusters, all through natural conversation.

<span id="lTLvyMr9"></span>
## Background

<span id="nz000Deh"></span>
### Supported data sources

VeOps CLI currently supports the most commonly used data sources in observability troubleshooting, including Server\-side Monitoring, VMP, Cloud Monitor, TLS, VKE, and local log/metric data for anomaly detection.


|**Data source** |**Capability coverage** |**Issues addressed** |
|---|---|---|
|Server\-side Monitoring |Services, metrics, traces, Spans, logs, alerts, notification groups, and GenAI sessions |Increased service error rates, slow API responses, downstream dependency anomalies, and AI application call chain analysis |
|Vital Managed Service for Prometheus |Instant queries, range queries, metric names, labels, series, alerts, and workspaces |PromQL queries, custom metric analysis, and Prometheus alert troubleshooting |
|Cloud Monitor |Namespace, metric, resource, alarm, event |ECS, CLB, RDS, and other cloud resource metrics and Cloud Monitor alert troubleshooting |
|Torch Log Service (TLS) |Project, topic, index, log search, and log histogram |Error log search, log trend analysis, and high\-frequency error classification |
|Vital Kubernetes Engine (VKE) |Cluster, NodePool, Node, Add\-on, Kubeconfig, Namespace, Pod, Deployment, StatefulSet, Service, Event, Pod logs |Cluster inspection, Pod anomalies, scheduling failures, image pull failures, and container log viewing |


<span id="hnDE5hBq"></span>
### Tool value

VeOps CLI improves productivity across different roles:


|**Role** |**Previous pain point** |**After VeOps CLI is used** |
|---|---|---|
|On\-call engineers |After an alert is triggered, they have to switch between multiple systems and piece together evidence manually. |Describe the alert or symptom directly, and let AI output a timeline, evidence, and recommended actions. |
|Application developers |Locating slow requests and error traces requires sifting through metrics, logs, and traces. |AI automatically correlates metrics, logs, Spans, and topology to shorten the troubleshooting path. |
|SRE/O&M |Inspecting clusters, cloud resources, and alerts requires a large number of repetitive queries. |Trigger an inspection with natural language and generate a structured report with risk items. |
|Platform teams |Users are unfamiliar with the query entry points of each product, and troubleshooting efficiency depends on experience. |Observability capabilities are exposed to general\-purpose agents in a unified manner, lowering the barrier to use. |
|New members |Not knowing which product to query first or what filter conditions to use. |Learn troubleshooting methods through the query path of the agent, reducing the learning curve. |


Comparison between VeOps CLI and basic AI tools: Rather than simply connecting AI to an observability backend, its value lies in resolving real engineering issues in agent\-based troubleshooting, such as how to reliably fetch data, how to handle results that exceed expectations, how to correlate data across products, and how to audit conclusions.


|**Comparison dimension** |**Screenshot or copy\-paste to AI** |**VeOps CLI** |
|---|---|---|
|Data retrieval |Relying on screenshots and web text, with fields and formats beyond control. |Structured JSON envelope with a schema that guarantees stable field names and types. |
|Large\-scale results |Context window overflow, causing information to be truncated or missed. |Use `--save-as` to persist results to disk, and then extract specific fields with jq or Python, so critical evidence is not lost due to context overflow. |
|Cross\-product correlation |Manually switching between Server\-side Monitoring, TLS, VMP, and other pages, with evidence scattered. |A unified operation ID interface spanning 5+ products, with results linked along a timeline. |
|Security |Agents may accidentally perform unintended operations or modify cloud resource configurations. |Read\-only mode. Agents can only query and cannot modify any cloud resources. |
|Troubleshooting quality |Reliance on individual experience and agent inconsistency. |A fixed schema constrains query paths, making results predictable and reproducible. |


<span id="Yh78rCOR"></span>
## Usage guide

<span id="YqBBMc5h"></span>
### Installation and configuration

We recommend that you quickly install, update, or uninstall VeOps CLI through a conversation with an agent.


<Tabs>
<Tab zoneid="P54IrpGjgk" title="Install VeOps CLI">
<TabTitle>Install VeOps CLI</TabTitle>

Send the following content to the agent.

```Plain Text
Help me install veops-cli：https://veops-cli.tos-cn-beijing.volces.com/public/install.md
```


Upon receiving the promt, the agent completes the following steps and finishes the VeOps CLI installation.


|Configuration procedure |Agent action |
|---|---|
|1. Download the binary file |Automatically detect the operating system and architecture, and download the binary file to a writable directory in PATH, such as `/usr/local/bin` or `~/.local/bin`. |
|2. Install the skill |Detect locally installed agents and write the `veops-cli` skill into each `skills` directory. |
|3. Guide authentication |Prompt you to log in with `veops-cli login` or configure AK/SK environment variables. Specific operations are as follows:<br><br><br>* **Log in with ** **`veops-cli login`** **:** <br><br>   * If a browser is available locally, use `veops-cli login` (console OAuth; requests 6\-hour temporary credentials via STS by default).<br><br>   * For SSH, remote machines, containers, or other headless environments, use `veops-cli login --remote`, and then paste the entire authorization response shown on the browser page into the terminal as\-is.<br><br>* **Configure AK/SK environment variables**: To use static AK/SK, set the `VOLCENGINE_ACCESS_KEY`, `VOLCENGINE_SECRET_KEY`, and `VOLCENGINE_REGION` environment variables.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Credentials are stored in <code>~/.volcengine/config.json</code>. <code>~/.veops-cli/config.yaml</code> stores operational preferences.   </div><br>    |
|4. Verify the availability |Automatically execute `veops-cli version`, `veops-cli schema`, and `veops-cli doctor` to confirm the installation result. |





</Tab>
<Tab zoneid="VANzhn9udM" title="Update VeOps CLI">
<TabTitle>Update VeOps CLI</TabTitle>

Send the following content to the agent. The agent downloads the latest binary file and replaces the current version, overwrites the existing skill in the installed directory with the latest version, and then automatically executes `veops-cli version`, `veops-cli schema`, and `veops-cli doctor` to confirm the update results.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The update does not delete your login status or local configuration.</div>


* <div data-tips="true" data-tips-type="warning">After updating the skill, you need to restart the agent manually. The restart method and command vary by agent. For example, to restart OpenClaw, execute the <code>openclaw gateway restart</code> command.</div>



```Plain Text
Help me update veops-cli
```





</Tab>
<Tab zoneid="pW1d8xymFe" title="Uninstall VeOps CLI">
<TabTitle>Uninstall VeOps CLI</TabTitle>

Send the following content to the agent. The agent deletes the binary file and cleans up the `veops-cli` skill in the skills directory of each agent.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">By default, <code>~/.volcengine/config.json</code> is not deleted, as it may be shared by other tools.</div>


* <div data-tips="true" data-tips-type="warning">By default, the <code>~/.veops-cli</code> local configuration is not deleted. You can delete it manually if needed.</div>


* <div data-tips="true" data-tips-type="warning">After VeOps CLI is uninstalled, you need to restart the agent manually. The restart method and command vary by agent. For example, to restart OpenClaw, execute the <code>openclaw gateway restart</code> command.</div>



```Plain Text
Help me uninstall veops-cli
```





</Tab>
</Tabs>


<span id="PtbIw2OE"></span>
### Usage method

Once VeOps CLI is installed, you can query metrics, logs, and traces, troubleshoot alerts, and inspect clusters directly through a conversation with an agent. When using VeOps CLI, you do not need to memorize any commands. Simply describe the issue in natural language, and the agent will call the appropriate commands on your behalf to complete the fault analysis. 

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">VeOps CLI currently supports querying only and does not make any modifications to cloud resources.</div>


* <div data-tips="true" data-tips-type="warning">Permissions follow the  account, and no data outside your authorized scope is accessible.</div>


* <div data-tips="true" data-tips-type="warning">VeOps CLI is designed for agents. If you encounter any issues, simply describe the symptoms and let AI troubleshoot the issues.</div>



The following is a usage example. For more typical scenarios, see [Typical scenarios](https://docs.byteplus.com/en/docs/314/113512#ISyUctgu).

```Plain Text
Please help me figure out why the error rate of order-api has risen over the past hour.
```


Upon receiving the issue, AI does not simply execute a single command. Instead, it first determines which data sources to query and then systematically collects evidence along a troubleshooting path. For example:


1. It starts by checking Server\-side Monitoring metrics to confirm whether the error rate has actually increased.

2. It then looks for slow Spans and error Spans, queries error logs to identify specific errors, and determines whether the errors are concentrated in a particular downstream service.

3. Finally, it combines the service topology to confirm dependencies. If the service is running in VKE, it also checks Pod restarts, events, and container logs.


<span id="wcRYYd8N"></span>
### Command list

`veops-cli` currently supports the following commands. This command list is intended to help you understand the capability boundaries of `veops-cli`.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You do not need to memorize these <code>veops-cli</code> commands. The agents will call them on your behalf.</div>


* <div data-tips="true" data-tips-type="default">After a version upgrade, the supported commands may change. Always refer to the output of <code>schema --index</code> and <code>schema <product></code> at runtime for the definitive command list.</div>




<Tabs>
<Tab zoneid="Y9SEhzVmm3" title="Vital Managed Service for Prometheus">
<TabTitle>Vital Managed Service for Prometheus</TabTitle>

The following commands are provided for VMP:


|Command |Feature |
|---|---|
|vmp.query |Perform instant PromQL queries. |
|vmp.query\-range |Perform range PromQL queries. |
|vmp.metric\-names |Query metric names. |
|vmp.metric\-labels |Query metric labels. |
|vmp.series |Query time series. |
|vmp.alert.rule\-list |Query the alert rule list. |
|vmp.alert.rule\-get |Query alert rule details. |
|vmp.alert.history\-list |Query alert history. |
|vmp.workspace.list |Query the workspace list. |
|vmp.workspace.get |Query workspace details. |
|vmp.workspace.instance\-types |Query workspace specifications. |





</Tab>
<Tab zoneid="RmhvaVe0OC" title="Server-side Monitoring">
<TabTitle>Server-side Monitoring</TabTitle>

The following commands are provided for Server\-side Monitoring:


|Command |Feature |
|---|---|
|apmplus\-server.metrics.query\-semantic |Query semantic metrics. |
|apmplus\-server.metrics.list |Query available metrics. |
|apmplus\-server.metrics.category\-list |Query metric categories. |
|apmplus\-server.metrics.filter\-keys / apmplus\-server.metrics.filter\-values |Query metric filter dimensions and values. |
|apmplus\-server.trace.detail |Query trace details. |
|apmplus\-server.trace.log |Query trace\-related logs. |
|apmplus\-server.span.list |Query the Span list. |
|apmplus\-server.log.list |Query Server\-side Monitoring logs. |
|apmplus\-server.service.list |Query the service list. |
|apmplus\-server.service.topo |Query service topology. |
|apmplus\-server.alert.rule\-list |Query alert rules. |
|apmplus\-server.alert.history\-list |Query alert history details. |
|apmplus\-server.alert.aggregated\-history\-list |Query aggregated alert history. |
|apmplus\-server.notify\-group.list |Query notification groups. |
|apmplus\-server.genai.session\-list |Query GenAI sessions. |





</Tab>
<Tab zoneid="MMp6TbBL9J" title="Cloud Monitor">
<TabTitle>Cloud Monitor</TabTitle>

The following commands are provided for Cloud Monitor:


|Command |Feature |
|---|---|
|cm.namespace.list |Query Cloud Monitor namespace. |
|cm.metric.query |Query cloud service metrics. |
|cm.metric.docs\-list |Query metric documentation. |
|cm.resource.list |Query resource metadata. |
|cm.resource.filter\-fields |Query resource filter fields. |
|cm.alarm.list |Query the alert rule list. |
|cm.alarm.get |Query alert rules by ID. |
|cm.alarm.history\-list |Query alert history. |
|cm.event.list |Query event history. |
|cm.event.types\-list |Query event types and sources. |





</Tab>
<Tab zoneid="B2LGxOSXId" title="Torch Log Service (TLS)">
<TabTitle>Torch Log Service (TLS)</TabTitle>

The following commands are provided for TLS:


|Command |Feature |
|---|---|
|tls.project.list |Query log projects. |
|tls.topic.list |Query log topics. |
|tls.topic.get |Query topic details. |
|tls.index.get |Query index configuration. |
|tls.search |Search logs. |
|tls.histogram |Query log volume histogram. |





</Tab>
<Tab zoneid="aCiaO4Svh0" title="Vital Kubernetes Engine (VKE)">
<TabTitle>Vital Kubernetes Engine (VKE)</TabTitle>

The following commands are provided for VKE:


|Command |Feature |
|---|---|
|vke.cluster.list |Query the cluster list. |
|vke.cluster.get |Query cluster details. |
|vke.nodepool.list |Query the node pool list. |
|vke.nodepool.get |Query node pool details. |
|vke.node.list |Query the node list. |
|vke.addon.list |Query cluster add\-ons. |
|vke.addon.supported\-list |Query the list of supported add\-ons. |
|vke.kubeconfig.list |Query kubeconfig. |
|vke.ns.list |Query Kubernetes namespaces. |
|vke.pod.list / vke.pod.get / vke.pod.logs |Query the Pod list, details, and logs. |
|vke.deployment.list / vke.deployment.get |Query Deployments. |
|vke.statefulset.list / vke.statefulset.get |Query StatefulSet. |
|vke.service.list / vke.service.get |Query services. |
|vke.event.list |Query Kubernetes events. |





</Tab>
<Tab zoneid="QVWBu5IhXZ" title="Other platforms and auxiliary commands">
<TabTitle>Other platforms and auxiliary commands</TabTitle>

Other platform and auxiliary commands:


|**Command** |**Feature** |
|---|---|
|login |Console OAuth login (writes a temporary STS profile). |
|login start / login finish |Two\-step remote login. Preferred for agent, SSH, or container scenarios. |
|logout |Clean up login status. |
|doctor |Check credentials, configuration, and network. |
|schema \-\-index |View an operation summary across all products. |
|schema <product\> |View the product\-level JSON Schema bundle. |
|list [product] |View the list of read\-only operations. |
|config show |View local preference configuration. |
|config set |Set local preference configuration. |
|version |View the CLI version. |
|update \-\-check \-\-json / update \-\-yes |Check for and apply built\-in release source updates. |
|completion |Generate shell completion scripts. |





</Tab>
</Tabs>


<span id="IAkXCbfg"></span>
### Capability description

The following describes commonly used capability dimensions in troubleshooting. Each capability can work across multiple data sources.


<Tabs>
<Tab zoneid="mFqBdodPlM" title="Metric">
<TabTitle>Metric</TabTitle>

Agents can query metrics from **VMP**, **Server\-side Monitoring**, and **Cloud Monitor** through `veops-cli`.


* VMP and Server\-side Monitoring are suitable for custom business and infrastructure metrics. An agent can first list workspaces, and then construct PromQL statements using metric names and labels for instant or range queries.

* Cloud Monitor is suitable for correlating application\-layer anomalies with metrics of cloud resources such as ECS, CLB, RDS, and networks. For example, a maxed\-out ECS CPU usage, disk I/O fluctuations, or unhealthy CLB backends can all manifest as slow API responses.



|**Objective** |**What you can see** |
|---|---|
|Determine whether a service is abnormal |Error rates, latency, throughput, and availability |
|Analyze resource bottlenecks |CPU, memory, disk, network, and instance dimension metrics |
|Compare metrics before and after the release |whether the metric has spiked, dropped suddenly, or shows a deteriorating trend |
|Locate the time of an anomaly |The exact time when the anomaly starts (down to the minute), and whether it has recovered |


Sample prompts:

```Plain Text
Could you check if the P99 latency of service-a has risen significantly over the past hour.
Please check the growth rate of request_error_total for service-a in workspace xxx in the last hour.
Could you check whether the CPU, memory and network metrics of ECS instance i-xxx are abnormal over the past two hours.
```





</Tab>
<Tab zoneid="zMHSlSmSOc" title="Logs">
<TabTitle>Logs</TabTitle>

Agents can query logs from **TLS** and **Server\-side Monitoring**, and can also view log context and log volume distribution.

When troubleshooting with TLS, an agent first identifies the Project and Topic, then searches using keywords or structured conditions, and finally classifies the large volume of logs into a small number of error patterns.


|**Objective** |**What you can see** |
|---|---|
|Search error logs |error, exception, timeout, panic, and other keywords |
|Find representative samples |High\-frequency error patterns, typical stacks, and request IDs |
|View error trends |The time distribution of a specific log type (log histogram) |
|View the context |The request context around a specific error log |


Sample prompts:

```Plain Text
Search timeout and exception logs of checkout-api over the last 30 minutes and group them by error type.
Check the time distribution of error logs from topic xxx in the past 6 hours.
Please retrieve the full context logs for this request_id.
```





</Tab>
<Tab zoneid="dLjf9B3KFJ" title="Alert">
<TabTitle>Alert</TabTitle>

Agents can query alert rules, alert history, and currently active alerts from **VMP**, **Server\-side Monitoring**, and **Cloud Monitor**.


|**Objective** |**What can you see** |
|---|---|
|Understand why the alert is triggered |Rule expressions, thresholds, levels, and trigger objects |
|Reconstruct the alert timeline |Start time, recovery time, and current status |
|Query the impact scope |Associate services, instances, workspaces, or cloud resources |
|Help assess severity |P0/P1, whether it is triggered continuously, and whether it has recovered |


Sample prompts:

```Plain Text
Please troubleshoot this VMP alert rule-xxx to identify its trigger cause and verify if it has been resolved.
List all current active P0 alerts and sort them by impact scope.
Check if there are any cloud monitoring alerts associated with this CLB resource recently.
```





</Tab>
<Tab zoneid="XVxE0Upm8q" title="Traces and service topology">
<TabTitle>Traces and service topology</TabTitle>

**Server\-side Monitoring** is the backbone of application troubleshooting. Agents can query the service list, service metrics, trace details, Span list, and service topology.


* For common service issues, the typical approach is to first check error rates, latency, and QPS, and then drill down into traces and Spans.

* Server\-side Monitoring also covers GenAI session scenarios, which is particularly useful for analyzing services that have integrated large model capabilities. For example, when the response of an AI assistant slows down or its failure rate increases, the agent can use session and trace data to determine whether the issue lies in a slow model call, a slow downstream tool, or an anomaly in the service itself.



|**Objective** |**What can you see** |
|---|---|
|Locate slow requests |Slow Spans and the slowest calls |
|Analyze error traces |Which node is reporting errors, and whether the errors originate from a downstream dependency |
|View dependencies |Upstream, downstream, call direction, and impact scope |
|Analyze AI application traces |GenAI session failure reasons: model call errors, tool call errors, or business exceptions |
|Verify the root cause |Whether metrics, logs, and traces point to the same dependency |


Sample prompts:

```Plain Text
Please check this trace-id to locate the latency bottleneck and confirm whether it is caused by downstream dependencies.
Group the error Spans of service-a from the last 30 minutes by downstream service.
Please pull the failed sessions of the AI assistant over the past hour and analyze whether the failures stem from model issues, tool errors or business exceptions.
```





</Tab>
<Tab zoneid="dHHAsiWQgA" title="VKE cluster resources">
<TabTitle>VKE cluster resources</TabTitle>

When troubleshooting container issues, the agent can drill down from cluster health to specific Pod logs layer by layer. VKE covers two layers of capabilities:


* One layer is VKE OpenAPI native information, such as cluster, node pool, node, plogin, and Kubeconfig metadata.

* The other layer is read\-only Kubernetes API passthrough, such as Namespace, Pod, Deployment, StatefulSet, Service, Event, and Pod logs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">For queries within VKE clusters, a read\-only passthrough channel is used. You do not need to expose the Kubernetes API Server to the public Internet or configure kubeconfig locally.</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Permissions follow the account. A 403 response typically means the current account lacks Kubernetes access to the cluster, not that the network is unreachable.</div>




|**Objective** |**What you can see** |
|---|---|
|Cluster inspection |Cluster status, node pool status, and add\-on status |
|Node troubleshooting |Node\-to\-instance mapping and node pool membership |
|Workloads and events |Pod/Deployment/StatefulSet/Service status, restarts, and Warning Events |
|Container logs |Container logs of anomalous Pods |


Sample prompts:

```Plain Text
Please check the status of node pools, nodes and plugins in the ccvke-xxx cluster.
List all Pods in the default namespace that have restarted recently, and check their associated events.
Check the logs and recent events of abnormal Pods under the kube-system namespace.
```





</Tab>
</Tabs>


&nbsp;

<span id="ISyUctgu"></span>
## Typical scenarios

VeOps CLI is not meant to query a single API and return a JSON response. Instead, it organizes multiple queries around a troubleshooting task. The following are typical scenarios:

<span id="Hrpb0Lvg"></span>
### Scenario 1: Alert troubleshooting

When an alert is triggered, the most important thing is to quickly answer three questions: why it is triggered, how much impact it has caused, and whether it has already recovered.

With VeOps CLI, simply provide AI with the alert rule ID, alert name, or approximate time. AI will query the alert rules, alert history, related metrics, logs, and service information to reconstruct a complete timeline.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Troubleshooting path comparison:</div>



* <div data-tips="true" data-tips-type="default"><strong>Before</strong>: Open the alert page to check the rule, open the metric page to view the curve, go to the log platform to find errors, and finally write the conclusion manually.</div>


* <div data-tips="true" data-tips-type="default"><strong>After</strong>: AI directly outputs the trigger cause, metric changes, log samples, affected objects, and recommended actions.</div>



```Plain Text
Please troubleshoot this alert rule-xxx with the following parameters:
Time range: 10:00 to 11:00 today
Related service: order-api
Please provide the root cause, impact scope, current recovery status, and recommended next steps.
```


<span id="KfPrU5xw"></span>
### Scenario 2: Slow API response

A slow API response is rarely an isolated issue. It may stem from slow service code, a slow downstream dependency, a slow database, insufficient resources, or new logic introduced in a recent release. Looking at metrics alone can tell you that something is slow, but not where the slowdown is.

With VeOps CLI, AI can simultaneously use Server\-side Monitoring metrics, traces, Spans, service topology, and logs to first confirm the time window when latency increases, then identify slow traces, sort by Span duration, and finally determine whether the slowdown is concentrated in a particular downstream dependency.

```Plain Text
The P99 latency of checkout-api has increased significantly over the past two hours.
Please help me locate which layer introduces the latency and check whether it is related to downstream services or the recent release.
```


<span id="agR0B1AO"></span>
### Scenario 3: Post\-release validation

The most common concern after a release is "there are no obvious errors, but has anything gotten worse?" When validating manually, engineers typically compare error rates, latency, QPS, resource metrics, and logs before and after the release.

With VeOps CLI, AI can bring together key metrics before and after the release for comparison. If an increased error rate or degraded latency is detected, it will drill down further into logs and traces. The final output is not just "something changed," but specifically which metrics are degraded, by how much, whether there are representative errors, and whether you should continue observing or roll back.

```Plain Text
Please conduct a post-release review for me with the information below:
Service: payment-api
Release time: 20:00
Comparison window: 30 minutes before and after the release
Focus metrics: error rate, P99 latency, QPS, CPU usage, error logs
Determine whether performance degradation occurred after the release.
```


<span id="Sm64EORr"></span>
### Scenario 4: Cloud resource anomaly diagnosis

Many application issues ultimately trace back to the resource layer. A sudden CPU usage spike, insufficient disk space, abnormal network packet volume, or unhealthy CLB backends can all manifest as service API timeouts.

With VeOps CLI, you can query cloud resource metrics and Cloud Monitor alerts and events through Cloud Monitor, and then combine them with service anomalies detected by Server\-side Monitoring for a unified analysis.

```Plain Text
Timeouts for order-api have been on the rise since 14:00.
Please check the APMPlus metrics, error logs, as well as the CPU, memory and network metrics of the associated ECS instances simultaneously.
```


<span id="qj3jr5Md"></span>
### Scenario 5: VKE cluster inspection

Cluster inspection typically covers many objects, such as clusters, node pools, nodes, add\-ons, namespaces, Pods, Deployments, Events, and Pod logs. Checking them one by one manually is time\-consuming and prone to oversights.

With VeOps CLI, you can generate a structured inspection report that identifies which nodes are NotReady, which Pods are in CrashLoopBackOff, which events are concentrated around image pull failures, and which Deployments have fewer replicas than expected.

```Plain Text
Please perform an inspection of the ccvke-xxx cluster as follows:
Check the status of node pools, nodes and plugins
Identify abnormal Pods and Pods that have restarted recently
Summarize Warning Events across all namespaces
Provide handling recommendations for all abnormal items
```


<span id="OWZBB2gF"></span>
### Scenario 6: AI application observability troubleshooting

If your business has integrated large models or agent capabilities, the troubleshooting scope extends beyond standard HTTP APIs to include model calls, tool calls, long\-chain sessions, and multi\-turn conversations. The GenAI session capability in Server\-side Monitoring helps analyze AI application traces, making VeOps CLI suitable not only for traditional microservices but also for business systems that are integrating AI capabilities.

```Plain Text
Please retrieve all failed sessions of the AI assistant over the past hour.
Analyze whether the failures are caused by model invocation failures, tool invocation failures, or abnormal responses from business services.
```


<span id="HOkhr7U8"></span>
###
