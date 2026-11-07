---
title: "Preset alert template list"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_alarm_templates"
---


|Dimension |Trigger condition |Number of associated instances |
|---|---|---|
|Deployment monitor |Replica replication latency average \> 30s, sustained for 3 cycles (1 cycle = 1 minute) |All |
|Resource monitor |Multi\-indicator alarm (any):<br><br><br>* CPU usage average max value \> 80%, lasting 3 cycles (1 cycle = 1 minute)<br><br>* Memory usage max value \> 80%, lasting 3 cycles (1 cycle = 1 minute)<br><br>* Disk usage max value \> 80%, lasting 3 cycles (1 cycle = 1 minute)<br><br>* Replication Slot Maximum WAL Stack Disk Ratio max value \> 50%, lasting 3 cycles (1 cycle = 1 minute) |All |
|Engine monitor |Multi\-indicator alarm (any):<br><br><br>* Database maximum age XIDs max value \> 1300000000, lasting 1 cycle (1 cycle = 1 minute)<br><br>* Connection utilization average \>= 80%, lasting 1 cycle (1 cycle = 1 minute)<br><br>* Global read\-only state average = 1, lasting 1 cycle (1 cycle = 1 minute)State |All |
|Proxy monitor |Multi\-indicator alarm (any):<br><br><br>* Proxy CPU utilization average \> 80%, sustained for 3 cycles (1 cycle = 1 minute)<br><br>* Proxy memory utilization max value \> 80%, sustained for 3 cycles (1 cycle = 1 minute) |All |
