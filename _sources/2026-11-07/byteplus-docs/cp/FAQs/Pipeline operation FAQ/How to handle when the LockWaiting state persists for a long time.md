---
title: "How to handle when the LockWaiting state persists for a long time"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/How_to_handle_when_the_LockWaiting_state_persists_for_a_long_time"
---

<span id="OGjIG2A6"></span>
## Issue description

When you view pipeline execution records in the CP Console, you find that the pipeline remains in the **LockWaiting** state for a long time and does not enter the **Running** state.

<span id="VVjnT0wC"></span>
## Cause

The **LockWaiting** state indicates that the pipeline is waiting to obtain a resource lock to ensure serialized access to shared resources. Prolonged waiting is usually caused by a preceding pipeline holding the lock and not releasing it.

<span id="YevrSwWW"></span>
## Solution


1. Log in to the [CP Console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Global settings \> concurrency lock**.

3. In the concurrency lock list, view all created concurrency locks.

4. Click the target concurrency lock name, and in **queue**, view the number of running pipelines.

5. Wait for the upstream pipeline to complete execution and release the lock automatically, or manually release the concurrency lock. For operation details, see [Manage concurrency lock](https://docs.byteplus.com/en/docs/cp/Manage_concurrency_locks).


<span id="hT4Rp6j2"></span>
###
