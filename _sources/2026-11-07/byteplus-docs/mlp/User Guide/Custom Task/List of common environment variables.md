---
title: "List of common environment variables"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/List_of_common_environment_variables"
---

When using the Custom Training module, the Machine Learning Platform injects a large number of common environment variables for users to easily use in their code.

**Training role independent**


|variable name |Error Message |variable description |
|---|---|---|
|MLP_TASK_ID |t\-20210924211641\-nznsh |The ID of the task. |
|MLP_TASK_OWNER |username |The user who created the task. |
|MLP_TASK_NAME |mnist |The task name at the time of submission. |
|MLP_TASK_IMAGE |cr\-cn\-beijing.ivolces/ml_platform/python:2.7_3.7 |Address of the training mirror. |
|MLP_TASK_CMD |python3 /root/code/main.py |The start command for the task. |
|MLP_TASK_ARGS |\-\-key1 value1 \-\-key2 value2 |Splice the parameter list directly after the start command. |
|MLP_ROLE |WORKER |Training roles in distribution. The value range is WORKER/SERVER/SCHEDULER/CHIEF/PS/EVALUATOR. |
|MLP_ROLE_INDEX |0 |The role number of this node (starting from 0), such as worker0, worker1... |
|MLP_${MLP_ROLE}_RACK_SW_ID |febd30c7302dda1fae1399fe0266930f |The switch hash id of the node where the task instance is located, which is injected only into the HPC container. |
|MLP_RACK_TOPO_FILE |/ml_platform/rack_topo |The path to the switch information file in the container. |
|MLP_${MLP_ROLE}_RACK_RANK_INDEX |0 |The sequence number of the instance's location, sorted by switch id. Sorting guarantees that worker0 has index = 0. |
|MLP_IFNAME |eth0 |The name of the default network interface card. |
|GLOO_SOCKET_IFNAME |eth0 |The network interface card name specified for Gloo. |
|MLP_HOST |10.128.97.74 |The IP of the current node is the RDMA IP when there is RDMA, otherwise it is the VPC IP. |
|MLP_PRIMARY_HOST |10.128.97.74 |The VPC IP of the current node. |


**Training role related**


|variable name |Error Message |variable description |
|---|---|---|
|MLP_${ROLE}_NUM |2 |The number of nodes for this role. |
|MLP_${ROLE}_CPU |2 |The number of CPUs for this role node. |
|MLP_${ROLE}_MEM |10240 |The MEM size of the role node in MB. |
|MLP_${ROLE}_GPU |3 |The number of GPUs for this role node. |
|MLP_${ROLE}_ALL_HOSTS |10.128.97.74,10.128.96.17,... |The host names of all instances of this role. |
|MLP_${ROLE}_${INEDX}_HOST |10.128.97.74 |The host name of the INEDX node of this role. |
|MLP_${ROLE}_${INEDX}_PORT |9006 |The port of the INEDX node of this role. |
|MLP_${ROLE}_ALL_PRIMARY_HOSTS |10.128.97.74 |The VPC IPs of all instances of this role. |
|MLP_${ROLE}_${INEDX}_PRIMARY_HOST |10.128.97.74 |The VPC IP of the INEDX node of this role. |
