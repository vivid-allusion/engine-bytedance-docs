---
title: "Connecting to Redis from client via SSL encryption"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/connect-redis-from-client-via-ssl"
---

Cache for Redis provides SSL (Secure Sockets Layer) encryption service. You can enable SSL encryption in advance, and improve the security of the data link by setting SSL encryption when connecting to the database. This topic describes the specific methods for multilingual clients to access Redis databases via SSL encrypted connections.

## Precautions

Accessing Redis instances through a private network is relatively secure, and typically requires no data link encryption. Using SSL encryption connection can increase the network response time of Redis services. We recommend that you enable SSL encryption only when necessary (such as when connecting to Redis instances via the internet).

## Preparation

Before connecting to Redis via SSL encryption at client, you should make the following preparations.

|Preparation |Description |
|---|---|
|Setting SSL encryption for Redis |Enable SSL encryption for the target Redis instance and download the SSL CA certificate. For specific procedures, refer to [Setting SSL encryption](https://docs.byteplus.com/en/docs/redis/setup-ssl). |
|Setting allowlist for Redis |Add the IP address of the local server or ECS instance with the client installed to the allowlist of the Redis instance. For specific procedures, refer to [Setting allowlist](https://docs.byteplus.com/en/docs/redis/set-allowlist).<br><br>> **tip**<br><br><br>> If your client device and Redis instance are not in the same VPC, you also need to enable public network access for the Redis instance. For specific procedures, refer to [Applying for public address](https://docs.byteplus.com/en/docs/redis/apply-public-address).<br> |
|Obtain database username information |Refer to the following steps to obtain the database login username and password for Cache for Redis:<br><br><br>* **Username**<br><br>   To ensure data security, a default username will be automatically created after the instance is created. You can also create a new username and set the permissions for it according to your service requirements. For more information, refer to [Creating and managing account](https://docs.byteplus.com/en/docs/redis/manage-account).<br><br>* **Password**<br><br>   Redis supports passwords in the following formats:<br><br>   * Enter the password directly (this method is only available with the default account).<br><br>   * `<username> <password>`.<br><br>   * `<username>:<password>`.<br><br>   > **tip**<br>   <br><br>   > If you forget your password, you can reset it. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password).<br>    |
|Obtain database connection information |You can follow these steps to obtain the connection address and port number information for Cache for Redis:<br><br><br>1. Log in to the [Redis console](https://console.byteplus.com/db/redis).<br><br>2. In the top menu bar, select the project and region to which the instance belongs.<br><br>3. On the Instances page, click the target instance.<br><br>4. On the instance details page, click the Connectivity tab to view the corresponding connection address and port number information in the Private network access or Public network access section.<br><br><br>> **tip**<br><br><br>> For more information about Redis connection addresses, refer to [Address types](https://docs.byteplus.com/en/docs/redis/view-address).<br> |

## Examples of client SSL connection

> **tip**

> For more details about the usage instructions of the third\-party SDK client program, refer to [Instructions for using third\-party SDK clients](https://docs.byteplus.com/en/docs/redis/instructions-for-third-party-sdk-clients).

**Java**

> **tip**

> The steps below are illustrated using [Jedis](https://github.com/redis/jedis) client version 3.6.0 as an example. Recommend using the latest version.

```Java
import java.io.FileInputStream;
import java.io.InputStream;
import java.security.KeyStore;
import java.security.SecureRandom;

import javax.net.ssl.SSLContext;
import javax.net.ssl.SSLSocketFactory;
import javax.net.ssl.TrustManager;
import javax.net.ssl.TrustManagerFactory;

import org.apache.commons.pool2.impl.GenericObjectPoolConfig;
import redis.clients.jedis.Jedis;
import redis.clients.jedis.JedisPool;

public class JedisSSLTest {
    private static SSLSocketFactory createTrustStoreSSLSocketFactory(String jksFile) throws Exception {
        KeyStore trustStore = KeyStore.getInstance("jks");
        InputStream inputStream = null;
        try {
            inputStream = new FileInputStream(jksFile);
            trustStore.load(inputStream, null);
        } finally {
            inputStream.close();
        }

        TrustManagerFactory trustManagerFactory = TrustManagerFactory.getInstance("PKIX");
        trustManagerFactory.init(trustStore);
        TrustManager[] trustManagers = trustManagerFactory.getTrustManagers();

        SSLContext sslContext = SSLContext.getInstance("TLS");
        sslContext.init(null, trustManagers, new SecureRandom());
        return sslContext.getSocketFactory();
    }

    public static void main(String[] args) throws Exception {
        // redis-shzl8lsda9uaa****_ca_certificate.jks is the certificate file name.
        final SSLSocketFactory sslSocketFactory = createTrustStoreSSLSocketFactory("redis-shzl8lsda9uaa****_ca_certificate.jks");
        // The connection pool settings are the instance's connection address, port number, timeout settings, and password.
        JedisPool pool = new JedisPool(new GenericObjectPoolConfig(), "redis-shzl8lsda9uaa****.redis.ibytepluses.com",
            6379, 2000, "SslTest:Pwd@1234", 0, true, sslSocketFactory, null, null);

        try (Jedis jedis = pool.getResource()) {
            jedis.set("key", "value");
            System.out.println(jedis.get("key"));
        }
    }
}
```

**Python**

> **tip**

> The steps below are illustrated using [redis\-py](https://github.com/andymccurdy/redis-py) client as an example. Recommend using the latest version.

* Connection to the connection pool

   ```Python
   #!/bin/pythonimport redis
   
   # Set up a connection pool, and replace the host, port, and password values with the address, port number, and password of the instance, respectively.
   # redis-shzl8lsda9uaa****_ca_certificate.pem is the certificate file name.
   pool = redis.ConnectionPool(connection_class=redis.connection.SSLConnection, max_connections=100,
                               host="redis-shzl8lsda9uaa****.redis.ibytepluses.com", port=6379, password="SslTest:Pwd@1234",
                               ssl_cert_reqs=True, ssl_ca_certs="redis-shzl8lsda9uaa****_ca_certificate.pem")
   client = redis.Redis(connection_pool=pool)
   client.set("hi", "redis")
   print client.get("hi")
   ```

* Regular connection

   ```Python
   #!/bin/python
   import redis
   
   # Set connection information, and replace the host, port, and password values with the address, port number, and password of the instance, respectively.
   # redis-shzl8lsda9uaa****_ca_certificate.pem is the certificate file name.
   client = redis.Redis(host="redis-shzl8lsda9uaa****.redis.ibytepluses.com", port=6379,
                        password="SslTest:Pwd@1234", ssl=True,
                       ssl_cert_reqs="required", ssl_ca_certs="redis-shzl8lsda9uaa****_ca_certificate.pem")
   
   client.set("hello", "world")
   print client.get("hello")
   ```

**PHP**

> **tip**

* > The steps below are illustrated using [predis](https://github.com/predis/predis) client as an example. Recommend using the latest version.

* > If you are using the [phpredis](https://github.com/phpredis/phpredis) client, refer to [SSL/TLS with certification file](https://github.com/phpredis/phpredis/issues/1600) for a connection example.

```PHP
<?php require __DIR__.'/predis/autoload.php';

/* Set connection information, and replace the host, port, and password values with the address, port number, and password of the instance, respectively.
 redis-shzl8lsda9uaa****_ca_certificate.pem is the certificate file name. */
 $client = new Predis\Client([
    'scheme' => 'tls',
    'host'   => 'redis-shzl8lsda9uaa****.redis.ibytepluses.com',
    'port'      =>  6379,
    'password'  =>  'SslTest:Pwd@1234',
    'ssl'        => ['cafile'  =>  'redis-shzl8lsda9uaa****_ca_certificate.pem',  'verify_peer'  =>  true,  'verify_peer_name'  =>  false],
]);
$client->set("hello", "world");
print $client->get("hello")."\n";
```

**GO**

> **tip**

> The steps below are illustrated using [go\-redis](https://github.com/redis/go-redis) client as an example. Recommend using the latest version.

```Go
package main

import (
    "crypto/tls"
    "crypto/x509"
    "fmt"
    "io/ioutil"

    "github.com/go-redis/redis"
)

func main() {

    // redis-shzl8lsda9uaa****_ca_certificate.pem is the certificate file name.
    bytes, err := ioutil.ReadFile("redis-shzl8lsda9uaa****_ca_certificate.pem")
    if err != nil {
       fmt.Printf("err:%v\n", err)
       return
    }
    pool := x509.NewCertPool()
    pool.AppendCertsFromPEM(bytes)
    tlsConfig := &tls.Config{
       RootCAs: pool,
       // Hostname for certificate validation; a private network address is sufficient.
       ServerName:         "redis-shzl8lsda9uaa****.redis.ibytepluses.com",
    }
    // Instance connection address.
    addr := "redis-shzl8lsda9uaa****.redis.ibytepluses.com"
    // Instance password.
    password := "SslTest:Pwd@1234"
    client := redis.NewClient(&redis.Options{
       Addr:      addr,
       TLSConfig: tlsConfig,
       Password:  password,
    })

    err = client.Set("hello", "world", 0).Err()
    if err != nil {
       fmt.Printf("err:%v\n", err)
       return
    }
    val, err := client.Get("hello").Result()
    if err != nil {
       fmt.Printf("err:%v\n", err)
       return
    }
    fmt.Printf("val:%s\n", val)
}
```
