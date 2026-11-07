---
title: "What if the network environment is unstable during data transmission over express networks?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/What_if_the_network_environment_is_unstable_during_data_transmission_over_express_"
---

During data transmission over an express network, network instability may cause the task to fail.

<span id=".5Y-v6IO95Y6f5Zug"></span>
## Possible causes

If the kernel parameters `net.ipv4.tcp_tw_recycle` and `net.ipv4.tcp_timestamps` of the remote server are both set to `1`, the remote server checks the timestamp in each message. If the timestamp is not incremental, the remote server does not respond to the message. If NAT is also configured on the remote server, the source IP addresses of the messages received by the remote server from different clients are the same, but the time of each client before NAT may be different, which causes the timestamp in the message to be non\-incremental, resulting in an unstable network environment.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions


1. Check that the `net.ipv4.tcp_tw_recycle` and `net.ipv4.tcp_timestamps` parameters have a value of `1`.

   1. Execute the following command on the client side to see the value of the `net.ipv4.tcp_tw_recycle` parameter:

      ```sql
      cat /proc/sys/net/ipv4/tcp_tw_recycle
      ```
      

   2. Execute the following command on the client side to see the value of the `net.ipv4.tcp_timestamps` parameter:

      ```sql
      cat /proc/sys/net/ipv4/tcp_timestamps
      ```
      

   If the value of the `net.ipv4.tcp_tw_recycle` or `net.ipv4.tcp_timestamps` parameter is `1`, the network of the transmission task may be unstable in the NAT environment.

2. Modify the values of the `net.ipv4.tcp_tw_recycle` and `net.ipv4.tcp_timestamps` parameters.

   1. Execute the following command to enter the configuration file:

      ```sql
      vi /etc/sysctl.conf
      ```
      

   2. Copy the following to the configuration file:

      ```sql
      net.ipv4.tcp_tw_recycle=0 
      net.ipv4.tcp_timestamps=0
      ```
      

   3. Press **ECS** to exit edit mode.

   4. Type` : wq` and then press **Enter** to save the changes and exit the vi editor.

   5. Execute the following command to apply the changes:

      ```sql
      sysctl -p
      ```
