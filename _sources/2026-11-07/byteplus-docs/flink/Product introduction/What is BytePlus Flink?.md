---
title: "What is BytePlus Flink?"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/What_is_BytePlus_Flink"
---

BytePlus Flink is a 100% Apache Flink\-compatible, fully managed streaming platform, integrating large\-scale enterprise task practices. It offers features such as plug\-and\-play, zero maintenance, extreme elasticity with Serverless, simplified SQL development, low TCO, and high SLA guarantees, accelerating enterprises' transformation towards real\-time and cloud\-native operations.

<span id="6fb80032"></span>
## Product Architecture

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ebab41e1231418dbb7bc8b47772d2df~tplv-goo7wpa0wc-image.image) </span>

<span id="0df7f30c"></span>
## Product Features


* **Fully Compatible Ecosystem**: 100% compatible with open\-source Apache Flink, with plug\-in enterprise\-level enhancements.

* **Fully Managed One\-stop**: Provides a fully managed Flink service, simple to operate, ready to use without maintenance.

* **Serverless Elasticity**: Possesses elastic scaling capabilities based on VKE/VCI.

* **Visual Interactive Collaboration**: Provides a low\-code, visual task development interface with real\-time printing of debug results.

* **Enterprise\-level Security**: Based on the IAM authorization system, it provides project and resource\-level role permission control.


<span id="a35ff626"></span>
## Glossary Explanation


|**Noun** |**Description** |
|---|---|
|Main Account |The main account is the principal to which resources belong, typically using a username as the login identifier for the account.<br><br>The main account can operate and access all service resources. |
|IAM User (Subuser) |Created by the main account, set with a password and access keys, the subuser can log in to the console but does not have operational permissions and needs to be authorized for projects. |
|Project |A project, created by the main account, is used to uniformly manage resource pools, tasks, and other resources within a project space.<br><br>Projects are isolated and independent from one another, each having its own internal permission control mechanism. |
|Flink Resource Pool |The Flink Resource Pool is used to manage computing resources, which are isolated within the pool and not affected by the resource consumption of other pools. |
|Data Source (Source) |Provides continuous input data for stream processing from upstream services, such as the BytePlus DataStreams Kafka. |
|Data Destination (Sink) |The place where stream processing data results are output, such as BytePlus DataStreams Kafka. |
|Schema |Represents the structural information of a table in SQL tasks, such as column names and types. |
