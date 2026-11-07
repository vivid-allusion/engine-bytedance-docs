---
title: "Proprietary high-performance collective communication library veCCL"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Proprietary_high-performance_collective_communication_library_veCCL"
---

This topic introduces the main features of veCCL and how to use veCCL in the hpcpni3ln instance.

<span id="FPiypCSe"></span>
## Background

<span id="dsJE6jgf"></span>
### veCCL Overview

veCCL is a high\-performance collective communication library independently developed by the cloud platform based on NCCL (Nvidia Collective Communication Library). It supports multiple GPU cards installed on single or multiple nodes and combines the network characteristics of the cloud platform with rich communication optimization experience for large\-scale model tasks to achieve high\-performance communication between multiple GPUs.

veCCL provides a series of highly optimized communication primitives that can significantly enhance communication efficiency in specific topologies or collective operations, enabling parallel computing tasks to synchronize and exchange data efficiently across multiple GPUs. As an enhanced version of NCCL, veCCL is completely transparent to users. By correctly loading the dynamic library, users can utilize veCCL without modifying how the application calls NCCL collective operations. Compared to NCCL's default implementation, veCCL can automatically load and execute algorithms optimized for specific topologies and communication scenarios, significantly reducing communication latency and improving data throughput. In scenarios not supported by veCCL, it intelligently falls back to NCCL's default implementation.

<span id="TAPneYiW"></span>
### Enhanced feature introduction


* High performance: veCCL can provide optimal algorithms based on specific models, specific topology, and specific communication patterns.

* Quick fault location: In distributed cluster collaboration tasks, it can achieve rapid identification and precise definition of fault points.

* Stability: It has the ability to handle simple and relatively complex exceptions, such as providing Softbond capability, which enables automatic switching when a network interface fails, thereby maintaining uninterrupted business stability. 


<span id="xEndqbOY"></span>
## Prepare the environment


* A high\-performance GPU Accelerated instance has been created, and the configuration shown in this article is as follows:

   * Instance type: ecs.hpcpni3ln.45xlarge

   * Image: Ubuntu 22.04 with GPU Driver 535.161.08 and doca

   * GPU driver version: 535.161.08

* Execute `nvcc -V` command to view the CUDA version. If CUDA is not installed, [install CUDA](https://docs.byteplus.com/en/docs/gpu/Installing-CUDA-toolkits).

* Execute the `python3 --version` command to view the Python version. If Python is not installed, [install Python](https://docs.byteplus.com/en/docs/gpu/GPU_-_Building_AIGC_capabilities_Linux#.5q2l6aqk5LqM77ya5a6J6KOFUHl0aG9u5ZKMUElQ).


<span id="VZMvNHXQ"></span>
## Procedure

<span id="E6KGkQRm"></span>
### Step 1: Install veCCL


1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run the following commands to install veCCL.

   ```Bash
   pip install veccl -i https://private.ivolces.com/pypi/simple
   ```
   

3. Run the following commands to verify whether the installation was successful.

   ```C++
   ls `python3 -c "import veccl; print(veccl.ld_library_path())"`
   ```
   

   The output below indicates that the veCCL has been installed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1818ea57bef60b6bda2cab94c6da7855.png) </span>


<span id="gZVZXNge"></span>
### Step 2: Configuration of the veCCL communication environment

This article provides two methods, Shell Script and Python Script, to configure the veCCL communication environment. Mainly ensure before running:


* `LD_PRELOAD` includes the veCCL library.

* `NCCL_NET_PLUGIN=soft-bonding` and `LD_LIBRARY_PATH` include the soft\-bonding path.



<Tabs>
<Tab zoneid="RqCYRX3Jbw" title="Method 1: Shell Script">
<TabTitle>Method 1: Shell Script</TabTitle>

1. Execute the following command to create a shell script file.

   ```Bash
   vim veccl_config.sh
   ```
   

2. Paste the following code into the file.

   ```Bash
   # Preload the veCCL library to ensure veCCL's communication optimization takes effect first.
   export LD_PRELOAD=$(python3 -c "import veccl; print(veccl.lib_paths())"):${LD_PRELOAD}
   # Specify using the Softbond plugin to enhance network reliability.
   export NCCL_NET_PLUGIN=soft-bonding
   export NCCL_IB_TIMEOUT=18
   # Add the dependency path of the veCCL library to the dynamic linker search paths.
   export LD_LIBRARY_PATH=$(python3 -c "import veccl; print(veccl.ld_library_path())"):$LD_LIBRARY_PATH
   export NCCL_DEBUG=INFO
   ```
   

      3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

      4. Execute the following commands in sequence to grant script execution permissions and run the script.

   ```Bash
   chmod +x veccl_config.sh
   ./veccl_config.sh
   ```
   

   You can determine the veCCL enabling status based on the log information in the red box section.

   * `NCCL version 2.23.4-veCCL-x.x.x+cuda12.2` indicates that veCCL has been successfully enabled.

   * `NET/IB : Soft-bonding Using` indicates that Softbond has been successfully enabled.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7619f5147d6cc2cae53d0fcd609b589e.png) </span>


</Tab>
<Tab zoneid="JIjC6qsnIW" title="Method 2: Python Script">
<TabTitle>Method 2: Python Script</TabTitle>

