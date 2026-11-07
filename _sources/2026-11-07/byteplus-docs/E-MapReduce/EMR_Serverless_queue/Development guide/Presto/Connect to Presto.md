---
title: "Connect to Presto"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Connect_Presto"
---

<span id="b74b2c13"></span>
# Java JDBC

<span id="4e597e64"></span>
## Environment preparation


* Dependency: JDK1.8

* JDBC Driver download: [Click to download the driver](https://serverless-spark.tos-cn-beijing.volces.com/presto/driver/emr-presto-jdbc-1.0.0.jar)


<span id="e5c54fc9"></span>
## Connect to Presto queue


1. Load the EMR Serverless Presto JDBC driver.

   ```Java
   Class.forName("com.facebook.presto.jdbc.PrestoDriver");
   ```
   

2. Create an EMR Serverless Presto connection.

   ```Java
   // The default value of las_queue_name is public-queue-presto, which is the Presto public queue
   String url = "jdbc:presto://${endpoint}:8080/${Catalog}/${Schema}?region=cn-beijing&sessionProperties=presto_queue_name:${your-queue-name};compute_group_name:${your-compute-group-name}" 
   
   Properties properties = new Properties();
   properties.setProperty("user", ${User});
   properties.setProperty("password", ${Password});
   Connection connection = DriverManager.getConnection(url, properties);
   ```
   

3. Note on JDBC connection string parameters.

   
   |Parameters |Required |Note |
   |---|---|---|
   |JDBC service address |Yes |EMR Serverless Presto JDBC service:<br><br><br>* Johor: 45.78.197.8<br><br>* Jakarta: 69.5.14.121 |
   |Catalog |Yes |Catalog name. Can be hive, hudi, iceberg, or delta. |
   |Schema |Yes |Database name |
   |region |Yes |The region where the EMR Serverless Presto service is deployed currently supports ap\-southeast\-1. Please specify according to your actual region. |
   |user |Yes |Access Key ID in Volcengine API key management |
   |password |Yes |Secret Access Key in Volcengine API key management |
   |presto_queue_name |No |Name of the queue where EMR Serverless Presto is located. The default value is the public queue: public\-queue\-presto |
   |compute_group_name |No |Name of the compute group where EMR Serverless Presto is located |
   

4. Complete code sample for querying data.

   ```Java
   import com.facebook.presto.jdbc.PrestoStatement;
   import java.sql.Connection;
   import java.sql.DriverManager;
   import java.sql.ResultSet;
   import java.util.Properties;
    
   public void demo() {
       try {
           Class.forName("com.facebook.presto.jdbc.PrestoDriver");
       } catch (ClassNotFoundException e) {
           System.out.println("Failed to load Presto JDCB driver...");
           return;
       }
   
       final String ak = "Access Key ID in Volcengine API key management";
       final String sk = "Secret Access Key in Volcengine API key management";
       final String jdbcUrl = "jdbc:presto://${endpoint}:8080/hive/serverless_presto_schema?region=ap-southeast-1";
       Properties properties = new Properties();
       properties.setProperty("user", ak);
       properties.setProperty("password", sk);
       try (PrestoConnection connection = (PrestoConnection) DriverManager.getConnection(url, properties)) {
           ResultSet resultSet = connection.createStatement().executeQuery("select name from serverless_presto_table");
           while (resultSet.next()) {
               System.out.println(resultSet.getString(1));
           }
       }
       catch (Exception e) {
           e.printStackTrace();
       }
   }
   ```
   

5. Compile and run the code.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After compiling the above code, you can submit the JAR package to the server for execution.   </div>
   

<span id="20980913"></span>
# Python JDBC

<span id="a57ab110"></span>
## Method 1: Pyhive

```Python
# -*- coding: utf-8 -*-
import requests
from pyhive import presto

if __name__ == "__main__":
    ak = 'xxxxxxxx'
    sk = 'xxxxxxxx'

    request_session = requests.Session()
    request_session.headers.update({
        'X-Presto-Extra-Credential':  f"access_key_id={ak},secret_access_key={sk}"  # Set authentication information
    })

    presto_config = {
        'presto_queue_name': 'xxx',
        'compute_group_name': 'xxx'
    }
    host = 'xxxxx'
    conn = presto.connect(host, port='8080', username = 'xxx', session_props=presto_config, requests_session=request_session)
    cur = conn.cursor()
    query = 'select 1'
    cur.execute(query)
    result = cur.fetchall()
    for row in result:
        print(row)
```


<span id="8a7caa65"></span>
## Method 2: Prestodb

```Python
import prestodb

ak = 'xxx'
sk = 'xxxx'

if __name__ == '__main__':
    headers = {'X-Presto-Extra-Credential':  f"access_key_id={ak},secret_access_key={sk}"}
    conn=prestodb.dbapi.connect(
        host='xxx',
        port=8080,
        user='xxx',
        catalog='xxx',
        schema='xxx',
        http_headers=headers,
        session_properties={
            'presto_queue_name': 'xxxx',
            'compute_group_name': 'xxxx'
        }
    )
    cur = conn.cursor()
    cur.execute('select 1')
    rows = cur.fetchall()
    for row in result:
        print(row)
```


<span id="5151f464"></span>
# Go Client

```Go
package main

import (
        "database/sql"
        "fmt"
        "log"
        "net/http"

        "github.com/prestodb/presto-go-client/presto"
)

type prestoRT struct {
        base http.RoundTripper
}

func (r *prestoRT) RoundTrip(req *http.Request) (*http.Response, error) {
        req.Header.Set("X-Presto-User", "abc")
        req.Header.Set(
                "X-Presto-Extra-Credential",
                "access_key_id=youraccesskey,secret_access_key=yoursecretKey",
        )
        req.Header.Add("X-Presto-Session", "presto_queue_name=yourqueuename")
        req.Header.Add("X-Presto-Session", "compute_group_name=yourcomputegroupname")

        return r.base.RoundTrip(req)
}

func main() {
        httpClient := &http.Client{
                Transport: &prestoRT{
                        base: http.DefaultTransport,
                },
        }
        
        dsn := "http://xxxx:8080?catalog=xxx&schema=xxx&custom_client=my_custom_client"

        presto.RegisterCustomClient("my_custom_client", httpClient)
        db, err := sql.Open("presto", dsn)
        if err != nil {
                log.Fatalf("open presto failed: %v", err)
        }
        defer db.Close()

        rows, err := db.Query("SHOW CATALOGS")
        if err != nil {
                log.Fatalf("query failed: %v", err)
        }
        defer rows.Close()

        for rows.Next() {
                var catalog string
                if err := rows.Scan(&catalog); err != nil {
                        log.Fatalf("scan failed: %v", err)
                }
                fmt.Println("catalog =", catalog)
        }
}
```


Usage process:


1. Create an HTTP client based on a custom interceptor and register it in the Presto client list

2. Construct a DSN connection string: specify the Presto service address, default catalog, default schema, and associate the custom HTTP client

3. Operate Presto using the standard Go `database/sql` interface: the example executes a `SHOW CATALOGS` query and prints the returned result


You need to modify the parameters according to your actual situation: `accesskey`, `secretKey`, queue name, compute group name, Presto service address, catalog, schema.
