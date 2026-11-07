---
title: "Code examples"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Java_SDK_code_example"
---

The code examples for the RDS for SQL Server Java SDK provided in this topic are for reference only.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have downloaded and installed the SDK. For details, see [Download and installation](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Download_and_Installation).

* You have initialized the client. For details, see [Client initialization](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Initialize_a_Client).


<span id=".6K-35rGC6LaF5pe25pe26Ze06K6-572u"></span>
## **Set request timeout**

By default, there is no timeout limit when you use the SDK to call SQL Server API operations. You can specify a request timeout in milliseconds by adding the `_request_timeout` parameter to your API call. If the request does not complete within the specified time, it terminates and reports a timeout error. For example, you can use the following code to set the timeout to 10 seconds when calling the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances) API operation.

```Java
public static ApiClient apiClient = new ApiClient()
        .setCredentials(Credentials.getCredentials(ak,sk))
        .setRegion(region)
        .setConnectTimeout(10 * 1000);
```


<span id=".5Yib5bu6LXNxbC1zZXJ2ZXIt5a6e5L6L"></span>
## **Create an SQL Server instance**

For more information about the parameters in the following SDK code, including their definitions and value ranges, see [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createdbInstance).

```Java
package  org.example;

import com.byteplus.sign.Credentials;
import com.byteplus.ApiClient;
import com.byteplus.ApiException;
import com.byteplus.rdsmssql.model.ChargeInfoForCreateDBInstanceInput;
import com.byteplus.rdsmssql.model.CreateDBInstanceRequest;
import com.byteplus.rdsmssql.model.CreateDBInstanceResponse;
import com.byteplus.rdsmssql.RdsMssqlApi;

public class Main  {

    public static String ak = "Your AK";
    public static String sk = "Your SK";
    public static String region = "Your Region";

    public static ApiClient apiClient = new ApiClient()
                        .setCredentials(Credentials.getCredentials(ak,sk))
                        .setRegion(region);
    public static RdsmssqlApi rdsmssqlApi  = new RdsmssqlApi(apiClient);
    
    public static void main(String[] args)throws  Exception {
        CreateDBInstanceRequest request = new CreateDBInstanceRequest();
        request.dbEngineVersion("SQLServer_2019_Std");
        request.instanceType("HA");
        request.setZoneId("cn-beijing-a");
        request.setNodeSpec("rds.mssql.3il.s2.medium.s2");
        request.setStorageSpace(20);
        request.setVpcId("vpc-*");
        request.setSubnetId("subnet-*");
        request.setSuperAccountPassword("********");
        request.setDbTimeZone("China Standard Time");
        ChargeInfoForCreateDBInstanceInput chargeInfo = new ChargeInfoForCreateDBInstanceInput();
        chargeInfo.setChargeType("PostPaid");
        request.setChargeInfo(chargeInfo);
        try  {
            CreateDBInstanceResponse response = rdsmssqlApi.createDBInstance(request);
            System.out.println(response);
        } catch (ApiException e) {
            System.out.println(e.getResponseBody());
        }
    }
}
```


<span id=".5p-l6K-iLXNxbC1zZXJ2ZXIt5a6e5L6L5L-h5oGv"></span>
## **Query SQL Server instance information**

For more information about the parameters in the following SDK code, including their definitions and value ranges, see [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances).

```Java
package  org.example;

import  com.byteplus.*;
import  com.byteplus.rdsmssql.RdsmssqlApi;
import  com.byteplus.rdsmssql.model.*;
import  com.byteplus.sign.Credentials;

public class Main  {

    public static String ak = "Your AK";
    public static String sk = "Your SK";
    public static String region = "Your Region";

    public static ApiClient apiClient = new ApiClient()
                        .setCredentials(Credentials.getCredentials(ak,sk))
                        .setRegion(region);
    public static RdsmssqlApi rdsmssqlApi  = new RdsmssqlApi(apiClient);
    
    public static void main(String[] args)throws  Exception {
        DescribeDBInstancesRequest request = new DescribeDBInstancesRequest();
        request.setPageNumber(1);
        request.setPageSize(10);
        try  {
            DescribeDBInstanceDetailResponse response = rdsmssqlApi.describeDBInstanceDetail(request);
            System.out.println(response);
        } catch (ApiException e) {
            System.out.println(e.getResponseBody());
        }
    }
}
```
