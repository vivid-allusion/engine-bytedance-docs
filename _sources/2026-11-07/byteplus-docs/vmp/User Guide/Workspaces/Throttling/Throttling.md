---
title: "Throttling"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Throttling"
---

Throttling allows a root user to allocate and manage the traffic of workspaces for its Identity and Access Management (IAM) users. This topic describes how to configure throttling for a workspace.

<span id="NgucSXWQ"></span>
## Background information

After an enterprise creates a Vital Managed Service for Prometheus (VMP) workspace, the workspace may be shared across multiple organizations (departments) within the enterprise, which use the same authentication information to write data or query data. To help enterprises properly manage workspace read permissions and prevent excessive read QPS from one organization from blocking other organizations' read access. The VMP workspace supports fine\-grained throttling configurations per IAM user for different business teams.

<span id="NgucSXWQ"></span>
## Prerequisites

A VMP workspace is created. For more details, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

<span id="fyzqqXWK"></span>
## Limit


* Common workspace: supports throttling based on IAM users and allows you to configure QPS, the number of time series scanned per second, and the maximum number of samples scanned per second.

* Aggregation/Local workspace: supports throttling based on IAM users and allows you to specify QPS limits.


<span id="fyzqqXWK"></span>
## Procedure

<span id="UW8Yevl7"></span>
### Step 1: Configure an IAM user

Before you configure throttling, you need to grant the read permissions on the workspace to the IAM user in the IAM console. You can perform the following steps to configure the IAM user:


1. Log in to the [IAM console](https://console.byteplus.com/iam).

2. Click Permission policy on the left navigation bar and click **Create Policy**.

3. Click the **JSON editor** tab, and use the following code to configure the read and write permissions on the specified workspace. `Workspace/agg-37860d39***` and `Workspace/939525b7-617***` indicate workspace IDs, which you can view on the workspace details page.

   ```JSON
   {
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "vmp:GetLabels",
                   "vmp:GetLabelValues",
                   "vmp:QueryMetrics",
                   "vmp:QueryMetricsRange",
                   "vmp:GetSeries",
                   "vmp:RemoteWrite",
                   "vmp:PushMetrics"
               ],
               "Resource": [
                   "trn:vmp:*:*:Workspace/agg-37860d39***",
                   "trn:vmp:*:*:Workspace/939525b7-617***"
               ]
           }
       ]
   }
   ```
   

4. On the left navigation bar, click **User management \> User**. On the page that appears, click **Create New User** to create a user.

5. Attach the created policy to the user.

6. After the IAM user is configured, the IAM user can query data in the workspace.  

   * The query address of the IAM user is the same as the query address of the root user. For more details, refer to [Obtaining workspace addresses](https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL).

   * For more information about how to query data by using the AK/SK of the IAM user, refer to [Using the Go language to query and write data in workspaces](https://docs.byteplus.com/en/docs/vmp/Writing_and_querying_workspace_data_using_Golang#.5L2_55SoIEFLL1NLIOafpeivouaMh-aghw==).

   * Query data by using BasicAuth authentication. Set `username` to `AccessKeyID`, and `password` to `SecretAccessKey`.


<span id="JXigd3mY"></span>
### Step 2: Configure throttling

When different organizations (departments) in an enterprise use different IAM users to query data in the same workspace, you can configure throttling for the workspace to allocate different quotas to different organizations. You can perform the following steps to configure throttling:


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. Click **Workspace** on the left navigation bar, find the target workspace in the workspace list, and then click the workspace name to go to the Overview page of the workspace.

3. Click **Traffic control** on the left navigation bar, and view the traffic configuration of the workspace on the right side.

4. Click **Add sub\-user traffic configuration** to allocate quotas to IAM users for the workspace and then click **OK**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_558e186246c6551e0027e458bb00f7f2.png) </span>

6. For the **Traffic configuration topology** parameter, select an IAM user to view the corresponding topology.
