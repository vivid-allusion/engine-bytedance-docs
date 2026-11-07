---
title: "Associate write processor"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Associate_data_processor"
---

This document describes how to associate or disassociate a write processor with a log topic.

## Prerequisites

* A log topic has been created. For details, see [Log topic](https://docs.byteplus.com/docs/tls/Managing_topics).

* A write processor has been created. For details, see [Create a write processor](https://docs.byteplus.com/docs/tls/Create_a_data_processor).

## Associate a write processor

**In write processor association**

1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where TLS is deployed.

3. In the left navigation pane, select **Data Processing** \> **Write Processor**.

4. In the write processor list, click the project name to expand the list of write processors in the project.

5. Click the write processor name to go to the write processor configuration page.

6. On the **Configuration Information** tab, click Add next to **Associate Topic**, select the log topics to associate, and click **OK**.

**In log topic association**

1. Log in to the [TLS Console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Resource Management** \> **Project**.

4. On the **Project** page, locate the specified project and click the project name.

5. In the **Log Topic** section, locate the specified log topic, and in the **Write Processor** column, click **Add**.

6. In the **Associate Write Processor** dialog box, select the write processor to associate, and click **OK**.

> **Note**

* > The association takes effect approximately 1 minute after it is successful.

* > Associating log topics across projects is not supported.

## Disassociate a write processor

1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where TLS is deployed.

3. In the left navigation pane, select **Data Processing** \> **Write Processor**.

4. In the write processor list, click the project name to expand the list of write processors in the project.

5. Click the write processor name to go to the write processor configuration page.

6. On the **Configuration Information** tab, in the list of associated log topics, click **Disassociate** in the **Actions** column for the corresponding log topic, then click **OK**.

## Switch the associated write processor

1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where TLS is deployed.

3. In the left navigation pane, select **Resource Management** \> **Project**.

4. On the **Project** page, find the specified project and click the project name.

5. In the **Log Topic** section, find the specified log topic, and in the **Write Processor** column, click **Switch**.

6. In the **Associate Write Processor** dialog box, select the write processor to associate and click **OK**.
