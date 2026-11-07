---
title: "Connecting to MongoDB from client via SSL encryption"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/connect-db-from-client-via-ssl"
---

MongoDB provides the Secure Sockets Layer (SSL) encryption service. You can enable the SSL and set SSL to improve the security of data links during database connection. This topic describes the specific methods for multilingual clients to access MongoDB databases via SSL encrypted connections.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* SSL has been enabled for MongoDB instances. For specific procedure, refer to [Setting SSL encryption](https://docs.byteplus.com/en/docs/mongodb/setup-ssl).

* Add the IP address of the local server or ECS instance with the client installed to the allowlist of the MongoDB instance. For specific procedures, refer to [Setting allowlist](https://docs.byteplus.com/en/docs/mongodb/set-allowlist).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Accessing MongoDB instances through a private network is relatively secure, and typically requires no data link encryption. Using SSL for connection will increase the CPU utilization of MongoDB instances. We recommend you enable SSL only for the need of encryption, for example, connecting to the database over the Internet.

<span id=".5a6i5oi356uvLXNzbC3ov57mjqXnpLrkvos="></span>
## Examples of client SSL connection

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">MongoDB instances include replica set and sharding cluster instances. Different types of instances provide different connection addresses. You can log in to the <a href="https://console.byteplus.com/db/mongodb">MongoDB console</a>, access the <strong>Connectivity</strong> tab, and view and copy the required addresses. For more information about MongoDB connection addresses, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/addresses-introduction">Address types</a>.</div>


* <div data-tips="true" data-tips-type="tip">All the examples in this topic use the latest versions of clients using each language.</div>




<Tabs>
<Tab zoneid="QgBTys56c5" title="C">
<TabTitle>C</TabTitle>

* **Relevant links**: [MongoDB C Driver](https://www.mongodb.com/docs/drivers/c/)

* **Code explanation**

   Set parameters in C client code as follows:

   1. At the end of the client URI, add the parameter `ssl=true` to enable SSL encrypted connections.

   2. You can configure SSL encrypted connection using the `mongoc_ssl_opt_t` parameter. Among them:

      1. Set the CA certificate path in the `ssl_opts.ca_file` field.

      2. Set the `ssl_opts.allow_invalid_hostname` field to `false` to ignore hostname verification.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For more information on the <code>mongoc_ssl_opt_t</code> parameter, refer to <a href="http://mongoc.org/libmongoc/current/mongoc_ssl_opt_t.html?spm=a2c4g.11186623.0.0.7ee519abjpeSJc">mongoc_ssl_opt_t</a>.      </div>
      

   The code example is as follows.

   ```C
   mongoc_client_t *client = NULL;
   
   client = mongoc_client_new (
         /* The following code uses the private network address of a replica set instance as an example.
         "mongodb://<user>:<password>@mongoreplicae9d7d321****0.mongodb.ibytepluses.com:3717,mongoreplicae9d7d321****1.mongodb.ibytepluses.com:3717/?authSource=admin&replicaSet=rs-mongo-replica-e9d7d321****&retryWrites=true&ssl=true");
   const mongoc_ssl_opt_t *ssl_default = mongoc_ssl_opt_get_default ();
   mongoc_ssl_opt_t ssl_opts = { 0 };
   
   /* optionally copy in a custom trust directory or file; otherwise the default is used. */
   memcpy (&ssl_opts, ssl_default, sizeof ssl_opts);
   ssl_opts.ca_file = "/path/to/ca.pem"
   ssl_opts.allow_invalid_hostname = false
   mongoc_client_set_ssl_opts (client, &ssl_opts);
   ```
   





</Tab>
<Tab zoneid="pFDM8DGwIe" title="C ++">
<TabTitle>C ++</TabTitle>

* **Relevant links**: [MongoDB C++ Driver](https://www.mongodb.com/docs/drivers/cxx/)

* **Code explanation**

   Set parameters in C++ client code as follows:

   1. At the end of the client URI, add the parameter `ssl=true` to enable SSL encrypted connections.

   2. You can configure the SSL encrypted connection using the `mongoc_ssl_opt_t` parameter. You need to set the path to the CA certificate in the `ssl_options.ca_file` field.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For more information on the <code>mongoc_ssl_opt_t</code> parameter, refer to <a href="http://mongoc.org/libmongoc/current/mongoc_ssl_opt_t.html?spm=a2c4g.11186623.0.0.7ee519abjpeSJc">mongoc_ssl_opt_t.</a>      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The mongocxx driver does not currently support ignoring hostname verification.      </div>
      

   The code example is as follows.

   ```C++
   #include <mongocxx/client.hpp>
   #include <mongocxx/uri.hpp>
   #include <mongocxx/options/client.hpp>
   #include <mongocxx/options/ssl.hpp>
   
   mongocxx::options::client client_options;
   mongocxx::options::ssl ssl_options;
   
   // If the server certificate is not signed by a well-known CA,
   // you can set a custom CA file with the `ca_file` option.
   ssl_options.ca_file("/path/to/ca.pem");
   
   client_options.ssl_opts(ssl_options);
   
   auto client = mongocxx::client{
       // The following code uses the private network address of a replica set instance as an example.
       uri{"mongodb://<user>:<password>@mongoreplicae9d7d321****0.mongodb.ibytepluses.com:3717,mongoreplicae9d7d321****1.mongodb.ibytepluses.com:3717/?authSource=admin&replicaSet=rs-mongo-replica-e9d7d321****&retryWrites=true&ssl=true"}, client_opts};
   ```
   





</Tab>
<Tab zoneid="wVu4vpR8a8" title="Golang">
<TabTitle>Golang</TabTitle>

* **Relevant links**: [MongoDB Golang Driver](https://www.mongodb.com/docs/drivers/go/current/), [Crypto tls package](https://golang.org/pkg/crypto/tls/)

* **Code explanation**

   The Golang driver uses the underlying SSL support provided by the crypto/tls package to establish SSL connections with MongoDB servers. Set SSL connection parameters in client code as follows:

   1. At the end of the client URI, add the parameter `ssl=true` to enable SSL encrypted connections.

   2. In the `tlsConfig` structure, set the following parameters:

      1. Use the `RootCAs` parameter to specify CA certificates.

      2. Set `InsecureSkipVerify` to `true` to ignore hostname verification.

   The code example is as follows.

   ```Go
   package main
   
   import (
       "context"
       "crypto/tls"
       "crypto/x509"
       "fmt"
       "go.mongodb.org/mongo-driver/bson"
       "go.mongodb.org/mongo-driver/mongo"
       "go.mongodb.org/mongo-driver/mongo/options"
       "go.mongodb.org/mongo-driver/mongo/readpref"
       "go.mongodb.org/mongo-driver/mongo/writeconcern"
       "io/ioutil"
       "log"
   )
   
   func main() {
       var filename = "ca.pem"
       rootPEM, err := ioutil.ReadFile(filename)
       roots := x509.NewCertPool()
       if ok := roots.AppendCertsFromPEM([]byte(rootPEM)); !ok {
           fmt.Printf("get certs from %s fail!\n", filename)
           return
       }
       tlsConfig := &tls.Config{
           RootCAs: roots,
           InsecureSkipVerify: true,
       }
   
       // Create a Client to a MongoDB server and use Ping to verify that the server is running.
       // The following code uses the private network address of a replica set instance as an example.
       clientOpts := options.Client().ApplyURI("mongodb://<user>:<password>@mongoreplicae9d7d321****0.mongodb.ibytepluses.com:3717,mongoreplicae9d7d321****1.mongodb.ibytepluses.com:3717/?authSource=admin&replicaSet=rs-mongo-replica-e9d7d321****&retryWrites=true&ssl=true")
       clientOpts.SetReadPreference(readpref.Secondary())
       clientOpts.SetWriteConcern(writeconcern.New(writeconcern.WMajority(), writeconcern.J(true), writeconcern.WTimeout(1000)))
       clientOpts.SetTLSConfig(tlsConfig)
       client, err := mongo.Connect(context.TODO(), clientOpts)
       if err != nil {
           fmt.Println("connect failed!")
           log.Fatal(err)
           return
       }
       fmt.Println("connect successful!")
   
       defer func() {
           if err = client.Disconnect(context.TODO()); err != nil {
               fmt.Println("disconnect failed!")
               log.Fatal(err)
           }
           fmt.Println("disconnect successful!")
       }()
   
       // Call Ping to verify that the deployment is up and the Client was configured successfully.
       // As mentioned in the Ping documentation, this reduces application resiliency as the server may be temporarily unavailable when Ping is called.
       if err = client.Ping(context.TODO(), nil); err != nil {
           fmt.Println("ping failed!")
           log.Fatal(err)
           return
       }
       fmt.Println("ping successful!")
   
       collection := client.Database("baz").Collection("qux")
       res, err := collection.InsertOne(context.Background(), bson.M{"hello": "world"})
       if err != nil {
           fmt.Println("insert result failed!")
           log.Fatal(err)
           return
       }
       id := res.InsertedID
       fmt.Println("Id: ", id)
       fmt.Printf("insert result: %v\n", res)
   
       result := bson.M{}
       filter := bson.D{{"_id", res.InsertedID}}
       if err := collection.FindOne(context.Background(), filter).Decode(&result); err != nil {
           fmt.Println("find failed!")
           log.Fatal(err)
           return
       }
   
       fmt.Printf("result: %v\n", result)
   }
   ```
   





</Tab>
<Tab zoneid="ES4LBVq2gA" title="Java">
<TabTitle>Java</TabTitle>

* **Relevant links**: [MongoDB Java Driver](https://www.mongodb.com/docs/drivers/java-drivers/)

* **Code explanation**

   Set SSL connection parameters in Java client code as follows:

   1. Configure the `MongoClientOptions` parameter group as follows:

      1. Set `sslEnabled` to `true` to enable SSL connections.

      2. Set `sslInvalidHostNameAllowed` to `true` to ignore hostname verification.

      The code example is as follows.

      ```Java
      import com.mongodb.MongoClientURI;
      import com.mongodb.MongoClientOptions;
      MongoClientOptions options= MongoClientOptions.builder().sslEnabled(true).sslInvalidHostNameAllowed(true).build();
      MongoClient client = new MongoClient("mongodb://<user>:<password>@mongoreplicae9d7d321****0.mongodb.ibytepluses.com:3717,mongoreplicae9d7d321****1.mongodb.ibytepluses.com:3717/?authSource=admin&replicaSet=rs-mongo-replica-e9d7d321****&retryWrites=true", options)
      ```
      

   2. Use the keytool utility to configure CA certificates.

      The code example is as follows.

      ```Java
      keytool -importcert -trustcacerts -file <path to certificate authority file> 
              -keystore <path to trust store> -storepass <password>
      ```
      

   3. Set JVM system properties in Java program to direct to the correct trust store and key store.

      The code example is as follows.

      ```Java
      System.setProperty("javax.net.ssl.trustStore","/trust/mongoStore.ts");
      System.setProperty("javax.net.ssl.trustStorePassword","StorePass");
      ```
      





</Tab>
<Tab zoneid="QwZqjmAy2s" title="Node.js">
<TabTitle>Node.js</TabTitle>

* **Relevant links**: [MongoDB Node.js Driver](https://www.mongodb.com/docs/drivers/node/current/)

* **Code explanation**

   Set parameters in Node.js client code as follows:

   1. At the end of the client URI, add the parameter `ssl=true` to enable SSL encrypted connections.

   2. Set the `sslCA` parameter to direct to the path of the CA certificate.

   3. Set `checkServerIndentity` to `false` to ignore hostname verification.

   The code example is as follows.

   ```JavaScript
   var MongoClient = require('mongodb').MongoClient
   // Read the certificate authority
   var ca = "/path/to/ca.pem"
   // Connect validating the returned certificates from the server
   // The following code uses the private network address of a replica set instance as an example.
   MongoClient.connect("mongodb://<user>:<password>=@mongoreplicae9d7d321****0.mongodb.ibytepluses.com:3717,ongoreplicae9d7d321****1.mongodb.ibytepluses.com:3717/?authSource=admin", {
       sslValidate:true,
       checkServerIdentity:false,
       sslCA: ca
   }, async function(err, db) {
     db.close();
   });
   ```
   





</Tab>
<Tab zoneid="jlA5sOYogl" title=".NET Core">
<TabTitle>.NET Core</TabTitle>

Use the .NET Core driver to access MongoDB database in SSL connection mode:


1. Install .NET. For more information about the installation method, refer to [Download .NET](https://dotnet.microsoft.com/download).

2. Execute the following command to create a project (in this example, the project directory name is `MongoDB`).

   ```Bash
   dotnet new console -o MongoDB
   ```
   

3. Execute the following command to enter the newly created directory.

   ```Bash
   cd MongoDB
   ```
   

4. Use the following command to install the MongoDB .NET Core driver package.

   ```Bash
   dotnet add package mongocsharpdriver --version 2.11.5
   ```
   

5. Set SSL connection parameters in the client code.

   The code example is as follows.

   ```C#
   using System;
   using System.Collections.Generic;
   using System.Security.Cryptography.X509Certificates;
   using MongoDB.Bson;
   using MongoDB.Driver;namespace dotnetCase
   {
   class Program
   {
   static void Main(string[] args)
   {
   // MongoDB instance information.
   const string host1 = "mongoreplicae9d7d321****0.mongodb.ibytepluses.com";
   const int port1 = 3717;
   const string host2 = "mongoreplicae9d7d321****1.mongodb.ibytepluses.com";
   const int port2 = 3717;
   const string replicaSetName = "rs-mongo-replica-e9d7d321****"; // Sharding cluster instance connection addresses do not require this parameter.
   const string admin = "admin";
   const string userName = "root";
   const string passwd = "********";        
   try
           {
               // Set connection host information.
               MongoClientSettings settings = new MongoClientSettings();
               List<MongoServerAddress> servers = new List<MongoServerAddress>();
               servers.Add(new MongoServerAddress(host1, port1));
               servers.Add(new MongoServerAddress(host2, port2));
               settings.Servers = servers;
               // Set the replica set name (sharding cluster instances do not require this parameter).
               settings.ReplicaSetName = replicaSetName;
               // Set the timeout to 3 seconds.
               settings.ConnectTimeout = new TimeSpan(0, 0, 0, 3, 0);
               // Set the login username and password.
               MongoCredential credentials = MongoCredential.CreateCredential(admin, userName, passwd);
               settings.Credential = credentials;
               // Set SSL information.
               SslSettings sslSettings = new SslSettings{
                   ClientCertificates = new[] {new X509Certificate("ca.pem")},
               };
               settings.UseTls = true;
               settings.AllowInsecureTls = true;
               settings.SslSettings = sslSettings;
               // Initializing client
               MongoClient client = new MongoClient(settings);
           }
           catch (Exception e)
           {
               Console.WriteLine("连接异常:"+e.Message);
           }
       }
   }
   }
   ```
   





</Tab>
<Tab zoneid="T7Foatiu2C" title="PHP">
<TabTitle>PHP</TabTitle>

* **Relevant link**: [MongoDB PHP Driver](https://www.mongodb.com/docs/drivers/php/)

* **Code explanation**

   Create a PHP client and set SSL connection parameters in the client code as follows:

   1. Set `ssl` to `true` to enable SSL encrypted connection.

   2. Set the CA certificate path in `ca_file`.

   3. Set `allow_invalid_hostname` to `true` to ignore hostname verification.

   The code example is as follows.

   ```PHP
   <?php  
   // The following code uses the private network address of a replica set instance as an example.
   $manager = new MongoDB\Driver\Manager('mongodb://<user>:<password>=@mongoreplicae9d7d321****0.mongodb.ibytepluses.com:3717,ongoreplicae9d7d321****1.mongodb.ibytepluses.com:3717/?authSource=admin',
   [   'ssl' => true,
   /* Sharding cluster instance connection addresses do not require the following parameters */
   'replicaSet' => 'rs-mongo-replica-e9d7d321****'  
       ],
       [
           "ca_file" => "/path/to/ca.pem",
           "allow_invalid_hostname" => true
       ]
   );
   ```
   





</Tab>
<Tab zoneid="chgBGfGMuK" title="Python">
<TabTitle>Python</TabTitle>

* **Relevant link**: [MongoDB Python Driver](https://www.mongodb.com/docs/drivers/python/?_ga=2.185766377.1999902664.1674894818-2046080392.1673582123)

* **Code explanation**

   Set SSL connection parameters in Python client code as follows:

   1. Set the `ssl` parameter to `True` to enable SSL encrypted connections.

   2. Set the `ssl_ca_certs` parameter to direct to the path of the CA certificate.

   3. Set `ssl_match_hostname` to `False` to ignore hostname verification.

   The code example is as follows.

   ```Python
   import ssl
   from pymongo import MongoClient
       
   uri = "mongodb://<user>:<password>@mongoreplicae9d7d321****0.mongodb.ibytepluses.com:3717,mongoreplicae9d7d321****1.mongodb.ibytepluses.com:3717/?authSource=admin&replicaSet=rs-mongo-replica-e9d7d321****&retryWrites=true"
   client = MongoClient(uri,
                        ssl=True,
                        ssl_ca_certs='ca.pem',
                        ssl_match_hostname=False)
   ```
   





</Tab>
<Tab zoneid="sDEmxwvc38" title="Scala">
<TabTitle>Scala</TabTitle>

* **Relevant links**: [MongoDB Scala Driver](https://www.mongodb.com/docs/drivers/scala/)

* **Code explanation**

   The Scala driver uses the SSL underlying support provided by Netty to establish SSL connection with the MongoDB server. Set SSL connection parameters in client code as follows:

   1. In the `MongoClientOptions` parameter group, configure the following settings in `sslSettings`.

      1. Set `enabled` to `true` to enable SSL connection.

      2. Set `invalidHostNameAllowed` to `true` to ignore hostname verification.

      The code example is as follows.

      ```Scala
      import org.mongodb.scala.connection.{NettyStreamFactoryFactory, SslSettings}
      
      MongoClientSettings.builder()
                         .sslSettings(SslSettings.builder()
                                                 .enabled(true)                 
                                                 .invalidHostNameAllowed(true)  
                                                 .build())                      
                         .streamFactoryFactory(NettyStreamFactoryFactory())
                         .build()
      // The following code uses the private network address of a replica set instance as an example.
      val client: MongoClient = MongoClient("mongodb://<user>:<password>@mongoreplicae9d7d321****0.mongodb.ibytepluses.com:3717,mongoreplicae9d7d321****1.mongodb.ibytepluses.com:3717/?authSource=admin&replicaSet=rs-mongo-replica-e9d7d321****&retryWrites=true")
      ```
      

   2. Use the keytool utility to configure CA certificates.

      The code example is as follows.

      ```Scala
      keytool -importcert -trustcacerts -file <path to certificate authority file> 
              -keystore <path to trust store> -storepass <password>
      ```
      

   3. Set JVM system properties in the program to direct to the correct trust store and key store.

      ```Scala
      System.setProperty("javax.net.ssl.trustStore","/trust/mongoStore.ts");
      System.setProperty("javax.net.ssl.trustStorePassword","StorePass");
      ```
      


</Tab>
</Tabs>
