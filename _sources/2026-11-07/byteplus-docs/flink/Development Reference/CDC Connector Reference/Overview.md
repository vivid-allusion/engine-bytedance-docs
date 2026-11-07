---
title: "Overview"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/CDC_Connector_Overview"
---

This article introduces the connectors for Change Data Capture Pipeline supported by BytePlus Flink.

<span id="2cc5489d"></span>
## Supported Connectors

The table below lists the connectors currently provided by BytePlus Flink, as well as the source tables & result types they support.


|**Connector** |**Description** |**Source Table** |**Result Table** |**Engine Version** |
|---|---|---|---|---|
|MySQL |Provides the ability to read snapshot data and incremental data from MySQL databases, and offers end\-to\-end synchronization capabilities for entire databases |✅ |❌ |Flink 1.16、<br><br>Flink 1.17 |
|Bytehouse CDW |Provides the capability to synchronize entire databases to ByteHouse CDW |❌ |✅ |Flink 1.16、<br><br>Flink 1.17 |
|Paimon |Provides full database synchronization and schema change synchronization capabilities to Paimon |❌ |✅ |Flink 1.16、<br><br>Flink 1.17 |
|Starrocks |Provides full database synchronization and schema change synchronization capabilities to Starrocks |❌ |✅ |Flink 1.16、<br><br>Flink 1.17 |
|Doris |Provides full database synchronization and Schema change synchronization to Doris |❌ |✅ |Flink 1.16、<br><br>Flink 1.17 |
|Kafka |Provides the capability to sync entire databases and schema changes to Kafka |❌ |✅ |Flink 1.16、<br><br>Flink 1.17 |
|Values |Provides the capability for data writing debugging |❌ |✅ |Flink 1.16、<br><br>Flink 1.17 |
