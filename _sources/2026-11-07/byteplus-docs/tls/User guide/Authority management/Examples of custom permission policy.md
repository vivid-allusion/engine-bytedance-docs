---
title: "Examples of custom permission policy"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Permissions_policy_template"
---

Before using TLS as an IAM user, you must first use your BytePlus account to grant the required permissions. TLS supports custom permission policies. This topic provides examples of custom access policies for various common scenarios in TLS.


|Feature modules |Access policy examples |
|---|---|
|Basic resources |* [View project information](https://docs.byteplus.com/docs/tls/Permissions_policy_template#a24f9487)<br><br>* [Star TLS resources](https://docs.byteplus.com/docs/tls/Permissions_policy_template#9ee48c3a)<br><br>* [Manage projects and topics](https://docs.byteplus.com/docs/tls/Permissions_policy_template#2a36b882) |
|Data collection |* [Access key configuration for collection](https://docs.byteplus.com/docs/tls/Permissions_policy_template#4dd90069)<br><br>* [Collect Trace data](https://docs.byteplus.com/docs/tls/Permissions_policy_template#.6YeH6ZuGLXRyYWNlLeaVsOaNrg==)<br><br>* [Manage collection configurations and host groups](https://docs.byteplus.com/docs/tls/Permissions_policy_template#63bbb5c9) |
|Query and analysis |* [Query and analyze logs](https://docs.byteplus.com/docs/tls/Permissions_policy_template#.6YCa6L-HLWFwaS3mo4DntKLliIbmnpDml6Xlv5c=)<br><br>* [All permissions for query module](https://docs.byteplus.com/docs/tls/Permissions_policy_template#59ee4d1b)<br><br>* [TLS Agent](https://docs.byteplus.com/docs/tls/Permissions_policy_template#2eb74af6) |
|Dashboard |[Manage dashboard](https://docs.byteplus.com/docs/tls/Permissions_policy_template#059629c0) |
|Alert |[Manage alarm policies and notification groups](https://docs.byteplus.com/docs/tls/Permissions_policy_template#2592287e) |
|Data processing |[Manage data transformation tasks](https://docs.byteplus.com/docs/tls/Permissions_policy_template#cdd67992) |
|Data consumption and shipping |[Has TOS shipping management permission for all log topics](https://docs.byteplus.com/docs/tls/Permissions_policy_template#.6YCa6L-H5raI6LS557uE5raI6LS55pWw5o2u) |
|Data import |[Data import](https://docs.byteplus.com/docs/tls/Permissions_policy_template#.5oqV6YCS5pel5b-X5YiwLWthZmth) |
|Log application |[Access log application tasks](https://docs.byteplus.com/docs/tls/Permissions_policy_template#d70a412a) |


<span id="1a58f555"></span>
## Basic resources

<span id="a24f9487"></span>
### View project information

With the following permission policy, IAM users can view all project information under the current account.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:DescribeProjects"
            ],
            "Resource": [
                "trn:tls:*:*:project/*"
            ]
        }
    ]
}
```


<span id="9ee48c3a"></span>
### Star TLS resources

With the following permission policy, IAM users can mark the specified TLS resources as favorites.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateSavedSearch",
                "tls:DescribeSavedSearches",
                "tls:DeleteSavedSearch"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="2a36b882"></span>
### Manage projects and topics

With the following permission policy, IAM users can manage all projects and topics under the current account, including creating, querying, deleting, and updating topics and projects.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateProject",
                "tls:CreateTopic",
                "tls:PutLogs",
                "tls:WebTracks",
                "tls:DeleteTopic",
                "tls:ModifyTopic",
                "tls:DescribeDownloadTasks",
                "tls:DescribeShards",
                "tls:DescribeTopic",
                "tls:DescribeTopics",
                "tls:DeleteProject",
                "tls:ModifyProject",
                "tls:DescribeProject",
                "tls:DescribeConsumerGroups",
                "tls:DescribeProjects",
                "tls:DescribeRules"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".5pWw5o2u6YeH6ZuG"></span>
## Data collection

<span id="4dd90069"></span>
### Access key configuration for collection

LogCollector requires access keys with at least the following permissions for collection configuration.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:PutLogs",
                "tls:GetLogCollectorConfig",
                "tls:LogCollectorHeartbeat",
                "tls:RemoteWrite"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".6YeH6ZuGLXRyYWNlLeaVsOaNrg=="></span>
### Collect Trace data

After receiving the following permission policies, IAM users can manage Trace instances, write collected Trace data to the corresponding log topic, and query and analyze Trace data via API.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateIndex",
                "tls:CreateTopic",
                "tls:PutLogs",
                "tls:ModifyIndex",
                "tls:ModifyTopic",
                "tls:DescribeTopic",
                "tls:CreateTraceInstance",
                "tls:ModifyTraceInstance",
                "tls:DeleteTraceInstance",
                "tls:DescribeTraceInstance",
                "tls:DescribeTraceInstances",
                "tls:SearchLogs"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="63bbb5c9"></span>
### Manage collection configurations and host groups

After receiving the following permission policies, IAM users can manage collection configurations and host groups, including the followings: querying the project list and topic list; creating, deleting, modifying, and querying collection configurations or host groups; and binding or unbinding collection configurations to host groups.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:DescribeProjects",
                "tls:DescribeProject",
                "tls:DescribeTopics",
                "tls:DescribeTopic"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateRule",
                "tls:DeleteRule",
                "tls:ModifyRule",
                "tls:DescribeRule",
                "tls:DescribeRules",
                "tls:ApplyRuleToHostGroups",
                "tls:DeleteRuleFromHostGroups",
                "tls:CreateHostGroup",
                "tls:DeleteHostGroup",
                "tls:ModifyHostGroup",
                "tls:DescribeHostGroup",
                "tls:DescribeHostGroups",
                "tls:DescribeHosts",
                "tls:DeleteHost",
                "tls:DescribeHostGroupRules",
                "tls:ModifyHostGroupsAutoUpdate",
                "tls:DeleteAbnormalHosts"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".5pel5b-X5qOA57Si"></span>
## Query and analysis

<span id=".6YCa6L-HLWFwaS3mo4DntKLliIbmnpDml6Xlv5c="></span>
### Query and analyze logs

After receiving the following permission policies, IAM users can query log data via OpenAPI or the console. In this example, the specified IAM user can only query and analyze the `c425****83d7` project in the Beijing region and the `6b30****4888` log topic.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:DescribeProjects",
                "tls:DescribeProject",
                "tls:DescribeTopics",
                "tls:DescribeTopic"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "tls:SearchLogs",
                "tls:DescribeIndex",
                "tls:DescribeSavedSearches",
                "tls:DescribeHistogram",
                "tls:DescribeHistogramV1"
            ],
            "Resource": [
                "trn:tls:cn-beijing:21****96:project/c425****83d7/topic/6b30****4888"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateSavedSearch",
                "tls:DescribeSavedSearches",
                "tls:DeleteSavedSearch"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="59ee4d1b"></span>
### All permissions for query module

After being granted the following permission policies, IAM users can manage index, query logs, download logs, and other query\-related permissions.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:DescribeProjects",
                "tls:DescribeProject",
                "tls:DescribeTopics",
                "tls:DescribeTopic"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "tls:DescribeIndex",
                "tls:CreateIndex",
                "tls:DeleteIndex",
                "tls:ModifyIndex",
                "tls:SearchLogs",
                "tls:DescribeHistogram",
                "tls:DescribeHistogramV1",
                "tls:DescribeLogContext"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateDownloadTask",
                "tls:DescribeDownloadTasks",
                "tls:DescribeDownloadUrl",
                "tls:CancelDownloadTask"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateSavedSearch",
                "tls:DescribeSavedSearches",
                "tls:DeleteSavedSearch"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="2eb74af6"></span>
### TLS Agent

After being granted the following permission policies, IAM users can use TLS Agent feature.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tls:CreateAppInstance",
        "tls:DescribeAppInstances",
        "tls:CreateAppSceneMeta",
        "tls:DescribeAppSceneMetas",
        "tls:ModifyAppSceneMeta",
        "tls:DeleteAppSceneMeta",
        "tls:DescribeSessionAnswer"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```


<span id="d4a8bb86"></span>
## Dashboard

<span id="059629c0"></span>
### Manage dashboard

After being granted the following permission policies, IAM users can manage all dashboards under the current account, including creating, deleting, modifying, and querying dashboards.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateDashboard",
                "tls:DeleteDashboard",
                "tls:ModifyDashboard",
                "tls:DescribeDashboard",
                "tls:DescribeDashboards"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="b797148d"></span>
## Alert

<span id="2592287e"></span>
### Manage alarm policies and notification groups

After being granted the following permission policies, IAM users can manage all alarm policies and notification groups under the current account, including querying projects and log topics, as well as creating, deleting, modifying, and querying alarm policies and notification groups.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:DescribeProjects",
                "tls:DescribeProject",
                "tls:DescribeTopics",
                "tls:DescribeTopic",
                "tls:SearchLogs"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateAlarmNotifyGroup",
                "tls:DeleteAlarmNotifyGroup",
                "tls:DescribeAlarmNotifyGroups",
                "tls:ModifyAlarmNotifyGroup",
                "tls:DescribeAlarmNotifyGroup",
                "tls:CreateAlarm",
                "tls:DeleteAlarm",
                "tls:DescribeAlarms",
                "tls:DescribeAlarm",
                "tls:ModifyAlarm",
                "tls:DescribeAlarmLogs",
                "tls:ManualTriggerAlarm",
                "tls:DescribeManualTriggerAlarmTask",
                "tls:ModifyAlarmIncident",
                "tls:DescribeAlarmIncident",
                "tls:DisableAlarm",
                "tls:EnableAlarm",
                "tls:CreateAlarmContentTemplate",
                "tls:DeleteAlarmContentTemplate",
                "tls:DescribeAlarmContentTemplates",
                "tls:ModifyAlarmContentTemplate",
                "tls:CreateAlarmWebhookIntegration",
                "tls:DeleteAlarmWebhookIntegration",
                "tls:DescribeAlarmWebhookIntegrations",
                "tls:ModifyAlarmWebhookIntegration"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="0cca31b6"></span>
## Data processing

<span id="cdd67992"></span>
### Manage data transformation tasks

After being granted the following permission policies, IAM users can manage all data transformation tasks under the current account, including querying projects and log topics, and creating, deleting, modifying, and querying data transformation tasks.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:DescribeProjects",
                "tls:DescribeProject",
                "tls:DescribeTopics",
                "tls:DescribeTopic",
                "tls:SearchLogs"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateETLTask",
                "tls:DeleteETLTask",
                "tls:DescribeETLFunctions",
                "tls:DescribeETLLogDataInfo",
                "tls:DescribeETLPreviewDataInfo",
                "tls:DescribeETLTask",
                "tls:DescribeETLTasks",
                "tls:ModifyETLTask",
                "tls:ModifyETLTaskStatus"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".5raI6LS55LiO5oqV6YCS"></span>
## Data consumption and shipping

<span id=".6YCa6L-H5raI6LS557uE5raI6LS55pWw5o2u"></span>
### Has TOS shipping management permission for all log topics

After being granted the following permission policies, IAM users can operate TOS shipping features, including querying projects and log topics, and creating, modifying, querying, deleting, and retrying shipping tasks.

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:DescribeProjects",
                "tls:DescribeTopics",
                "iam:Createrole",
                "tos:ListBuckets"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateShipper",
                "tls:DeleteShipper",
                "tls:DescribeShipper",
                "tls:DescribeShipperTasks",
                "tls:DescribeShippers",
                "tls:ModifyShipper",
                "tls:RetryShipperTask"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".5oqV6YCS5pel5b-X5YiwLWthZmth"></span>
## Data import

After being granted the following permission policies, IAM users can manage all data import tasks under the current account, including querying projects and log topics, as well as creating, deleting, modifying, and querying data import tasks.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:DescribeProjects",
                "tls:DescribeProject",
                "tls:DescribeTopics",
                "tls:DescribeTopic",
                "tos:ListBuckets",
                "tos:ListBucket"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateImportTask",
                "tls:DeleteImportTask",
                "tls:DescribeImportTask",
                "tls:DescribeImportTasks",
                "tls:ModifyImportTask",
                "tls:PreviewImportTask"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="c4f60d4a"></span>
## Log application

<span id="d70a412a"></span>
### Access log application tasks

After being granted the following permission policies, IAM users can manage all log application tasks under the current account, including creating, deleting, modifying, and querying log application tasks. Data pivot tasks can also be created and managed for CloudLens for TOS.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:DescribeProjects",
                "tls:DescribeProject",
                "tls:DescribeTopics",
                "tls:DescribeTopic",
                "tls:SearchLogs"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "tls:CreateApp",
                "tls:ModifyApp",
                "tls:DescribeApp",
                "tls:DescribeApps",
                "tls:DeleteApp",
                "tls:ModifyCloudLensInstanceStatus",
                "tls:DescribeCloudLensInstances",
                "tls:DescribeCloudLensInstanceStatus",
                "tls:DescribeCloudLensTargetTopics",
                "tls:DescribeCloudLensOverview",
                "tls:CreateTosLensTask",
                "tls:ModifyTosLensTask",
                "tls:DescribeTosLensTasks",
                "tls:DescribeTosLensTask",
                "tls:DeleteTosLensTask"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```
