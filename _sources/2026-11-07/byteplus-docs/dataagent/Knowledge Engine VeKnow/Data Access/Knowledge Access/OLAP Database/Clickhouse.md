---
title: "Clickhouse"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Clickhouse_"
---

Clickhouse data connection is supported. This article describes how to access Clickhouse data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before connecting to the database, please clarify the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The username and password of the database.</div>


* <div data-tips="true" data-tips-type="tip">The database method that needs to be connected.</div>



<span id="df99d782"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="22b9216e"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the **data connection** screen select **OLAP \> ClickHouse** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4464669401d4584a1d5623565023f55~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cea312af205f4817b97ad73ef50c287b~tplv-goo7wpa0wc-image.image) </span>

   
   |name |describe |
   |---|---|
   |server |Deploy ClickHouse the public address of the database host, which is the host Internet Protocol Address. |
   |Port |Deploy ClickHouse the port number corresponding to the database public network address. |
   |Username and password |Login ClickHouse username and password for the database. |
   |agreement |The default is the HTTP protocol. |
   

4. Click **Save** after successful connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/867cb641110b404c9dc7ff223c724e11~tplv-goo7wpa0wc-image.image) </span>
