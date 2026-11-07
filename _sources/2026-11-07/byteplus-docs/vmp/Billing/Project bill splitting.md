---
title: "Project bill splitting"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Project_bill_splitting"
---

Vital Managed Service for Prometheus supports using projects to manage workspace resources and perform bill splitting based on projects, solving the problem of financial cost sharing.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Resource projects (Project) are a resource grouping management mechanism provided by BytePlus, helping users achieve logical resource isolation. You can perform operations including project\-based authorization and bill splitting through resource projects.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The project has been created on the **Identity and Access Management** page.

<span id=".5Yib5bu65bel5L2c5Yy65bm25Yqg5YWl6aG555uu"></span>
## Create a workspace and add to a project


1. Log in to the [VMP Console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region and project.

3. Click **Workspace** on the left navigation bar to go to the workspace list page.

4. Click **Create Workspace** to configure the workspace. For workspace configuration details, refer to [Create Workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).


<span id=".5p-l55yL57uT5p6c"></span>
## View results

<span id=".5p-l55yL6aG555uu6LWE5rqQ"></span>
### View project resources


1. Log in to BytePlus [Identity and Access Management](https://console.byteplus.com/iam).

2. Select **Resource Management** \> **Project** on the left navigation bar. In the project list, select the target project and click **Manage** under the **Operation** column to view project details.

3. On the **Resources** tab, you can view the resource details of the project.


<span id=".5p-l55yL5YiG6LSm6LSm5Y2V"></span>
### View splitting bills

After adding a project to the Vital Managed Service for Prometheus workspace, it supports viewing splitting bills by project. The detailed operations are as follows:


1. Log in to the BytePlus [Cost Center](https://console.byteplus.com/finance).

2. Select **Bill Management** \> **Splitting Bills** in the left navigation bar.

3. On the **Splitting Bills** page, select a project from the **Project** dropdown menu to view the splitting bills for the specified project.
