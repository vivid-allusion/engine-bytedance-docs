---
title: "Customer managed"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Customer_managed_policy"
---

EMR provides multiple system default permission policies, including management permissions, read\-only permissions, and developer permissions. You can use the default system permission policies to grant permissions to sub\-accounts. To grant other permissions to sub\-accounts for more granular and flexible permission control, you can implement this by using customer managed permission policies. This article uses a customer managed Submit Job policy as an example to demonstrate the key steps for creating a customer managed permission policy and performing permission control.

<span id="bd6f2252"></span>
## Context

Currently, EMR Serverless Spark provides the following system default policies: EMRServerlessFullAccess, EMRServerlessReadOnlyAccess, and EMRServerlessDeveloperAccess. Details:


* EMRServerlessFullAccess: Grants all management permissions.

* EMRServerlessReadOnlyAccess: Grants read\-only permissions.

* EMRServerlessDeveloperAccess: This is the default permission policy for the EMR Serverless developer role, which supports viewing all EMR Serverless feature interfaces, as well as job and job instance management, SQL editor operations, Submit Job operations, and other permissions commonly required by developers. (Queues can be viewed but cannot be created.)


<span id="fdca4ef4"></span>
## Create a customer managed policy


1. Log in to [EMR Serverless console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless/queue_manage?StatusesInclude=0&projectName=default).

2. In the personal information section in the upper right corner, click **Access control \> Policy management \> Create customer managed policy** to enter the customer managed policy creation page.

3. Edit the policy using either the visual editor or the JSON editor. The JSON editor is recommended.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/432b3f1972fc417699c0a63dfce96725~tplv-goo7wpa0wc-image.image) </span>

**Policy example**

Policy with only Submit Job permission:

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "emr_serverless:Query*",
                "emr_serverless:Get*",
                "emr_serverless:Fetch*",
                "emr_serverless:List*",
                "emr_serverless:MonitorScanData",
                "emr_serverless:MonitorStorage",
                "emr_serverless:ConsolePermission",
                "emr_serverless:EditorGetLog",
                "emr_serverless:EditorGetBatchQueryStatus",
                "emr_serverless:EditorListAllBatchQueries",
                "emr_serverless:EditorListAllHistoryRecords",
                "emr_serverless:EditorDeleteTab",
                "emr_serverless:EditorSaveQuery",
                "emr_serverless:EditorListAllTabs",
                "emr_serverless:ShowTablesNotCheckPrivilege",
                "emr_serverless:EditorExecuteQuery",
                "emr_serverless:EditorAnalyzeQuery",
                "emr_serverless:EditorGetBatchQueryStatus",
                "emr_serverless:EditorListBatchQueryData",
                "emr_serverless:EditorListAllQueuesExt",
                "emr_serverless:CheckJobStatus",
                "emr_serverless:EditorListAllJobTabs"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="1f2709f1"></span>
## Policy authorization

After the policy is created, you need to authorize the customer managed policy to the sub\-account.

On the customer managed policy page, click **Add Authorization** and search for the user, user group, or role you want to authorize.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b6aa7dcfd9542cd892ac23e19d4d061~tplv-goo7wpa0wc-image.image) </span>

Once authorization is successful, the sub\-account will have the corresponding permissions.
