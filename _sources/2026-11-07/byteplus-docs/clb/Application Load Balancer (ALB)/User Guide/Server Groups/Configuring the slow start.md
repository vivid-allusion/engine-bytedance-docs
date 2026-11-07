---
title: "Configuring the slow start"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-the-slow-start"
---

<span id="E18wUtTu"></span>
## Overview

After slow start is enabled, newly added backend servers in the server group will have their weights gradually increased by ALB from 0 to the configured target weight at a constant rate within the slow start duration. This achieves smooth distribution of service traffic and prevents the new backend from being instantly overwhelmed.

<span id="0i7qctik"></span>
## Action notes


* The slow start feature can only be enabled when the scheduling algorithm of the server group is weighted round robin.

* In addition to newly added backend servers, when a backend server recovers from an exception health check status to a healthy status, the slow start feature will also be triggered.

* The valid range for the slow start duration: 30 to 900 seconds.


<span id="s2VcBfw2"></span>
## Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select **Server group**.

4. Click the target server group name to go to the details page.

   * Enable: Turn on **Slow start** switch, enter the slow start duration, and click **Save** to complete this action.

   * Disable: Turn off **Slow start** switch to complete this action.


<span id="beKjLPUz"></span>
## Related documents

[ModifyServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/ALB-ModifyServerGroupAttributes)
