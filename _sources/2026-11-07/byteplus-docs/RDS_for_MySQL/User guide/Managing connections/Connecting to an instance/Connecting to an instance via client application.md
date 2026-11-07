---
title: "Connecting to an instance via client application"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/connecting_to_an_instance_via_client_application"
---

## Connecting to an instance via client application

You can establish a connection using any MySQL\-compatible client program. This topic describes how to connect to a MySQL instance by using a client program.

### Background

RDS for MySQL supports various types of connection addresses. It is recommended to connect by using a Private network address. Before you use a local application to access MySQL instances, you should first request a public address for MySQL instances.

The RDS for MySQL instance uses port 3306 by default. You can modify the connection address prefix and port of a MySQL instance. If necessary, refer to [Modifying the connection address prefix and port](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_address_prefix_and_port).

### Procedure

Complete the following operations based on the location where the client program is deployed.

* Deploy the client on an [ECS instance](https://console.byteplus.com/ecs/instance) (recommended)

   1. Make sure that ECS instances and MySQL instances are in the same VPC network.

   2. Get the private IPv4 address of ECS instances.

   3. Add the private IPv4 address of ECS instances to the allowlist of MySQL instances. For more information on how to set allowlist, refer to [Setting allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_allowlists_to_instances).

   4. Complete the required configuration in the client application and connect to the instance.

* Deploy the client locally

   1. Apply for a public network address for the MySQL instance. For more information about how to apply for a public address, refer to [Enabling or disabling public network access](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_internet_access).

   2. Obtain the public IPv4 address of your local device.

   3. Add the public IPv4 address of the local device to the IP allowlists of the MySQL instance. For more information on how to set allowlist, refer to [Setting allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_allowlists_to_instances).

   4. Complete the configuration in the client program to connect to the instance.

## Connect to an instance using caching_sha2_password authentication

MySQL 8.0 and above versions use the caching_sha2_password authentication plugin, which uses a new encryption algorithm to verify login credentials. This plugin is applicable to both direct connection endpoints and database proxy endpoints. For users or IP addresses whose login credentials have not yet been cached by the server, the plugin performs stricter **full authentication**: the client must either send the plaintext password over a TLS channel or encrypt the password using the RSA public key of the MySQL server, after which the server decrypts it using the private key through asymmetric cryptography. For users who have previously logged in successfully, the plugin uses more efficient **fast authentication**.

### Prerequisites

When connecting to an instance that uses the caching_sha2_password plugin, whether through a direct connection endpoint or a database proxy endpoint, the client must meet at least one of the following prerequisites:

* TLS transmission (SSL encryption) is enabled. For more information, see [Enable SSL encryption](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_ssl_encryption).

* The client has locally cached the RSA public key of the MySQL server.

* The client supports retrieving the RSA public key from the server when establishing a connection.

> **tip**

* > When the client is allowed to retrieve the RSA public key from the server (for example, by setting allowPublicKeyRetrieval=true in Connector/J), it trusts the public key obtained during the connection process, which poses a risk of attacks in an untrusted network environment. This method is recommended only for trusted private networks. In production environments, prefer SSL encryption or a local public key file.

* > You can retrieve the RSA public key from the server by executing the `SHOW STATUS LIKE 'Caching_sha2_password_rsa_public_key';` statement. Save the public key as a local file in PEM format (for example, `mysql_server_public_key.pem`), and then specify the file path in the client connection parameters. However, when connecting through a database proxy, ensure that you retrieve the public key of the primary node. If the instance undergoes a primary and secondary switch, you must retrieve the public key again.

### Connection example

The following examples show how to configure clients for different programming languages. In the examples, replace `{ip}`, `{port}`,` {db}`, `{user}`, and `{password}`, respectively, with the actual connection endpoint (a direct connection endpoint or a database proxy endpoint), port, database name, account, and password of the instance.

#### **Java (MySQL Connector/J) connection example**

When SSL is not enabled, set `allowPublicKeyRetrieval=true` to allow the client to retrieve the public key from the server:

```Plain Text
import java.sql.Connection;
import java.sql.DriverManager;

public class MysqlJdbcDemo {
    public static void main(String[] args) throws Exception {
        String url = "jdbc:mysql://{ip}:{port}/{db}"
                + "?sslMode=DISABLED"
                + "&allowPublicKeyRetrieval=true";

        try (Connection conn = DriverManager.getConnection(url, "{user}", "{password}")) {
            System.out.println("connected");
        }
    }
}

 // 连接串示例  
 jdbc:mysql://{ip}:{port}/your_db?sslMode=DISABLED&allowPublicKeyRetrieval=true
```

#### **C# (MySQL Connector/NET) connection example**

* Allow the client to retrieve the public key from the server.

   ```C#
   using MySql.Data.MySqlClient;
   
   var cs = "Server={ip};"
          + "Port={port};"
          + "Database={db};"
          + "User ID={user};"
          + "Password={password};"
          + "SslMode=None;"
          + "AllowPublicKeyRetrieval=True;";
   
   using var conn = new MySqlConnection(cs);
   conn.Open();
   
   Console.WriteLine("connected");
   ```

* Use the locally cached RSA public key file of the server.

   ```C#
   using MySql.Data.MySqlClient;
   
   var cs = "Server={ip};"
          + "Port={port};"
          + "Database={db};"
          + "User ID={user};"
          + "Password={password};"
          + "SslMode=None;"
          + "ServerRSAPublicKeyFile=/path/to/mysql_server_public_key.pem;";
   
   using var conn = new MySqlConnection(cs);
   conn.Open();
   
   Console.WriteLine("connected");
   ```

#### **C# (MySqlConnector) connection example**

* Allow the client to retrieve the public key from the server.

   ```C#
   using MySqlConnector.MySqlClient;
   
   var cs = "Server={ip};"
          + "Port={port};"
          + "Database={db};"
          + "User ID={user};"
          + "Password={password};"
          + "SslMode=None;"
          + "AllowPublicKeyRetrieval=True;";
   
   await using var conn = new MySqlConnection(cs);
   await conn.OpenAsync();
   
   Console.WriteLine("connected");
   ```

* Use the locally cached RSA public key file of the server.

   ```C#
   using MySqlConnector.MySqlClient;
   
   var cs = "Server={ip};"
          + "Port={port};"
          + "Database={db};"
          + "User ID={user};"
          + "Password={password};"
          + "SslMode=None;"
          + "ServerRSAPublicKeyFile=/path/to/mysql_server_public_key.pem;";
   
   await using var conn = new MySqlConnection(cs);
   await conn.OpenAsync();
   
   Console.WriteLine("connected");
   ```

#### **C (MySQL C API / libmysqlclient) connection example**

* Retrieve the public key from the server using the `MYSQL_OPT_GET_SERVER_PUBLIC_KEY` option.

   ```C++
   #include <mysql.h>
   #include <stdio.h>
   #include <stdlib.h>
   
   int main(void) {
       MYSQL *mysql = mysql_init(NULL);
       if (mysql == NULL) {
           return 1;
       }
   
       unsigned int get_server_public_key = 1;
       mysql_options(mysql, MYSQL_OPT_GET_SERVER_PUBLIC_KEY, &get_server_public_key);
   
       if (mysql_real_connect(
               mysql,
               "{ip}",
               "{user}",
               "{password}",
               "{db}",
               3306,
               NULL,
               0) == NULL) {
           fprintf(stderr, "connect failed: %s\n", mysql_error(mysql));
           mysql_close(mysql);
           return 1;
       }
   
       printf("connected\n");
       mysql_close(mysql);
       return 0;
   }
   ```

* Specify the locally cached RSA public key file of the server using the `MYSQL_SERVER_PUBLIC_KEY` option.

```C++
const char *pubkey = "/path/to/mysql_server_public_key.pem";
mysql_options(mysql, MYSQL_SERVER_PUBLIC_KEY, pubkey);
```
