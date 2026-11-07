---
title: "Common issues with data verification tasks"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Why_do_some_data_verification_tasks"
---

This topic applies to scenarios where the state or progress of a created DTS data verification task does not match expectations. Common scenarios are shown as follows:


* **Scenario 1: why does the progress of the full data verification always show as 0%?** 

   * **Cause analysis**: before formal verification, the full data verification task may need to split the data to be verified into blocks. If the full data to be verified is large or the data structure is complex, the splitting process may take a long time. During this phase, the <task progress\> may show 0%.

      The purpose of splitting is to divide the full data into segments better suited for subsequent verification, improving verification efficiency. Therefore, 0% progress does not necessarily indicate task abnormality but may indicate the task is still in the data splitting phase before verification.

   * **Handling suggestion**: it is recommended to observe whether the task is still running. If the validation object has a large data volume or complex structure, it is appropriate to wait. If the task shows no changes for a long time, it is recommended to check the task log or task details to confirm whether there are any errors.

* **Scenario 2: why do some data verification tasks remain in execution and do not automatically complete?** 

   * **Cause analysis**: If a data migration task or data synchronization task is associated with a data verification task, and the incremental data migration or incremental data synchronization task has not ended, the data verification task will continue running and will not automatically complete. This is because the incremental task continuously processes changes from the source end, and the data verification task needs to constantly follow the data changes on both the source end and the destination for verification. With incremental migration or incremental synchronization tasks still running, it is expected that the verification task remains "in progress."

   * **Handling suggestion**: If you need to continuously verify data between the source end and the destination, you can let the verification task keep running. If verification is no longer needed, you can manually terminate the verification task. For more information, refer to [Data verification task management](https://docs.byteplus.com/en/docs/DTS/viewing_data_validation#.5ZCO57ut5pON5L2c).
