---
title: "Lifecycle hook FAQ"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Lifecycle-hook-FAQs"
---

<span id=".5aaC5L2V57uT5p2f6KKr5oyC6LW355qE5Ly457yp5rS75Yqo77yf"></span>
## How do I end a suspended scaling activity?

You can end it by using either of the following methods:


* When the instance suspension time exceeds the timeout period specified by the lifecycle hook, the suspended status ends automatically.

* You can manually perform a callback operation to proactively end the instance's suspended status.


<span id=".5q2j5Zyo6Kem5Y-R55qE55Sf5ZG95ZGo5pyf5oyC6ZKp77yM5Y-v5Lul5Yig6Zmk5ZCX77yf"></span>
## Can a lifecycle hook that is being triggered be deleted?

If there are suspended instances at this time, after the hook is deleted, adjustments will continue based on the hook's execution policy. For a detailed introduction to the specific process, see [Execution process and policy](https://docs.byteplus.com/en/docs/as/Overview-of-lifecycle-hooks#.5omn6KGM5rWB56iL5ZKM562W55Wl).

<span id=".5piv5ZCm5pSv5oyB5Zyo5a6e5L6L5YaF5om56YeP5omn6KGM5ZG95Luk77yf"></span>
## Is batch command execution within instances supported?

Yes. In scenarios where a large number of instances are added to or removed in a batch, lifecycle hooks support association with cloud assistant. This allows you to conveniently execute O&M commands on one or multiple objects. This feature enables you to create one O&M command and execute it across multiple instances, significantly improving O&M efficiency. For more information, see [Related features](https://docs.byteplus.com/en/docs/as/Overview-of-lifecycle-hooks#.55u45YWz5Yqf6IO9).
