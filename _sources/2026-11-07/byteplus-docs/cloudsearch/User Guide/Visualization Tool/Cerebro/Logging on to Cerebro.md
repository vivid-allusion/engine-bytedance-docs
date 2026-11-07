---
title: "Logging on to Cerebro"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Logging-Cerebro"
---

Cloud Search supports Cerebro, which is an open source, visualized management tool for Elasticsearch (ES) clusters. Cerebro allows you to monitor cluster loads, node resources, index distribution, and other information in real time.

This topic describes how to log on to Cerebro.

<span id="前提条件"></span>
## Before you begin


* If you want to access Cerebro by using a public endpoint, enable internet\-facing access to Cerebro first. For more information, refer to [Configuring public network access to Cerebro](https://docs.byteplus.com/en/docs/cloudsearch/public-access-Cerebro).

* The default ports in all endpoints of the visualization tool Cerebro are 9000. Open this port in the related security group.


<span id="公网访问-cerebro"></span>
## Accessing Cerebro over the internet


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Region of the target instance.

3. On the **Instances** page, click the name of the instance.

4. In **Instance management \>**  **Visulization configuration**, click public network access addresson the **Cerebro** card.

5. On the Cerebro logon page, click the cluster ID, then type the username and password.

   The username is admin, and the password is the one you set when creating the instance. If you forgot your password, reset the password on the **Basic information** page. For more information, refer to [Resetting the instance password](https://docs.byteplus.com/en/docs/cloudsearch/resetting-password).


<span id="内网访问-cerebro"></span>
## Accessing Cerebro over an internal network


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Region of the target instance.

3. On the **Instances** page, click the name of the instance.

4. In **Instance management \>**  **Visulization configuration**, click private network access address on the **Cerebro** card.

5. On the Cerebro logon page, click the cluster ID, then type the username and password.

   The username is admin, and the password is the one you set when creating the instance. If you forgot your password, reset the password on the **Basic information** page. For more information, refer to [Resetting the instance password](https://docs.byteplus.com/en/docs/cloudsearch/resetting-password).
