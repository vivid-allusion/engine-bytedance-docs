---
title: "Get cluster connection information"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/get-cluster-connection-information"
---

This article explains how to obtain the cluster connection information required to connect to ByteHouse Enterprise edition in a development environment.

Generally, you need to obtain the following information:


* Cluster Connection Information:

   * HOST: Cluster Connection Address.

   * PORT: Cluster Connection Port.

* User Login Information:

   * USERNAME: User Account.

   * PASSWORD: User Password.


<span id="3a66dd0c"></span>
## Retrieve cluster information

You can view the basic connection information of the cluster in **Manage Clusters \> Cluster List \> Cluster \> Basic information**.

<span id="347bc507"></span>
### Common connection methods

ByteHouse Enterprise version currently supports data access via graphical interface tools (such as DataGrip, DBeaver and others), and common development tools (such as ClickHouse Client, JDBC and others). You can view the usage instructions and connection commands in **Cluster Management \> Cluster List \> Cluster \> Connect** tab.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/864fa145a3c1467681783b56ce5ce2a1~tplv-goo7wpa0wc-image.image) </span>

<span id="6ab9e6d0"></span>
### Cluster connection address

In **Manage Clusters \> Cluster List \> Cluster \> Basic Cluster**, we can view the current cluster’s connection address (i.e. `Host` address).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90b9a176ba9543aba7aacaefacd75233~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">An error will occur when binding to the public network, and the relevant issue is under urgent repair.</div>


* <div data-tips="true" data-tips-type="warning">ByteHouse Enterprise does not currently support accessing the public network via a domain name; however, you can directly use a public IP to establish a connection.</div>



<span id="c58d5357"></span>
### Cluster connection port

Ports used in common connection methods can be referred from the table below.


|Connection Methods |Common Tools |Port number (BytePlus PaaS version) |
|---|---|---|
|TCP |[ClickHouse Client](https://docs.byteplus.com/docs/bytehouse/clickhouse-client)<br><br>[Python Driver](https://docs.byteplus.com/docs/bytehouse/python-driver)<br><br>[Go Driver](https://docs.byteplus.com/docs/bytehouse/go-driver) |9000 |
|HTTP |[JDBC](https://docs.byteplus.com/docs/bytehouse/jdbc) |8123 |
|HTTPS | |8443 |
|MySQL Client |MySQL Client |9004 |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Some users may change the default connection port when deploying privately.</div>


<div data-tips="true" data-tips-type="warning">For the specific port, please refer to the port displayed in <strong>Cluster management \> Cluster List \> Cluster \> Basic information \> Connect</strong> interface.</div>


<span id="c697cd0c"></span>
## Retrieve account and password

<span id="1e461dbf"></span>
### Retrieve connection account

When connecting to ByteHouse, you need to use the ByteHouse Service username and Password:


* The username for ByteHouse Service and the IAM Account **are the same**;;

* The Password for ByteHouse Service and the IAM Log\-in password **are different**; The IAM Log\-in password is only used for logging into the official BytePlus website.


<span id="9f131fd8"></span>
### Reset connection password

After the first log\-in to BytePlus using the IAM account password, the system will automatically generate an initial Service password for ByteHouse.

You can also reset and set a new password in **Manage clusters \> Cluster list \> Cluster \> Connect to cluster**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f68b6a2638248cc9c31874abed792a4~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed180d7686d24075a6fb6c6478d19864~tplv-goo7wpa0wc-image.image" width="480px" /></div>
