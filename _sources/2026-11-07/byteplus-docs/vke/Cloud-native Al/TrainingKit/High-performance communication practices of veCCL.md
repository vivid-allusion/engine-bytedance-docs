---
title: "High-performance communication practices of veCCL"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/High-performance_communication_practices_of_veCCL"
---

<span id="R3vUWDzw"></span>
## Introduction

BytePlus Collective Communication Library (veCCL) is a high\-performance collective communication library independently developed by BytePlus based on NVIDIA Collective Communication Library (NCCL). It can be installed on multiple GPUs within a single node or across multiple nodes. Leveraging the unique network infrastructure and extensive experience in communication optimization for large model tasks of BytePlus, veCCL achieves high\-performance communication among multiple GPUs.

veCCL provides a set of highly optimized communication primitives that can significantly enhance communication efficiency in specific topologies or collective operations, enabling parallel computing tasks to efficiently synchronize and exchange data across multiple GPUs. As an enhanced version of NCCL, veCCL is completely transparent to users. You can use veCCL by loading the dynamic library as expected without the need to change the way your application calls NCCL collective operations. Compared with the default implementation of NCCL, veCCL can automatically load and run algorithms optimized for specific topologies and communication scenarios, which significantly reduces communication latency and increases data throughput. In scenarios where the advanced features of veCCL are not supported, veCCL will intelligently fall back to the default implementation of NCCL.

<span id="LUdUzn5r"></span>
### Enhanced features


* High performance: veCCL provides optimal algorithms and implementations for specified machine types, topologies, and communication modes.

* Quick fault identification: veCCL can quickly identify faults in collaborative tasks within distributed clusters.

