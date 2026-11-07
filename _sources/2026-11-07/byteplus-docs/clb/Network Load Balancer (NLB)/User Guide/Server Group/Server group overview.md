---
title: "Server group overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Server-Group-Overview"
---

<span id=".566A5LuL"></span>
## Introduction​

A server group is a collection of backend servers.

In addition to adding backend servers to the group, you need to configure a scheduling algorithm and health checks for the server group.


* Scheduling algorithm: Distributes access requests reasonably among backend servers to prevent any single server from being overloaded while others remain idle. [Prerequisite](https://docs.byteplus.com/en/docs/clb/Server-Group-Overview#YF78LR8p)

* Health check: Determines whether backend servers are functioning normally, preventing requests from being forwarded to abnormal servers and ensuring service availability. [Prerequisite](https://docs.byteplus.com/en/docs/clb/NLB-Health-check-overview)


<span id="bm0wQXLI"></span>
## Classification


|Topic |Explanation |Application scenario |
|---|---|---|
|Server type |Support adding the following resources as backend servers:<br><br><br>* ECS in the VPC where the NLB resides.<br><br>* The secondary network interface mounted to the ECS in the VPC where the NLB resides.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the NLB instance enables client address is maintained in a public network client access scenario, binding an EIP to a server\-type backend server causes traffic for that IP address to be unreachable.</div><br> |* Backend servers reside in the same VPC as NLB<br><br>* The client IP address is transparent |
|IP type |Supports IPv4 addresses as backend servers as long as the network is reachable. e.g.<br><br><br>* The IP address of the VPC where NLB resides.<br><br>* IPv4 address of other VPCs.<br><br>* IPv4 address of the server in the data center. |* Backend servers reside in different VPC as NLB<br><br>* No need to pass through client IP address |


<span id="UIHQWXJJ"></span>
## Protocol and port


* Backend server protocol type

   
   |Topic |Explanation |Limits |
   |---|---|---|
   |TCP |NLB forwards the access requests to the backend server through TCP protocol. |Only support attaching TCP and TLS listeners |
   |UDP |NLB forwards the access requests to the backend server through UDP protocol. |Only support attaching UDP listeners |
   

* Backend server port

   The port where the backend server provides services, receiving and processing requests from the listener.

   Requests from the same listening port can be forwarded to different backend servers, which may receive requests on different ports.


<span id="YF78LR8p"></span>
## Scheduling algorithm

NLB supports configuring the scheduling algorithm by taking server group as the dimension. When Creating a server group, the scheduling algorithm can be selected from Weighted Round Robin (WRR), Weighted Least Connections (WLC), and Source Address Hashing (SH). Description of scheduling algorithm:


|Scheduling algorithm |Explanation |Application scenario |
|---|---|---|
|Weighted Round Robin (WRR) |This algorithm distributes access requests from users to different backend servers in sequence based on the weight of each backend server. The better the performance of a server, the higher the weight. Backend servers with higher weights receive polling more frequently (higher probability). |Applicable to short connection services. This algorithm is recommended when each request consumes roughly the same processing time on the backend server, handles the same or similar request types, and request times vary little. |
|Weighted Least Connections (WLC) |First calculate the value of current connections/weight on the backend server, then distribute the requests to the backend server with the smallest value. This algorithm requires tracking the current connection count of each server. When a request is assigned to a backend server, its connection count increases by one; when the request connection terminates, times out, or completes, the connection count decreases by one. |WLC is applicable to persistent connection services, such as FTP. This algorithm is recommended when handling different requests with significantly varying processing times. |
|Source IP Hash (SH) |Based on source IP address consistency hashing, requests from the same source address are mapped to the same backend server via a hash table. When removing or adding a backend server, it minimizes changes to the mapping between existing service requests and processing servers as much as possible. |Applicable to protocols without cookie functionality. Use this algorithm when requests from the same user need to be forwarded to the same backend server. |


&nbsp;

&nbsp;

&nbsp;

&nbsp;

<span id=".5YGl5bq35qOA5p-l5Y6f55CG"></span>
##
