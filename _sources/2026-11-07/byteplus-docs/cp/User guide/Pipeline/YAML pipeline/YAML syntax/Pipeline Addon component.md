---
title: "Pipeline Addon component"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Pipeline_component"
---

An Addon is an atomic unit of the pipeline that encapsulates a specific feature and is reusable. It is typically an agentless task (a task that can be completed without a workload inside the Cluster). When tasks directly use the Addon, there is no need to configure steps.

<span id="PgcE9BdO"></span>
## Parameter


|**Parameter** |Required |**Description** |
|---|---|---|
|tasks.component |Yes |Specify the target Addon and version in the format <Addon name\>@<Version\>, for example `manualApproval@1.0.0`. For details, see [Addon list](https://docs.byteplus.com/en/docs/cp/List_of_component). |
|tasks.inputs |Yes |Input parameters passed to the step. The parameters differ in each step. For specific parameter descriptions, see  ** ** [Step list](https://docs.byteplus.com/en/docs/cp/List_of_steps) **.**  |


<span id="WlIG8Tvv"></span>
## YAML example

<span id="ACmoUQMw"></span>
#### Manual approval checkpoint example

```YAML
stages:
    - stage: stage-c1
      displayName: Manual Approval Stage
      tasks:
        - task: task-c2
          displayName: Manual Checkpoint 
          component: manualApproval@1.0.0/manual-approval
          inputs:
            approvalType: Or
            approvers: 210048****,0;210048****,539****
            notification:
                enable: false
            timeout: 24h
```


<span id="wkBWSB1E"></span>
#### Kubernetes image upgrade example

```YAML
stages:
    - stage: stage-c3
      displayName: deply stage
      tasks:
        - task: task-c4
          displayName: Kubernetes image upgrade
          component: appdeliver@2.0.0/kubernetes-update-image
          inputs:
            app:
              kind: Deployment
              name: prod-cluster
            containerName: prod-cluster
            deployImage:
              content: $(stages.stage-c6.tasks.task-c7.outputs.imageOutput_step-c2)
              type: Output
            deployResource: aa0900bb79a94de6a55f30b7ac7****
            namespace: ai-prod-cluster
```
