---
title: "Read-only node"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/read-only_nodes"
---

This topic summarizes frequently asked questions about RDS for PostgreSQL read\-only nodes.

<span id=".5LuA5LmI5piv5Y-q6K-76IqC54K577yf"></span>
#### **What is a read\-only node?** 

For applications with a large number of read requests, you can create one or more read\-only nodes to meet the high demand for database reads and increase application throughput. For detail, refer to [Read-only node overview](https://docs.byteplus.com/en/docs/RDS_for_PG/overview_of_read-only_nodes).

<span id=".5aaC5L2V6YCJ5oup5Y-q6K-76IqC54K555qE6KeE5qC877yf"></span>
#### **How to choose the node specification for a read\-only node?** 

They can be different from the primary node specification, and can also be modified at any time. We recommend that the specification of a read\-only node be higher than that of the primary node, or else it can easily result in high delays and high load on the read\-only node.

<span id=".5Y-q6K-76IqC54K555qE572R57uc57G75Z6L5Y-v5Lul5LiO5Li76IqC54K55LiN5LiA5qC35ZCX77yf"></span>
#### **Can the network type of the read\-only node be different from that of the primary node?** 

Currently, only VPC is supported.

<span id=".5Y-q6K-76IqC54K555qE6LSm5Y-35ZKM5Li76IqC54K55LiA5qC35ZCX77yf"></span>
#### **Is the account of the read\-only node the same as the primary node?** 

A read\-only node can be accessed through the account of the primary node. Both the account and database are synced from the primary node.

<span id=".5LiA5Liq6IqC54K55LiL5pyA5aSa5Y-v5Lul5Yib5bu65aSa5bCR5Liq5Y-q6K-76IqC54K577yf"></span>
#### **How many read\-only nodes can I create under a single node?** 

10.

<span id=".5Y-q6K-76IqC54K55Li65L2V5rKh5pyJ5aSH5Lu95Yqf6IO977yf"></span>
#### **Why do read\-only nodes have no backup function?** 

Because the primary node already has backups, read\-only nodes currently do not support backup settings or manual backup initiation.

<span id=".5Yib5bu65Y-q6K-76IqC54K55Lya5b2x5ZON5Li76IqC54K55ZCX77yf"></span>
#### **Will creating a read\-only node affect the primary node?** 

Creating a read\-only node replicates data from the secondary node, so it does not affect the primary node. Any data updates on the primary node will be automatically synced to all the read\-only nodes immediately when the operation is completed on the primary node.
