---
title: "Building a high-availability primary-secondary cluster using HaVip and Keepalived"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Building-high-availability-primary-and-secondary-clusters-using-HAVIP-and-Keepalived"
---

High\-Availability Virtual IP Addresses (HaVip) are typically used to build high availability primary\-secondary services. This document introduces how to use HaVips to build high availability primary\-secondary clusters.

<span id="C7kIrpK3"></span>
## Application scenarios

You can build high\-availability primary and secondary clusters using HaVip. Specifically, HaVip is simultaneously associated with two Elastic Compute Service (ECS) instances. After the association, the two ECS instances jointly announce the same HaVip through Address Resolution Protocol (ARP), forming a primary\-secondary architecture (one acting as the primary instance and the other as the secondary instance).

Deploy the Keepalived component on both the primary and secondary ECS instances. This component will regularly check the operational status of the ECS instances. When the primary ECS encounters an exception, Keepalived will trigger an automatic switching mechanism: the secondary ECS will take over the primary role and continue providing external services, ensuring business continuity.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cf0481d7e92e53966f0f8ba3f48a1fe1.png) </span>

<span id="IduqtjMa"></span>
## Preparations


* Create Virtual Private Cloud (VPC\-1) and its subnet (Subnet\-1). For actions, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* Create two Elastic Compute Service (ECS) instances, ECS\-A and ECS\-B, in subnet Subnet\-1. In this topic, the Elastic Compute Service (ECS) image CentOS 7.9 is used. You can also replace it as needed with CentOS 7.6 or other CentOS 7 series images. For specific instructions, see [Purchasing Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id="6LFuxpTn"></span>
## Procedures

<span id="OI1mlxfd"></span>
### Step 1: Create HaVip


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **HaVip**.

3. In the top menu bar, select your target region. This topic selects China (Beijing).

4. Click **Create ** **HaVip**.

5. Configure relevant parameters based on the table below.

   
   |**Parameter** |**Description** |**Sample value** |
   |---|---|---|
   |Name |Input the HaVip name. |HAVIP\-01 |
   |VPC |Select the Virtual Private Cloud (VPC) to which the HaVip belongs. |VPC\-01\|192.168.0.0/16 |
   |Subnet |Select the subnet to which the HaVip belongs. This subnet will provide an IP address for the HaVip, and the HaVip can only be associated with an Elastic Compute Service (ECS) instance or a network interface within this subnet. |subnet\-01\|192.168.1.0/24 |
   |Allocation method |Select the IP address allocation method, supporting Custom\-assign and Auto\-assign. |Custom\-assign \| 192.168.1.9 |
   

6. Click Create to complete the action. The IP address of HaVip in this topic is `192.168.1.9`.


<span id="hjTn717I"></span>
### Step 2: Install Keepalived on the ECS


1. [Log in to ECS-A.](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance)

2. Execute the following command to check the version of the Keepalived installation package.

   ```JSON
   yum list keepalived
   ```
   

   The default version of Keepalived on CentOS 7.9 is shown in the figure below.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c7f92f22c32dfb2dd2cc7a3b6a5c74e.png) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The following configurations are based on Keepalived version 1.3.5\-19.e17 as an example.   </div>
   

3. Execute the following command to install Keepalived.

   ```JSON
   yum install -y keepalived
   ```
   

4. Execute the following command to navigate to the keepalived.conf file directory.

   ```JSON
   vim /etc/keepalived/keepalived.conf
   ```
   

5. Press`i`on the keyboard to enter edit mode.

6. Modify the Keepalived configuration file according to the information below.

   ```JSON
   ! Configuration file for keepalived
   
   global_defs {
      notification_email {
        acassen@firewall.loc
        failover@firewall.loc
        sysadmin@firewall.loc
      }
      notification_email_from Alexandre.Cassen@firewall.loc
      smtp_server 192.168.200.1
      smtp_connect_timeout 30
      router_id LVS_DEVEL  
      vrrp_skip_check_adv_addr
      vrrp_garp_interval 0
      vrrp_gna_interval 0
   }
     vrrp_script checkhaproxy
   {
        script "/etc/keepalived/do_sth.sh"   # Add this code segment to check if the business process is running normally. "do_sth.sh" is a custom business process detection script, which you should replace with your actual script when operating.
        interval 5
   }
   
   vrrp_instance VI_1 {
       state MASTER       # Set the initial state of the keepalived node in ECS-A. MASTER indicates the primary state, and BACKUP indicates the standby state. This example sets ECS-A to MASTER.
       interface eth0    # Set the network interface in the ECS bound to the HAVIP, which is used to send VRRP packets. This example uses eth0.
       virtual_router_id 51
       nopreempt  # Add this line of code to set non-preemptive mode, which means that after high-priority ECS instances recover, low-priority ECS instances remain MASTER.
       preempt_delay 10  # Set preemption delay only when state is MASTER, in seconds. Value range is 0-1000
       priority 100   # Set priority. A larger number indicates a higher priority. In this example, the priority of ECS-A is set to100.
       advert_int 1
       authentication {
           auth_type PASS
           auth_pass 1111
       }
       unicast_src_ip 192.168.1.19   # This line configures the private IP address of ECS instance ECS-A; the example uses192.168.1.19; replace it with your actual private IP address when operating.
       unicast_peer {
         192.168.1.20             # This code sets the private IP address of ECS-B. In this example, it is 192.168.1.20, and you should replace it with the actual private IP address during operation.
     }
       virtual_ipaddress {
           192.168.1.9  # Set the IP address of the HAVIP. This example uses192.168.1.9. Replace it with the actual IP address of your HAVIP during operation.   
       }
       notify_master "/etc/keepalived/notify_action.sh MASTER"     # Add this line of code
       notify_backup "/etc/keepalived/notify_action.sh BACKUP"   # Add this line of code
       notify_fault "/etc/keepalived/notify_action.sh FAULT"  # Add this line of code
       notify_stop "/etc/keepalived/notify_action.sh STOP"   # Add this line of code
       garp_master_delay 1    # Add this line of code to set the time to update the ARP cache after switching to the master state.
       garp_master_refresh 5   # Add this line of code to set the interval for the master node to send ARP packets.
       track_interface {
                   eth0               # Add this code segment to set the network interface of ECS-A, which is eth0 in this example.
           }
       track_script {
        checkhaproxy   # Add this code segment
     }
   }   
   ```
   

