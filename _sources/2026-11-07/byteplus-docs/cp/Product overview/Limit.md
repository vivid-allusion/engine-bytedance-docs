---
title: "Limit"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Limit"
---

This article introduces some constraints and limitations in the process of using the Code Pipeline Product. Please use your quota appropriately to avoid affecting business operations.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to adjust your quota, please <a href="https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000168">submit a ticket</a> to apply.</div>


<span id=".5bel5L2c5Yy6"></span>
## Workspace


|Indicator items |Description |Limit value |
|---|---|---|
|Number of workspaces |Number of workspaces that can be created by each BytePlus root user. |500 items |


<span id=".5rWB5rC057q_"></span>
## Pipeline

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Pipeline runtime duration</strong> and <strong>pipeline concurrency</strong> restrictions apply only when running pipelines using the public resource pool. </div>



|**Indicator items** |**Description** |**Limit value** |
|---|---|---|
|Free pipeline running time |Available pipeline runtime for each BytePlus root user |None |
|Number of concurrent pipelines |The number of pipelines that can run concurrently for each BytePlus root user. |20 items |
|Pipeline run records |Number of runtime records that can be displayed for each pipeline. |No limit |
|Custom step count |Number of custom steps that can be created per BytePlus account. |No limit |
|The maximum number of pipeline stages |Maximum number of stages supported by each pipeline. |10 |
|Maximum number of tasks per stage |Maximum number of tasks supported per stage. |10 |
|Maximum steps per task |Maximum number of steps supported per task. |10 |
|Run time for each step |Maximum runtime for each step. |Limited by the task timeout duration you set |


<span id=".6YCa55-l5o-Q6YaS"></span>
## Notification

Pipelines, manual checkpoint tasks, and application delivery workflows are subject to message receiving frequency limitations when using the following notification methods. The specific restrictions are as follows:


|Notification method |Limit dimensions |Maximum receiving frequency per minute |Maximum receiving frequency per hour |Maximum daily receiving frequency |
|---|---|---|---|---|
|Site message |the same BytePlus account |20 items per minute |25 items per hour |30 items per day |
|Email |The same email address |20 items per minute |25 items per hour |30 items per day |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Minute\-level, hour\-level, and day\-level frequency limits take effect simultaneously. If any level limit is exceeded, the message will fail to send.</div>


* <div data-tips="true" data-tips-type="tip">Frequency limits at the minute, hour, and day levels are calculated starting from the receipt of the first message.</div>
