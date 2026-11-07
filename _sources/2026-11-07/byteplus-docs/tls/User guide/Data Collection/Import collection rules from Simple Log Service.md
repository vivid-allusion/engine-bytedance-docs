---
title: "Import collection rules from Simple Log Service"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Importing_collection_rules_from_sls"
---

In scenarios such as cross\-service data migration, you can use the collection rule import feature of Torch Log Service (TLS) to batch import the collection rules of the log services of other cloud vendors. This topic describes how to import the collection rules of Simple Log Service (SLS).

<span id="背景信息"></span>
## Background

In scenarios such as cross\-platform application migration and cross\-service data migration, you should batch migrate log\-service collection rules in the application to BytePlus TLS besides existing log data. This helps you quickly apply the rules to BytePlus TLS and improve the efficiency of business migration. Currently, BytePlus TLS allows you to import the log collection rules of Alibaba Cloud SLS. Imported collection rules include the collection rule of Logstore where logs are written. These rules are not associated with host groups and exclude host group resource configurations and index configurations.

<span id="注意事项"></span>
## Precautions


* If the name of an imported collection rule is the same as the name of an existing rule, TLS updates the existing collection rule according to the imported rule.

* When you import a collection rule, TLS automatically creates a default topic for you. After the import is complete, you can refer to the shard configuration of the original SLS Logstore to modify the topic configuration as needed.


<span id="前提条件"></span>
## Before you begin


* Create a collection rule in Alibaba Cloud SLS.

* Get an Alibaba Cloud AccessKey pair. To ensure data security, use a RAM user with read permissions on the collection rule. For more information on authorization policies, refer to [Sample SLS RAM authorization policy](https://docs.byteplus.com/docs/tls/Importing_collection_rules_from_sls#sls-ram-%E6%8E%88%E6%9D%83%E7%AD%96%E7%95%A5%E7%A4%BA%E4%BE%8B).

* Create a project in BytePlus TLS. For more information, refer to [Manage a project](https://docs.byteplus.com/docs/tls/Managing_projects).

* If you use the feature for the first time, grant the required permissions on access to cloud resources or authorize TLS to access and write resources. If TLS is not authorized, it guides you through the related operation when you create an import task in the console. We recommend that you use a BytePlus account to authorize access. For more information, refer to [Authorize cross-service access](https://docs.byteplus.com/docs/tls/Authorizing_cross-service_access).


<span id="创建采集配置导入任务"></span>
## Creating a task for importing collection rules


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common Functions** \> **Log Collection**.

4. In the **SLS configuration migration** pane, select **Alibaba Cloud SLS configuration migration**.

5. Specify the following task parameters and click **Create**.

   
   |Parameter |Description |
   |---|---|
   |Import source |Fixed value: **Alibaba Cloud SLS**. |
   |Task name |The name of the destination TLS project that you want to use to store the collection rules. |
   |Task name |The name of the task for importing collection rules. |
   |Source domain name |The endpoint of Alibaba Cloud SLS. To view the endpoint, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
   |key |The AccessKey pair of the Alibaba Cloud account or RAM user. To view the AccessKey pair, refer to [AccessKey pairs](https://www.alibabacloud.com/help/en/sls/developer-reference/accesskey-pair?spm=a2c63.p38356.0.0.36ab4a217pdFQY).<br><br>To ensure data security and information security, we recommend that you use the AccessKey pair of a RAM user with required permissions. For more information on authorization policies, refer to [Sample SLS RAM authorization policy](https://docs.byteplus.com/docs/tls/Importing_collection_rules_from_sls#sls-ram-%E6%8E%88%E6%9D%83%E7%AD%96%E7%95%A5%E7%A4%BA%E4%BE%8B). |
   |Project |The project in Alibaba Cloud SLS. The collection rules of the specified project can be imported. |
   |Import item |The SLS collection rules that you want to import to BytePlus TLS. |
   


After the import task is created, you can view basic information about the import task on the import list page of collection rules. The page displays the name, ID, status, source, import quantity, progress, and creation time of each import task. You can judge how an import task runs based on the import status.

<span id="sls-ram-授权策略示例"></span>
## Sample SLS RAM authorization policy

Assume that you use a RAM user to authenticate the operations for importing SLS collection rules and read the SLS collection rule information. In this case, grant the RAM user the permissions on projects and collection rules. The recommended policy for granting these permissions is as follows:

```json
{
  "Version": "1",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "log:GetConfig",
        "log:ListProject"
      ],
      "Resource": [
        "acs:log:*:*:project/*/logtailconfig/*",
        "acs:log:*:*:project/*"
      ]
    }
  ]
}
```


<span id="后续操作"></span>
## What to do next


* By default, an imported collection rule is not associated with a host group. To allow the collection rule to take effect, associate it with a specified host group.

* The system does not set an index for an automatically created topic. You can set indexes for the topic according to the index configuration of the original SLS Logstore.
