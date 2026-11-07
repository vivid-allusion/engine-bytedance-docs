---
title: "RayCluster supports multiple WorkerGroups"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/RayCluster_supports_multiple_WorkerGroups"
---

<span id="6256b327"></span>
## Background

Starting from EMR on VKE version 3.15, RayCluster supports the capability for multiple WorkerGroups. Structurally, each WorkerGroup corresponds to a group of pods, and a RayCluster consists of one headgroup and multiple WorkerGroups. Users can specify in code which WorkerGroup a Ray job runs on, which helps address resource isolation issues in persistent RayClusters. For reference, see: [WorkerGroup related documentation](https://docs.ray.io/en/latest/cluster/kubernetes/user-guides/config.html#pod-configuration-headgroupspec-and-workergroupspecs).

<span id="b518acbb"></span>
## Prerequisites


1. The cluster version must be 3.15.0 or above.

2. The Ray service in the EMR on VKE product has been deployed.

3. The Ray component KubeRayOperator is running properly.


<span id="8dd4c3d0"></span>
## User guide

<span id="de170ea9"></span>
### RayCluster management

Currently, RayCluster can be managed using either a form or YAML. For basic developers, it is recommended to add RayClusters using the form; for those familiar with Kubernetes or RayCluster, adding via YAML provides more comprehensive configuration options.

<span id="0615ca33"></span>
#### Add a RayCluster


1. Add a RayCluster using the form:

   1. In the basic information section: Enter the RayCluster name, which only supports lowercase letters.

   2. In the resource configuration section: By default, a configuration template for the headgroup and one workergroup is provided. Here, you can edit the group name, pod specifications, pod count, storage configuration, and so on. If one workergroup does not meet business requirements, click the Add Workergroup button below to add more.

   3. In the advanced configuration section: You can use the EMR recommended base image or select an image from a custom image repository as the runtime image for the headgroup and workergroup pods; it is recommended to enable the GCS switch in production environments and use an external Redis to ensure RayCluster availability.

2. Adding a RayCluster via YAML is the same as the method used before EMR on VKE version 3.14. EMR also provides a YAML editing template, which you can modify as needed.


Please note the following:


* Currently, a single RayCluster supports up to 10 workergroups. Please plan your business requirements accordingly.

* To use GPU resources, manually configure the node scheduling policy and use hard constraints to ensure that the workergroup can be scheduled to the corresponding node.

* Storage configuration supports mounting VEPFS/NAS/TOS/EBS storage. The corresponding PVC must be created in the VKE cluster in advance to enable binding.

* When selecting EBS as the storage PVC, since this type of PVC only allows one Pod to be mounted, only one Pod can exist under the corresponding workergroup, and scaling operations cannot be performed successfully.

* The Resource label is bound to the workergroup. After the submitted job code is correctly configured with the corresponding Resource label, RayCluster will route the job to the corresponding workergroup for execution.


<span id="c5539bf9"></span>
#### Restart RayCluster

Restarting RayCluster will delete and relaunch all related Pods. Please proceed with caution.

<span id="d35b69c0"></span>
#### Edit RayCluster

The console supports editing existing RayClusters. You can choose either form editing or YAML editing as needed.


1. Form editing is performed at the group level and does not affect other workergroups in the RayCluster being edited:

   1. Existing RayClusters support adding new workergroups, and the configuration is consistent with the workergroup\-related settings used when creating a RayCluster via the form.

   2. The left side of RayCluster displays the number of groups. After expanding the group list, you can view information about each group. Click the group name to view more details, including the number of Workers (actual running Pod count / expected Pod count), storage configuration, scheduling policy, and more.

   3. Scaling operations are used to control the number of Worker Pods under a workergroup.

   4. The delete operation will remove the current workergroup and clean up the corresponding Worker Pods.

   5. The restart operation will relaunch all Worker Pods under the current workergroup.

2. Modifying RayCluster via YAML editing is consistent with the behavior prior to EMR on VKE version 3.14. Important: After YAML editing is saved, the RayCluster CR will be updated directly (this can be viewed in VKE Cluster \- Object Browser \- raycluster). After the RayCluster CR changes, different types of changes have different handling logic according to the open\-source version's behavior.

   1. When the change is to add a workergroup or edit the replica count of a workergroup, the change takes effect immediately (after adding a workergroup, the related Pods are created immediately; after editing the workergroup replica count, the number of related Pods will increase or decrease accordingly).

   2. When the change is to delete a workergroup or edit resources related to a workergroup, the change does not take effect immediately (after deleting a workergroup, the related Pods under that workergroup are not automatically cleaned up; after editing CPU or memory resources for a workergroup, the related Pods are not relaunched). Therefore, after these types of operations, you need to manually restart RayCluster or delete the corresponding Pods in the VKE cluster and wait for them to be relaunched for the changes to take effect.


<span id="81a7c2be"></span>
#### Remove RayCluster

Removing RayCluster will delete the related CR and clean up all Pods. Please proceed with caution.

<span id="866b6f7f"></span>
### Submit a job to an existing RayCluster

Job management now supports submitting jobs to an existing RayCluster. The submission method is as follows:


1. On the Create Job page, select Ray Job as the job type, and select the EMR cluster where RayCluster has already been deployed as the execution resource.

2. Enter the RayJob YAML example, and specify the target RayCluster for job execution through ray.io/cluster.


```YAML
apiVersion: ray.io/v1
kind: RayJob
metadata:
  name: rayjob-use-existing-raycluster
spec:
  entrypoint: python -c "import ray; ray.init(); print(ray.cluster_resources())"
  # Select an existing RayCluster called ${ray-cluster-name} instead of creating a new one.
  clusterSelector:
    ray.io/cluster: ${ray-cluster-name}
  submissionMode: "HTTPMode"
```



3. To specify that the job runs on a particular workergroup, for example, if there are two workergroups with resource labels {"Custom1": 1} and {"Custom1": 1, "Custom2": 5}, configure the job code to be executed as follows.


```Python
import socket
import ray 
import time

# Specify the default resource requirements for this remote function.
@ray.remote(resources={"Custom1": 1})
def func():
    # Get the hostname
    hostname = socket.gethostname()
    # Obtain the IP address using the hostname
    ip_address = socket.gethostbyname(hostname)
    print(f"1--当前机器IP地址: {ip_address}")
    
@ray.remote(resources={"Custom1": 1, "Custom2": 5})
def func2():
    # Get the hostname
    hostname = socket.gethostname()
    # Obtain the IP address using the hostname
    ip_address = socket.gethostbyname(hostname)
    print(f"2--当前机器IP地址: {ip_address}")   

def test():
    for i in range(0,10):
        func.remote()
        time.sleep(5)
        func2.remote()

ray.init()
test()
```


Save the code as a test.py file and upload it to the target RayCluster headpod directory. After modifying the RayJob YAML, click Save, then Submit Job.

```YAML
apiVersion: ray.io/v1
kind: RayJob
metadata:
  name: rayjob-use-existing-raycluster
spec:
  # execute task
  entrypoint: python "${headpod_path}/test.py"
  clusterSelector:
    ray.io/cluster: ${ray-cluster-name}
  submissionMode: "HTTPMode"
```
