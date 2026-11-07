---
title: "API Release Notes"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/API-release-notes"
---

<span id="25043a06"></span>
## Version Notes

Message queue Kafka has officially released two versions of the Open API so far:


|Version |Description |
|---|---|
|[V1 (2018-01-01)](https://docs.byteplus.com/en/docs/kafka/API-overview-v1) |The V1 version API was released in April 2022. This version supports basic functions such as instance lifecycle management, topic management, and group management. |
|[V2 (2022-05-01)](https://docs.byteplus.com/en/docs/kafka/API-overview-2) |The V2 version API was released in March 2023. It is recommended that new users choose this version to access.<br><br>This version covers all the functions of the current V1 version. In addition to supporting functions such as instance lifecycle management, Topic management, and Group management, it also supports functions such as tag management. |


<span id="65973f93"></span>
## Compatibility Notes

In order to ensure the compatibility of the old and new versions and not affect the normal use of old users, the V1 version Open API will not stop the service, will not go offline, but will stop iteration, and will not add new functions in principle. For a better experience and more comprehensive functions, we strongly recommend that you use the V2 version Open API.

Compared with the V1 version, the V2 version Open API added functions such as label management and ACL management, which can create Kafka instances of all specifications and continue to iterate and update.
