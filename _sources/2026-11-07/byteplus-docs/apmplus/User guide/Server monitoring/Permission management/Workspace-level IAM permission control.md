---
title: "Workspace-level IAM permission control"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Workspace-level_IAM_permission_control"
---

Workspaces are a data isolation method provided by Server\-side Monitoring. Each workspace has independent data reporting credentials. Workspaces not only support centralized management of traces, logs, and metric data but also allow fine\-grained control over IAM user permissions based on workspaces. This topic describes how to perform workspace\-level IAM permission control.

<span id="LpNqHUFw"></span>
## Background

The  IAM service provides fine\-grained access control capabilities for resources. You can log in as a  root user to create IAM users and assign them permission policies to enable multi\-user collaboration or secure access in various scenarios. For example, O&M personnel have permissions to manage all resources and view specific resources. 

Server\-side Monitoring uses the IAM service of  for permission management. A permission policy consists of two key elements:


* **Action**: The operations that an IAM user can perform. They are in the format of `apmplus_server:{ActionName}`, such as `apmplus_server:GetWorkspace` and `apmplus_server:ListWorkspaces`.

* **Resource**: The resource scope on which the operations are performed, which is described by the Top Resource Name (TRN). The TRN for workspace resources is in the format of `trn:apmplus_server:{region}:{accountID}:workspace/{workspaceName}`.


<span id="O824VA1U"></span>
## Prerequisites


* An IAM user has been created. 

* The key information required for workspace resource TRN configuration has been obtained.

   
   |Key information |Obtaining method |
   |---|---|
   |`{region}` |The region IDs supported by Server\-side Monitoring. For supported regions and their IDs, see [Available regions](https://docs.byteplus.com/en/docs/apmplus/server-launching_region). |
   |`{accountID}` |Account ID. You can obtain it from the personal information in the upper‑right corner of the console. |
   |`{workspaceName}` |Workspace name. You can obtain it on the Workspace Management page. For details, see [Managing workspaces](https://docs.byteplus.com/en/docs/apmplus/Workspace_management). |
   

* (Optional) If you need to configure TLS permissions for corresponding resources, make sure that the key information for the TLS resource TRN configuration has been obtained.

   
   |Key information |Obtaining method |
   |---|---|
   |`{region}` |The region IDs supported by TLS. For supported regions and their IDs, see [Service addresses](https://docs.byteplus.com/en/docs/tls/endpoint). |
   |`{accountID}` |Account ID. You can obtain it from the personal information in the upper‑right corner of the console. |
   |`{projectID}` |The ID of the log project. You can obtain it on the log project management page in the TLS console. For details, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects). |
   |`{topicID}` |The ID of the log topic. You can obtain it on the log topic management page in the TLS console. For details, see [Log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics). |
   


<span id="fL4IMlHV"></span>
## Procedure

<span id="MmMTRxnT"></span>
### Step 1: Configure a custom workspace\-level policy


1. Log in to the [IAM console](https://console.byteplus.com/iam) as a  root user.

2. Click **Permission policy** in the left navigation pane and click **Create Policy**.

3. Set the policy name and policy content, and click **Submit**.

   To control the workspace scope that IAM users can view or operate in Server\-side Monitoring, pay attention to the following configurations:

   * When you configure a custom policy with edit permissions, we recommend disabling Actions related to workspace creation, deletion, and modification, including `CreateWorkspace`, `DeleteWorkspace`, and `UpdateWorkspace`.

      ```JSON
      ... ...
          {
              "Effect":"Deny",
              "Action":[
              "apmplus_server:CreateWorkspace",
              "apmplus_server:DeleteWorkspace",
              "apmplus_server:UpdateWorkspace"
              ],
              "Resource": [
              "*"
            ]
          }
      ... ...
      ```
      

   * Use `trn:apmplus_server:{region}:{accountID}:workspace/{workspaceName}` to restrict Actions to the target workspace resource TRN.

      ```JSON
      ... ...
          {
            "Effect": "Allow",
            "Action": [
              "apmplus_server:Get*",
              "apmplus_server:List*"
            ],
            "Resource": [
              "trn:apmplus_server:*:210xxxx:workspace/friday",
              "trn:apmplus_server:*:210xxxx:workspace/today"
            ]
          }
      ... ...
      ```
      


Common examples of workspace\-level custom policies are as follows:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">In practice, replace the <strong>region</strong>, <strong>account ID</strong>, and <strong>workspace name</strong> in the workspace resource TRN with actual values.</div>


* <div data-tips="true" data-tips-type="default">By default, AI‑related metrics are stored in the default workspace. If AI applications are involved, we recommend granting permissions on the default workspace when you configure custom policies.</div>




<Tabs>
<Tab zoneid="jWdwSKjetx" title="Full permission">
<TabTitle>Full permission</TabTitle>

Example of a custom policy that grants full permissions on Server\-side Monitoring to a specified workspace:

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "apmplus_server:*",
        "Volc_InfluxDB_Proxy:Write",
        "cloudmonitor:Write",
        "cloudmonitor:AgentHeartBeat",
        "cloudmonitor:ReportAgentStatus",
        "cloudmonitor:ReportAgentDeployStatus",
        "cloudmonitor:FetchAgentDeploy",
        "cloudmonitor:ReportPipelineStatus",
        "cloudmonitor:FetchPipelineConfig"
      ],
      "Resource": [
        "trn:apmplus_server:*:210xxxx:workspace/default",
        "trn:apmplus_server:*:210xxxx:workspace/today"
      ]
    },
    {
        "Effect":"Deny",
        "Action":[
        "apmplus_server:CreateWorkspace",
        "apmplus_server:DeleteWorkspace",
        "apmplus_server:UpdateWorkspace"
        ],
        "Resource": [
        "*"
      ]
    }
  ]
}
```





</Tab>
<Tab zoneid="FJivFjDhez" title="Read-only permission">
<TabTitle>Read-only permission</TabTitle>

Example of a custom policy that grants read\-only permissions on Server\-side Monitoring to a specified workspace:

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "apmplus_server:Get*",
        "apmplus_server:List*"
      ],
      "Resource": [
        "trn:apmplus_server:*:210xxxx:workspace/default",
        "trn:apmplus_server:*:210xxxx:workspace/today"
      ]
    }
  ]
}
```



