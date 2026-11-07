---
title: "Atomic actions"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Atomic_actions"
---

This topic introduces demos related to atomic actions.

<span id="GgKmXyOM"></span>
## API actions

API\-related actions include VOS::ExecuteAPI, VOS::WaitFor, and VOS::CheckFor.

<span id="MmMl4rtc"></span>
### VOS::ExecuteAPI example

```JSON
{
    "Tasks": [
        {
            "Name": "RebootInstance",
            "Description": "{\"zh-cn\":\"Restart Instance\",\"en\":\"RebootInstance\"}",
            "Action": "VOS::ExecuteAPI",
            "Parameters": {
                "APIInfo": {
                    "Service": "ecs",
                    "APIName": "RebootInstance",
                    "Version": "2020-04-01",
                    "Parameters": {
                        "ForceStop": "Value1",
                        "InstanceId": "Value2"
                    }
                }
            },
            "Outputs": {
                "Result1": {
                    "Type": "List",
                    "Value": [

                    ]
                }
            }
        }
    ]
}
```


<span id="SyEiVueH"></span>
### VOS::WaitFor example

```JSON
{
    "Tasks": [
        {
            "Name": "untilInstanceRunningOrStopped",
            "Description": "Wait for the ECS instance to reach the running or stopping state",
            "Action": "VOS::WaitFor",
            "Parameters": {
                "APIInfo": {
                    "Service": "ecs",
                    "APIName": "DescribeInstances",
                    "Version": "2020-04-01",
                    "Parameters": {
                        "InstanceIds": "{{ [.\"describeVolumeStatus.attachedInstanceId\"] }}"
                    },
                    "DesiredValues": [
                        "RUNNING",
                        "STOPPED"
                    ],
                    "NotDesiredValues": [
                        "STOPPING"
                    ],
                    "ValueSelector": "{{ [.Instances[].Status] }}"
                }
            }
        }
    ]
}
```


<span id="ox3Kxhaq"></span>
### VOS::CheckFor example

```JSON
{
    "Tasks": [
        {
            "Name": "checkInstanceReady",
            "Description": "Check instance status",
            "Action": "VOS::CheckFor",
            "Parameters": {
                "APIInfo": {
                    "Service": "ecs",
                    "APIName": "DescribeInstances",
                    "Version": "2020-04-01",
                    "Parameters": {
                        "InstanceIds": "{{ [.instanceId] }}"
                    },
                    "DesiredValues": [
                        "RUNNING",
                        "STOPPED"
                    ],
                    "NotDesiredValues": [
                        "ERROR"
                    ],
                    "ValueSelector": "{{  [.Instances[].Status] }}"
                }
            }
        }
    ]
}
```


<span id="O6CP3Ikb"></span>
## PeriodTriggerInfo (trigger type)

<span id="gB60hwCL"></span>
### VOS::PeriodicTrigger example

```JSON
{
    "Tasks": [
        {
            "Name": "periodicTask",
            "Action": "VOS::PeriodicTrigger",
            "Description": "Trigger tasks on schedule by specifying the task type and cycle expression",
            "Parameters": {
                "PeriodTriggerInfo": {
                    "RepeatMode": "{{ .repeatMode }}",
                    "LaunchTime": "{{ .launchTime }}",
                    "RecurrenceEndTime": "{{ .recurrenceEndTime }}",
                    "Frequency": "{{ .frequency }}"
                }
            }
        }
    ]
}
```


<span id="BsDEKPvU"></span>
## ChoiceInfo (control type)

ChoiceInfo includes VOS::Choice and VOS::SelectTargetInstances.

<span id="r3j6s3sl"></span>
### VOS::Choice example

```JSON
{
    "Tasks": [
        {
            "Name": "whetherToDeleteLaunchTemplateVersion",
            "Description": "Whether to delete the original latest version of the startup template",
            "Action": "VOS::Choice",
            "Parameters": {
                "ChoiceInfo": {
                    "Condition": [
                        {
                            "When": {
                                "FN::Equals": [
                                    "{{ .deleteSourceTemplateVersion }}",
                                    true
                                ]
                            },
                            "Next": "whetherToModifyTemplateDefaultVersion"
                        }
                    ],
                    "Default": "VOS::END"
                }
            }
        }
    ]
}
```