1. Run the following commands to create a Python script file.

   ```Bash
   vim veccl_config.py
   ```
   

2. Paste the following code into the file.

   ```Bash
   import veccl
   import os
   import subprocess
   # Set critical environment variables and enable veCCL HPC-optimized communication optimization.
   veccl.enable() # Configure LD_PRELOAD, NCCL_NET_PLUGIN, and LD_LIBRARY_PATH.
   os.environ['NCCL_DEBUG'] = 'INFO'
   os.environ['NCCL_IB_TIMEOUT'] = '18'
   ```
   

      3. Run the following commands to grant the script executable permissions and run the script.

   ```Bash
   chmod +x veccl_config.py
   python3 veccl_config.py
   ```
   

   After the script runs successfully, the status of veccl.enable() settings will output as follows, indicating that the key environment variable configuration succeeded.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_29a1df27f2da895142b793f175025529.png) </span>


</Tab>
</Tabs>


<span id="JezYh9Gh"></span>
### Step 3: Verification of veCCL performance

The following example provides a script, test.py, to demonstrate the acceleration effect on an 8\-card single\-machine instance using the PyTorch distributed training framework with the allreduce communication algorithm.


1. Run the following command to view the PyTorch version. If not installed, please [install Pytorch](https://docs.byteplus.com/en/docs/gpu/GPU_-_Deploying_PyTorch_applications#.5q2l6aqk5LiJ77ya5a6J6KOFUHl0b3JjaA==).

   ```Bash
   python3 -c "import torch; print(torch.__version__)"
   ```
   

2. Run the following command to create a test script file.

   ```Bash
   vim test.py
   ```
   

3. Paste the following code into the file.

   ```Python
   import os
   import torch
   import torch.distributed as dist
   
   def main():
       # Resolve environment variables.
       rank = int(os.environ["RANK"])
       local_rank = int(os.environ["LOCAL_RANK"])
       world_size = int(os.environ["WORLD_SIZE"])
       # Initialize the device and communication.
       torch.cuda.set_device(local_rank)
       dist.init_process_group(backend="nccl")
       # Generate random tensors on each GPU and perform all_reduce operations.
       tensor = torch.randn(1024, device=f"cuda:{local_rank}")
       print(f"Rank {rank}: before allreduce tensor sum = {tensor.sum().item()}")
       dist.all_reduce(tensor, op=dist.ReduceOp.SUM)
       # Verify the results of all_reduce operations and release resources.
       print(f"Rank {rank}: after allreduce tensor sum = {tensor.sum().item()}")
       dist.destroy_process_group()
   
   if __name__ == "__main__":
       main()
   ```
   

      4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

      5. Grant executable permission to the script.

   ```Bash
   chmod +x test.py
   ```
   

      6. Run the following script to execute test.py.

         * Shell:

      ```Bash
      NCCL_DEBUG=INFO torchrun --nproc_per_node=8 test.py
      ```
      

   * Python:

      1. Execute the `python3` command to enter the Python interactive mode.

      2. After displaying the `>>>` prompt, input `import subprocess`, which is used to execute external commands.

      3. Continue executing the following commands.

         ```Bash
         # Execute the test.py script to start a single-machine eight-GPU distributed training task.
         torchrun_command = ["torchrun","--nproc_per_node=8","test.py"] # Note: If a message is displayed indicating that torchrun cannot be found, enter the absolute path.
         try:
             subprocess.run(torchrun_command, check=True) # Note: Modifications to LD_PRELOAD only take effect for child processes. Therefore, subprocess.run is required.
         # Capture and print information about torchrun command execution failure.
         except subprocess.CalledProcessError as e:
             print(f"torchrun failed with error: {e}")
         ```
         

7. View the allreduce computation results based on the veCCL communication library.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_22ac919ed377b572f0de63ac62bc1150.png) </span>


<span id="KjRxmODZ"></span>
## Explanation of key environment variables.


|**Environment variable** |**The description.**  |
|---|---|
|NCCL_SOCKET_IFNAME |NCCL requires selecting the network interface used for socket communication during initialization. Network interfaces may vary across instances of different specifications. Not configuring or misconfiguring may cause NCCL to fail to establish a connection. The instance demonstrated in this document uses the eth0 network interface. |
|NCCL_IB_GID_INDEX |This variable is valid during multi\-machine operation.<br><br>Set the GID used by RDMA; misconfiguration or absence may cause NCCL to report an error during operation. |
|NCCL_IB_TIMEOUT |This variable is valid in multi\-machine operations.<br><br>The recommended value is 18 when using Softbond, and 23 when not using Softbond.<br><br>This environment variable determines the RDMA data transmission timeout period. Setting it to 18 means that approximately 1.07 seconds after data transmission, it triggers RDMA network interface retransmission due to packet loss; when Softbond is enabled, this variable also determines the threshold for judging a link as unavailable to reroute. |
|NCCL_NET_PLUGIN |It is recommended to configure as soft\-bonding to enable the Softbond stability enhancement capability of veCCL.<br><br>If you do not want to use Softbond, it is recommended to set it to none to prevent accidental loading of other unintended plugins. |
|NCCL_DEBUG |It is common to set the log level to INFO, enabling more NCCL\-related log outputs, which are helpful for troubleshooting when issues arise. INFO\-level logs are only printed during initialization if no other log settings are configured, without affecting communication performance. |
