---
title: "Pipeline tasks"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Pipeline_tasks"
---

A task is an independent execution unit in a pipeline. Tasks within the same stage run in parallel by default, but can be configured for serial execution by setting task dependencies with `dependsOn`.

<span id="wDrB1jOd"></span>
## Application scenarios

A task can consist of multiple [Step (steps)](https://docs.byteplus.com/en/docs/cp/Pipeline_steps) or consist of a single [Addon (component)](https://docs.byteplus.com/en/docs/cp/Pipeline_component).


* **Step combination**: Suitable for executing strongly associated actions sequentially. For example, a build task can be divided into steps such as installing dependencies, running tests, and compiling code, with all steps sharing the same workspace environment.

* **Single Addon**: Suitable for invoking standardized, self\-contained, and independent capabilities. For example, in scenarios such as manual approval checkpoints or Kubernetes image upgrades, the addon encapsulates the underlying complex logic, and you only need to provide the required input parameters to use it directly.


<span id="lArnfbVV"></span>
## Basic configuration parameters


|**Parameter** |Required |**Description** |
|---|---|---|
|tasks.task |Yes |Task ID. ID must meet the following requirements:<br><br><br>* Only lowercase letters (a\-z), digits (0\-9), and hyphens (\-) are allowed.<br><br>* Must start with a lowercase letter or digit.<br><br>* Must end with a lowercase letter or digit.<br><br>* Length must be 1–40 characters. |
|tasks.displayName |No |Task display name, shown in the pipeline Console interface. The displayName length must be 1–50 characters. |
|tasks.timeout |Yes |Default is 2h. The timeout time for task execution. Supports m (minutes), h (hours), and d (days) units. The maximum is 3 days. |
|tasks.retries |No |Number of task retries, value range is 1–5. If not specified, no retry will be performed. |
|tasks.resourcesPolicy |No |Whether to download the code source. The following values are supported:<br><br><br>* `all`: Download the code source. Currently, only a single code source is supported.<br><br>* `none`: Do not download the code source. |
|tasks.steps |No |List of steps for task execution. If there is no component in the task, steps are required. |
|tasks.component |No |Specify the target Addon. If there are no steps in the task, component is required. |
|tasks.inputs |No |Input parameters passed to the Addon. Required when tasks.component exists. Parameters differ among Addons. For detailed parameter description, see  ** ** [Add-on list](https://docs.byteplus.com/en/docs/cp/List_of_component) **.**  |


<span id="f6aO85h8"></span>
## Workspace configuration


|**Parameter** |Required |**Description** |
|---|---|---|
|tasks.workspace |No |The workspace ID. The ID must meet the following requirements:<br><br><br>* Only lowercase letters (a\-z), digits (0\-9), and hyphens (\-) are allowed.<br><br>* Must start with a lowercase letter or digit.<br><br>* Must end with a lowercase letter or digit.<br><br>* Length must be between 1 and 40 characters. |
|tasks.workspace.resources |No |Workspace resource reference list.Required when workspace is not specified or resourcesPolicy is set to all. |
|tasks.workspace.resources.ref |No |Name of the referenced code source, corresponding to sources.name.Required when workspace is not specified or resourcesPolicy is set to all. |
|tasks.workspace.resources.directory |No |Code download directory, typically use the `$(CP_WORKSPACE) ` variable.Required when workspace is not specified or resourcesPolicy is set to all. |


**Workspace example**

```YAML
          workspace:
            resources:
                - ref: svcConn-demo
                  directory: $(CP_WORKSPACE)
```


<span id="Wu7IzaQQ"></span>
## Cache configuration

The cache feature allows files or directories to be persistently stored and reused across multiple pipeline runs, thereby accelerating build speed.


|**Parameter** |Required |**Description** |
|---|---|---|
|tasks.workspace.caches.key |No |Cached ID. ID must meet the following requirements:<br><br><br>* Only lowercase letters (a\-z), digits (0\-9), and hyphens (\-) are allowed.<br><br>* Must start with a lowercase letter or digit.<br><br>* Must end with a lowercase letter or digit.<br><br>* Length must be 1–40 characters. |
|tasks.workspace.caches.path |No |Directory path to be cached. |


**Cache example**

```YAML
    workspace:
      caches:
        - cacheKey: m2
          directory: $(CP_WORKSPACE)/.m2
          cachePolicy: pull-push
```


<span id="xwZvv4Se"></span>
## Resource configuration


|**Parameter** |Required |**Description** |
|---|---|---|
|tasks.resources.limits.cpu |Yes |CPU LimitRange (default: 1C). |
|tasks.resources.limits.memory |Yes |Memory LimitRange (default: 2Gi). |


**Resource configuration example**

```YAML
resources:
  limits:
      cpu: 1C
      memory: 2Gi
```


<span id="wO4p96cs"></span>
## Task dependency configuration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">dependsOn only supports configuring task dependencies within the same stage. Please avoid circular dependencies during configuration, such as task A depending on B, B depending on C, and C depending on A.</div>



|**Parameter** |Required |**Description** |
|---|---|---|
|tasks.dependsOn |No |List of identifiers for dependent tasks. This task is executed only after all preceding dependent tasks succeed. |


**Dependency example**

```YAML
tasks:
  - task: go-test
    displayName: test
    timeout: 2h
    steps: [...]
  - task: go-compile
    displayName: compile
    dependsOn:
      - go-test
    timeout: 2h
    steps: [...]
```


<span id="IU7nq6X4"></span>
## Notification add\-on configuration


|**Category** |**Parameter** |Required |**Description** |
|---|---|---|---|
|Basic configuration |tasks.plugins.plugin |Yes |The type of add\-on. Must be set to webhook. |
||tasks.plugins.conditions<br><br> |Yes |Trigger condition. Supported values are as follows:<br><br><br>* `TaskStarted`: Task started.<br><br>* `TaskSucceeded`: Task succeeded.<br><br>* `TaskFailed`: Task failed.<br><br>* `TaskCanceled`: Task canceled.<br><br>* `TaskWaiting`: Task waiting. |
|Input parameters |tasks.plugins.inputs.type |Yes |Notification type. Supported values are as follows:<br><br><br>* `Feishu`: Feishu bot.<br><br>* `Common`: Standard Webhook. |
||tasks.plugins.inputs.url |Yes |Webhook receiving address. |
||tasks.plugins.inputs.token |No |Authentication token, used for API authentication. |
||tasks.plugins.inputs.content |No |Custom notification content. |
||tasks.plugins.inputs.optionValues |No |Information fields included in the notification. Required when `tasks.plugins.inputs.type` is `Lark`. The following values are supported:<br><br><br>* `BasicInfo`: Basic information.<br><br>* `TriggerPerson`: Trigger person.<br><br>* `TriggerEvent`: Trigger event.<br><br>* `TriggerTime`: Trigger time.<br><br>* `TriggerDetail`: Trigger details.<br><br>* `PipelineAddress`: Pipeline address. |


**Notification add\-on example**

```YAML
plugins:
  - plugin: webhook
    conditions:
      - TaskStarted
      - TaskSucceeded
    inputs:
      content: custom
      optionValues: BasicInfo,TriggerPerson,TriggerEvent,TriggerTime,TriggerDetail,PipelineAddress
      token: token
      type: Lark
      url: https://open.larkoffice.com/open-apis/bot/v2/hook/<your-hook-id>
```
