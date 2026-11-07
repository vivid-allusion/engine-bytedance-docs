---
title: "User Log Service collects logs from fully managed OLAP clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/User_Log_Service_collects_logs_from_fully_managed_OLAP_clusters"
---

<span id="e0cfb26a"></span>
## Prerequisites

The EMR Serverless instance status and the status of each node group must be Running.

<span id="8df1bf5d"></span>
## Enable log service collection


1. On the EMR Serverless console **Instance Details** page, click to enable log collection.

2. Go to the [TLS Log Service](https://console.byteplus.com/tls/region:tls+ap-southeast-1/v2?projectName=default) to configure collection settings.

   1. Refer to the documentation [Create host group (IP address)](https://docs.byteplus.com/en/docs/tls/Create_an_IP_address-based_host_group). Focus only on the **Create host group** process, where the machine identifier is set to the OLAP cluster instance ID. After configuration, check the host group's **heartbeat status**. Normally, the connection will be established within three minutes.

   2. Refer to the documentation [Collect logs in Single-line full-text mode](https://docs.byteplus.com/en/docs/tls/single_line_full_text_mode) to configure specific collection rules for the relevant services. The log collection paths currently provided by OLAP are as follows and can be configured as needed.

      1. Audit log path: `/var/log/emr/*/fe/audit/fe.audit.log`

      2. FE log paths: `/var/log/emr/*/fe/log/fe.out`, `/var/log/emr/*/fe/sys/fe.log`, `/var/log/emr/*/fe/sys/fe.warn.log`

      3. BE log paths: `/var/log/emr/*/be/log/be.out`, `/var/log/emr/*/be/sys/be.INFO`, `/var/log/emr/*/be/sys/be.WARNING`

      4. CN log paths: `/var/log/emr/*/be/log/cn.out`, `/var/log/emr/*/be/sys/cn.INFO`, `/var/log/emr/*/be/sys/cn.WARNING`


<span id="06facc64"></span>
## Disable log service collection


1. On the EMR Serverless console **Instance Details** page, click to disable log collection.

2. After log collection is disabled, the corresponding host group heartbeat will be lost. Users can decide whether to go to the **Log Service Console** to delete the host group and the corresponding log topic as needed.
