---
title: "Pipeline sources"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Pipeline_sources"
---

Pipeline sources (sources) are used to declare the code sources and artifacts that trigger the pipeline, defining "where the pipeline comes from and why it starts". Through the sources block, you can connect to multiple code repositories such as GitHub, GitLab, and more, configure branch filtering, path filtering, and event trigger rules, and support configuring multiple code sources simultaneously.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In Pipeline as Code, code sources only support access through service connection. For methods to create a service connection, see <a href="https://docs.byteplus.com/en/docs/cp/Service_connection">Service connection</a>.</div>


<span id="yi7O0PlZ"></span>
## YAML example

```YAML
sources:
    - name: svcConn-demo
      type: Gitee
      url: https://gitee.com/volc-code-pipeline/demo.git
      branch: master
      credential:
        type: serviceConnection
        serviceConnectionId: ctAIccWNZvRLkgffPWXF
      trigger:
        triggerExecutionType: AllEvents
        autoPRComment: 
            commentRule: PipelineStatus
        triggerEvents:
          - eventType: Push
            branchFilters:
              - master
              - dev
```


<span id="wanZy0T9"></span>
## Basic configuration parameters


|**Parameter** |Required |**Description** |
|---|---|---|
|sources.name |Yes |Code source name. During pipeline runtime, source files will be downloaded to the `/workspace` directory. The name must meet the following requirements:<br><br><br>* Can only include lowercase letters (a\-z), digits (0\-9), and hyphens (\-).<br><br>* Must start with a lowercase letter or digit.<br><br>* Must end with a lowercase letter or digit.<br><br>* Length must be 1~40 characters. |
|sources.type |Yes |Code source type. For supported code source types, see [Code source overview](https://docs.byteplus.com/en/docs/cp/An_overview_of_the_code_source). |
|sources.url |Yes |Code source repository URL, supports HTTPS protocol. |
|sources.branch |Yes |Pipeline running branch. |
|sources.branchMode |No |Branch mode is not enabled by default. Only one code source is allowed to enable branch mode. |
|sources.branchMode.baseBranch |Required when branch mode is enabled. |Required when branch mode is enabled. The base branch for pulling code in branch mode. |
|sources.cloneDepth<br><br> |No |Default is 1. Clone depth value represents the number of recent versions to clone.<br><br><br>* 0 means clone all versions.<br><br>* 1 means clone only the most recent version. |


<span id="VX8HjCs7"></span>
## Authorization configuration


|**Parameter** |Required |**Description** |
|---|---|---|
|sources.credential |Yes |Authorization information for cloning the code source. |
|sources.credential.type |Yes |Enter `serviceConnection` as a fixed value, indicating the use of a service connection. |
|sources.credential.serviceConnectionId |Yes |ID. Go to **Global settings \> Service connection** to view the target service connection's ID in the service list. |


<span id="lVgyegH8"></span>
## Trigger configuration


|**Parameter** |Required |**Description** |
|---|---|---|
|sources.trigger |No |If not configured, the pipeline cannot be triggered by code source events. |
|sources.trigger.triggerEvents.eventType |Yes |<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The trigger events supported by different code sources may vary. For details, see <a href="https://docs.byteplus.com/en/docs/cp/Trigger_events_and_trigger_conditions">code source trigger</a>.</div><br><br><br>Trigger event types, with the following values:<br><br><br>* `Push`: Code push event, commonly used for continuous integration with the main and feature branches.<br><br>* `CreateTag`: Tag creation event, commonly used for version release.<br><br>* `PRMerged`: Event after a merge request is merged.<br><br>* `PRUpdated`: Event when a merge request is created or updated, commonly used for pre\-merge validation. |
|sources.trigger.triggerEvents.branchFilters |No |Branch filter list, supports entering branch names or Go language regular expressions. |
|sources.trigger.triggerExecutionType |No |Type of trigger event execution. The values are as follows:<br><br><br>* `OnlyLatest`: Only the latest event triggers execution.<br><br>* `AllEvents`: All events trigger execution. |
|sources.trigger.triggerExecutionType.autoPRComment.commentRule |No |After pipeline execution is complete, automatically post a comment in the pull request (PR). Only takes effect when `eventType` is `PRUpdated`. Valid values:<br><br><br>* PipelineTaskStatus: The comment includes the pipeline running state and each task running state.<br><br>* PipelineStatus: The comment only includes the pipeline running state.<br><br>* None: No automatic comment. |
