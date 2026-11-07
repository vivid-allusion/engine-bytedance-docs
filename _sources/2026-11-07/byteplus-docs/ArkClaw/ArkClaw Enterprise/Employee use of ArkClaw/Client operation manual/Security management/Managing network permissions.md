---
title: "Managing network permissions"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/managing-network-permissions"
---

Network access permissions control whether commands in the security sandbox can establish network connections, including access to the internet and local services.

> **warning**

> If the system detects that the security sandbox on the current device is unavailable, the configured network access restrictions temporarily do not take effect. The page then displays the following message: "The security sandbox on the current device is unavailable, so network access restrictions cannot take effect temporarily."

## Application scenarios

If a task needs to run commands that access the network, or you need to restrict a task from accessing the network, you can adjust network access permissions in the ArkClaw client. You can configure permissions for the default scope or separately for a specified project.

* **Scope**: Network access permissions apply only to commands executed in the security sandbox. This setting does not apply when you use full access permissions.

* **Impact**: After you restrict network access, commands in the security sandbox cannot initiate network connections, including access to local services. Tasks that depend on network access may fail.

## Configuration scope

|**Parameter** |**Applicability** |
|---|---|
|Global default |Applies to projects for which network access permissions are not set separately. |
|Project configuration |Sets the network access permissions for a specified project. |

## Prerequisites

To configure project\-level permissions, make sure that the  already exists in the [local assistant or cloud assistant mode](https://docs.byteplus.com/en/docs/ArkClaw/Managing_projects_11).

## Configure network access

1. Log in to the ArkClaw client locally.

2. Switch to the target ArkClaw.

3. Click "![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_733c3e75c42df2726b84b0bb6a1cd7bc.png)\> Security management".

4. On the "Security management" page, click the "Network access" tab.

5. Select the scope:

   * To configure this for the **main session** (the task session initiated by clicking "Initiate task"), select **Global default**.

   * To configure this for a specified project, select the target project in **Project configuration**.

6. In the drop\-down list, select **Allow network access (default)**  or **Deny network access**.
