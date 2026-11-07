---
title: "Ray GCS usage guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Ray_GCS_usage_guide"
---

<span id="85b8fd04"></span>
## Prerequisites


1. A Redis instance has been created and a password has been set. If not, refer to [Create instance](https://www.volcengine.com/docs/6293/71107).

2. An EMR Ray cluster has been created. To create a Ray cluster, refer to [Create virtual cluster](https://docs.byteplus.com/docs/E-MapReduce/109064).

3. The EMR Ray cluster and Redis are in the same network, and the network where the Ray cluster resides is included in the allowlist of the Redis instance.

4. Remove 'keys' from the `disabled-commands` parameter in the Redis instance to allow execution of the keys command.


<span id="e38c1a7f"></span>
## Create GCS HA Ray cluster


1. In the **Service list**, click **Ray** to enter the **Deployment topology** page.

2. Click **Add RayCluster**. On the **Add RayCluster** page, enable **GCS high availability**, select the corresponding Redis instance, enter the corresponding Redis password, and click **Confirm** to create the RayCluster.


<span id="617ea7f9"></span>
## Verification

<span id="f0a57798"></span>
### Create two Python files in the Ray Head Pod

detached_actor.py

```Python
import ray

@ray.remote(num_cpus=1)
class Counter:
    def __init__(self):
        self.value = 0

    def increment(self):
        self.value += 1
        return self.value

ray.init(namespace="default_namespace")
Counter.options(name="counter_actor", lifetime="detached").remote()
```


increment_counter.py

```Python
import ray

ray.init(namespace="default_namespace")
counter = ray.get_actor("counter_actor")
print(ray.get(counter.increment.remote()))
```


<span id="1b89f9a3"></span>
### Create actor

```Python
python3 detached_actor.py
2025-01-21 21:48:55,351 INFO worker.py:1461 -- Using address 127.0.0.1:6379 set in the environment variable RAY_ADDRESS
2025-01-21 21:48:55,351 INFO worker.py:1601 -- Connecting to existing Ray cluster at address: 10.1.0.134:6379...
2025-01-21 21:48:55,357 INFO worker.py:1777 -- Connected to Ray cluster. View the dashboard at http://10.1.0.134:8265 

python3 increment_counter.py

2025-01-21 21:49:18,140 INFO worker.py:1461 -- Using address 127.0.0.1:6379 set in the environment variable RAY_ADDRESS
2025-01-21 21:49:18,141 INFO worker.py:1601 -- Connecting to existing Ray cluster at address: 10.1.0.134:6379...
2025-01-21 21:49:18,146 INFO worker.py:1777 -- Connected to Ray cluster. View the dashboard at http://10.1.0.134:8265 
1
```


<span id="f84ac829"></span>
### Terminate GCS service

```XML
ps aux | grep gcs_server | grep -v grep | awk '{print $2}' | xargs kill -9
```


<span id="b323e5de"></span>
### After the head recovers, check the actor value

The return value is 2, which meets expectations.

```Python
python3 increment_counter.py
2025-01-21 21:53:12,456 INFO worker.py:1461 -- Using address 127.0.0.1:6379 set in the environment variable RAY_ADDRESS
2025-01-21 21:53:12,456 INFO worker.py:1601 -- Connecting to existing Ray cluster at address: 10.1.0.134:6379...
2025-01-21 21:53:12,462 INFO worker.py:1777 -- Connected to Ray cluster. View the dashboard at http://10.1.0.134:8265 
2
```
