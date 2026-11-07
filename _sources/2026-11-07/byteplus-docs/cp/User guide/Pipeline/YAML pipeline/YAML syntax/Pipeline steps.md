---
title: "Pipeline steps"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Pipeline_steps"
---

A step is the smallest execution unit within a task. A task can be composed of a single step or multiple steps, which are executed sequentially in the declared order.

<span id="4kSipsVR"></span>
## YAML example

```YAML
    tasks:
      - task: cmd-exec
        displayName: command
        timeout: 2h
        resourcesPolicy: all
        steps:
          - step: exec-cmd
            displayName: command
            component: exec@1.0.0
            inputs:
              cmd: echo hello
              shell: BASH
        resources:
          limits:
            cpu: 1C
            memory: 2Gi
```


<span id="8voru18e"></span>
## Parameter


|**Parameter** |Required |**Description** |
|---|---|---|
|steps.step |Yes |The ID of the step **.**  The ID must meet the following requirements:<br><br><br>* Only lowercase letters (a\-z), digits (0\-9), and hyphens (\-) are allowed.<br><br>* Must begin with a lowercase letter or digit.<br><br>* Must end with a lowercase letter or digit.<br><br>* Length must be between 1 and 40 characters. |
|steps.component |Yes |Specify the actual add\-on and its version to be executed for this step, in the format <Addon name\>@<Version\>, for example `execCmd@1.0.0`. For a description of the add\-on parameters, see  ** ** [Add-on list](https://docs.byteplus.com/en/docs/cp/List_of_component?lang=en) **.**  |
|steps.displayName |No |The name of the step as displayed in the pipeline console interface. The displayName must be between 1 and 50 characters in length. |
|steps.allowFail |No |Whether failure skipping is allowed. Valid values:<br><br><br>* `true`: Failure skipping is allowed.<br><br>* `false`: Default value, failure skipping is not allowed. |
|steps.inputs |Yes |Input parameters passed to the step. Parameters differ among steps; for specific parameter descriptions, see  ** ** [Step list](https://docs.byteplus.com/en/docs/cp/List_of_steps) **.**  |
