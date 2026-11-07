---
title: "Data backflow overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Log_backflow_overview"
---

TLS supports creating data backflow tasks, allowing specified log fields to be returned to log topics, and also supports delivery to TOS for long\-term storage.

This section introduces the data backflow feature, cost information, and other related details.

<span id="630330fe"></span>
## Features overview

Data backflow refers to the process of re\-importing or synchronizing data from one system back to another system. It is mainly used for data backup, synchronization, migration, recovery, and integration to ensure data security, improve consistency, and optimize management processes.

Data backflow supports collecting and storing data generated in the environment (such as input requests and prediction results) for subsequent optimization. Data continuously generated in the environment can be filtered or optimized through data backflow tasks, and used for subsequent data analysis or as higher\-quality data sources.

For example, in AI Agent scenarios, it is necessary to observe real user requests and key node data during processing in order to identify unknown performance issues. Additionally, online data can be returned as needed, including end\-to\-end input and output, input and output of LLM calls, and data used to supplement evaluation or training sets, to continuously optimize AI Agent performance.

<span id="a8fdd8d5"></span>
## Feature principles

Data backflow tasks created by TLS are essentially scheduled SQL tasks and TOS delivery tasks. When creating a data backflow task, the system automatically creates an associated scheduled SQL task. Based on the preset time window, scheduling cycle, and selected backflow fields, it performs query and analysis on the specified range of log data, and saves the query and analysis results (containing only the specified backflow fields) to the designated log topic for scenarios such as data analysis, log aggregation, and information filtering.

If the target is set to deliver to TOS, a TOS delivery task is automatically created on top of the scheduled SQL task. For details on TOS delivery tasks, refer to [Overview](https://docs.byteplus.com/docs/tls/Ship_logs_to_tos_overview1).

Data backflow tasks support the following data sources and destinations:


|Data source type |Destination types |
|---|---|
|TLS (log topic) |* TLS (log topic) in the current region<br><br>* TLS (log topic) in other regions<br><br>* TOS object storage in the current region |


<span id="2df18f57"></span>
## Billing description


* If TLS log topic is selected as the data backflow destination, the cost is the same as a regular log topic.

* If log shipping to TOS is selected as the data backflow destination, this involves both the log shipping cost for TLS and the data storage cost for TOS. For details, refer to [Overview](https://docs.byteplus.com/docs/tls/Ship_logs_to_tos_overview1).


<span id="82e59beb"></span>
##
