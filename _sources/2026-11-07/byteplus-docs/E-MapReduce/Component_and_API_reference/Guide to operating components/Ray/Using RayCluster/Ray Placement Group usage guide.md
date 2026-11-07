---
title: "Ray Placement Group usage guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Ray_Placement_Group_usage_guide"
---

Placement Group is a feature in Ray that allows users to reserve resources in a cluster atomically—that is, either all resources are successfully reserved, or none are reserved, ensuring that partial resource reservation does not occur. This is very useful for ensuring sufficient resources to run specific tasks or collections of actors.

A Placement Group consists of a set of resource bundles, with each bundle representing a group of resources to be reserved. Users can specify the size and type of each resource bundle. For example, creating a resource bundle: {"CPU": 1, "GPU": 1} represents 1 CPU and 1 GPU.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_796f9c1a416e0cd4ab76867fbe860793.png) </span>


1. A resource bundle cannot be created across nodes; the required resources must be fully satisfied on a single node. As shown above, creating `{"CPU": 9}` will not be scheduled onto this node.

2. After a resource bundle `{"CPU": 1, "GPU": 1}` has been created, creating `{"CPU": 2, "GPU": 2}` will remain in the pending state.


<span id="_1-适用场景"></span>
## 1 **Use cases**


1. **Tightly collaborating tasks and actors**: For tasks and actors that require frequent communication or shared state, placing them in the same Placement Group can reduce communication latency and improve overall efficiency.

2. **Resource\-intensive tasks**: For tasks that require a large amount of specific resources, such as GPUs, using Placement Group ensures these tasks can obtain the required resources and do not compete with other tasks for them.

3. **Multi\-tenant environments**: In multi\-tenant environments, it may be necessary to isolate jobs from different users onto separate nodes. Placement Group can be used to allocate resources based on user or job tags.

4. **Performance testing and tuning**: By grouping tasks and actors and running them on specific nodes, it is easier to conduct performance testing and tuning, as the job's runtime environment can be controlled more precisely.

5. **Fault isolation**: By distributing tasks or actors across multiple nodes, the impact of a single node failure on the overall application can be reduced. This can be achieved by using the SPREAD or STRICT_SPREAD strategy.


Therefore, when using Placement Group, it is necessary to consider the cluster's resource allocation, the communication patterns of tasks and actors, and the overall performance objectives. Proper use of Placement Group enables better management and optimization of Ray cluster resource utilization, improving application performance and reliability.

<span id="_2-placement-group-策略"></span>
## Placement Group strategies

In Ray, Placement Group strategies are used to specify how bundles of resources are placed within the cluster. The following are the four placement strategies supported by Ray:


1. PACK: This strategy attempts to pack all bundles onto the same node as much as possible. If a single node cannot satisfy the requirements of all bundles, the bundles will be distributed across other nodes. This is a soft strategy; even if all bundles cannot be packed onto the same node, the creation of the Placement Group will not fail.

2. SPREAD: This strategy attempts to distribute bundles across different nodes as much as possible. If the number of nodes in the cluster is less than the number of bundles, multiple bundles may be placed on the same node. This is also a soft strategy; even if all bundles cannot be distributed across different nodes, the creation of the Placement Group will not fail.

3. STRICT_PACK: This strategy is similar to PACK, but it is a hard strategy. If a single node cannot satisfy the requirements of all bundles, the creation of the Placement Group will fail.

4. STRICT_SPREAD: This strategy is similar to SPREAD, but it is also a hard strategy. If the number of nodes in the cluster is less than the number of bundles, the creation of the Placement Group will fail.


These strategies can be specified using the `ray.util.placement_group` function's `strategy` parameter. By appropriately selecting and using these strategies, users can control how tasks and actors are placed within the cluster according to their needs.

<span id="_3-适用示例"></span>
## Applicable examples


1. Create placement group


Use the `ray.util.placement_group` module to create a Placement Group, specifying the resource labels and quantities for the group, as well as whether to place the group on the same node.

```python
from pprint import pprint
import time
# Import placement group APIs.
from ray.util.placement_group import (
    placement_group,
    placement_group_table,
    remove_placement_group,
)
from ray.util.scheduling_strategies import PlacementGroupSchedulingStrategy
# Initialize Ray.
import ray
head_ip = {xxx}
head_port = {xxx} # The default is 10001
# Initialize connection using existing ray clusters
ray.init(address="ray://{}:{}".format(head_ip, head_port))
# OR create a single node Ray cluster.
# ray.init(num_cpus=2, num_gpus=2)
# Reserve a placement group of 2 bundles# that have to be packed on the same node.
pg = placement_group([{"CPU": 1}, {"CPU": 1}], strategy="STRICT_PACK")
```


In the example, head_ip and head_port need to be filled in with the address of the RayCluster.

In the example, `strategy="STRICT_PACK"` indicates that these resource labels will be packed as tightly as possible onto available nodes.


2. Use the command\-line tool `ray status` to view the resource usage and scheduling requirements of the Placement Group.

   ```bash
   ray status
   ```
   


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2c9e113118e2f232eae7ae003821065f.png) </span>


3. Bind tasks and actors to the Placement Group.

   After creating the Placement Group, bind tasks and actors to this group. This means they will only run on the nodes specified by the Placement Group.

   ```python
   # Start an actor and bind it to the Placement Group
   @ray.remote(num_cpus=1)
   class Actor:
       def __init__(self):
           pass
       def ready(self):
           pass
   
   # Start an actor instance and bind it to the Placement Group
   actor = Actor.options(
       scheduling_strategy=PlacementGroupSchedulingStrategy(
           placement_group=pg,
       )
   ).remote()
   
   # Schedule a task and bind it to the Placement Group
   ray.get(actor.ready.remote(), timeout=10)
   ```
   


Use the following command to check the execution status of actors.

```bash
ray list actors --detail
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e0543f151f1ec18e1f4dd65c190c1243.png) </span>


4. Manage Placement Group.

   Use functions from the `ray.util.placement_group` module to manage the Placement Group, such as querying its status or deleting it.

   ```python
   # Query the status of the Placement Group
   print(placement_group_table(pg))
   
   # Delete the Placement Group
   remove_placement_group(pg)
   # Wait for the placement group to be killed.
   time.sleep(1)
   
   # Query the status of the Placement Group
   pprint(placement_group_table(pg))
   """
   
   {'bundles': {0: {'CPU': 1.0}, 1: {'CPU': 1.0}},
     'bundles_to_node_id': {0: '80392f59de1342137f765234dd680631840a7980042fbef1dbd6fdf5',
                                                   1: '80392f59de1342137f765234dd680631840a7980042fbef1dbd6fdf5'},
     'name': '',
     'placement_group_id': '002fb67e762f4bc0805e22e0dcc322000000',
     'state': 'REMOVED',
     'stats': {'end_to_end_creation_latency_ms': 1.649,
                         'highest_retry_delay_ms': 0.0,
                         'scheduling_attempt': 1,
                         'scheduling_latency_ms': 1.41,
                         'scheduling_state': 'REMOVED'},
     'strategy': 'STRICT_PACK'}
   
   """
   ```
