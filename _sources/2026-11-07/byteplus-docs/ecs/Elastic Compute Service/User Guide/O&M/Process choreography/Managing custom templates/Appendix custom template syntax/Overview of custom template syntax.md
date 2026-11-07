---
title: "Overview of custom template syntax"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview_of_custom_template_syntax"
---

Template syntax defines the template structure, including parameters, execution order, constraints on input/output fields, and validation rules. BytePlus allows you to define custom templates in JSON format. The following template structure is supported.

```JSON
{
  "FormatVersion": "0.2",
  "Description": "",
  "Parameters": {},
  "Tasks": [],
  "Outputs": {}
}
```



|Parameter |Description |
|---|---|
|FormatVersion |Optional. The engine version. The default value is 0.2. |
|Description |Optional. The description of details such as the usage and purpose of the template. |
|Parameters |Optional. Defines the list of parameters used during template execution. [Learn more](https://docs.byteplus.com/en/docs/ecs/Overview_of_custom_template_syntax#2kEHdh1B). |
|Tasks |Required. The Tasks parameter is the most important component of a template. Each task defines a specific action to be executed. These actions are defined and implemented by the Orchestration service. [Learn more](https://docs.byteplus.com/en/docs/ecs/Overview_of_custom_template_syntax#iLk2JfAg).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If multiple tasks exist, they are executed sequentially by default, following the top\-to\-bottom order.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If a task is a loop task, concurrent sub\-executions may occur within that task.</div><br> |
|Outputs |Optional. The Outputs parameter defines key data produced after template execution and can reference the output of a task (by specifying the task name). [Learn more](https://docs.byteplus.com/en/docs/ecs/Overview_of_custom_template_syntax#A39kFSTs). |


<span id="2kEHdh1B"></span>
## Parameters description

The Parameters parameter defines the list of parameters used during template execution, including parameter names, types, and default values.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If no default value is specified, the default value is the zero value of the parameter type (that is, the default initial value for that type).</div>


```JSON
{
    "Parameters": {
        "InstanceId": {
            "Type": "String" // Required. The type, which can be String, Number, List, Boolean, and Map.
            "DisplayName":"" // Optional. The display name. If this field is added, the value of DisplayName is shown when you create an orchestration plan. If this field is not added, the key of the field is shown instead.
        },
        "ForceStop": {
            "Type": "Boolean", // Optional. The type, which can be String, Number, List, Boolean, and Map.
            "Default": true // Optional. The default value. You can set Default to true or false. The default value is true.
        }
    }
}

```


<span id="iLk2JfAg"></span>
## Tasks description

The Tasks parameter is the most important component of a template. Each task defines a specific action to be executed. These actions are defined and implemented by the Orchestration service, and include atomic actions and cloud product\-specific actions. [Learn more](https://docs.byteplus.com/en/docs/ecs/Action_list).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If multiple tasks exist, they are executed sequentially by default, following the top\-to\-bottom order. If a task is a loop task, concurrent sub\-executions may occur within that task.</div>


* <div data-tips="true" data-tips-type="default">The number of tasks specified by the Tasks parameter in a custom template cannot exceed 30.</div>



<span id="IkboF2zu"></span>
### Tasks structure

```JSON
{
    "Tasks": [
        {
            "Name": "TaskNa****",
            "Description": "description",
            "Action": "TaskType",
            "ActionInfo": "TaskType",
            "Timeout": 10,
            "Parameters": { 
                "Property1": "Value1",
                "Property2": "Value2"
            },
            "Outputs": { 
                "outputParameterName1": {
                    "Type": "String",
                    "ValueSelector": "{{ .jqselector }}"
                }
            },
            "Loop": { 
                
            },
            "OnError": "VOS::END/VOS::NEXT/other-task-name",
            "OnSuccess": "VOS::NEXT/other-task-name/VOS::END"
        }
    ]
}
```



|Parameter​ |Required |Description |
|---|---|---|
|Name |Yes |The task name. Valid values:<br><br><br>* It can contain only letters, digits, hyphens (\-), and underscores (_).<br><br>* It can contain 1 to 200 characters in length. |
|Description |No |The description that explains the purpose of the current task. |
|Action |Yes |The name of the action. |
|Timeout |No |Optional. The timeout period. The maximum timeout period is 600 seconds. |
|Parameters |No |The set of parameters required for the execution of the current task. The parameter values can be obtained by using JQ expressions. The required parameters are determined by the specific actions. For more information, see the "Actions" topic. |
|Outputs |No |The output definition of the current task, which can be used as the input for subsequent tasks or as the output of the template. [Learn more](https://docs.byteplus.com/en/docs/ecs/Overview_of_custom_template_syntax?lang=zh&TagIDs=2,288,70,69#A39kFSTs).<br><br><br>* Type: The field type.<br><br>* Value: The field value. |
|Loop |No |The task loop. For more information, see [Loop tasks](https://docs.byteplus.com/en/docs/ecs/Overview_of_custom_template_syntax#QMJxK9iL). |
|OnError/OnSuccess |No |The subsequent operation when the task execution result is either failure or success. Value:<br><br><br>* **OnError**: Used to define the operation when task execution fails. When you set OnError to:<br><br>   * VOS::END (**default**): The entire execution is terminated.<br><br>   * VOS::Next: The next task is executed.<br><br>* **OnSuccess**: Used to define the operation when task execution succeeds. When you set OnSuccess to:<br><br>   * VOS::END: The entire execution is terminated.<br><br>   * VOS::Next (**default**): The next task is executed. |


<span id="QMJxK9iL"></span>
### Loop tasks

BytePlus provides a special attribute called "loop task" for the Tasks parameter. In a loop task, batch tasks are automatically generated and executed based on the item list specified by LoopItem. You can specify parameters such as execution batches and concurrency to enable large\-scale task scheduling.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Tasks for API actions and cloud product actions support looping, while tasks for functional actions such as Trigger and Sleep do not support looping.</div>


* <div data-tips="true" data-tips-type="default">Loop tasks support concurrent execution. However, when running in single\-step mode, looped tasks are automatically adjusted to execute sequentially with no concurrency.</div>


* <div data-tips="true" data-tips-type="default">A loop task is equivalent to executing the same task multiple times with different input parameters.</div>


* <div data-tips="true" data-tips-type="default">VOS::LoopItem is a built\-in variable used to specify that the parameter value is sourced from the loop items defined by the Loop field. For example, each element in {{ .InstanceIds }} is retrieved sequentially by using this variable.</div>



<span id="CwJiBsl1"></span>
#### Limits

The maximum number of loop items is currently 1,000.

<span id="OUdXAEoo"></span>
#### Syntax structure

```JSON
{
    "Parameters": {
        "InstanceIds": {
            "Type": "List"
        }
    }, 
    "Tasks": [
        {
            "Name": "StartInstances", 
            "Action": "VOS::ECS::StartOneInstance", 
            "Parameters": {
                "InstanceId": "{{ VOS::LoopItem }}"
            }, 
            "Outputs": {
                "InstanceStatus": {
                    "Type": "String", 
                    "Value": "{{ .InstanceStatus }}"
                }
            }, 
            "Loop": {
                "LoopItem": "{{ .InstanceIds }}", 
                "Outputs": {
                    "LoopInstanceStatus": {
                        "SelectedOutputFiled": "InstanceStatus"
                    }
                }
            }
        }
    ], 
    "Outputs": {
        "InstanceStatus": {
            "Type": "List", 
            "Value": "{{ .\"StartInstances.LoopInstanceStatus\" }}"
        }
    }
}
```


<span id="kfVTtm94"></span>
#### Parameter description


* LoopItem: The loop object.

* Outputs: The output of a single task.

* Concurrency control

   * Mode: Executes tasks by group. You can set this parameter to Batch or Concurrency and specify the maximum number of errors.

      * Batch: Divides the total number of tasks into batches. Parameter Description:

         * BatchSize: The number of items in each batch. The default value is 1.

         * BatchPauseOption: Specifies whether a pause is required between batches. By default, the next batch is executed automatically.

         * MaxErrorsValue: The maximum number of errors.

      * Concurrency: Concurrent execution.

         * ConcurrencySize: The concurrency level.

         * MaxErrorsValue: The maximum number of errors.


<span id="A39kFSTs"></span>
## Outputs description

The Outputs parameter retrieves key data after template execution. It ensures users can accurately obtain required results such as post\-operation instance statuses, task IDs, and execution time.

Example:

```JSON
{
  "Parameters": {
    "InstanceId": {
      "Type": "String"
    },
    "ForceStop": {
      "Type": "Boolean"
    }
  },
  "Tasks": [
    {
      "Name": "CheckInst****",
      "Action":"VOS::CheckFor",
      "Parameters": {
        "APIInfo":{
          "Service": "ecs",
          "APIName": "DescribeInst****",
          "Version": "2020-04-01",
          "Parameters": {
            "InstanceIds": "{{ [.InstanceId] }}"
          },
          "DesiredValues": ["RUNNING"],
          "NotDesiredValues": ["ERROR", "STOPPED"],
          "ValueSelector": "{{ [.Instances[].Status] }}"
        }
      },
      "Outputs": {
        "InstanceStatus": {
          "Type": "List",
          "Value": "{{ [.Instances[].Status] }}"
        }
      }
    }
  ],
  "Outputs": {
    "InstanceStatus": {
      "Type": "String",
      "Value": "{{ .\"CheckInstances.InstanceStatus\".[0] }}"
    }
  }
}
```
