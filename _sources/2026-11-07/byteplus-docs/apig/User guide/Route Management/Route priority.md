---
title: "Route priority"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Priority_of_route"
---

The API Gateway processes incoming requests according to the priority of previously configured route rules arranged one by one. The matching process is carried out from custom Priority rules to high Priority rules and then to low Priority rules sequentially.

<span id=".6Lev55Sx5Yy56YWN5LyY5YWI57qn"></span>
## Route Matching Priority

When multiple route rules exist, they are sorted from high to low priority in the order of **custom priority** \> **Path** \> **Header \> Query** \> **creation time**, with detailed rules as follows:


1. Based on **custom Priority**: the range of values is 0 to 100, with smaller numbers indicating higher priority, default is 100.

2. Based on **Path matching rule(s)** :

   1. When **matching rule(s)**  differ: **equal to** \> **prefix** \> **regular expression matching**.

   2. When **matching rule(s)**  are the same: a longer **path** string indicates higher priority.

3. Based on the total number of key\-value pairs in the **Header**: the greater the total number, the higher the priority.

4. Decide based on the key\-value pairs of **request parameters (Query)** : the higher the total number, the higher the Priority.

5. Decide based on the **creation time**: the earlier the creation time, the higher the priority.


<span id=".6IOM5pmv6K-05piO"></span>
## Background description

The API Gateway provides two Priority configuration methods, gateways created before June 14, 2024, will by default use v1 version matching logic, and those created after June 14, 2024, will by default use v2 version matching logic. The matching logic of both versions' Priority is as follows:


|Version |Priority logic |Advantages |**Disadvantages** |
|---|---|---|---|
|v1 |Determine the priority based on the creation time of the route. The earlier the creation time, the higher the priority. |The logic is simple and easy to learn. |The route's precision is low. |
|v2 |Priority is judged based on the accuracy of the route. The higher the accuracy, the higher the priority. |High routing accuracy. |The logic is complex and has a certain understanding cost. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* To switch from v1 version to v2 version, you need to [Submit  a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000170) to upgrade the gateway.

* Both v1 and v2 versions can turn on the custom Priority feature.

* Activation and custom Priority are opt\-in features; if you want to use them, please [Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000170).


<span id=".5Zy65pmv6K-05piO"></span>
## Scenario description

When a request can match multiple rules, it is necessary to define the priority of these rules to prevent the request from matching only by the highest precision.


|Request scenario |Routing configuration |Matching rule(s). |
|---|---|---|
|Scene 1<br><br>/abcd |* route1<br><br>   * Path: prefix /abcd<br><br>   * Creation time: 2024\-06\-13 00:00:00<br><br>* route2:<br><br>   * Path: equal to /abcd<br><br>   * Creation time: 2024\-06\-13 00:00:02<br><br>* route3:<br><br>   * Path: prefix /abcd<br><br>   * Header: x\-forward\-for equal to xxx<br><br>   * Creation time: 2024\-06\-13 00:00:03<br><br>* route4:<br><br>   * Path: equal to /abcd<br><br>   * Header: x\-forward\-for equal to xxx<br><br>   * Creation time: 2024\-06\-13 00:00:04 |v1：<br><br>route1 \> route2<br><br>v2:<br><br>route2 \> route1 |
|Scene 2<br><br>/abcd<br><br>Heade：x\-forword\-for =xxx ||v1:<br><br>route1 \> route2 \> route3 \> route4<br><br>v2:<br><br>route4 \> route3 \> route2 \> route1 |


This is used solely for explaining the Priority of Ingress effectiveness; in reality, only one Ingress takes effect. Priority description:


* Scenario 1, configuration of version v1 matching rule(s): Priority is given to route 1. Because route 1 was created earlier than route 2.

* Scenario 1, configuration of version v2 matching rule(s): Priority is given to route 2. Because equal to matching has higher precision than prefix matching, the precision of route 2 is higher than that of route 1. In this case, route 3 and route 4 have matching conditions that require valid header information, therefore, they do not hit the match.

* Scenario 2, configuration of version v1 matching rule(s): route 1 \> route 2 \> route 3 \> route 4. Sorted by creation time, from earliest to latest.

* Scenario 2, configuration of version v1 matching rule(s): route 4 \> route 3 \> route 2 \> route 1. Sort by accuracy from highest to lowest.
