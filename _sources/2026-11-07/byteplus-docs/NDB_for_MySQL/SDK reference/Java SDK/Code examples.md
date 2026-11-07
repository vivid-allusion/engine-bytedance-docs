---
title: "Code examples"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Code_examples_java"
---

This article introduces code examples of NDB for MySQL Java SDK for your reference.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The [Downloading and installing SDK](https://www.byteplus.com/en/docs/NDB_for_MySQL/Download_and_installation_java) has been completed.

* The [Initializing client](https://www.byteplus.com/en/docs/NDB_for_MySQL/Initializing_client_java) has been completed.


<span id=".6K-35rGC6LaF5pe25pe26Ze06K6-572u"></span>
## Request timed out time settings

There is no timeout setting by default when calling the interface with the Java SDK. When initializing the client, you can use `.setConnectTimeout(timeout)` to specify the client's request timeout. If the request is not completed within this time, the request will be terminated immediately and a timeout error will be reported. For example, you can set the client's request timed out to 10 seconds with the following code.

```java
ApiClient client = new ApiClient()
        .setCredentials(credentials)
        .setRegion(region)
        .setEndpoint(host)
        .setConnectTimeout(10);
```


<span id=".5Yib5bu6LXZlZGItbXlzcWwt5a6e5L6L"></span>
## Creating an instance

For a detailed description of the parameters in the following example, see [CreateDBInstance](https://www.byteplus.com/en/docs/NDB_for_MySQL/CreateDBInstance#请求参数).

```java
private String ConvertToJsonString(Object value) throws JsonProcessingException {
    DefaultPrettyPrinter.Indenter indenter = new DefaultIndenter("    ", DefaultIndenter.SYS_LF);
    DefaultPrettyPrinter defaultPrettyPrinter = new DefaultPrettyPrinter();
    defaultPrettyPrinter.indentObjectsWith(indenter);
    defaultPrettyPrinter.indentArraysWith(indenter);

    ObjectMapper mapper = new ObjectMapper();
    return mapper.writer(defaultPrettyPrinter).writeValueAsString(value);
}

public void TestCreateDBInstance() {
    CreateDBInstanceRequest req = new CreateDBInstanceRequest();
    req.setChargeType("PostPaid");
    req.setDbEngineVersion("MySQL_8_0");
    req.setDbTimeZone("UTC +08:00");
    req.setInstanceName("your instance name");
    req.setLowerCaseTableNames("0");
    req.setNodeNumber(2);
    req.setNodeSpec("vedb.mysql.x4.large");
    req.setSubnetId("your subnet id");
    req.setSuperAccountName("your super account name");
    req.setSuperAccountPassword("your super account password");
    req.setVpcId("your vpc id");
    req.setZoneIds("cn-beijing-b");

    try {
        CreateDBInstanceResponse resp = VeDBMClient.createDBInstance(req);
        System.out.println(ConvertToJsonString(resp));
    } catch (ApiException e) {
        System.out.println(e.getResponseBody());
    } catch (JsonProcessingException e) {
        throw new RuntimeException(e);
    }
}
```


<span id=".5p-l6K-iLXZlZGItbXlzcWwt5a6e5L6L"></span>
## Query instance information

```java
public void TestDescribeDBInstanceDetail() {
    DescribeDBInstanceDetailRequest req = new DescribeDBInstanceDetailRequest();
    req.setInstanceId("your instance id");

    try {
        DescribeDBInstanceDetailResponse resp = VeDBMClient.describeDBInstanceDetail(req);
        System.out.println(ConvertToJsonString(resp));
    } catch (ApiException e) {
        System.out.println(e.getResponseBody());
    } catch (JsonProcessingException e) {
        throw new RuntimeException(e);
    }
}
```