<span id="g2Jeq1w1"></span>
### VOS::SelectTargetInstances example

**Custom Action template**

```JSON
{
    "Parameters": {
        "targets":{
            "Type":"Map"
        }
        "ForceStop": {
            "Type": "Boolean"
        }
    },
    "Tasks": [
        {
            "Name": "getInstance",
            "Action": "VOS::SelectTargetInstances",
            "Parameters": {
                "Filters": "{{ targets }}"
            },
            "Outputs": {
                "instanceIds": {
                    "Type": "List",
                    "ValueSelector": "Instances.Instance[].InstanceId"
                }
            },
            "Description": "{\"zh-cn\":\"Select Instance\",\"en\":\"SelectTargetInstances\"}"
        },
        {
            "Name": "RebootInstances",
            "ActionId": "ac-ycc8brgqe5f10****",
            "Parameters": {
                "InstanceId": "{{ VOS::LoopItem }}",
                "ForceStop": "{{ .ForceStop }}"
            },
            "Outputs": {
                "InstanceStatus": {
                    "Type": "String",
                    "Value": "{{ .InstanceStatus }}"
                }
            },
            "Loop": {
                "LoopItem": "{{ getInstance.instanceIds }}",
                "Outputs": {
                    "LoopInstanceStatus": {
                        "SelectedOutputFiled": "InstanceStatus"
                    }
                },
                "Concurrency": 1
            },
            "Description": "{\"zh-cn\":\"Batch restart instances\",\"en\":\"RebootInstances\"}"
        }
    ],
    "Outputs": {
        "InstanceStatus": {
            "Type": "List",
            "Value": "{{ .\"RebootInstances.LoopInstanceStatus\" }}"
        }
    }
}
```


**Specify parameters for invoking the template:** 

Type specifies the method for selecting instances. Valid values:


* Tags: Select instances based on key\-value pairs of tags.

* Project: Select all instances in the specified project.

* All: Select all instances.


```JSON
{"targets":{"Type":"Tags","Tags":[{"Key":"tagKey1","Value":"tagValue1"}]}}
{"targets":{"Type":"Project","Project":"projectName"}}
{"targets":{"Type":"All"}}
```


<span id="wYBAm8JB"></span>
## Execute functions

<span id="wYBAm8JB"></span>
### VOS::InvokeInnerFunction example

The following compute functions are currently preconfigured:


* FN::Equals

* FN::Now

* FN::AddMinute

* FN::FormatUTCTime

* FN::ExecuteJQExpression

* FN::GetExecutionId


```JSON
{
    "Tasks": [
        {
            "Name": "getSplitInstanceIdList",
            "Description": "Get the list of instance IDs after segmentation",
            "Action": "VOS::InvokeInnerFunction",
            "Parameters": {
                "FunctionName": "FN::ExecuteJQExpression",
                "Input": " def split($array; $len):\n if $array | length > $len then $array | .[0:$len] as $temp | [$temp] + split(.[$len:]; $len) else [$array] end; split(.InstanceIds; 100) "
            },
            "Outputs": {
                "instanceIdList": {
                    "Type": "List",
                    "Value": "{{ . }}"
                }
            }
        }
    ]
}
```


<span id="s3lY77bY"></span>
## Nesting

<span id="s3lY77bY"></span>
### VOS::InvokeTemplate example

```JSON
"Tasks": [
    {
        "Name": "BulkyModifyInstanceVpcAttribute",
        "Action": "VOS::InvokeTemplate",
        "Description": "{\"zh-cn\":\"Batch modify instance VPC information\",\"en\":\"BulkyModifyInstanceVpcAttribute\"}",
        "Parameters": {
            "TemplateId": "tl-ydsu3hnja4kkk1k****",
            "VPCInfo": "{{ VOS::LoopItem }}",
            "NeedStart": "{{ .NeedStart }}"
        },
        "Outputs": {
            "NetworkInterfaceId": {
                "Type": "String",
                "Value": "{{ .NetworkInterfaceId }}"
            }
        },
        "Loop": {
            "LoopItem": "{{ .AllVPCInfo }}",
            "Outputs": {
                "NetworkInterfaceIds": {
                    "SelectedOutputFiled": "NetworkInterfaceId"
                }
            },
            "RateControl": "{{ .RateControl }}"
        }
    }
]
```
