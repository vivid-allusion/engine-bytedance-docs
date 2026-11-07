---
title: "Use HTTP interface to connect to ByteHouse"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/use-http-interface-to-connect-to-bytehouse"
---

The HTTP interface supports the use of ByteHouse on any platform in any programming language through the REST API. This article introduces how to connect to ByteHouse using the HTTP method.

<span id="2a39adad"></span>
# Prerequisites

Ensure you have installed curl. For details, refer to [the official website](https://curl.se/download.html).

<span id="e7c47af0"></span>
# Connect to ByteHouse

You can connect to ByteHouse using the following command.

```Shell
curl "https://<domain>:8123?user=bytehouse&password=${APItoken}"
```



|Parameter |Configuration |
|---|---|
| |Configure the host information for ByteHouse. You can obtain public or private domain name information in ByteHouse Console's **Tenant management** \> **Basic information** \> **Network information**. The format for `<domain>` is as follows:<br><br><br>* Private Network: `tenant-{TENANT_ID}-{REGION}[-{ENVIRONMENT}].bytehouse.ibytepluses.com`<br><br>* Public Network: `tenant-{TENANT_ID}-{REGION}[-{ENVIRONMENT}]-public.bytehouse.bytepluses.com`<br><br><br>`{ENVIRONMENT}` is optional, if using the default environment, it does not need to be filled; if specifying another environment, add this parameter . |
|user |Username for logging into the ByteHouse database, configured as bytehouse. |
|password |Password for logging into the ByteHouse database, configured as ByteHouse's <API_Key\>, which can be obtained in the **Tenant management** \> **Connection information** on the ByteHouse console. For more details, refer to [Retrieve API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d9bd3430). |


<span id="9a242d08"></span>
# Examples

You can connect to ByteHouse via HTTP and manage data. This section uses table `t` as an example, demonstrating how to create, write, query, and delete tables. Replace the `domain`, `api_token`, and query statements according to your environment information and business needs in actual use.

<span id="a5713616"></span>
## Create table

```Bash
echo 'CREATE TABLE t (a UInt8) ENGINE = 'CnchMergeTree' ORDER BY a' | curl 'https://<domain>:8123?user=bytehouse&password=<api_token>&' --data-binary @- 
```


<span id="27022e24"></span>
## Write data

You can insert data via INSERT query.

```Bash
echo 'INSERT INTO t VALUES (1),(2),(3)' | curl 'https://<domain>:8123?user=bytehouse&password=<api_token>&' --data-binary @- 
```


You can also send data separately from the query.

```Bash
echo '(4),(5),(6)' | curl 'https://<domain>:8123?user=bytehouse&password=<api_token>&query=INSERT%20INTO%20t%20VALUES' --data-binary @- 
```


You can specify any data format. For example, the 'Values' format, the same format as the one used when writing `INSERT INTO t VALUES`, can be specified as follows.

```Bash
echo '(7),(8),(9)' | curl 'https://<domain>:8123?user=bytehouse&password=<api_token>&query=INSERT%20INTO%20t%20FORMAT%20Values' --data-binary @- 
```


To insert data from a tab\-separated dump, specify the corresponding format.

```Bash
echo -ne '10\n11\n12\n' | curl 'https://<domain>:8123?user=bytehouse&password=<api_token>&query=INSERT%20INTO%20t%20FORMAT%20TabSeparated' --data-binary @- 
```


You can use the following commands to insert data via a CSV file.

```Bash
curl "https://<domain>:8123?user=bytehouse&password=<api_token>&query=INSERT%20INTO%20t%20FORMAT%20CSV" --data-binary @data.csv 
```


<span id="d441f28a"></span>
## Query data

```Bash
curl 'https://<domain>:8123/?user=bytehouse&password=<api_token>&query=SELECT%20a%20FROM%20t' 
```


<span id="68787687"></span>
## Delete table

```Bash
$ echo 'DROP TABLE t' | curl 'http://<domain>:8123/' --data-binary @- 
```


<span id="a9c2d1af"></span>
## Optimize output style using the format parameter

You can use `format Pretty` to optimize the style of your query results.

```Shell
curl "https://<domain>:8123?query=select%20100%20format%20Pretty&user=bytehouse&password=${APItoken}" 
```


You can also use `format JSON` to output query results in JSON format.

```Shell
curl "https://<domain>:8123?query=select%20100%20format%20JSON&user=bytehouse&password=${APItoken}" 
```


&nbsp;