7. After configuring, press the `Esc` key on the keyboard, then enter `:wq` to save and exit the edit mode.

8. Execute the following command to start Keepalived on ECS\-A, making the configuration in Step 5 take effect.

   ```Plain Text
   systemctl start keepalived
   ```
   

9. Log in to Elastic Compute Service (ECS)\-B, refer to Steps 1–4 to install Keepalived and enter keepalived.conf file's edit mode.

10. Modify the Keepalived configuration file according to the information below.

   ```Plain Text
   ! Configuration File for keepalived
   
   global_defs {
      notification_email {
        acassen@firewall.loc
        failover@firewall.loc
        sysadmin@firewall.loc
      }
      notification_email_from Alexandre.Cassen@firewall.loc
      smtp_server 192.168.200.1
      smtp_connect_timeout 30
      router_id LVS_DEVEL  
      vrrp_skip_check_adv_addr
      vrrp_garp_interval 0
      vrrp_gna_interval 0
   }
     vrrp_script checkhaproxy
   {
        script "/etc/keepalived/do_sth.sh"   # Add this code to check if the business process is running normally. "do_sth.sh" is a custom business process detection script. You should replace it with your actual script when operating.
        interval 5
   }
   
   vrrp_instance VI_1 {
       state BACKUP       # Set the initial status of the keepalived node in ECS-B. This example sets ECS-B as BACKUP.
       interface eth0    # Set the network interface bound to the HAVIP on the cloud server to send VRRP packets. This example uses eth0.
       virtual_router_id 51
       nopreempt
       preempt_delay 10
       priority 50   # Set priority; the larger the number, the higher the priority. In this example, the priority of ECS-B is set to 50.
       advert_int 1
       authentication {
           auth_type PASS
           auth_pass 1111
       }
       unicast_src_ip 192.168.1.20   # Add this line to set the private IP address of ECS-B. This example uses 192.168.1.20; replace it with your actual private IP address when operating.
       unicast_peer {
         192.168.1.19             # Add this code to set the private IP address of ECS-A. This example uses 192.168.1.19; you should replace it with the actual private IP address during operation.
     }
       virtual_ipaddress {
           192.168.1.9  # Set the IP address of the HAVIP. This example uses 192.168.1.9. Replace it with the actual HAVIP IP address during your operation.   
       }
       notify_master "/etc/keepalived/notify_action.sh MASTER"     # Add this line of code
       notify_backup "/etc/keepalived/notify_action.sh BACKUP"   # Add this line of code
       notify_fault "/etc/keepalived/notify_action.sh FAULT"  # Add this line of code
       notify_stop "/etc/keepalived/notify_action.sh STOP"   # Add this line of code
       garp_master_delay 1    # Add this line of code to set the time to update the ARP cache after switching to the root status.
       garp_master_refresh 5   # Add this line of code to set the interval at which the master node sends ARP packets.
       track_interface {
                   eth0               # Add this code segment to set the network interface of ECS-B, which is eth0 in this example.
           }
       track_script {
        checkhaproxy   # Add this code segment
     }
   }   
   ```
   

11. After configuring, press the `Esc` key on the keyboard, then enter `:wq` to save and exit the edit mode.

12. Execute the following command to start Keepalived on ECS\-B, making the configuration in Step 9 take effect.

   ```Plain Text
   systemctl start keepalived
   ```
   


<span id="8d1l7iyY"></span>
### Step 3: Associate HaVip to the ECS


1. Log in to the [High Availability Virtual IP console](https://console.byteplus.com/vpc/haVip).

2. In the top menu bar, select your target region. The region selected here must be consistent with the region of VPC\-01. For this operation, select China (Beijing).

3. Click the name of the HaVip to be associated, HAVIP\-01.

4. Click one of the **Associate now** buttons under the **Instances** in the **Associate resource** section.

5. Click the **ECS** tab and select ECS\-A.

6. Click **Associate** to complete the action.

7. Similarly, click another **Associate now** under the **Instances** in the **Associate resource** section to associate ECS\-B.


<span id="hqPUq1DA"></span>
### Step 4: Associate an EIP to HaVip

If your ECS\-A and ECS\-B need to provide internet services, bind an Elastic IP (EIP) to the HaVip for implementation. If your ECS instances ECS\-A and ECS\-B do not have to provide services for the internet, skip this step.


1. Enter the details page of HaVip. In **Associate resource** section, click **Associate now** under the **EIP** column.

2. Select the EIP to be associated and click **Associate** to complete the action.


If no EIP is available, you can apply for one first. For specific operations, see[ Applying for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).

<span id="TJX6PodS"></span>
### Step 5: Access testing under simulated failure conditions


* Normal scenario: ECS\-A is active to provide related services, ECS\-B is in standby mode and does not provide services, and HaVip is used by ECS\-A.

* Simulate an exception: Simulate an ECS\-A failure by stopping the Keepalived process of ECS\-A, then check in the HaVip console whether the master/standby switchover is completed.

* Expected result: The master/standby switchover is successful. ECS\-B is activated and takes over ECS\-A's services, and HaVip is used by ECS\-B.
