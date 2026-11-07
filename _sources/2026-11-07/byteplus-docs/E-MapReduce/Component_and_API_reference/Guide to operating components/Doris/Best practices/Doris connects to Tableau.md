---
title: "Doris connects to Tableau"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Doris_connects_to_Tableau"
---

Doris supports connecting to Tableau. You can connect your Tableau by following the steps below.

<span id="_1-准备工作"></span>
## Preparation

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The screenshots in this article are from Tableau Desktop Mac version</div>



1. Install Tableau software. For details, see: [Tableau official website](https://www.tableau.com/zh-cn/why-tableau/what-is-tableau).

2. Bind an EIP to the Master Node of the Doris cluster. For instructions, see: [Bind public IP](https://www.volcengine.com/docs/6401/68687).

3. Ensure that the security group port 9030 is open. For instructions, see: [Add access rule](https://www.volcengine.com/docs/6401/68895).


<span id="_2-下载-mysql-驱动"></span>
## 2. Download MySQL driver

Download the corresponding MySQL driver from the Tableau [official website](https://www.tableau.com/zh-cn/support/drivers?edition=pro&lang=zh-cn&platform=mac&cpu=64&version=2022.1&__full-version=20221.22.0415.1144#mysql), including iODBC Driver Manager and MySQL ODBC Connector.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Doris only supports <strong>version 5.3</strong> of the MySQL ODBC Connector.</div>


<span id="_3-连接-doris"></span>
## 3. Connect to Doris


1. Launch **Tableau**, click **More**, and select **MySQL.** 

2. Fill in **IP/Host/Username/Password**. Other fields can be left blank.

* **Server**: Enter the EIP address bound to the Master Node of Doris (public address for Master Node protocol)

* **Port**: Enter the port number for the MySQL protocol connection target, typically 9030 by default

* **Database**: Leave blank

* **Username**: The account created in the Doris cluster, or use the root administrator account

* **Password**: The connection password set when the cluster was created

3. Click Login to enter the workbook page