* Stability: veCCL can handle both simple and relatively complex exceptions. For example, veCCL provides the Softbond capability to achieve automatic failover when an elastic network interface (ENI) fails, which ensures stable and sustained business operations. For information about using the Softbond capability, see [Use the NCCL Softbond add-on to ensure training traffic recovery when a single ENI fails](https://docs.byteplus.com/en/docs/gpu/Use_the_NCCL_Softbond_Plugin_to_ensure_training_traffic_recovery).


<span id="UoeqHZnn"></span>
## Usage notes


* To ensure successful deployment, which involves multiple add\-ons that depend on each other and have complex configurations, you need to exactly follow the instructions in this topic.

* To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of VKE, you need to perform operations by following the solution described in this topic or on the recommended resources. If you want to use another solution, consult your account manager of BytePlus.

* Some features required to complete the deployment process are at the beta stage. To use the following feature, contact your account manager of BytePlus.



|**Beta features/resources** |**Related service** |**Description** |
|---|---|---|
|hpcpni3ln instance family of the High Performance Computing Optimized type |ECS |You need to apply for the beta trial of high\-performance instances. |


<span id="igFeXOX1"></span>
## Prerequisites

<span id="oRtz5trH"></span>
### Create an HPC cluster

The high\-performance compute (HPC) cluster is used to achieve logical isolation of HPC GPU instances (compute nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The HPC cluster must be deployed in the same availability zone as the VKE node.</div>


<span id="G16SGE1l"></span>
### Create a VKE cluster

When you create a cluster in VKE, take note of the configurations of the following parameters. For more details, refer to [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).


|Parameter |Description |
|---|---|
|**Cluster configuration** ||
|Kubernetes version |Select v1.28 or later.<br><br> |
|Network model |Select VPC\-CNI. |
|**Node pool configuration** ||
|Managed node pool |Select Enable to enable the managed node pool. |
|Availability zone |The VKE cluster is deployed in the same availability zone as the **HPC cluster**. |
|Instance type |Select ecs.hpcpni3ln because veCCL optimizes the network topologies of instances with specific specifications ** ** . |
|High\-performance computing cluster |Select the HPC cluster that you created.<br><br> |
|Number of nodes |Set the value to 1. |


**Add\-on configuration**: Except for add\-ons labeled as **system\-required**, you can install the following add\-ons based on your business requirements.


|<div style="text-align: center"><br><strong>Field</strong></div><br> |<div style="text-align: center"><br><strong>Add\-on name</strong></div><br> |<div style="text-align: center"><br><strong>Required</strong></div><br> |<div style="text-align: center"><br><strong>Add\-on description</strong></div><br> |
|---|---|---|---|
|<div style="text-align: center"><br>GPU</div><br> |nvidia\-device\-plugin |<div style="text-align: center"><br>Required</div><br> |The NVIDIA device driver, which is a management add\-on that allows the use of GPU devices in containers. |
|<div style="text-align: center"><br>Monitoring</div><br> |prometheus\-agent |<div style="text-align: center"><br>Required</div><br><br><br><div style="text-align: center"><br></div><br> |The monitoring add\-on of VMP, which collects and sends metrics of Kubernetes clusters to VMP. |
|<div style="text-align: center"><br>Storage</div><br> |csi\-ebs |<div style="text-align: center"><br>Required</div><br> |It allows VKE clusters to use the standard Container Storage Interface (CSI) of Elastic Block Storage (EBS). |


<span id="m4cQljw1"></span>
### Create a Deployment


* Create a Deployment. In the left navigation bar of the cluster management page, click **Workload \> Deployment**. On the page that appears, click **Click with Yaml**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9efe6de10dcc916f536154c6d51bd8ee.png) </span>


* Set the `containers.image` parameter to the image used by the training task. The image in this topic is for illustration purposes only.


```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-wan21
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      app: example-wan21
  strategy:
    rollingUpdate:
      maxSurge: 100%
      maxUnavailable: 100%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: example-wan21
    spec:
      containers:
      - args:
        - -c
        - tail -f /etc/hosts
        command:
        - sh
        image: vke-ap-southeast-1.cr.volces.com/vke/sglang:v0.4.7.byted_ep.0.0.4.202506201849
        imagePullPolicy: Always
        name: main
        resources:
          limits:
            nvidia.com/gpu: "8"
        volumeMounts:
        - mountPath: /data00/models
          name: models
        - mountPath: /dev/shm  # Mount a shared memory volume
          name: dshm
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 5
      volumes:
      - hostPath:
          path: /data01
          type: Directory
        name: models
      - name: dshm  # Add a shared memory volume of the emptyDir type
        emptyDir:
            medium: Memory
            sizeLimit: 100Gi  # Set the shared memory size to 100 GB
```


The image used in this topic is installed with NCCL. If NCCL is not installed in the image, go to the console of the created Deployment and run the following command to install NCCL.

```Bash
git clone -b v2.21.5-1 https://github.com/NVIDIA/nccl
cd nccl
make -j src.build
make install 
```


<span id="jEGWAOH3"></span>
## Procedure

<span id="NgezROuH"></span>
### Step 1: Install MPI


1. Run the following command to install Message Passing Interface (MPI).


```Bash
apt update
apt install openmpi-bin openmpi-common libopenmpi-dev
```


<span id="RE4eYdEi"></span>
### Step 2: Install NCCL tests


1. Run the following commands to view CUDA_HOME, MPI_HOME, and NCCL_HOME.


```Bash
#View NCCL_HOME
find / -name "nccl.h" 2>/dev/null
#View CUDA_HOME
echo $CUDA_HOME
#View MPI_HOME
find / -name "libmpi.so*" 2>/dev/null
which mpicc  # Locate mpicc # Sample output: /usr/local/openmpi/bin/mpicc# MPI_HOME: /usr/local/openmpi
```



2. Run the following command to install NCCL tests.


```Bash
git clone https://github.com/NVIDIA/nccl-tests.git
cd nccl-tests
make MPI=1 MPI_HOME=/usr/local/mpi/ CUDA_HOME=/usr/local/cuda/ NCCL_HOME=/usr/local/lib/python3.10/dist-packages/nvidia/nccl/
```


<span id="bQmLy6yt"></span>
### Step 3: Install veCCL


1. Run the following command to install veCCL.


```Bash
pip install veccl -i https://private.ivolces.com/pypi/simple
```



2. Run the following command to check whether veCCL is installed.


```Bash
ls `python3 -c "import veccl; print(veccl.ld_library_path())"`
```


The following figure shows the expected result, which indicates that veCCL is installed.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5278e92fb851d513496e396e829effaa.png) </span>

