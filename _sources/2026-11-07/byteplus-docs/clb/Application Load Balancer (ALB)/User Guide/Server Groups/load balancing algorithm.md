---
title: "load balancing algorithm"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Load-balancing-algorithms"
---

The routing algorithm at the server group level is also called the load balancing algorithm. The load balancing algorithm determines how client requests distribute among backend servers.

<span id="e4944088"></span>
### Weighted Round Robin

**Implementation principle:** 

The Weighted Round Robin (WRR) algorithm generates a fixed request distribution sequence based on preset weight values. Within one polling cycle, servers with higher weights receive more requests. The WRR algorithm only considers server weights and does not consider load.

**Example:** 

Assuming server A has a weight of 100, server B has a weight of 50, and server C has a weight of 50.

In this situation:


* The proportion of requests received by server A, server B, and server C is 2:1:1.

* Within one polling cycle, the request distribution sequence is: A→A→B→C (repeats cyclically).


**Advantages**:


* Users can assign different weights to servers based on their performance and processing capacity. This allows servers with stronger performance and capacity to handle more requests, making full use of server resources.

* Request distribution is predictable, facilitating server capacity planning.


**Disadvantages:** 

The WRR algorithm cannot detect servers' real\-time load status. When processing times of individual requests vary greatly, it can easily cause load imbalance among servers. e.g., if a server receives requests with long processing times, it may get new requests before completing the current ones, leading to accumulated load.

**Applicable scenarios:** 

This algorithm applies when server performance and processing capacity vary, but the processing time per request is basically the same. Commonly used for short connection services, such as HTTP services. These services have relatively short and consistent request processing times.

<span id="0b7b885f"></span>
### Weighted least connections

**Mechanism:** 

The weighted least connections (WLC) algorithm dynamically calculates the load metric for each server and routes new requests to the server with the lowest load metric. The load metric of a server is calculated as: load metric = current connections / server weight. The WLC algorithm considers both server load and weight.

**Example:** 

Assuming:


* Server A: weight 100, current connections 1000

* Server B: weight 50, current connections 500

* Server C: weight 50, current connections 200


Load metric calculation:


* Server A: 1000 / 100 = 10

* Server B: 500 / 50 = 10

* Server C: 200 / 50 = 4


Server C has the lowest load metric. Therefore, new requests will be distributed to server C.

**Advantages**:

The WLC algorithm can dynamically adjust request distribution based on the current number of connections and weight of servers, avoiding server overload or idleness.

**Disadvantages:** 


* The algorithm has high complexity. The system needs to monitor the number of connections on each server in real time and dynamically adjust request distribution based on connections and weight. This may increase system overhead, especially in large\-scale deployments or high\-concurrency scenarios.

* When the number of connections is large, if a new server joins, many new connections will be scheduled to the new server, which may cause sudden traffic spikes and affect business stability.


**Applicable scenarios:** 

This algorithm suits scenarios where individual request processing times vary significantly and server performance and capacity differ. Commonly used for long connection services. These services have longer request processing times and require considering the server's real\-time load to maintain load balancing.

<span id="02c00a9f"></span>
### Source IP hash

**Implementation principle:** 

The Source IP hash (SH) is a load balancing algorithm based on the source IP address. This algorithm hashes the client IP address to generate a hash value, then maps this hash value to a specific server within the server group. The SH algorithm routes requests from the same source IP address to the same server, achieving session persistence. The SH algorithm does not consider the server's weight or load.

**Example:** 

Assume the servers handling client requests are Server A and Server B. Requests from clients with IP address 192.168.1.1 are forwarded to server A after hash calculation. When this client initiates a new request, the hash result remains the same because the IP address does not change. Therefore, the request will still be forwarded to server A.

**Advantages**:

The SH algorithm always routes requests from the same source IP address to the same server, achieving session persistence. This is especially important for applications that require maintaining user state, as the algorithm ensures all consecutive requests from a user are handled by the same server, avoiding state inconsistencies.

**Disadvantages:** 

When the number of servers changes, the hash result also changes. Requests originally assigned to a certain server will be redistributed to other servers, potentially causing data inconsistency issues.

**Applicable scenarios:** 

This algorithm applies to scenarios requiring session persistence, such as shopping cart systems and user log in authentication systems.
