---
title: "Runtime instance overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Runtime_instance_overview"
---

A runtime instance (referred to as "instance" hereafter) is the underlying hosting unit of the AgentKit agent runtime, running agent tasks in an isolated compute and network environment and providing observability capabilities such as logs, metrics, and events.

<span id="Sb3OcltB"></span>
## What is an instance

An instance is the independent runtime environment that AgentKit allocates for an agent application. Think of an instance as the "execution unit" of your application: the application's code, configuration, dependencies, and runtime version all take effect within the instance, and incoming external requests are handled by the instance.

On the "Instance management" page, you can view the number of running instances and get a resource overview covering CPU, memory, and public outbound traffic. Once an instance is reclaimed by the platform and its runtime environment is released, it no longer processes requests.

<span id="biyDLbnm"></span>
## How it works

An instance is the execution unit of an agent application. The system launches instances based on the application configuration. An instance is in the "Starting" state when it becomes visible in the console, and transitions to "Ready" once initialization is complete, at which point it begins serving external requests.

Instances can be launched in two ways: on\-demand launch and minimum instance guarantee. When incoming traffic is detected, instances are automatically launched to handle requests. If a minimum instance count is configured (greater than 0), at least that number of instances will remain active even when there is no traffic. Once a request enters an instance, it is processed according to the application logic, including inference and tool calls. Logs, resource usage, and network traffic are recorded to support troubleshooting and cost monitoring.

<span id="ZMKTTz4a"></span>
## Core capabilities


|**Capability** |**Description** |**Typical scenarios** |
|---|---|---|
|Runtime hosting |Provides an independent runtime environment for agent applications, enabling them to continuously handle requests. |Once the application is deployed, it serves external requests such as agent Q&A, task processing, and tool calls. |
|Status viewing |Displays the instance name, status, runtime version, and creation time, helping you quickly determine whether an instance is available. |Confirm whether an application has started, or look up the creation time and version of a specific instance. |
|Resource observability |Displays the number of running instances, cumulative CPU usage, cumulative memory usage, and public outbound traffic. |Assess the application's operational scale, resource consumption trends, and network traffic usage. |
|Log\-based troubleshooting |Supports viewing instance logs to help identify startup failures, request errors, or business logic errors. |Troubleshoot issues when the application responds abnormally, a tool call fails, or an instance enters an abnormal state. |
|Webshell debugging |Supports accessing the instance runtime environment via Webshell to inspect the live runtime state or perform necessary debugging operations. |Perform online troubleshooting when you need to inspect files, dependencies, environment variables, or the state of running processes. |
|Instance reclamation |Supports automatic instance reclamation, with the minimum instance count configuration controlling instance keep\-alive and termination. |Instances are automatically terminated after the application goes idle. Configure the minimum instance count to keep instances alive, or set the minimum instance count to 0 to trigger reclamation. |


<span id="LAjBAviJ"></span>
## Instance lifecycle

The instance lifecycle begins when the application is deployed. After the platform generates the runtime environment, the instance enters the "Starting" state when it becomes visible in the console, and transitions to "Ready" once initialization is complete, at which point it begins handling requests. While running, an instance continuously generates the following three types of observability data for monitoring and troubleshooting:


* **Resource usage**: Compute resources on the instance side, such as CPU and memory.

* **Network traffic**: Inbound and outbound traffic metrics, including public outbound traffic.

* **Runtime logs**: Runtime logs generated during application startup, dependency loading, and request processing.


<span id="58VhkQfr"></span>
### Two scenarios for instance termination

How an instance is terminated depends on the configuration of the **Minimum number of instances** parameter:

> **Minimum number of instances**: The minimum number of instances that the platform keeps running at all times to preserve immediate responsiveness during idle periods.



|**Minimum number of instances** |**Behavior when idle** |**How to reclaim proactively** |Application scenarios and trade\-offs |
|---|---|---|---|
|0 |When the application is idle, the platform automatically reclaims the instance. |No action required. Wait for automatic reclamation. |This approach lowers resource costs, but the first request after being idle requires a cold start and has higher latency. It is suitable for workloads with volatile traffic that are not sensitive to first\-request latency. |
|Greater than 0 |The configured instances remain active at all times and are not automatically reclaimed when idle. |Manually set the value to 0 first. Existing instances will be gradually terminated and reclaimed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Setting the "Minimum number of instances" to 0 may affect the continuous availability of your application. Before making this change, confirm whether the application still has active online traffic, and retain any necessary logs and troubleshooting information to avoid difficulties reproducing issues after the instance is reclaimed.</div><br> |Persistent instances ensure immediate responsiveness with fewer cold starts. Resource costs are higher accordingly. Suitable for production workloads with stable traffic or those sensitive to cold start latency. |


<span id="iV8qkrsc"></span>
### Instance status description

Instance status describes the current phase of an instance during its lifecycle, from startup through running to termination. You can use the status to determine whether an instance is ready to handle requests or whether you need to check the logs for further troubleshooting.


|**Status** |**Explanation** |**Recommendation** |
|---|---|---|
|Starting |The instance is visible in the console. The platform is preparing the runtime environment and initializing the application. |Wait for the instance to finish starting. If the instance remains in this state for an extended period, check the logs to troubleshoot the initialization process. |
|Ready |The instance has been successfully initialized and is ready to handle requests. |You can access the application and use the resource overview to monitor CPU, memory, and public outbound traffic. |
|Failed |The instance failed to initialize. This typically indicates an error during application startup, dependency loading, or runtime environment preparation. |Check the instance logs to identify the cause of the failure, and then redeploy or adjust the application configuration. |
|Terminating |The instance is stopping and releasing its runtime environment. |Wait for termination to complete. During this phase, the instance may not be able to handle requests reliably. We recommend that you do not route production traffic to this instance. |
|Unknown |The platform is temporarily unable to retrieve the instance status. This may be caused by a status synchronization error or a failure to read instance information. |Refresh the page later or check the logs. If the status remains unknown, contact technical support for further troubleshooting. |


<span id="UuPuVikZ"></span>
## Usage suggestions


* **Routine inspection:**  Start by checking the instance status and resource overview. If the instance count, CPU/memory usage, or public outbound traffic appears abnormal, use the instance list and logs to identify the cause.

* **Troubleshooting:**  Check the logs first. If you need to further inspect the environment, dependencies, or processes, access the Webshell. Before reclaiming instances, making configuration changes, or taking the application offline, assess the potential impact.

* **Releasing resources:**  In a testing scenario, reclaim instances promptly after verification is complete. In a production scenario, confirm that the instance is no longer receiving active traffic and retain any necessary logs before setting the minimum instance count to 0 to trigger reclamation.


<span id="uILMbFXt"></span>
## Related operations


* [Viewing runtime instance logs](https://docs.byteplus.com/en/docs/86681/2616988): Use this feature to help identify issues when an instance fails to start, a task encounters an error, or an instance remains in the "Starting" state for an extended period or enters the "Failed" state.

* [Updating instance configurations](https://docs.byteplus.com/en/docs/agentkit/Updating_instance_configurations): Use this feature to adjust the minimum instance count, maximum instance count, and concurrent request threshold per instance when your workload scales up or down.

* [Running Shell commands in runtime instances](https://docs.byteplus.com/en/docs/agentkit/Viewing_runtime_instances_via_WebShell): Use this feature to access the instance runtime environment for online troubleshooting and temporary debugging, such as inspecting files, processes, and environment variables.
