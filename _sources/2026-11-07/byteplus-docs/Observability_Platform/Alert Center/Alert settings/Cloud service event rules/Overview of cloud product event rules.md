---
title: "Overview of cloud product event rules"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Overview_of_cloud_service_event_rules"
---

By monitoring events for relevant cloud products, you can promptly track status changes and exceptions, maintaining the health and stability of business applications. This topic describes how to view events supported by cloud products. You can assess the impact of these events on your business and send notifications based on the severity level to better meet business needs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The data of cloud product events can be retained for 30 days.</div>


<span id="xOgakgAr"></span>
## Supported cloud products

Cloud Monitor supports integration with the following cloud products. When you use a supported cloud product, Cloud Monitor automatically detects basic events.


|Product category |Product name |
|---|---|
|Elastic Computing |* ECS<br><br>* Server Migration Center<br><br>* Auto Scaling |
|Container |* VCI<br><br>* VKE |
|CDN and acceleration |* Edge Networking \- EAG<br><br>* Edge Computing \- Edge Intelligence |
|Storage |EBS |
|Database |* Database Transmission Service<br><br>* Document Database for MongoDB \- replica set<br><br>* Document Database for MongoDB \- sharding cluster<br><br>* RDS for MySQL<br><br>* Cache for Redis<br><br>* RDS for SQL Server |
|Domain names and websites |TrafficRoute \- GTM |
|Network |* Direct Connect<br><br>* VPN<br><br>* EIP |
|Data platform |* E\-MapReduce<br><br>* ByteHouse CDW |
|Security |* Advanced DDoS Protection<br><br>* Advanced DDoS Protection \- Domain |


<span id="rsfLliBF"></span>
## View events

After an event of a cloud product occurs, detailed event data is saved to the Event Center. Different cloud products may generate different events. For the complete list of cloud product events, see [Querying Cloud Monitor events](https://console.byteplus.com/cloud_monitor/docs?tabKey=event&namespace=advanced_ddos_protection).
