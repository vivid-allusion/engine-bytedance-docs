---
title: "Product specifications"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Product-Overview-02"
---

<span id="gbRrRKl1"></span>
## Product specifications


* The maximum number of connections: Refers to the maximum number of concurrent connections that a Classic Load Balancer (CLB) instance can handle. When the connections on the instance exceed the max connections defined by the specification, new connection requests will be dropped.

* New connection rate (CPS): Refers to the rate of new connections per second that a CLB instance can handle. When the rate of new connections per second exceeds the defined CPS specification, new connection requests will be dropped.

* **Queries Per Second (QPS)** : QPS is a metric specific to Layer\-7 listeners, representing the number of HTTP/HTTPS queries (requests) completed per second. New connection requests will be dropped when the query rate exceeds the defined QPS specification.

* Bandwidth (Mbps): Refers to the maximum traffic rate supported by the Classic Load Balancer (CLB) instance when processing network traffic.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">CLB adopts a distributed high availability deployment architecture. When the number of clients is too small, the bandwidth and QPS limits of the instance type cannot be reached.</div>



|**Specification** |**Max Connections** |**CPS** |**QPS** |**Bandwidth (Mbps)**  |
|---|---|---|---|---|
|Small I |10000 |2000 |2000 |200 |
|Small II |50000 |5000 |5000 |500 |
|medium_1: Medium I |100000 |10000 |10000 |1000 |
|medium_2: Medium II |200000 |20000 |20000 |2000 |
|Large I |500000 |50000 |50000 |5000 |
|large_2: Large II |1000000 |100000 |100000 |10000 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When the actual traffic exceeds the bandwidth defined in the CLB specification, it may affect normal business operations. Therefore, carefully evaluate the business traffic and choose an appropriate specification.</div>


* <div data-tips="true" data-tips-type="tip">If the specifications in the above table do not meet your needs, please contact your account manager to apply for a larger specification.</div>


* <div data-tips="true" data-tips-type="tip">For fee descriptions of different specifications, see the <a href="https://docs.byteplus.com/en/docs/clb/Billing-methods">billing method</a> for spec config fee.</div>



<span id="S6qwvCSA"></span>
## 

&nbsp;

&nbsp;

&nbsp;
