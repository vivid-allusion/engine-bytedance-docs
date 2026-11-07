---
title: "Connecting to database using Mongo shell via SSL encryption"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/connect-db-use-mongo-shell-through-ssl"
---

Document Database for MongoDB provides SSL (Secure Sockets Layer) encryption service. You can enable SSL encryption in advance, and improve the security of the data link by setting SSL encryption when connecting to database using Mongo shell via SSL encryption. This topic describes how to access the database using MongoDB shell with SSL encryption.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* SSL has been enabled for instances. For specific procedure, refer to [Setting SSL encryption](https://docs.byteplus.com/en/docs/mongodb/setup-ssl).

* If you need to use ECS to access MongoDB instance, ensure that the purchased ECS server and the MongoDB instance are in the same VPC. For specific procedures to purchase ECS instance, refer to [Purchasing ECS instance](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances).

* Add the IP address of the local server or ECS instance with the client installed to allowlist of MongoDB instance. For specific procedures, refer to [Setting allowlist](https://docs.byteplus.com/en/docs/mongodb/set-allowlist).

* Install the correct version of the mongo shell tool on your local machine or an ECS instance:

   * MongoDB 4.x: For detailed installation steps, refer to [mongo shell](https://www.mongodb.com/docs/v4.4/mongo/#the-mongo-shell).

   * MongoDB 5.0 and later: For detailed installation steps, refer to [MongoDB shell](https://www.mongodb.com/docs/mongodb-shell/).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Accessing MongoDB instances through a private network is relatively secure, and typically requires no data link encryption. Using SSL for connection will increase the CPU utilization of MongoDB instances. We recommend you enable SSL only for the need of encryption, for example, connecting to the database over the Internet.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

The procedure for connecting to a database in SSL mode on the Linux operating system (installed on ECS instance) is as follows.


1. Download the SSL CA certificate. For specific procedures, refer to [Setting SSL encryption](https://docs.byteplus.com/en/docs/mongodb/setup-ssl).

2. Decompress the certificate package, and upload the certificate to the local server or ECS instance where Mongo shell is installed.

   For example, upload the `.pem` certificate to the `root/mongodbsslca` directory of ECS.

3. On a local server or ECS with mongo shell installed, enter the following command to connect to the MongoDB instance.

   ```Bash
   # If the Mongo shell version is less than 4.2, use the following command:
   mongo --host <host> -u <username> -p --authenticationDatabase <database> --ssl --sslCAFile <sslCAFile_path> --sslAllowInvalidHostnames
   # If the Mongo shell version is greater than or equal to 4.2, use the following command:
   mongo --host <host> -u <username> -p --authenticationDatabase <database> --tls --tlsCAFile <sslCAFile_path>  --tlsAllowInvalidHostnames
   ```
   

   The descriptions of the relevant parameters in the command are shown in the following table.

   
   |Parameter |Description |Example |
   |---|---|---|
   |`<host>` |Address of a single node, including the domain name and port number. Supports using the connection addresses of the following nodes:<br><br><br>* Replica set instances: Each node in instance.<br><br>* Sharding cluster instance<br><br>   * Each Mongos node.<br><br>   * Each node in a single shard.<br><br>   * Each ConfigServer node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only the private addresses of Mongos nodes are provided in MongoDB sharding cluster instances. To use private addresses of shard nodes or ConfigServer nodes, apply for them separately. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/apply-private-address">Applying for private address</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To connect to the database by using a public address, apply for the public address first. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address">Applying for public address</a>.</div><br> |* Replica set instance<br><br>   * Private address of a single node<br><br>      `mongoreplicae9d7d321****0.mongodb.ibytepluses.com:3717`<br><br>   * Public address of a single node<br><br>      `mongoreplicae9d7d321****0.mongodb.bytepluses.com:3717`<br><br>* Sharding cluster instance<br><br>   * Public address of a single Mongos node<br><br>      `mongoshard75fef301****0.mongodb.bytepluses.com:3717`<br><br>   * Public address of a single node in a shard<br><br>      `mongoshard75fef301****s00.mongodb.bytepluses.com:3717`<br><br>   * Private address of a single ConfigServer node<br><br>      `mongoshard75fef301****config0.ibytepluses.com:3717` |
   |`<username>` |The database account to connect to.<br><br>The default MongoDB account is root. Do not directly use the root account to connect to the database in a production environment. You can create accounts and assign permissions to them based on business requirements. For more information, refer to [Creating account](https://docs.byteplus.com/en/docs/mongodb/create-account) and [Account permissions](https://docs.byteplus.com/en/docs/mongodb/account-overview#.6LSm5Y-35p2D6ZmQ). |`root` |
   |`<database>` |The database to which the account belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the database account is root, the corresponding database must be admin.</div><br> |`admin` |
   |`<sslCAFile_path>` |Path to the SSL CA certificate file. |`/root/mongodbsslca/mongoshellshard.pem` |
   

   The following example demonstrates accessing database using SSL encrypted connection, with the public network address of a Mongos node in a sharding cluster instance.

   ```Bash
   mongo --host mongoshard75fef3010****01.mongodb.bytepluses.com:3717 -u root -p --authenticationDatabase admin --tls --tlsCAFile /root/mongodbsslca/mongoshellshard.pem  --tlsAllowInvalidHostnames
   ```
   

4. When the command line prompts `Enter password:`, enter the password for the database account and press Enter to confirm.

   If you forget the password for the root account, you can reset it on the MongoDB console. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/mongodb/reset-password).