</Tab>
</Tabs>


<span id="rAglIlCP"></span>
### Step 2: (Optional) Configure TLS permissions for the corresponding resources

The trace and log data of a workspace are stored in TLS. By default, users only have access permissions to the trace and log data. If you need to strictly prohibit IAM users from accessing certain TLS resources, you can manually configure custom policies. For more information about TLS resource configuration, see [Configuring TLS permissions](https://docs.byteplus.com/en/docs/tls/authority_management?lang=en).

TLS resources are in the TRN format of `trn:tls:{region}:{accountID}:project/{projectID}/topic/{topicID}`. A sample custom policy is as follows:

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tls:Search*",
        "tls:Describe*"
      ],
      "Resource": [
        "trn:tls:cn-beijing:21xxxxx515:project/fdcxxxxx-ea27-d00xxxxx/topic/73bdxxxxx",
        "trn:tls:cn-beijing:21xxxxx515:project/fdcxxxxx-ea27-d00xxxxx/topic/ce92xxxxx"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "tls:DescribeProjects",
        "tls:DescribeTopics",
        "tls:DescribeTopic"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```


<span id="fNFZQn9Q"></span>
### Step 3: Use the custom policy to grant permissions to IAM users


1. Return to the **Permission policy** page, search for the custom policy created in [Step 1](https://docs.byteplus.com/en/docs/299/113393#MmMTRxnT), and click **Authorize** in the Actions column.

2. Select the IAM users to be authorized and then click **Submit**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To enable fine\-grained permission control at the project level, select the target project.   </div>
   

<span id="E4N17qCI"></span>
## FAQ

<span id="IiGjvJNJ"></span>
### Why am I still unable to view the workspace after authorization?

Check whether the following configurations are valid:


* Check whether `apmplus_server:GetWorkspace` is included in the custom policy.

* Check whether `{region}`, `{accountID}`, and `{workspaceName}` in the TRN are valid.

* In a multi‑region deployment scenario, you need to configure a separate Resource for the workspace in each region, or use the `*` wildcard in the region configuration.


<span id="4LPnzu57"></span>
### Why does the Server\-side Monitoring console display that I do not have permissions during a login?

This indicates that the current account already has workspaces, but the logged‑in user lacks workspace permissions. Contact the root user to grant the necessary permissions.

<span id="vuSsbM0u"></span>
### How do I batch‑configure permissions when multiple workspaces exist under the root user?

Use the `*` wildcard based on naming conventions, such as `workspace/payment-*`.

&nbsp;

&nbsp;
