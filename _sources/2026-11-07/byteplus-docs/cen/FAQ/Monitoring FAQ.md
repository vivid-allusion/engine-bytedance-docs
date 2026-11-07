---
title: "Monitoring FAQ"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Monitoring-faq"
---

## After inter\-region bandwidth is configured, are monitoring metrics immediately available?

No, they are not immediately available. Monitoring data is synchronized at regular intervals and is not triggered instantly upon configuration completion.

## How can I view the outbound and inbound bandwidth traffic of CEN inter\-region bandwidth?

The outbound network traffic of inter\-region bandwidth in a CEN refers to the direction from the Local TransitRouter Region to the Peer Region, and the monitoring metric is inter\-region outbound bandwidth.

The inbound network traffic of inter\-region bandwidth in a CEN refers to the direction from the Peer Region to the Local TransitRouter Region, and the monitoring metric is inter\-region inbound bandwidth.

For example, if you configure inter\-region bandwidth from China (Beijing) to China (Shanghai), the Local TransitRouter Region is China (Beijing), and the Peer Region is China (Shanghai).

For detailed steps on how to view monitoring data, see [Viewing monitoring data](https://docs.byteplus.com/en/docs/cen/Monitoring-01).

## Why can't IAM users view monitoring data?

If an IAM user is granted permissions on CEN, but not on CloudMonitor, the IAM user cannot view the monitoring data of CEN. You can use your account to view the monitoring data, or grant the IAM user permissions on CloudMonitor. For more information, see Managing users.

|Policy name |Supported action |
|---|---|
|CloudMonitorFullAccess |Management permissions for CloudMonitor. With this policy, the IAM user can both view monitoring data and use features of the CloudMonitor. |
|CloudMonitorReadOnlyAccess |Access permissions for CloudMonitor. With this policy, the IAM user can view monitoring data only. |
