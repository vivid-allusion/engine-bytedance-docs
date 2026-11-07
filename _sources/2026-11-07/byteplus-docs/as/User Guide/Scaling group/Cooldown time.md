---
title: "Cooldown time"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Cooldown-period"
---

<span id=".5qaC6L-w"></span>
## Overview

Cooldown time refers to the period allocated for cooling down after adjustments. The system initiates cooldown timing immediately upon the completion of each adjustment. During the cooldown time, adjustments triggered by scheduled, periodic, or alert\-based scaling rules will be rejected, but manual scaling, instance count checks, and health checks are not subject to the cooldown time restriction.

<span id=".5Ya35Y205pe26Ze055qE55Sf5pWI6KeE5YiZ"></span>
## Rules for cooldown time validity

You can configure cooldown time for scaling groups and scaling rules. The following rules determine which cooldown setting takes effect.


* If you configure cooldown time for both the scaling group and the scaling rule, Auto Scaling will prioritize the cooldown time of the scaling rule.

* If cooldown time is not configured for your scaling rule, Auto Scaling will follow the cooldown time of the scaling group. The cooldown time for the scaling group is required.


<span id=".5Ya35Y205pe26Ze055qE55Sf5pWI5pe26Ze0"></span>
## Effective time of cooldown time


* The cooldown time starts from the moment the last instance in the current adjustment joins or is removed from the scaling group. If no instance joins or is removed from the scaling group, the adjustment is considered failed, and the cooldown time will not be calculated.

* After the scaling group or scaling rule is restarted, the cooldown time will be recalculated, allowing a new adjustment to be executed immediately. Once the execution is successful, the cooldown time will be recalculated.

* Adjustments outside the control of scaling rules are not subject to the cooldown time restriction and can be executed at any time, such as manual scaling or changing the expected instance count.


<span id=".5bqU55So5Zy65pmv"></span>
## Scenario

After a new instance is created, it needs time for initialization and deployment, such as running startup scripts or deploying basic services. The instance can serve traffic only after deployment succeeds. The cooldown period reserves this initialization time for new instances and prevents the scaling group from continuously creating new instances before they are ready to serve traffic.
