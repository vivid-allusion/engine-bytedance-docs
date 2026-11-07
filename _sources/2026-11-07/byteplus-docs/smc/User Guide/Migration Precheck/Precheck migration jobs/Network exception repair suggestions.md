---
title: "Network exception repair suggestions"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Solutions_to_network_issues"
---

This topic describes solutions to network exceptions detected during pre\-checks on source servers and target instances.

<span id=".5qOA5p-l572R57uc6L-e6YCa"></span>
## Check network access


1. Log in to the source server.

2. Execute the following command to verify whether the source server can access the target instance's EIP.

   ```Plain Text
   ping -w 10 10.249.xxx.xxx
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>10</code> with the desired duration (unit: seconds) of the <code>ping</code> command.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>10.249.xxx.xxx</code> with the actual EIP of the target instance.   </div>
   

   * If the target instance cannot be accessed through the `ping` command (as shown in the figure below), follow the steps below for further troubleshooting.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d5dcf274f48c10817dbbf3c0e066763.png) </span>

      1. Confirm whether the security group associated with the target instance allows inbound ICMP traffic. If inbound ICMP traffic is not allowed, follow the figure below to [add the security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).

      2. Check the network configuration based on the migration task network mode.

         * For the "Internet" mode, check the EIP configurations of the source server and target instance to ensure both can access the public network.

         * For the "Private network" mode, check whether the source server and target instance are in the same CIDR block.

   * If the target instance can be accessed through the `ping` command, continue to check the network port.

3. Use telnet to check port connectivity between the source server and the target instance.

   1. Execute the corresponding command provided below based on the actual environment to install telnet.

      * CentOS / Red Hat Enterprise Linux (RHEL)

         ```Plain Text
         yum install -y telnet
         ```
         

      * Ubuntu / Debian

         ```Plain Text
         apt-get install  -y telnet
         ```
         

   2. Execute the following command to check via telnet whether the source server can access the target instance port required by the migration service.

      ```Plain Text
      telnet 10.249.xxx.xxx 8080
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Replace <code>10.249.xxx.xxx</code> with the actual EIP of the target instance.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Replace <code>8080</code> with the port number required by the migration task.      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Migrate to Linux instance:      </div>
      

            * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For block replication migration: ports <code>22</code> and <code>8080</code>.      </div>
      

            * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For file replication migration: port <code>22</code>.      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Migrate to Windows instance: ports <code>5986</code> and <code>8080</code>.      </div>
      

      * If the port can be accessed, fix other issues and then [perform the pre-check again](https://docs.byteplus.com/en/docs/smc/Perform_a_migration_job_precheck#.6L-b6KGM6L-B56e75Lu75Yqh6aKE5qOA).

      * If the port cannot be accessed, check whether the target instance's security group allows inbound traffic through the corresponding port. If inbound traffic through the corresponding port is not allowed, follow the figure below to [add the security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).

         * Migrate to Linux instance

         * Migrate to Windows instance


<span id=".5qOA5p-l572R57uc5Luj55CG"></span>
## Check network proxy


1. Log in to the source server.

2. Execute the corresponding command provided below to check the source proxy configuration.

   
   <Tabs>
   <Tab zoneid="wRlE6yNGSY" title="Linux operating system">
   <TabTitle>Linux operating system</TabTitle>
   
   &nbsp;
   
   ```Plain Text
   env | grep -E ""http_proxy|https_proxy""
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="qkjROgwLis" title="Windows operating system">
   <TabTitle>Windows operating system</TabTitle>
   
   &nbsp;
   
   ```Plain Text
   set http_proxy
   set https_proxy
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

   * If the returned output is not empty, make sure that the source server and the proxy server, as well as the proxy server and the target instance, can access each other properly.

   * If the returned output is empty, make sure that both the proxy server and the migration tool Agent are correctly configured. [Learn more](https://docs.byteplus.com/en/docs/smc/Management-Migration-Tool-Agent#.6YWN572u5Luj55CG5pyN5Yqh5Zmo5L-h5oGv).


<span id=".5qOA5p-l572R57uc6LSo6YeP"></span>
## Check network quality


1. Log in to the source server.

2. Execute the following command to view the network connection quality between the source server and the target instance.

   ```Plain Text
   ping -w 20 10.249.xxx.xxx
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>20</code> with the desired duration (unit: seconds) of the <code>ping</code> command.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>10.249.xxx.xxx</code> with the actual EIP of the target instance.   </div>
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f8cb7f4a0ce549760ed591e0f58804e3.png) </span>

   Description of important parameters:

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |time |Indicates the time duration (RTT) from sending the ICMP echo request to receiving the ICMP echo reply.<br><br>If the network latency exceeds 100 ms, we recommend improving network quality, for example, by selecting a migration target region geographically closer to the source server to avoid ultra\-long\-distance migration. |2.50 |
   |packet loss |Indicates the packet loss rate. Packet loss rate = Number of lost packets ÷ Number of sent packets × 100 %.<br><br>If the packet loss rate exceeds 0.1 %, we recommend improving network performance, for example, by checking the network connection status or increasing network bandwidth. |0 % |
   |min/avg/max/mdev |The minimum, maximum, and average round\-trip times. Specifically, they indicate the minimum, maximum, and average values of the round\-trip times, respectively, for all successfully received data packets.<br><br>If the RTT jitter (the difference between the minimum and maximum round\-trip times) exceeds 10 ms, we recommend improving network performance, for example, by switching to a higher\-quality line type to reduce network fluctuations. |2.486/2.506/2.554/0.068 ms |