<span id="ccb1mlZ1"></span>
### Step 4: Configure the veCCL communication environment

After veCCL is installed, you need to configure the veCCL communication environment and make sure that LD_PRELOAD includes the veCCL library before veCCL is run.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic provides two configuration methods: shell script and Python script.</div>


<span id="WnFgIIlS"></span>
#### Shell script


1. Run the following scripts to configure the veCCL communication environment.


```Bash
# Preload the veCCL library to make sure that veCCL communication optimization takes precedence
export LD_PRELOAD=$(python3 -c "import veccl; print(veccl.lib_paths())"):${LD_PRELOAD}
# Specify the use of the Softbond add-on to improve network reliability
export NCCL_NET_PLUGIN=none
export NCCL_IB_TIMEOUT=23
# Add the dependency path of the veCCL library to the search path of the dynamic-link library
export LD_LIBRARY_PATH=$(python3 -c "import veccl; print(veccl.ld_library_path())"):$LD_LIBRARY_PATH
```



2. Specify `NCCL_DEBUG=INFO`. You can check whether veCCL is enabled based on the log in the red box. `NCCL version 2.23.4-veCCL-x.x.x+cuda12.2` indicates that veCCL is enabled.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bd530f006b5b1cc62584e2b8bdce04a4.png) </span>

<span id="PJqxziWJ"></span>
#### Python script


1. Run the following scripts to configure the veCCL communication environment.


```Python
import veccl
import os
import subprocess
# Configure key environment variables and enable veCCL high-performance communication optimization
veccl.enable() # Configure LD_PRELOAD, NCCL_NET_PLUGIN, and LD_LIBRARY_PATH
os.environ['NCCL_DEBUG'] = 'INFO'
os.environ['NCCL_IB_TIMEOUT'] = '23'
```



2. After the scripts are run, `veccl.enable()` will print the following information, which indicates that the key environment variables are configured.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7a1f97e031c160a3f154d868afb8bae8.png) </span>

<span id="YNDKS4lD"></span>
### Step 5: Verify veCCL operation results

The following sample code provides a script, test.py, which demonstrates the acceleration result achieved by the allreduce communication algorithm within the PyTorch distributed training framework on a single machine with eight GPUs.

```Python
import os
import torch
import torch.distributed as dist

def main():
    # Parse environment variables
    rank = int(os.environ["RANK"])
    local_rank = int(os.environ["LOCAL_RANK"])
    world_size = int(os.environ["WORLD_SIZE"])
    # Initialize the device and communication
    torch.cuda.set_device(local_rank)
    dist.init_process_group(backend="nccl")
    # Generate random tensors on each GPU and perform the all_reduce operation
    tensor = torch.randn(1024, device=f"cuda:{local_rank}")
    print(f"Rank {rank}: before allreduce tensor sum = {tensor.sum().item()}")
    dist.all_reduce(tensor, op=dist.ReduceOp.SUM)
    # Validate the result of the all_reduce operation and release resources
    print(f"Rank {rank}: after allreduce tensor sum = {tensor.sum().item()}")
    dist.destroy_process_group()

if __name__ == "__main__":
    main()
```



1. Run the `python3 -c "import torch; print(torch.__version__)"` command to view the PyTorch version.

2. Run the following script to run test.py.


<span id="MizwGbCq"></span>
####   Shell

```Bash
NCCL_DEBUG=INFO torchrun --nproc_per_node=8 test.py
```


<span id="xCmsFcqv"></span>
####   Python

