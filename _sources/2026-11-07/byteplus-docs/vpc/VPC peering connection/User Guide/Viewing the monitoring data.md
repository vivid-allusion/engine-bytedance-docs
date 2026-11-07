---
title: "Viewing the monitoring data"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Viewing-the-monitoring-data"
---

You can view cross\-region traffic monitoring data for a peering connection through the Peering Connection console or the CloudMonitor console.

## Action notes

* CloudMonitor collects monitoring metric data for a peering connection every 30 seconds, and the data represents the average value over that 30‑second period.

* If an IAM user is only granted Peering Connection permissions but not CloudMonitor permissions, they will be unable to view the Peering Connection service's monitoring data. Please use the root user (to which the IAM user belongs) to add the system\-predefined CloudMonitor policy permissions to the IAM user according to your actual needs. For detailed instructions, .

   |Policy name |Supported action |
   |---|---|
   |CloudMonitorFullAccess |Management permissions for CloudMonitor. With this policy, the IAM user can both view monitoring data and use features of the CloudMonitor. |
   |CloudMonitorReadOnlyAccess |Access permissions for CloudMonitor. With this policy, the IAM user can view monitoring data only. |

## Procedures

### View via Peering Connection console

1. Log in to the [Peering Connection console](https://console.byteplus.com/vpc/region:vpc+cn-beijing/peerConnection).

2. On the top menu bar, select the target region and project.

3. Click the monitoring icon under the **Monitor** column of the target peering connection to view the cross\-region traffic monitoring data for the peering connection.

### View data via CloudMonitor console

For detailed steps, see [Cloud service monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor#.5p-l55yL5LqR5Lqn5ZOB55uR5o6n5pWw5o2u)[Cloud service monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor#.5p-l55yL5LqR5Lqn5ZOB55uR5o6n5pWw5o2u)[Cloud service monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor#.5p-l55yL5LqR5Lqn5ZOB55uR5o6n5pWw5o2u).
