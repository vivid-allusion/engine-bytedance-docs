---
title: "HPC - Configuring NCCL"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/HPC_-_Configuring_NCCL"
---

This topic describes how to manually configure NCCL for HPC\-optimized instances, aiming to prevent RDMA network disconnections that could disrupt normal service operations.

<span id=".TkNDTOeugOS7iw=="></span>
## NCCL overview

Nvidia Collective Communication Library (NCCL) is a collective communication library developed by NVIDIA. It enables fast communication between multiple GPUs either within a single instance or across multiple instances.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

**CentOS 7.8/veLinux 1.0/Ubuntu 16.04**


1. Log in to the ECS instance. For more information, see [Logging in to Linux instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Modify the timeout period and retry count for your business.

   1. Execute the `vim /etc/profile` command to open the /etc/profile file.

      > You can also execute the `vim /etc/environment`, `vim ~/.bash_profile`, or `vim ~/.bashrc` command to open the corresponding configuration file for the following settings. We recommend that you prioritize the /etc/profile file.      
      

   2. Press `i` to enter edit mode.

   3. Add the following NCCL parameters to the end of the /etc/profile file.

      ```Plain Text
      export NCCL_IB_TIMEOUT=23
      export NCCL_IB_RETRY_CNT=7        
      ```
      

   4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

   5. Execute the `source /etc/profile` command to apply the configuration update.


**Ubuntu 20.04**

If you want to create an HPC\-optimized instance using Ubuntu 20.04, in addition to the preceding operations, you need to perform the following extra operations:


1. Run the following script to initialize the rdma\-agent service.

   ```Plain Text
   #!/bin/bash
   wget http://rdma-config-beijing.tos-cn-beijing.ivolces.com/rdma-agent_1.0.2-0_all.deb
   dpkg -r rdma-agent
   dpkg -i rdma-agent_1.0.2-0_all.deb
   rm -f rdma-agent_1.0.2-0_all.deb
   cat > /etc/networkd-dispatcher/routable.d/50-ifup-hooks << EOF
   #!/bin/bash
   systemctl restart rdma-agent
   EOF
   chmod +x /etc/networkd-dispatcher/routable.d/50-ifup-hooks
   systemctl daemon-reload
   systemctl enable rdma-agent.service
   systemctl restart rdma-agent.service
   ```
   

2. Configure the Ubuntu image for static IP addresses by using the provided script and restart the service to apply the changes.

   ```Bash
   #!/bin/bash
   ln -s /dev/null /etc/systemd/network/10-netplan-eth1.network
   ln -s /dev/null /etc/systemd/network/10-netplan-eth2.network
   ln -s /dev/null /etc/systemd/network/10-netplan-eth3.network
   ln -s /dev/null /etc/systemd/network/10-netplan-eth4.network
   
   systemctl restart systemd-networkd
   ```
   

3. Add the network interface initialization dhclient configuration to the /etc/rc.local file.

   1. Execute the following command to open the /etc/rc.local file.

      `vim /etc/rc.local`

   2. Press `i` to enter edit mode.

   3. Add the following parameters to the configuration file.

      ```Plain Text
      dhclient eth1
      dhclient eth2
      dhclient eth3
      dhclient eth4
      ```
      

   4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

4. Execute the `chmod 755 /etc/rc.local` command to grant execution permission to /etc/rc.local.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result verification

Execute the `env | grep -i nccl` command. If the output contains the following information, the configuration is successful.

```Plain Text
NCCL_IB_TIMEOUT=23 
NCCL_IB_RETRY_CNT=7
```
