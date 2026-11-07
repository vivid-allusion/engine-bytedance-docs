---
title: "Code examples"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/code_examples_4"
---

The code examples for the RDS for MySQL JAVA SDK in this topic are for reference only.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The [download and installation](https://docs.byteplus.com/en/docs/RDS_for_MySQL/download_and_installation_4) of the SDK is completed.

* [Client initialization](https://docs.byteplus.com/en/docs/RDS_for_MySQL/client_initialization_4) is completed.


<span id=".6K-35rGC6LaF5pe25pe26Ze06K6-572u"></span>
## Configure the request timeout

By default, there is no timeout limit when you use the SDK to call MySQL APIs. When you make an API call, you can add the `_request_timeout` parameter at the end of the code to specify the request timeout in seconds. If the request does not complete within this period, it terminates and a timeout error is reported. For example, when you call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API, you can use the following code to set the timeout to 10 seconds.

```java
public static ApiClient apiClient = new ApiClient()
        .setCredentials(Credentials.getCredentials(ak,sk))
        .setRegion(region)
        .setConnectTimeout(10);
```


<span id=".5Yib5bu6LW15c3FsLeWunuS-iw=="></span>
## Create a MySQL instance

For the definitions, value ranges, and other information about the parameters used in the following SDK code, refer to [CreateDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbinstance1).

```java
package org.example;

import com.volcengine.*;
import com.volcengine.rdsmysqlv2.RdsMysqlV2Api;
import com.volcengine.rdsmysqlv2.model.*;
import com.volcengine.sign.Credentials;
import java.util.ArrayList;
import java.util.List;

public class Main {
    // 设置 AKSK 验证信息及 Region
    public static String ak = "Your AK";
    public static String sk = "Your SK";
    public static String region = "Your Region";

    // 创建 RDS MySQL SDK 客户端，后续可以利用此客户端调用 API 执行任务请求
    public static ApiClient apiClient = new ApiClient()
            .setCredentials(Credentials.getCredentials(ak, sk))
            .setRegion(region)
            .setConnectTimeout(10);
    public static RdsMysqlV2Api rdsmysqlv2api = new RdsMysqlV2Api(apiClient);

    // 创建一个接口入参，并根据需要调用接口的参数说明配置来设置接口入参
    public static void main(String[] args) throws Exception {
        CreateDBInstanceRequest request = new CreateDBInstanceRequest();
        request.setDbEngineVersion("MySQL_Community_5_7");
        request.setStorageType("LocalSSD");
        request.setStorageSpace(20);
        request.setVpcId("vpc-*");
        request.setSubnetId("subnet-*");

        List<NodeInfoForCreateDBInstanceInput> nodesInfo = new ArrayList<>();
        NodeInfoForCreateDBInstanceInput primaryNodeInfo = new NodeInfoForCreateDBInstanceInput();
        primaryNodeInfo.setNodeType("Primary");
        primaryNodeInfo.setZoneId("cn-beijing-a");
        primaryNodeInfo.setNodeSpec("rds.mysql.1c2g");

        NodeInfoForCreateDBInstanceInput secondaryNodeInfo = new NodeInfoForCreateDBInstanceInput();
        secondaryNodeInfo.setNodeType("Secondary");
        secondaryNodeInfo.setZoneId("cn-beijing-a");
        secondaryNodeInfo.setNodeSpec("rds.mysql.1c2g");

        nodesInfo.add(primaryNodeInfo);
        nodesInfo.add(secondaryNodeInfo);
        request.setNodeInfo(nodesInfo);

        ChargeInfoForCreateDBInstanceInput chargeInfo = new ChargeInfoForCreateDBInstanceInput();
        chargeInfo.setChargeType("PostPaid");
        request.setChargeInfo(chargeInfo);

        // 调用接口完成接口所对应的操作
        try {
            CreateDBInstanceResponse response = rdsmysqlv2api.createDBInstance(request);
            System.out.println(response);
        } catch (ApiException e) {
            System.out.println(e.getResponseBody());
        }
    }
}
```


The following table describes the parameters in this example.


|Configuration item |Description |Value |
|---|---|---|
|DBEngineVersion |Instance name. |Your Instance Name |
|NodeInfo |The specifications of the instance. |[<br><br>{<br><br>"NodeType": "Primary",<br><br>"ZoneId": "cn\-beijing\-a",<br><br>"NodeSpec": "rds.mysql.1c2g"<br><br>},<br><br>{<br><br>"NodeType": "Secondary",<br><br>"ZoneId": "cn\-beijing\-a",<br><br>"NodeSpec": "rds.mysql.1c2g"<br><br>},<br><br>{<br><br>"NodeType": "ReadOnly",<br><br>"ZoneId": "cn\-beijing\-a",<br><br>"NodeSpec": "rds.mysql.1c2g"<br><br>}<br><br>] |
|StorageType |The storage type of the instance. |LocalSSD |
|StorageSpace |The storage space for the instance. |100 |
|VpcId |Proprietary network (VPC) ID. |vpc\-\*\*\*\* |
|SubnetId |Subnet ID. |Subnet123456 |
|InstanceName |Instance name. |Your Instance Name |
|SuperAccountName |Super account name. |Test1 |
|SuperAccountPassword |Password for the super account. |Test@123456 |
|LowerCaseTableNames |Whether table names are case sensitive. |1 |
|DBTimeZone |Time zone. |UTC +08:00 |
|DBParamGroupId |Parameter templates ID. |ParamGroup123456 |
|ProjectName |The project to which the instance belongs. |Test |
|ChargeInfo |Billing method. |{<br><br>"ChargeType": "PostPaid"<br><br>} |
|InstanceTags |Instance tag. |{<br><br>"Key": ""aa,<br><br>"Value":"aa"<br><br>} |
|Number |The number of instances to purchase. |1 |


<span id=".5p-l6K-iLW15c3FsLeWunuS-i-S_oeaBrw=="></span>
## Query MySQL instance summary

For the definitions, value ranges, and other information about the parameters used in the following SDK request, refer to [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances).

```java
package org.example;

import com.volcengine.*;
import com.volcengine.rdsmysqlv2.RdsMysqlV2Api;
import com.volcengine.rdsmysqlv2.model.DescribeDBInstanceDetailRequest;
import com.volcengine.rdsmysqlv2.model.DescribeDBInstanceDetailResponse;
import com.volcengine.sign.Credentials;

public class Main {
    // 设置 AKSK 验证信息及 Region
    public static String ak = "Your AK";
    public static String sk = "Your SK";
    public static String region = "Your Region";

    // 创建一个 MySQL SDK 客户端，后续可以利用此客户端调用 API 执行任务请求
    public static ApiClient apiClient = new ApiClient()
            .setCredentials(Credentials.getCredentials(ak, sk))
            .setRegion(region);
    public static RdsMysqlV2Api rdsmysqlv2api = new RdsMysqlV2Api(apiClient);

    // 创建一个接口入参，并根据需要调用接口的参数说明配置来设置接口入参
    public static void main(String[] args) throws Exception {
        DescribeDBInstanceDetailRequest request = new DescribeDBInstanceDetailRequest();

        // 调用接口完成接口所对应的操作
        try {
            DescribeDBInstanceDetailResponse response = rdsmysqlv2api.describeDBInstanceDetail(request);
            System.out.println(response);
        } catch (ApiException e) {
            System.out.println(e.getResponseBody());
        }
    }
}
```


&nbsp;
