---
title: "Manually ending suspension"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Ending-the-pending-state-of-instances-manually"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

For an instance in the "Adding/removal suspended" state, if you need it to exit from the suspended state before a timeout, you can refer to the following operations to manually end the suspension.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Make sure that all required custom actions are completed, and that target instances can provide external services or be released.

<span id=".5byA5ZCv5a6e5L6L5L-d5oqk"></span>
## Enable instance protection


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Instance Management" tab.

4. Click the "Continue", "Reject", or "Roll back" button corresponding to the instance in the "Adding/removal suspended" state. The instance will then exit from the suspended state.

   For a detailed introduction to the instance change process after execution, refer to [Execution processes and policies](https://docs.byteplus.com/en/docs/as/Overview-of-lifecycle-hooks#.5omn6KGM5rWB56iL5ZKM562W55Wl).


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[CompleteLifecycleActivity](https://docs.byteplus.com/en/docs/as/CompleteLifecycleActivity)