```Python
# Start a distributed training task on a single machine with eight GPUs by running the test.py script
torchrun_command = ["torchrun","--nproc_per_node=8","test.py"] # Note: If you are prompted that torchrun cannot be found, enter the absolute path
try:
    subprocess.run(torchrun_command, check=True) # Note: The modifications to LD_PRELOAD only take effect on child processes. Therefore, subprocess.run is required.
# Capture and print information about the execution failure of the torchrun command
except subprocess.CalledProcessError as e:
    print(f"torchrun failed with error: {e}")
```



3. View the allreduce operation results based on veCCL.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_05b02d63b04f44d13a03ada228b95d54.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e988bdc8cdb6ae3395495ae53ff626e1.png) </span>

<span id="ogPj2ash"></span>
## Key environment variables


|**Environment variable** |**Description** |
|---|---|
|NCCL_SOCKET_IFNAME |You need to select an ENI used for socket communication during the initialization of NCCL. The used ENI may vary based on the instance specification. If you do not configure this variable or if you specify an invalid value, NCCL connections may fail. The ENI used in this topic is eth0. |
|NCCL_IB_GID_INDEX |This variable takes effect during multi\-node operations.<br><br>Specify the global ID used by RDMA. If you do not configure this variable or if you specify an invalid value, NCCL may encounter an error. |
|NCCL_IB_TIMEOUT |This variable takes effect during multi\-node operations.<br><br>We recommend that you set this variable to 18 when you use Softbond and 23 when you do not use Softbond.<br><br>This environment variable determines the timeout duration for RDMA data transmission. If you set this variable to 18, retransmission due to packet loss will be triggered by the RDMA network interface card (NIC) about 1.07 seconds after data is sent. In addition, when Softbond is enabled, this variable defines the time threshold for determining link unavailability and triggering traffic switching. |
|NCCL_NET_PLUGIN |We recommend that you set the variable to soft\-bonding to enable the Softbond stability enhancement capability of veCCL.<br><br>If you do not want to use Softbond, we recommend that you set the variable to none to prevent accidentally loading other unexpected add\-ons. |
|NCCL_DEBUG |In most cases, the log level is set to INFO to obtain more NCCL\-related logs, which helps troubleshoot issues. INFO\-level logs are printed only during initialization if no other log settings are configured, which does not affect communication performance. |


<span id="KeE5GjzM"></span>
## Performance testing

<span id="fUgs3WxL"></span>
### All Reduce

```Plain Text
#veccl
mpirun --report-bindings --map-by slot --bind-to none --mca btl ^openib --mca pml ob1  --allow-run-as-root -np 8 -x NCCL_DEBUG=INFO -x LD_LIBRARY_PATH=/usr/local/lib/python3.10/dist-packages/veccl/lib /sgl-workspace/nccl-tests/build/all_reduce_perf -b 128 -e 2GB -f 2 -g 1 -c 1 -n 10 -w 5
#nccl
mpirun --report-bindings --map-by slot --bind-to none --mca btl ^openib --mca pml ob1  --allow-run-as-root -np 8 -x NCCL_BCCL_ENABLE=0 -x LD_LIBRARY_PATH=/usr/local/lib/python3.10/dist-packages/veccl/lib /sgl-workspace/nccl-tests/build/all_reduce_perf -b 128 -e 2GB -f 2 -g 1 -c 1 -n 10 -w 5
```



