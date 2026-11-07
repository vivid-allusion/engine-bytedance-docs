---
title: "Setting SSL encryption"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/setup-ssl"
---

Document Database for MongoDB offers Secure Sockets Layer (SSL) encryption services to improve the security of the link. You can enable SSL and install the SSL CA certificate to the application service. This topic describes how to set up SSL encryption\-related functions via the console.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

By encrypting network connections at the transport layer, SSL encryption improves communication data security and ensures data integrity.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Enabling, disabling SSL encryption, or updating SSL certificate validity period will cause the instance to restart. Perform this during off\-peak hours and ensure your business has a reconnection mechanism.

* Accessing MongoDB instances through a private network is relatively secure, and typically requires no data link encryption. Using SSL for connection will increase the CPU utilization of MongoDB instances. We recommend you enable SSL only for the need of encryption, for example, connecting to the database over the Internet.

* After SSL is enabled, MongoDB supports the SSL and non\-SSL connection modes. You can select a connection mode as needed.

* You can only download the SSL CA certificate from the [MongoDB console](https://console.byteplus.com/db/mongodb).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Security** tab.

6. Click the **SSL** sub\-tab.

7. On the **SSL** sub\-tab, you can execute corresponding commands according to your service requirements.

   
   <Tabs>
   <Tab zoneid="z0nQ64Tt4p" title="Enable SSL encryption">
   <TabTitle>Enable SSL encryption</TabTitle>
   
   1. Turn on the switch on the right of the SSL certificate.
   
   2. In the pop\-up dialog box, click **OK**.
   
      After enabling, the instance status changes to **SSL modifying**. When **SSL certificate validity** changes to **Valid** (instance status is **Running**), SSL is enabled.
   
   
   </Tab>
   <Tab zoneid="sL1OUwvkKS" title="Disable SSL encryption">
   <TabTitle>Disable SSL encryption</TabTitle>
   
   1. Turn off the switch on the right of the SSL certificate.
   
   2. In the pop\-up dialog box, click **OK**.
   
      After disabling, the instance status changes to **SSL modifying**. When **SSL certificate validity** changes to **Invalid** (instance status is **Running**), SSL is disabled.
   
   
   </Tab>
   <Tab zoneid="PbJGfp6yfE" title="Update SSL certificate validity period">
   <TabTitle>Update SSL certificate validity period</TabTitle>
   
   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="0">tip</div>
   
   
   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">After enabling SSL encryption, you can determine whether the current SSL certificate is within its validity period by checking <strong>SSL certificate validity</strong> status is <strong>Valid</strong>, and by checking the <strong>SSL certificate validity period</strong>. We recommend you update the validity period of the SSL certificate before it expires.</div>
   
   
   1. Click **Renew certificate**.
   
   2. In the pop\-up dialog box, click **OK**.
   
      After updating the validity period, the instance status changes to **SSL modifying**. When the instance status changes to **Running**, the validity period of the SSL certificate is updated.
   
   
   </Tab>
   <Tab zoneid="kw0BB2uT3S" title="Download SSL CA certificate">
   <TabTitle>Download SSL CA certificate</TabTitle>
   
   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="0">tip</div>
   
   
   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">After SSL encryption is enabled, you can download the SSL CA certificate to specify the SSL parameters and corresponding certificate for accessing MongoDB instances from the client. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/connect-db-use-mongo-shell-through-ssl">Connecting to database using Mongo shell via SSL encryption</a>.</div>
   
   
   Click **Download CA certificate** to download the SSL CA certificate to a local device.
   
   
   </Tab>
   </Tabs>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeDBInstanceSSL](https://docs.byteplus.com/en/docs/mongodb/describedbinstancessl) |Call the DescribeDBInstanceSSL interface to query the SSL encryption settings of the target MongoDB instance, including whether the function has been enabled, the expiration time of the SSL certificate, and other information. |
|[ModifyDBInstanceSSL](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancessl) |Call the ModifyDBInstanceSSL API to change the SSL encryption settings of the target MongoDB instance, including enabling/disabling the encryption function, or updating the SSL certificate validity period. |
