---
title: "Viewing node difference parameters"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Viewing_instance_node_parameter_differences"
---

This topic describes how to view parameter differences among the nodes of an RDS for MySQL instance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

RDS for MySQL supports modifying instance parameters and allows setting different running values for read\-only nodes than for the primary node. To provide a clearer and more accurate overview of an instance's state, RDS for MySQL provides a node difference parameter list to view parameter differences among the instance's nodes.

The node difference parameter list displays the parameters that differ among an instance's nodes. It also shows the Node ID, availability zone, node specification, the value of each differing parameter on each node (excluding secondary nodes), and the formula (if any).

<span id=".5pON5L2c5q2l6aqk"></span>
## Precautions

Single\-node instances do not support this feature.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click the instance name of the target instance to enter the **Summary** page.

5. Click the **Parameter configuration** tab at the top of the page, then click the **Node difference parameter list** tab to view the instance's **node difference parameter list.**
