---
title: "Setting alerts"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/set-alert"
---

Cloud Monitor allows you to set alert policies, so that you can monitor the performance and running information of Redis instances on Cloud Monitor. This topic describes how to create alert policies for Redis instances.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click **Monitoring** tab.

5. In the upper\-right corner of the **Monitoring** tab, click **Create an alert policy**.

6. On the **Create alarm strategy** page, configure each parameter according to business needs. For detailed parameter configuration instructions, refer to [Creating alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

> **tip**

* > When configuring the **Alarm objects** on the **Create alarm strategy** page, select **Database \> Cache for Redis** as the **Resource type**.

* > Cache for Redis supports the use of preset trigger conditions. When setting alert rules for **Server** or **Aggregate server**, you can select to use preset trigger conditions. The system pre\-configures trigger conditions based on alarm dimensions, allowing you to quickly set up the alarm policy, including metric types and trigger conditions. For more details, refer to [Creating alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).
