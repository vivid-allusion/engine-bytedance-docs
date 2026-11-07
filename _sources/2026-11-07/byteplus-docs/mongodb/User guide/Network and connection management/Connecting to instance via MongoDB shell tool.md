---
title: "Connecting to instance via MongoDB shell tool"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/ug-connect-instance-via-mongo-shell"
---

After successfully creating a Document Database for MongoDB instance, you can connect to the MongoDB instance using the MongoDB shell tool and perform various management operations.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* Install the correct version of the MongoDB shell tool on your local machine or an ECS instance:

   * MongoDB 4.x: For detailed installation procedures, refer to [mongo shell](https://www.mongodb.com/docs/v4.4/mongo/#the-mongo-shell).

   * MongoDB 5.0 and later: For detailed installation procedures, refer to [mongosh](https://www.mongodb.com/docs/mongodb-shell/).

* MongoDB instance has been created. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance).

* Set up allowlist for the MongoDB instance and add the client device IP address to the instance's allowlist. For specific procedures, refer to [Setting allowlist](https://docs.byteplus.com/en/docs/mongodb/set-allowlist).

* If your client device and MongoDB instance are not in the same VPC, you also need to enable public network access for the MongoDB instance. For more information about how to apply for a public address, refer to [Applying for public address](https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to use MongoDB shell to connect to the database with SSL encryption, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/connect-db-use-mongo-shell-through-ssl">Connect to the database using MongoDB Shell with SSL encryption</a>.</div>



1. Log in to the [MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click on the **Connectivity** tab.

6. Locate the address type you need to use and click <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_6da1a6571a3b9cc35b99ef2d70cfb6c1.jpg) </span> icon next to the address to copy it.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more details about connection address types, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/addresses-introduction">Connection address type</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can replace <code><user></code> and <code><password></code> in the connection address with the corresponding database username and password according to actual business requirements. You can view and manage accounts on the <strong>Accounts</strong> tab. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/viewing_account_information">Viewing account details</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you create a MongoDB instance, the system will, by default, create an administrator account root in the admin database. Therefore, the value of <code>authSource</code> in MongoDB's default connection address is <code>admin</code> (that is, it will connect to the <code>admin</code> database by default).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the account you created yourself belongs to another database (such as <code>testdb1</code>), you need to change <code>admin</code> after <code>authSource</code> to the database where the self\-created account is located (such as <code>testdb1</code>). For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/create-account">Creating account</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Document Database for MongoDB adds the <code>&retryWrites=true</code> field by default at the end of each connection address to ensure the reconnection mechanism.   </div>
   

7. On a local server or ECS with MongoDB shell installed, enter the following command to connect to the MongoDB instance.

   Different versions of the connection tool use different connection commands. Specifically:

   * For MongoDB 4.x versions, the connection tool is [mongo shell](https://www.mongodb.com/docs/v4.4/mongo/#the-mongo-shell)

      ```Bash
      mongo "<Address copied with username and password changed in step 5>"
      ```
      

   * For MongoDB 5.0 and later versions, the connection tool is [mongosh](https://www.mongodb.com/docs/mongodb-shell/)

      ```Bash
      mongosh "<Address copied with username and password changed in step 5>"
      ```
      

   Example is as follows.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The example below uses the MongoDB 5.0 connection tool <a href="https://www.mongodb.com/docs/mongodb-shell/">mongosh</a>, with the private network address of a sharding cluster.   </div>
   

   ```Bash
   mongosh "mongodb://root:Pwd_123@mongoshardcn01e8ab0d20c****.mongodb.ivolces.com:3717,mongoshardcn01e8ab0d20c****.mongodb.ivolces.com:3717/?authSource=admin&connect=direct&retryWrites=true"
   ```
   

8. After logging in, if the following message appears, it indicates a successful connection to the Document Database for MongoDB instance via MongoDB shell.

   * If connecting to replica set instance

      ```Bash
      rs-instance_id: PRIMARY>
      ```
      

   * If connecting to Mongos node of sharding cluster instance

      ```Bash
      mongos>
      ```
      


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQs

[Why does reading or writing data fail after creating a new database with the same name as a deleted one?](https://docs.byteplus.com/en/docs/mongodb/rw-failure-with-same-name-new-db-created)
