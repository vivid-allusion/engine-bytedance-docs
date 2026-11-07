---
title: "Kubernetes image upgrade failed Logs target app operated by other parallel pipelines or tasks"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Kubernetes_image_upgrade_failed_Logs_target_app_operated_by_other_parallel_pipelines_or_tasks"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue phenomenon

The pipeline failed to execute the Kubernetes image upgrade task. The log indicates: "The target application is currently being operated on by other parallel pipelines or tasks. Please wait until the application upgrade is complete before retrying." Actual inspection showed that no other pipeline was performing actions on the target application at the same time.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

Under normal circumstances, the pipeline marks the target workload as being operated on by adding an annotation, and removes the annotation after the operation is completed. If a workload has been rolled back via the container service console or Kubernetes, or if the pipeline fails to delete annotations due to network or service fluctuations, the workload will retain incorrect annotations. This may cause a subsequent pipeline executing the task to mistakenly identify the target application as being operated on by other parallel pipelines or tasks, resulting in task failure.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

Check the annotations of the target workload, delete annotations that start with `deploy.cp`, and then rerun the pipeline.