| |<div style="text-align: center"><br>NCCL 2.23</div><br> |||<div style="text-align: center"><br>veCCL</div><br> |||||
|---|---|---|---|---|---|---|---|---|
|size (B) |time (us) |algbw (GB/s) |busbw (GB/s) |time (us) |algbw (GB/s) |busbw (GB/s) |speedup |algorithm |
|128 |15.67 |0.01 |0.01 |9.75 |0.01 |0.02 |1.61 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|256 |15.64 |0.02 |0.03 |9.97 |0.03 |0.04 |1.57 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|512 |15.93 |0.03 |0.06 |9.82 |0.05 |0.09 |1.62 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|1024 |16.13 |0.06 |0.11 |9.86 |0.1 |0.18 |1.64 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|2048 |16.09 |0.13 |0.22 |9.77 |0.21 |0.37 |1.65 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|4096 |16.75 |0.24 |0.43 |9.90 |0.41 |0.72 |1.69 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|8192 |16.57 |0.49 |0.87 |9.95 |0.82 |1.44 |1.67 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|16384 |17 |0.96 |1.69 |10.35 |15.8 |2.77 |1.64 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|32768 |18.2 |1.8 |3.15 |11.26 |2.91 |5.09 |1.62 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|65536 |18.5 |3.54 |6.2 |12.36 |5.3 |9.28 |1.50 |allreduce_a100_allpairs\-\-gpus_8\-instances_4.xml |
|131072 |18.79 |6.97 |12.21 |13.09 |10.01 |17.53 |1.44 |allreduce_a100_allpairs\-\-gpus_8\-instances_4.xml |
|262144 |19.12 |13.71 |24 |14.69 |17.84 |31.22 |1.30 |allreduce_a100_allpairs\-\-gpus_8\-instances_4.xml |
|524288 |19.38 |270.6 |47.35 |18.27 |28.7 |50.22 |1.06 |allreduce_a100_allpairs\-\-gpus_8\-instances_4.xml |
|1048576 |24.55 |42.7 |74.73 |24.94 |42.04 |73.57 |0.98 |ndv5_r48ll.xml |
|2097152 |41.15 |50.96 |89.18 |41.12 |51 |89.24 |1.00 |ndv5_r48ll.xml |
|4194304 |53.54 |78.33 |137.08 |53.51 |78.38 |137.17 |1.00 |ndv5_r48ll128.xml |
|8388608 |81.11 |103.42 |180.98 |81.15 |103.38 |180.91 |1.00 |allreduce_a100_ring\-\-gpus_8\-channels_8\-instances_4.xml |
|16777216 |120.9 |138.73 |242.78 |122.30 |137.18 |240.06 |0.99 |NCCL |
|33554432 |197.2 |170.12 |297.71 |196.20 |171.01 |299.26 |1.01 |NCCL |
|67108864 |320.1 |209.68 |366.94 |319.40 |210.12 |367.71 |1.00 |NCCL |
|134217728 |570.1 |235.42 |411.99 |571.20 |234.96 |411.18 |1.00 |NCCL |
|268435456 |1091 |246.04 |430.56 |1087.00 |246.95 |432.16 |1.00 |NCCL |
|536870912 |2122.7 |252.91 |442.6 |2120.30 |253.2 |443.1 |1.00 |NCCL |
|1073741824 |4011 |267.7 |468.48 |4011.30 |267.68 |468.44 |1.00 |NCCL |
|2147483648 |7918 |271.21 |474.63 |7906.30 |271.62 |475.33 |1.00 |NCCL |


<span id="rhC3RKry"></span>
### All Gather

```Bash
#veccl
mpirun --report-bindings --map-by slot --bind-to none --mca btl ^openib --mca pml ob1  --allow-run-as-root -np 8 -x NCCL_DEBUG=INFO -x LD_LIBRARY_PATH=/usr/local/lib/python3.10/dist-packages/veccl/lib /sgl-workspace/nccl-tests/build/all_gather_perf -b 128 -e 2GB -f 2 -g 1 -c 1 -n 10 -w 5
#nccl
mpirun --report-bindings --map-by slot --bind-to none --mca btl ^openib --mca pml ob1  --allow-run-as-root -np 8 -x NCCL_BCCL_ENABLE=0 -x LD_LIBRARY_PATH=/usr/local/lib/python3.10/dist-packages/veccl/lib /sgl-workspace/nccl-tests/build/all_gather_perf -b 128 -e 2GB -f 2 -g 1 -c 1 -n 10 -w 5
```



