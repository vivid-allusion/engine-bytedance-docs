---
title: "How do I handle the disconnection of an agent-registered cluster caused by a missing agent?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How_can_you_address_the_cluster_going_offline_due_to_the_lack_of_an_Agent"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description 

A cluster that is registered through an agent remains in a disconnected status for a long period of time.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

When you register a cluster by using an agent, you need to install the agent for communication on an existing node in the cluster. If the agent cannot be installed, the registered cluster will become disconnected in VKE. The following scenarios may occur:


* **Scenario 1**: If the node to which the Agent belongs is taken offline but other nodes still exist, the Agent will be automatically migrated to another available node. As a result, the registered cluster will become disconnected for a short period of time.

* **Scenario 2**: If all nodes are taken offline, the Agent cannot be installed. As a result, the registered cluster will become disconnected.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

We recommend that you retain at least one node that runs as expected to ensure the Agent can be installed and thus the cluster can be connected. To resolve the preceding issues, use the following methods:


* **Solution 1**: For Scenario 1, no additional operations are required. The cluster will become connected after the agent is migrated.

* **Solution 2**: For Scenario 2, the cluster is disconnected, and nodes cannot be added or published through VKE. Go to the source platform to add or publish nodes. Then, the agent will automatically recover, and the cluster will become connected.
