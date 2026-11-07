---
title: "Service scaling"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Service_scaling"
---

During cluster operation, if service deployment is found to be suboptimal, such as resource contention due to load or missing topology settings during deployment, service components can be scaled in or out. This allows dynamic adjustment of service deployment locations based on load and resource contention, without the need to rebuild the entire service. This document introduces the configuration methods for service scaling.

<span id="968b3974"></span>
# Limits


* Components that support scaling: Presto, Trino.

* Node groups that support service scaling: Core node group, Task node group.

* When the sum of the number of core node groups and Task node groups currently covered by Presto or Trino deployment is less than 2, **service scale\-in** is unavailable.


<span id="e26355f8"></span>
# Feature details


* Service scale\-out: If the cluster has Core or Task node groups where the service is not deployed, deployment can be added to these node groups. The deployment topology after scaling out remains effective.

* Service scale\-in: Components can be removed from certain Core or Task node groups. The deployment topology after scaling in remains effective.

* Sources of node groups available for service scaling:

   * Node groups added during cluster creation.

   * Node groups expanded during cluster operation. For scaling operations, see [Scale clusters](https://docs.byteplus.com/docs/E-MapReduce/Scale_up_clusters).


<span id="173aac11"></span>
# Procedure

<span id="173aac11"></span>
## Feature entry

Log in to [EMR Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?) and click the cluster name to enter the cluster details. On the cluster **Service list**page, locate the service to be scaled in or out, click the More icon on the right, and in the pop\-up menu, select **service scale\-out** or **service scale\-in.** 

<span id="2498c05f"></span>
## Scaling configuration

On the service scale\-out or scale\-in configuration page, in **Target deployment topology**, select the node group to be scaled in or out, enter **operation remarks**, and click **Confirm scale\-out** to submit the task. When the task succeeds, a prompt appears at the top **Operation successful**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Some <strong>component roles</strong> do not support scaling, and the options are grayed out and cannot be selected.</div>


<span id="adf9374d"></span>
## Operation audit

After submitting the service scaling task, you can view the task log in **Operation logs**.