| |<div style="text-align: center"><br>NCCL 2.23</div><br> |||<div style="text-align: center"><br>veCCL</div><br> |||||
|---|---|---|---|---|---|---|---|---|
|size (B) |time (us) |algbw (GB/s) |busbw (GB/s) |time (us) |algbw (GB/s) |busbw (GB/s) |speedup |algorithm |
|128 |10.52 |0.01 |0.01 |7.67 |0.02 |0.01 |1.37 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|256 |10.74 |0.02 |0.02 |7.67 |0.03 |0.03 |1.40 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|512 |10.56 |0.05 |0.04 |7.64 |0.07 |0.06 |1.38 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|1024 |10.57 |0.1 |0.08 |7.67 |0.13 |0.12 |1.38 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|2048 |10.94 |0.19 |0.16 |7.41 |0.28 |0.24 |1.48 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|4096 |10.99 |0.37 |0.33 |7.56 |0.54 |0.47 |1.45 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|8192 |11.17 |0.73 |0.64 |7.62 |1.08 |0.94 |1.47 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|16384 |11.5 |1.43 |1.25 |7.66 |2.14 |1.87 |1.50 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|32768 |13.6 |2.41 |2.11 |8.43 |3.89 |3.4 |1.61 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|65536 |13.65 |4.8 |4.2 |7.82 |8.38 |7.33 |1.75 |allreduce_a100_allpairs\-\-gpus_8\-instances_4.xml |
|131072 |14 |9.36 |8.19 |8.45 |15.51 |13.57 |1.66 |allreduce_a100_allpairs\-\-gpus_8\-instances_4.xml |
|262144 |14.16 |18.51 |16.2 |9.14 |28.67 |25.08 |1.55 |allreduce_a100_allpairs\-\-gpus_8\-instances_4.xml |
|524288 |14.25 |36.8 |32.2 |10.95 |47.87 |41.89 |1.30 |allreduce_a100_allpairs\-\-gpus_8\-instances_4.xml |
|1048576 |17.43 |60.16 |52.64 |14.09 |74.43 |65.13 |1.24 |ndv5_r48ll.xml |
|2097152 |23.52 |89.16 |78.02 |17.14 |122.33 |107.04 |1.37 |ndv5_r48ll.xml |
|4194304 |34.76 |120.68 |105.59 |24.02 |174.65 |152.82 |1.45 |ndv5_r48ll128.xml |
|8388608 |43.75 |191.73 |167.77 |43.79 |191.57 |167.63 |1.00 |allreduce_a100_ring\-\-gpus_8\-channels_8\-instances_4.xml |
|16777216 |64.04 |261.97 |229.23 |64.02 |262.05 |229.29 |1.00 |NCCL |
|33554432 |113.7 |295.04 |258.16 |113.50 |295.5 |258.57 |1.00 |NCCL |
|67108864 |200.7 |334.33 |292.54 |199.30 |336.8 |294.7 |1.01 |NCCL |
|134217728 |378.1 |354.98 |310.61 |381.50 |351.81 |307.83 |0.99 |NCCL |
|268435456 |735.6 |364.93 |319.32 |736.60 |364.41 |318.86 |1.00 |NCCL |
|536870912 |1400.1 |383.46 |335.53 |1414.40 |379.58 |332.13 |0.99 |NCCL |
|1073741824 |2710.1 |396.21 |346.68 |2740.80 |391.76 |342.79 |0.99 |NCCL |
|2147483648 |5362 |400.5 |350.44 |5368.00 |400.05 |350.05 |1.00 |NCCL |


<span id="83S1r5JQ"></span>
### Reduce Scatter

```Bash
#veccl
mpirun --report-bindings --map-by slot --bind-to none --mca btl ^openib --mca pml ob1  --allow-run-as-root -np 8 -x NCCL_DEBUG=INFO -x LD_LIBRARY_PATH=/usr/local/lib/python3.10/dist-packages/veccl/lib /sgl-workspace/nccl-tests/build/reduce_scatter_perf -b 128 -e 2GB -f 2 -g 1 -c 1 -n 10 -w 5
#nccl
mpirun --report-bindings --map-by slot --bind-to none --mca btl ^openib --mca pml ob1  --allow-run-as-root -np 8 -x NCCL_BCCL_ENABLE=0 -x LD_LIBRARY_PATH=/usr/local/lib/python3.10/dist-packages/veccl/lib /sgl-workspace/nccl-tests/build/reduce_scatter_perf -b 128 -e 2GB -f 2 -g 1 -c 1 -n 10 -w 5
```



