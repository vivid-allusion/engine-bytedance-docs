---
title: "Configuring SQL forwarding rules"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Configuring_SQL_forwarding_rules"
---

This topic describes the details of how to configure SQL forwarding rules for a proxy connection endpoint.

## Background

RDS for MySQL allows you to configure forwarding rules for a proxy connection endpoint by using SQL keywords to forward matched SQL statements to specified nodes. SQL forwarding rules configured for a connection endpoint override the read request scheduling policy in the read/write separation configuration.

## Precautions

* Only the proxy read/write endpoints of double\-node and multiple\-node instances support the configuration of SQL forwarding rules.

* You can configure a maximum of 15 forwarding rules for each connection endpoint.

* SQL keywords are case\-sensitive. Changes in the case of keywords may cause rules to fail silently.

## Prerequisites

* The database proxy service for the instance is enabled.

* The target connection endpoint is a database proxy read/write endpoint, and the read/write separation feature is enabled. For more information about enabling read/write separation, refer to [Enabling or disabling read/write separation](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_read-write_splitting).

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project to which the instance belongs is not set, this operation should select the project as **All resources**.

3. In the left navigation bar, choose **MySQL** \> **Instances**.

4. On the **Instances** page, click the target instance name.

5. Click the **Connectivity** tab at the top of the page.

6. On the **Connectivity** page, in the **Endpoints** list, click **Edit** in the **Actions** column for the target connection endpoint to open the **Modify endpoint** page.

7. On the **Modify endpoint** page, click  **+ Add** to add SQL forwarding rules for the endpoint, and then click **OK**.

   * Enter SQL keywords for the rule, and press Enter or space to confirm. The rules for setting SQL keywords are as follows:

      * Each rule can contain a maximum of 20 keywords.

      * The maximum length is 64 characters, and it can contain English letters, digits, underscores `_`, `@`, `#`, `:=`, and Chinese characters.

   * Set the forwarding target for the SQL forwarding rule.

      * For a double\-node instance, you can select the primary node or the read\-only node.

      * For a multiple node instance, you can select the primary node or the secondary node.
