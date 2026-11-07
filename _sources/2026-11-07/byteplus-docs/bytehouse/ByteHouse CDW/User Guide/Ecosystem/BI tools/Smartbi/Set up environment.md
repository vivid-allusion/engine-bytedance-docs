---
title: "Set up environment"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/smartbi-set-up-environment"
---

Smartbi Insight is the latest all\-in\-one BI big data analysis platform launched by Smartbi Software Co., Ltd.

Smartbi Insight connects to various business databases, data warehouses, and big data platforms for data processing, analysis, mining, and visualization; it supports diverse data analysis applications, such as big data analysis, visual analysis, exploratory analysis, complex reports, and application sharing.

<span id="13d29c3d"></span>
# Background information

ByteHouse allows you to connect to it via Smartbi using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="b97f3047"></span>
# Prerequisites


1. Install Smartbi. Follow the installation and deployment instructions according to the system requirements [here](https://wiki.smartbi.com.cn/pages/viewpage.action?smt_poid=49&pageId=114987408).

2. ByteHouse account.


<span id="6181f63e"></span>
# Prepare data

import example data into ByteHouse.

<span id="5422a32f"></span>
### Prepare example databases

We use the following third\-party example data, which contains 5 tables and data.

<span id="b2bd4591"></span>
### DDL

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4101344b2eaa4582883ebd14f84d5429~tplv-goo7wpa0wc-image.image" name="ddl.sql">ddl.sql</Attachment>


&nbsp;

<span id="a52589e6"></span>
### Data

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eec4b402775849d8b623c6040e8c7fba~tplv-goo7wpa0wc-image.image" name="categories.csv">categories.csv</Attachment>


&nbsp;

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d8324bf27144d8395335d5f7d6f5250~tplv-goo7wpa0wc-image.image" name="orderdetails.csv">orderdetails.csv</Attachment>


&nbsp;

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e2d1521b2dd414596ed57dce4c7faba~tplv-goo7wpa0wc-image.image" name="products.csv">products.csv</Attachment>


&nbsp;

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e36a515ccbf48c58a54f74cc2112851~tplv-goo7wpa0wc-image.image" name="customers.csv">customers.csv</Attachment>


&nbsp;

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f884e0bfe5704d718f26c125bf3053c1~tplv-goo7wpa0wc-image.image" name="orders.csv">orders.csv</Attachment>


&nbsp;

<span id="8760aae8"></span>
### Import data into ByteHouse


1. Create a database in ByteHouse based on the above SQL statements.

2. Import the above data using the ByteHouse Client tool. For instructions on using the ByteHouse Client tool, see [ByteHouse CLI](https://docs.byteplus.com/docs/bytehouse/docs-gateway-client).

   
   <Tabs>
   <Tab zoneid="solyneXgzA" title="Use an IAM user">
   <TabTitle>Use an IAM user</TabTitle>
   
   ```SQL
   bytehouse-cli --host <host> --port 19000 --secure --token <API Key> --send_timeout=3600 --receive_timeout=3600 --database=northwind  -q "INSERT INTO northwind.categories FORMAT CSVWithNames" < categories.csv
    
   bytehouse-cli --host <host> --port 19000 --secure --token <API Key> --send_timeout=3600 --receive_timeout=3600 --database=northwind  -q "INSERT INTO northwind.customers FORMAT CSVWithNames" < customers.csv
   
   bytehouse-cli --host <host> --port 19000 --secure --token <API Key> --send_timeout=3600 --receive_timeout=3600 --database=northwind  -q "INSERT INTO northwind.orderdetails FORMAT CSVWithNames" < orderdetails.csv
   
   bytehouse-cli --host <host> --port 19000 --secure --token <API Key> --send_timeout=3600 --receive_timeout=3600 --database=northwind  -q "INSERT INTO northwind.orders FORMAT CSVWithNames" < orders.csv
   
   bytehouse-cli --host <host> --port 19000 --secure --token <API Key> --send_timeout=3600 --receive_timeout=3600 --database=northwind  -q "INSERT INTO northwind.products FORMAT CSVWithNames" < products.csv
   ```
   
   
   
   </Tab>
   <Tab zoneid="RhSYSIDLZV" title="Use a database account">
   <TabTitle>Use a database account</TabTitle>
   
   ```SQL
   bytehouse-cli --user {accountID_or_accountName}::{username}[::{envID}] --password {password} --host {HOST} --port 19000 --secure --send_timeout=3600 --receive_timeout=3600 --database=northwind  -q "INSERT INTO northwind.categories FORMAT CSVWithNames" < categories.csv
    
   bytehouse-cli --user {accountID_or_accountName}::{username}[::{envID}] --password {password} --host {HOST} --port 19000 --secure --send_timeout=3600 --receive_timeout=3600 --database=northwind  -q "INSERT INTO northwind.customers FORMAT CSVWithNames" < customers.csv
   
   bytehouse-cli --user {accountID_or_accountName}::{username}[::{envID}] --password {password} --host {HOST} --port 19000 --secure --send_timeout=3600 --receive_timeout=3600 --database=northwind  -q "INSERT INTO northwind.orderdetails FORMAT CSVWithNames" < orderdetails.csv
   
   bytehouse-cli --user {accountID_or_accountName}::{username}[::{envID}] --password {password} --host {HOST} --port 19000 --secure --send_timeout=3600 --receive_timeout=3600 --database=northwind  -q "INSERT INTO northwind.orders FORMAT CSVWithNames" < orders.csv
   
   bytehouse-cli --user {accountID_or_accountName}::{username}[::{envID}] --password {password} --host {HOST} --port 19000 --secure --send_timeout=3600 --receive_timeout=3600 --database=northwind  -q "INSERT INTO northwind.products FORMAT CSVWithNames" < products.csv
   ```
   
   
   
   </Tab>
   </Tabs>
   

   
   |Parameters |Configuration Highlights |
   |---|---|
   |host |Configure the network domain name for ByteHouse. {TENANT_ID} and {REGION} represent the main account ID of BytePlus and the region information of ByteHouse, respectively. You can find the corresponding information in ByteHouse Console under **Tenant Management**\>**basic information**\>**Network Information**. See details in [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
   |port |Set to: 19000. |
   |token |This is ByteHouse’s API Key. You can obtain the API Key in ByteHouse Console under **Tenant Management**\>**Connection Information**. See details in [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
   |username & password |When connecting using a database account, configure the following connection information:<br><br><br>* Set username to `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889):<br><br>   * `{accountID_or_accountName}` refers to the ByteHouse user account ID or name. You can log in to the ByteHouse console, click the top\-right profile to view and copy the account ID or name.<br><br>   * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* password is the database account password, customized by the administrator when creating the account. You may contact the administrator to obtain the password. If the password is lost or forgotten, contact the administrator to reset it. Refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043) for details. |
   |database |database name configured to connect to ByteHouse. |
   |secure |secure: set to true. |
