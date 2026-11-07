---
title: "Flow log use cases"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Use-cases"
---

This topic introduces the usage example of flow logs.

## Cloud public network

**View traffic between ECS instances and the Internet via EIP**

You can use flow logs to view traffic between ECS instances and the Internet, as shown in the figure below:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_391e032d039a1bee6af29727eac7702d.png)

Procedures:

1. With reference to the figure above, create a Network Interface\-type flow log and configure an index.

2. Using ECS to access the public address `14.XX.XX.40` as an example, input the following SQL search and analysis statements.

   ```SQL
   srcaddr:"192.168.1.22" and dstaddr: "14.XX.XX.40" | SELECT DATE_FORMAT(t, '%H:%i:%S') AS time, dstaddr, SUM((bytes * 8) / (`end` - start)) AS bandwidth FROM (SELECT `end`, start, dstaddr, bytes, (__time__ - (__time__ % 3600)) AS t limit 1000) GROUP BY time, dstaddr ORDER BY time ASC limit 1000
   ```

   > When inputting the analysis statement, please replace the source IP address (ECS address) `192.168.1.22` and the destination IP address (public address) `14.XX.XX.40 `with the actual IP addresses.

3. View the analysis results.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_04d3df37c25745cbff7cb4b261f5403f.png)

   As shown in the figure above, over the past 15 minutes, the traffic from ECS (192.168.1.22) accessing the EIP address (14.XX.XX.40) has shown a wave\-like fluctuation.

**View ECS instances with high traffic through the Public NAT Gateway**

You can use flow logs to identify high\-traffic ECS instances behind a Public NAT Gateway, as shown in the figure below:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d3171dd09be41c1e1942057b0c6fad14.png)

Procedures:

1. With reference to the figure above, create a subnet\-type flow log and configure an index.

2. To view the data transfer for ECS accessing the public IP address` 101.XX.XX.146`, enter the following SQL query and analysis statement.

   ```SQL
   dstaddr: "101.XX.XX.146" and action: ACCEPT  | select DATE_FORMAT(t, '%H:%i:%S') AS time,srcaddr,SUM((bytes * 8) / (`end` - start)) AS bandwidth FROM (SELECT `end`, start, srcaddr, bytes, (__time__ - (__time__ % 3600)) AS t limit 1000) GROUP BY time, srcaddr ORDER BY time ASC limit 1000
   ```

   > When inputting the analysis statement, replace the destination IP address `101.XX.XX.146` with the actual IP address.

3. View the analysis results.

    ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_32def5d35da7c3ecef91d1f6b3fe358b.png)

   As shown in the figure above, over the past 15 minutes, ECS\-A (192.168.1.11) and ECS\-B (192.168.1.22) have been the high\-traffic ECS instances behind the Public NAT Gateway.

**View traffic accessing ECSs through a CLB via the Internet**

You can use flow logs to view traffic accessing ECSs through a CLB (Classic Load Balancer) from the Internet, as shown in the figure below:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c946ceeae05aa4a1f668d298b9c628c8.png)

Procedures:

1. With reference to the figure above, create a VPC\-type flow log and configure an index.

2. To analyze the number of requests received by backend servers as an example, enter the following SQL query and analysis statement.

   ```SQL
   dstport:80  | SELECT COUNT(*) as PV,dstaddr WHERE dstaddr LIKE '192.168.%' GROUP BY dstaddr
   ```

   > When inputting the analysis statement, please replace the target port 80 with the actual target port and modify the fuzzy match of the `192.168.%` field based on the actual VPC address segment.

3. View the analysis results.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f37fb020d7dc9f52a566fda51a96faa4.png)

   As shown in the figure above, you can see the number of requests served by different backend servers of the CLB, as well as the percentage of total requests handled by each backend server.

## Virtual Private Cloud

**View traffic between ECSs within the same VPC**

You can use flow logs to view traffic between ECSs within the same VPC, as shown in the figure below:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_df9fc6ad0c1079af11b28585812958f7.png)

Procedures:

1. With reference to the figure above, create a Network Interface\-type flow log and configure an index.

2. To view the traffic from ECS\-A accessing ECS\-B, enter the following SQL query and analysis statement.

   ```SQL
   srcaddr:"192.168.1.11" and dstaddr: "192.168.1.22" | SELECT DATE_FORMAT(t, '%H:%i:%S') AS time, dstaddr, SUM((bytes * 8) / (`end` - start)) AS bandwidth FROM (SELECT `end`, start, dstaddr, bytes, (__time__ - (__time__ % 3600)) AS t limit 1000) GROUP BY time, dstaddr ORDER BY time ASC limit 1000
   ```

   > When inputting the analysis statement, please replace the source IP address (ECS\-A's address) `192.168.1.11` and the destination IP address (ECS\-B's address) `192.168.1.22` with the actual IP address.

3. View the analysis results.

   As shown in the figure above, over the past 10 minutes, the traffic from ECS\-A (192.168.1.11) to ECS\-B (192.168.1.22) has shown a step\-like increase.

**View traffic between different VPCs**

You can use flow logs to view traffic between Virtual Private Clouds (VPCs), as shown in the figure below:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b11ca0f5ff06c9f5b343dfdc7875549.png)

Procedures:

1. With reference to the figure above, create a VPC\-type flow log and configure an index.

