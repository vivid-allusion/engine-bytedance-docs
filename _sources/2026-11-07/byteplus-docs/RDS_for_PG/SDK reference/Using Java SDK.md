---
title: "Using Java SDK"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/use_java_sdk"
---

This topic describes the download, installation, and client initialization of the PostgreSQL Java SDK for RDS for PostgreSQL.

<span id=".5LiL6L295LiO5a6J6KOF"></span>
## Download and install

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### **Prerequisites**

Prerequisites For more details, see [Java Downloads](https://www.oracle.com/java/technologies/downloads/).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can run the <code>java -version</code> command to check the version of the current Java.</div>


<span id=".U0RLIOS4i-i9veWcsOWdgA=="></span>
### **SDL download URL**

Java SDK source code address for RDS for PostgreSQL, see [SDK list](https://docs.byteplus.com/en/docs/RDS_for_PG/sdk_overview).

<span id=".5a6J6KOFIFNESw=="></span>
### **Install SDK**

Configure Maven project dependencies. Create a new Maven project and add the following settings in `pom.xml` in the project directory to introduce service dependencies. When a dependency is introduced, the Maven project management tool automatically downloads the relevant JAR package.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your Java JDK version is JDK 9 or later and you need to add additional <code>javax.annotation-api</code> dependencies, add the following in <code>pom.xml</code>.</div>


<div data-tips="true" data-tips-type="tip">```xml
<dependency>
  <groupId>javax.annotation</groupId>
  <artifactId>javax.annotation-api</artifactId>
  <version>1.3.2</version>
</dependency>
```
</div>


```xml
<dependency>
    <groupId>com.volcengine</groupId>
    <artifactId>volcengine-java-sdk-rdspostgresql</artifactId>
    <version>0.1.157</version>
</dependency>
```


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## Initialize client side

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* The Access Key ID (AK) and Secret Access Key (SK) information of the account have been obtained. For specific operations, refer to [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).

* For Regions supported by RDS for PostgreSQL, see[ service address](https://docs.byteplus.com/en/docs/RDS_for_PG/request_structure#.5pyN5Yqh5Zyw5Z2A).

* The RDS for PostgreSQL Java SDK has been downloaded and installed. For specific steps, see [Download and Install](https://docs.byteplus.com/en/docs/RDS_for_PG/use_java_sdk#.5LiL6L295LiO5a6J6KOF).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
### Initialize client

Initialize the client with the following code.

```java
package org.example;

import com.volcengine.*;
import com.volcengine.sign.Credentials;
import com.volcengine.rdspostgresql.RdsPostgresqlApi;
import com.volcengine.rdspostgresql.model.*;

public class Main {
    // Set AKSK authentication information and Regionpublic static String ak = "Your AK";
    public static String sk = "Your SK";
    public static String region = "Your Region";
    public static String host = "Your Host";
    //Create an RDS for PostgreSQL SDK client, which can be used to call the API to perform task requests later public static ApiClient apiClient = new ApiClient()
            .setCredentials(Credentials.getCredentials(ak, sk))
            .setRegion(region)
            .setEndpoint(host);
    public static RdsPostgresqlApi rdsPostgresql = new RdsPostgresqlApi(apiClient);
}
```


<span id=".5Luj56CB56S65L6L"></span>
## Sample

<span id=".6K-35rGC6LaF5pe25pe26Ze06K6-572u"></span>
### Request timed out time settings

When calling the PostgreSQL interface with the SDK, there is no timeout limit by default. You can specify a timeout (in seconds) for the request by adding a `_request_timeout` parameter at the end of the code when initiating an interface call request. If the request is not completed within this time, the request will terminate with a timeout error. For example, you can set the timeout to 10 seconds with the following code when calling the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) interface.

```java
public static ApiClient apiClient = new ApiClient()
        .setCredentials(Credentials.getCredentials(ak,sk))
        .setRegion(region)
        .setConnectTimeout(10);
```


<span id=".5Yib5bu6IFBvc3RncmVTUUwg5a6e5L6L"></span>
### Creating PostgreSQL instance

For information about the definition, range, and other parameters used in the following SDK code, see [CreateDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance).

```java
package org.example;

import com.volcengine.*;
import com.volcengine.sign.Credentials;
import com.volcengine.rdspostgresql.RdsPostgresqlApi;
import com.volcengine.rdspostgresql.model.*;
import java.util.ArrayList;
import java.util.List;

public class Main {
    // Set AKSK authentication information and Regionpublic static String ak = "Your AK";
    public static String sk = "Your SK";
    public static String region = "Your Region";
    public static String host = "Your Host";
    //Create an RDS for PostgreSQL SDK client, which can be used to call the API to perform task requests later public static ApiClient apiClient = new ApiClient()
            .setCredentials(Credentials.getCredentials(ak, sk))
            .setRegion(region)
            .setEndpoint(host)
            .setConnectTimeout(10);
    public static RdsPostgresqlApi rdsPostgresql = new RdsPostgresqlApi(apiClient);
    
    //Create an interface imported parameter, and set the interface imported parameter according to the parameter description configuration of the interface that needs to be called public static void main(String[] args) throws Exception {
        List<NodeInfoForCreateDBInstanceInput> nodesInfo = new ArrayList<>();
        NodeInfoForCreateDBInstanceInput primaryNodeInfo = new NodeInfoForCreateDBInstanceInput();
        primaryNodeInfo.setNodeType("Primary");
        primaryNodeInfo.setZoneId("cn-beijing-c");
        primaryNodeInfo.setNodeSpec("rds.postgres.1c2g");
        NodeInfoForCreateDBInstanceInput secondaryNodeInfo = new NodeInfoForCreateDBInstanceInput();
        secondaryNodeInfo.setNodeType("Secondary");
        secondaryNodeInfo.setZoneId("cn-beijing-c");
        secondaryNodeInfo.setNodeSpec("rds.postgres.1c2g");
        nodesInfo.add(primaryNodeInfo);
        nodesInfo.add(secondaryNodeInfo);
        
        ChargeInfoForCreateDBInstanceInput chargeInfo = new ChargeInfoForCreateDBInstanceInput();
        chargeInfo.setChargeType("PostPaid");
        
        CreateDBInstanceRequest request = new CreateDBInstanceRequest();
        request.setInstanceName("pg-test-sdk-java");
        request.setDbEngineVersion("PostgreSQL_12");
        request.setStorageType("LocalSSD");
        request.setStorageSpace(30);
        request.setVpcId("vpc-2bzo8w6m87v282dx0eemg****");
        request.setSubnetId("subnet-2d6b6byrhtts058ozfenq****");
        request.setNodeInfo(nodesInfo);
        request.setChargeInfo(chargeInfo);
        
        //Call the interface to complete the operation corresponding to the interface try {
            CreateDBInstanceResponse response = rdsPostgresql.createDBInstance(request);
            System.out.println(response);
        } catch (ApiException e) {
            System.out.println(e.getResponseBody());
        }
    }
}
```


The parameters in this example are described in the following table.


|Configuration item |Note |Value |
|---|---|---|
|DBEngineVersion |Compatible version. |PostgreSQL_12 |
|NodeInfo |Instance specification configuration. |[<br><br>{<br><br>"NodeType": "Primary",<br><br>"ZoneId": "cn\-beijing\-c",<br><br>"NodeSpec": "rds.postgres.1c2g"<br><br>},<br><br>{<br><br>"NodeType": "Secondary",<br><br>"ZoneId": "cn\-beijing\-c",<br><br>"NodeSpec": "rds.postgres.1c2g"<br><br>}<br><br>] |
|StorageType |Storage type. |LocalSSD |
|StorageSpace |Instance storage space. |30 |
|VpcId |A proprietary network (VPC) ID. |vpc\-2bzo8w6m87v282dx0eemg\*\*\*\* |
|SubnetId |Subnet ID. |subnet\-2d6b6byrhtts058ozfenq\*\*\*\* |
|InstanceName |Storage type. |pg\-test\-sdk\-java |
|ChargeInfo |Billing method. |{<br><br>"ChargeType": "PostPaid"<br><br>} |


<span id=".5p-l6K-iIFBvc3RncmVTUUwg5a6e5L6L5L-h5oGv"></span>
## Query PostgreSQL instance information

For information about the definition, range, and other parameters used in the following SDK requests, see [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail).

```java
package org.example;
import com.volcengine.*;
import com.volcengine.sign.Credentials;
import com.volcengine.rdspostgresql.RdsPostgresqlApi;
import com.volcengine.rdspostgresql.model.*;

public class Main {
    //Set AKSK authentication information and Region
    public static String ak = "Your AK";
    public static String sk = "Your SK";
    public static String region = "Your Region";
    public static String host = "Your Host";
    // create an RDS for PostgreSQL SDK client, which can be used to call the API to perform task requests later
    public static ApiClient apiClient = new ApiClient()
            .setCredentials(Credentials.getCredentials(ak, sk))
            .setRegion(region)
            .setEndpoint(host)
            .setConnectTimeout(10);
    public static RdsPostgresqlApi rdsPostgresql = new RdsPostgresqlApi(apiClient);

    // create an interface parameter, and set the interface parameter according to the parameter description configuration of the interface that needs to be called
    public static void main(String[] args) throws Exception {
        DescribeDBInstanceDetailRequest request = new DescribeDBInstanceDetailRequest();
        // call the interface to complete the operation corresponding to the interface
        try {
            DescribeDBInstanceDetailResponse response = rdsPostgresql.describeDBInstanceDetail(request);
            System.out.println(response);
        } catch (ApiException e) {
            System.out.println(e.getResponseBody());
        }
    }
}
```
