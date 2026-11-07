---
title: "Applicable scenarios"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Application-scenarios"
---

<span id=".5oyB57ut5bmz56iz5Zy65pmv"></span>
## Stable and continuous scenario

For a stable business without obvious fluctuations over the long term, set an expected number of instances for the scaling group and use the health check feature to automatically detect and replace abnormal instances. This prevents business disruptions caused by delays in adjustments and repairs.

For example, if you set the expected number of instances to five, the scaling group continuously maintains this number. When an instance exception is detected, a new instance is automatically created to replace the faulty one.

<span id=".5a6a5pyf5L-D6ZSA5Zy65pmv"></span>
## Scheduled promotion scenario

For expected business growth or downturns at specific times, use the scheduled scaling feature to execute scaling actions at the specified time automatically.

For example, during the Double 11 period, when business surges, configure adding 4 instances at 23:00 on November 10 and reducing 4 instances at 00:00 on November 14.

<span id=".5Lia5Yqh5rWq5raM5Zy65pmv"></span>
## Business surge scenario

Business operations may experience unpredictable surges in traffic, for example, when trending news breaks, making advance anticipation and adjustment impossible. Use the Auto Scaling feature with Cloud Monitor to achieve intelligent dynamic adjustment. This enables you to monitor business metric data in real time, assess business load, and automatically adjust the number of instances.

<span id=".5Li05pe25Y-Y5pu05Zy65pmv"></span>
## Temporary change scenario

For temporary business adjustments, you can add or remove instances from the scaling group at any time. This enables prompt changes whenever unexpected business changes occur.
