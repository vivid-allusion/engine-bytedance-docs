---
title: "ByteHouse CE"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/ByteHouse_CE"
---

This article describes how to integrate ByteHouse CE to create datasets for BI analysis and report presentation.

<span id="bfa4b21d"></span>
# Prerequisites

The user must have a [ByteHouse CE Enterprise Edition](https://www.byteplus.com/en/product/bytehouse) account.

<span id="c17e5fdc"></span>
# Preparation


1. Refer to [ByteHouse Enterprise Edition Quick Start](https://www.volcengine.com/docs/6464/152221) to complete the operations for purchasing and activation, creating clusters, creating databases and tables, and importing data.

2. (SaaS version only) The user must add the "DataWind public IP for access" to the allowlist settings area to enable data integration in the SaaS environment. The "DataWind public IP for access" can be viewed at [Data Connection Overview](https://docs.byteplus.com/docs/undefined/68bea0b486defa05443e87ce). For detailed steps, see [ByteHouse CE Allowlist Management](https://www.volcengine.com/docs/6464/1581716).

3. Obtain the server. Go to the "Cluster Management" \- "Cluster List" page and obtain the server domain name from the network information section.

4. Obtain the port. Refer to [ByteHouse CE Cluster Connection Information](https://www.volcengine.com/docs/6464/1139202).

5. Obtain the username and password. Click "Account Management" to view the username and connection password.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eacbdf42f61145dd9dc6508e43a28cf8~tplv-goo7wpa0wc-image.image) </span>

6. (SaaS version only) Obtain the VPC ID. Click "Cluster Management" \- "Cluster List" and obtain the VPC ID from the "Network Information" section.


<span id="573a53e3"></span>
# Create from data connection


1. Go to BytePlus, click to get into a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select ByteHouse CE on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ede693ae096e4de9b6689943a44d3058~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information, test the connection, and click Save after a successful connection.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e9ec10c37ec4367807c13ecb7a7d7c0~tplv-goo7wpa0wc-image.image) </span>


* The parameter configuration instructions are as follows:

   
   |Parameters |Configuration description |
   |---|---|
   |Data connection name |Name for the new data connection, used to distinguish connections to different databases in the system. The default is Bytehouse_CE_timestamp. The name can be modified, but please enter a standard name. Only Chinese characters, English letters, numbers, and underscores are allowed, and there must be no spaces at the beginning or end. |
   |Server |Data connection IP or domain name. When using VPC mode:<br><br><br>* VPC mode: Only private network IP addresses are supported; domain names are not supported. How to obtain a private network IP: It is recommended to obtain it by pinging the local area network domain name or through the data source console.<br><br>* Non\-VPC mode: Domain names can be used. |
   |Port |Default: 8123. |
   |Username |See [Preparation](https://docs.byteplus.com/docs/DataWind/ByteHouse_CE#c17e5fdc) for how to obtain it. |
   |Password |See [Preparation](https://docs.byteplus.com/docs/DataWind/ByteHouse_CE#c17e5fdc) for how to obtain it. |
   |Permission mode |Both read and write modes are supported.<br><br><br>* Read: Only data in the data source can be retrieved; data cannot be modified, added, or deleted.<br><br>* Write: Users need to write data to the data connection through visual modeling and must have permission to perform operations on the data. |
   |vpcMode and VPC ID |Whether to use VPC mode (private network mode). Only the SaaS version requires these two parameters.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dda7598026a4452287c5b097ab2d6ea1~tplv-goo7wpa0wc-image.image) </span><br><br>The usage scenarios are as follows:<br><br><br>* **Enable VPC mode**: When the data source is a **BytePlus database or data warehouse product**, **it is recommended to use VPC mode**. Set vpcMode to **Yes** and enter the VPC ID. See [Preparation](https://docs.byteplus.com/docs/DataWind/ByteHouse_CE#c17e5fdc) for how to obtain the VPC ID.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to use VPC mode for BytePlus products to ensure data security and avoid additional data transfer costs.   </div><br>   <br><br>* **Disable VPC mode**: When the data source has public network access enabled, vpcMode does not need to be set, or can be set to No. |
   


<span id="6d2e7a52"></span>
# Create from dataset


1. Go to BytePlus, click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. When selecting the data connection, click New Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

3. The subsequent steps are the same as steps 2 and 3 of **Create from data connection** above. After completing the configuration, you will remain in the popup window for selecting the data connection for the dataset, where you can proceed directly to the next step of dataset creation.


<span id="fcb44b95"></span>
# Subsequent steps: Create a dataset


1. Use the previously created data connection to create a dataset: Click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6753b4124394ae8aec91b6d92e22524~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Search for or select from the dropdown the previously created data connection.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f47ed98b06e0425a82095d8288663ad8~tplv-goo7wpa0wc-image.image" width="500px" /></div>


<span id="68970b75"></span>
# FAQ

<span id="c76b767e"></span>
## Identity verification

To access the BytePlus ByteHouse Enterprise Edition console, complete [real-name authentication](https://www.volcengine.com/docs/6261/64935).

<span id="f4a24934"></span>
## **Obtain the database private IP and VPC ID**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When purchasing the SaaS version, it is necessary to use VPC mode to connect with a local area network IP. Only when the data source region is North China 2 do you need to obtain the database LAN IP and VPC ID.</div>


<span id="dbc38c39"></span>
### **Obtain the database private IP**

There are two methods to obtain the database private IP. The first method is to query by pinging the private domain name, and the second method is to query through the network interface management under the VPC. The following sections provide detailed instructions.

<span id="3a06bb31"></span>
#### Query by pinging the private domain name


1. Open the command\-line tool: In Windows, press `Windows+R`, enter `cmd`, and press Enter to open the Command Prompt window; in macOS or Linux, open the Terminal application.

2. Ping the private domain name: Enter `ping [database private domain name]`, for example, `ping mysql-server.local`, and press Enter. After executing the command, the IP address corresponding to the domain name will be displayed. This IP address is the database server's IP address in the private network.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81d0544871d348ba8e342bdb99752a9a~tplv-goo7wpa0wc-image.image" width="1178px" />   </div>
   


<span id="1f30745b"></span>
#### Query through VPC network interface management

Taking MySQL as an example, the same applies to databases built in environments such as PostgreSQL, load balancing, ECS, and many other products.


1. Go to the MySQL instance list page and click to view "Instance Information".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb153e14d61a41bcae7e0c2d303177a7~tplv-goo7wpa0wc-image.image) </span>


2. Go to the network interface page. In the Private IP Address section, you can view the private IP.


<span id="d90a6eb9"></span>
### Obtain the VPC ID

The user can only query the VPC ID through VPC network interface management.

Taking MySQL as an example, the same applies to databases built in environments such as PostgreSQL, load balancing, ECS, and many other products.


1. Go to the MySQL instance list page and click to view "Instance Information".

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc8838583520402fb264cb72ff05d658~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Copy the "ID" in the "Basic Information" section as shown in the figure below to obtain the VPC ID.


<span id="ee4ff570"></span>
### Enter the server IP and VPC ID


1. Go to the data connection configuration page and enter the copied "ID" into field A "VPC ID".

2. Copy the private IP and enter this IP into field B "Server" on the data connection page.