2. To view the traffic from VPC\-B (192.168.1.0/16) accessing VPC\-A (172.16.1.0/16) as an example, enter the following SQL query and analysis statement.

   ```SQL
   srcaddr:192.168.1.* and dstaddr: 172.16.1.* | SELECT DATE_FORMAT(t, '%H:%i:%S') AS time, dstaddr, SUM((bytes * 8) / (`end` - start)) AS bandwidth FROM (SELECT `end`, start, dstaddr, bytes, (__time__ - (__time__ % 3600)) AS t limit 1000) GROUP BY time, dstaddr ORDER BY time ASC limit 1000
   ```

   > When entering the analysis query, please replace the source IP address segment (VPC\-B's CIDR block) `192.168.1.*` and the destination IP address segment (VPC\-A's CIDR block) `172.16.1.*` with the actual IP address ranges.

3. View the analysis results.

   As shown in the figure above, over the past 20 minutes, three ECSs in VPC\-A (with IP addresses `172.16.1.2`, `172.16.1.11`, and `172.16.1.3`) were accessed by servers within VPC\-B. Among them, the server with IP address `172.16.1.3` exhibited highly stable traffic.

**View traffic through PrivateLink connection endpoints**

You can use flow logs to view traffic accessing resources via PrivateLink connection endpoints, as shown in the figure below:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4560334bcf0276375d36e106d6a2c5b4.png)

Procedures:

1. Create a VPC\-type flow log for VPC\-A and configure an index.

2. Enter the following SQL query and analysis statement.

   ```SQL
   dstport:80 and dstaddr: 172.16.1.3 | SELECT    COUNT(*) as PV,srcaddr  WHERE srcaddr LIKE '172.16.%'  GROUP BY srcaddr
   ```

   > When inputting the analysis statement, please replace the target port80 and destination IP address `172.16.1.3` with the actual endpoint port and IP address, and modify the fuzzy match `172.16.%` field according to the actual VPC address segment.

3. View the analysis results.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b07810aa5e09c75b6ce89f60c9e5006.png)

   As shown in the figure above, you can view the number of requests from ECSs in VPC\-A to the PrivateLink connection endpoint, as well as the percentage of total requests contributed by each ECS.

   > **tip**

   > Similarly, you can create flow logs for the VPC where the endpoint service is deployed to monitor its traffic.

## Hybrid cloud

You can use flow logs to view the traffic between your on\-cloud Virtual Private Cloud (VPC) and your on\-premises IDC, as shown in the figure below:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f44c684de044e800e79e69e1b8625fbc.png)

Procedures:

1. With reference to the figure above, create VPC\-type flow logs for both VPC\-A and VPC\-B, and **have both flow logs share the same log topic**. Simultaneously, configure an index for the log topic.

2. To view the traffic proportion of VPC\-A and VPC\-B accessing the on\-premises IDC as an example, enter the following SQL query and analysis statement:

   ```sql
   action: ACCEPT  |SELECT COALESCE(vpc_A_traffic.minute, vpc_B_traffic.minute) AS minute,
           COALESCE(vpc_A_traffic.total_vpc_A_traffic, 0) * 100 / NULLIF(COALESCE(vpc_A_traffic.total_vpc_A_traffic, 0) + COALESCE(vpc_B_traffic.total_vpc_B_traffic, 0), 0) AS vpc_A_percentage, 
           COALESCE(vpc_B_traffic.total_vpc_B_traffic, 0) * 100 / NULLIF(COALESCE(vpc_A_traffic.total_vpc_A_traffic, 0) + COALESCE(vpc_B_traffic.total_vpc_B_traffic, 0), 0) AS vpc_B_percentage
   FROM (
           SELECT date_trunc('minute', __time__) AS minute,
     SUM (bytes * 8 / CASE
       WHEN "end" - start = 0 THEN 1
       ELSE "end" - start
       END) AS total_vpc_A_traffic
     WHERE srcaddr LIKE '192.168.%'
           GROUP BY date_trunc('minute', __time__)) as vpc_A_traffic
   FULL JOIN (
           SELECT date_trunc('minute', __time__) AS minute,
           SUM (bytes * 8 / CASE
       WHEN "end" - start = 0 THEN 1
       ELSE "end" - start
       END) AS total_vpc_B_traffic
                   WHERE srcaddr LIKE '172.16.%'
                   GROUP BY date_trunc('minute', __time__)) as vpc_B_traffic
   ON vpc_A_traffic.minute = vpc_B_traffic.minute
   ORDER BY minute
   ```

   > When entering the analysis query, please modify the wildcard patterns `'192.168.%'` and `'172.16.%'` according to the actual CIDR blocks of your VPCs.

3. View the analysis results.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c59fd9b098b6a67fa1b6209c4f54fab.png)

   As shown in the figure above, the traffic proportion of VPC\-A and VPC\-B accessing the on\-premises IDC over the past 30 minutes is displayed.

## Rejected traffic

You can use flow logs to view traffic rejected by security groups and network ACLs, as shown in the figure below:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1043320dad83a043bf743944201c1ee5.png)

Procedures:

1. With reference to the figure above, create a Network Interface\-type flow log and configure an index.

2. Taking the traffic rejected by ECS\-B as an example, enter the following SQL query and analysis statement.

   ```sql
   dstaddr: 172.16.1.4 and action: "REJECT"   | SELECT  dstaddr,srcaddr, action ORDER BY dstaddr
   ```

   > When entering the analysis query, replace the destination IP address `172.16.1.4` with the actual IP address.

3. View the analysis results.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_692b7ff637852701ddcc4c2b5184ce63.png)

   As shown in the figure above, you can view detailed information about the traffic rejected by ECS\-B (172.16.1.4).
