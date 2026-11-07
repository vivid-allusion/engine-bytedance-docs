---
title: "Code examples"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Java_Code_examples"
---

The code examples for the Cloud Search Java SDK are for reference only.

<span id="wTb6mhwI"></span>
## Prerequisites


* You have downloaded and installed the SDK. For more information, see [Download and installation](https://docs.byteplus.com/en/docs/cloudsearch/Java_Download_and_installation).

* You have initialized the client. For more information, see [Client initialization](https://docs.byteplus.com/en/docs/cloudsearch/Java_Client_initialization).


<span id="RWgzN6iU"></span>
## Set the request timeout

By default, there is no timeout limit when you use the SDK to call Cloud Search API operations. You can specify a request timeout in milliseconds by adding the `_request_timeout` parameter to your API call. If the request does not complete within the specified time, it terminates and reports a timeout error. For example, you can use the following code to set the timeout to 10 seconds when calling the DescribeInstance API operation.

```java
public static ApiClient apiClient = new ApiClient()
        .setCredentials(Credentials.getCredentials(ak,sk))
        .setRegion(region)
        .setConnectTimeout(10);
```


<span id="Tbia17lX"></span>
## Create an instance

For more information about the parameters in the following SDK code, including their definitions and value ranges, see [CreateInstance](https://docs.byteplus.com/en/docs/cloudsearch/CreateInstance).

```Java
package my;

import static com.byteplus.escloud.model.InstanceConfigurationForCreateInstanceInOneStepInput.ChargeTypeEnum;
import static com.byteplus.escloud.model.InstanceConfigurationForCreateInstanceInOneStepInput.VersionEnum;
import static com.byteplus.escloud.model.NodeSpecsAssignForCreateInstanceInOneStepInput.TypeEnum;

import com.byteplus.ApiClient;
import com.byteplus.ApiException;
import com.byteplus.escloud.EscloudApi;
import com.byteplus.escloud.model.CreateInstanceInOneStepRequest;
import com.byteplus.escloud.model.CreateInstanceInOneStepResponse;
import com.byteplus.escloud.model.DescribeInstanceRequest;
import com.byteplus.escloud.model.DescribeInstanceResponse;
import com.byteplus.escloud.model.InstanceConfigurationForCreateInstanceInOneStepInput;
import com.byteplus.escloud.model.NodeSpecsAssignForCreateInstanceInOneStepInput;
import com.byteplus.escloud.model.SubnetForCreateInstanceInOneStepInput;
import com.byteplus.escloud.model.TagForCreateInstanceInOneStepInput;
import com.byteplus.escloud.model.VPCForCreateInstanceInOneStepInput;
import com.byteplus.sign.Credentials;
import java.util.ArrayList;
import java.util.List;

public class java_demo {


    // Set the AK, SK authentication information, and Region
    public static String ak = "You";
    public static String sk = "xxx";
    public static String region = "cn-beijing";

    // Use a regional API service address
    public static String endpoint = "escloud.cn-beijing.byteplusapi.com";


    // Create a Cloud Search SDK client to call APIs and execute task requests
    public static ApiClient apiClient = new ApiClient()
            .setCredentials(Credentials.getCredentials(ak, sk))
            .setRegion(region)
            .setEndpoint(endpoint)
            .setConnectTimeout(5000)
            .setReadTimeout(5000);

    public static void main(String[] args) {
        // Create an instance
        EscloudApi api = new EscloudApi(apiClient);

        CreateInstanceInOneStepRequest createRequest = new CreateInstanceInOneStepRequest();
        List<TagForCreateInstanceInOneStepInput> tags = new ArrayList<>();
        tags.add(new TagForCreateInstanceInOneStepInput().key("key1").value("value1"));
        tags.add(new TagForCreateInstanceInOneStepInput().key("key2").value("value2"));
        createRequest.setTags(tags);

        InstanceConfigurationForCreateInstanceInOneStepInput instanceConfig = new InstanceConfigurationForCreateInstanceInOneStepInput();
        instanceConfig.setInstanceName("test-create-instance2");
        instanceConfig.setAdminPassword("sdk@es");
        instanceConfig.setVersion(VersionEnum.OPEN_SEARCH_2_9);
        instanceConfig.setChargeType(ChargeTypeEnum.POSTPAID);
        instanceConfig.setRegionId("cn-beijing");
        instanceConfig.setZoneId("cn-beijing-a");
        instanceConfig.setVPC(new VPCForCreateInstanceInOneStepInput().vpcId("test-vpc-id").vpcName("es-vpc"));
        instanceConfig.setSubnet(new SubnetForCreateInstanceInOneStepInput().subnetId("test-subnet-id").subnetName("es-subnet"));
        instanceConfig.enableHttps(true);

        List<NodeSpecsAssignForCreateInstanceInOneStepInput> nodeSpecsAssigns = new ArrayList<>();
        NodeSpecsAssignForCreateInstanceInOneStepInput hotSpec = new NodeSpecsAssignForCreateInstanceInOneStepInput()
                .type(TypeEnum.HOT)
                .number(3)
                .resourceSpecName("es.x2.medium")
                .storageSpecName("es.volume.essd.pl0")
                .storageSize(50);
        nodeSpecsAssigns.add(hotSpec);
        instanceConfig.setNodeSpecsAssigns(nodeSpecsAssigns);
        createRequest.setInstanceConfiguration(instanceConfig);

        try {
            CreateInstanceInOneStepResponse response = api.createInstanceInOneStep(createRequest);
            System.out.println("Creation initiated. Instance ID: " + response.getInstanceId());
        } catch (ApiException e) {
            System.out.println(e.getResponseBody());
        }
    }
}
```


<span id="DqHAzPkj"></span>
## Query instance information

```Java
package my;

import static com.byteplus.escloud.model.InstanceConfigurationForCreateInstanceInOneStepInput.ChargeTypeEnum;
import static com.byteplus.escloud.model.InstanceConfigurationForCreateInstanceInOneStepInput.VersionEnum;
import static com.byteplus.escloud.model.NodeSpecsAssignForCreateInstanceInOneStepInput.TypeEnum;

import com.byteplus.ApiClient;
import com.byteplus.ApiException;
import com.byteplus.escloud.EscloudApi;
import com.byteplus.escloud.model.CreateInstanceInOneStepRequest;
import com.byteplus.escloud.model.CreateInstanceInOneStepResponse;
import com.byteplus.escloud.model.DescribeInstanceRequest;
import com.byteplus.escloud.model.DescribeInstanceResponse;
import com.byteplus.escloud.model.InstanceConfigurationForCreateInstanceInOneStepInput;
import com.byteplus.escloud.model.NodeSpecsAssignForCreateInstanceInOneStepInput;
import com.byteplus.escloud.model.SubnetForCreateInstanceInOneStepInput;
import com.byteplus.escloud.model.TagForCreateInstanceInOneStepInput;
import com.byteplus.escloud.model.VPCForCreateInstanceInOneStepInput;
import com.byteplus.sign.Credentials;
import java.util.ArrayList;
import java.util.List;

public class java_demo {


    // Set the AK, SK authentication information, and Region
    public static String ak = "Your AK";
    public static String sk = "Your SK";
    public static String region = "cn-beijing";

    // Use a regional API service address
    public static String endpoint = "escloud.cn-beijing.byteplusapi.com";


    // Create a Cloud Search SDK client to call APIs and execute task requests
    public static ApiClient apiClient = new ApiClient()
            .setCredentials(Credentials.getCredentials(ak, sk))
            .setRegion(region)
            .setEndpoint(endpoint)
            .setConnectTimeout(5000)
            .setReadTimeout(5000);

    public static void queryInstance() {
        // Query instance information
        EscloudApi api = new EscloudApi(apiClient);
        DescribeInstanceRequest req = new DescribeInstanceRequest();
        req.setInstanceId("o-xxx");
        try {
            DescribeInstanceResponse describeInstanceResponse = api.describeInstance(req);
            System.out.println(describeInstanceResponse);
        } catch (ApiException e) {
            System.out.println(e.getResponseBody());
        }
    }
}

    
```
