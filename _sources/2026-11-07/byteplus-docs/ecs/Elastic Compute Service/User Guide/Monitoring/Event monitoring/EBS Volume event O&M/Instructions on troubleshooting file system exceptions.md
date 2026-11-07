---
title: "Instructions on troubleshooting file system exceptions"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/File_system_exception_repair_instructions"
---

This topic mainly describes precautions and  provided by BytePlus, after you authorize the shutdown repair due to an "InstanceFileSystemFailure.StopAndRepair (Downtime repair due to file system exception)" event.

<span id="RyIbwd2i"></span>
## Prerequisite

You have [authorized the shutdown repair](https://docs.byteplus.com/en/docs/ecs/File-system-exception-shutdown-repair-operation-and-maintenance-description).

<span id="RyIbwd2i"></span>
## Usage notes


* Currently, you can authorize shutdown repairs only for Windows instances.

* To use the automatic repair capability offered by BytePlus, make sure that the instance is in a Stopped state. We recommend that you [stop the instance](https://docs.byteplus.com/en/docs/ecs/Stopping-instances) first. If the instance is not in a **Stopped** status, BytePlus will forcibly stop it.
