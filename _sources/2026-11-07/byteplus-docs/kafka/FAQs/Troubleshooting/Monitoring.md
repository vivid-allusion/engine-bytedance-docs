---
title: "Monitoring"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/monitoring-FAQ"
---

<span id="ebc8f988"></span>
## Why is the monitoring data of a group retained after I delete the group?

Vitality Cloud Monitor (VCM) collects monitoring data of each Kafka instance at intervals of minutes. It also sorts the raw monitoring data based on various data aggregation methods and instance types. Only processed data is displayed in the monitoring charts. It takes around 10 minutes for the monitoring data to be reflected on the monitoring charts after a change occurs. After you delete resources such as a group, we recommend that you wait for some time and then view the change in the corresponding monitoring data.