| |<div style="text-align: center"><br>NCCL 2.23</div><br> |||<div style="text-align: center"><br>veCCL</div><br> |||||
|---|---|---|---|---|---|---|---|---|
|size (B) |time (us) |algbw (GB/s) |busbw (GB/s) |time (us) |algbw (GB/s) |busbw (GB/s) |speedup |algorithm |
|128 |10.99 |0.01 |0.01 |10.62 |0.01 |0.01 |1.03 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|256 |11.04 |0.02 |0.02 |10.67 |0.02 |0.02 |1.03 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|512 |11.34 |0.05 |0.04 |10.70 |0.05 |0.04 |1.06 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|1024 |11.46 |0.09 |0.08 |10.61 |0.1 |0.08 |1.08 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|2048 |12 |0.17 |0.15 |10.60 |0.19 |0.17 |1.13 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|4096 |11.53 |0.36 |0.31 |10.62 |0.39 |0.34 |1.09 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|8192 |11.43 |0.72 |0.63 |10.65 |0.77 |0.67 |1.07 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|16384 |12.03 |1.36 |1.19 |10.77 |1.52 |1.33 |1.12 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|32768 |12.57 |2.61 |2.28 |11.81 |2.78 |2.43 |1.06 |allreduce_1step\-\-gpus_8\-instances_4.xml |
|65536 |12.63 |5.19 |4.54 |12.52 |5.24 |4.58 |1.01 |allreduce_a100_allpairs\-\-gpus_8\-instances_4.xml |
|131072 |12.85 |10.2 |8.92 |12.65 |10.36 |9.06 |1.02 |allreduce_a100_allpairs\-\-gpus_8\-instances_4.xml |
|262144 |13.79 |19.01 |16.64 |13.00 |20.17 |17.65 |1.06 |allreduce_a100_allpairs\-\-gpus_8\-instances_4.xml |
|524288 |13.26 |39.53 |34.59 |15.56 |33.69 |29.48 |0.85 |allreduce_a100_allpairs\-\-gpus_8\-instances_4.xml |
|1048576 |17.36 |60.39 |52.84 |17.61 |59.53 |52.09 |0.99 |ndv5_r48ll.xml |
|2097152 |22.83 |91.85 |80.37 |22.94 |91.41 |79.99 |1.00 |ndv5_r48ll.xml |
|4194304 |39.51 |106.15 |92.88 |39.72 |105.61 |92.41 |0.99 |ndv5_r48ll128.xml |
|8388608 |46.61 |179.96 |157.46 |46.86 |179.01 |156.63 |0.99 |allreduce_a100_ring\-\-gpus_8\-channels_8\-instances_4.xml |
|16777216 |67.5 |248.57 |217.5 |69.09 |242.85 |212.49 |0.98 |NCCL |
|33554432 |112.2 |299.02 |261.64 |113.10 |296.77 |259.67 |0.99 |NCCL |
|67108864 |198.7 |337.67 |295.46 |200.20 |335.16 |293.27 |0.99 |NCCL |
|134217728 |375.9 |357.03 |312.4 |375.20 |357.7 |312.99 |1.00 |NCCL |
|268435456 |717.9 |373.92 |327.18 |715.20 |375.35 |328.43 |1.00 |NCCL |
|536870912 |1388.8 |386.58 |338.25 |1383.10 |388.16 |339.64 |1.00 |NCCL |
|1073741824 |2692.3 |398.82 |348.97 |2689.90 |399.17 |349.28 |1.00 |NCCL |
|2147483648 |5318.2 |403.8 |353.32 |5320.10 |403.66 |353.2 |1.00 |NCCL |


&nbsp;

&nbsp;
