---
title: "Code examples"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Go_Code_examples"
---

The code examples for the Cloud Search Go SDK are for reference only.

<span id="LZf91xxj"></span>
## **Prerequisites**


* You have downloaded and installed the SDK. For more information, see [Download and installation](https://docs.byteplus.com/en/docs/cloudsearch/Go_Download_and_installation).

* You have initialized the client. For more information, see [Client initialization](https://docs.byteplus.com/en/docs/cloudsearch/Go_Client_initialization).


<span id="Vd5uvrxA"></span>
## **Set a request timeout**

By default, there is no timeout limit when you use the SDK to call Cloud Search APIs. When you initialize the client, you can use `WithHTTPClient(&http.Client{Timeout: <timeout> * time.Second})` to specify the request timeout. If a request does not complete within the specified period, it terminates and a timeout error is reported. For example, you can use the following code to set the client's request timeout to 10 seconds.

```Go
config = byteplus.NewConfig().
    WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
    WithRegion(region).
    WithHTTPClient(&http.Client{Timeout: 10 * time.Second})
```


<span id="lhSTyfTF"></span>
## Creating an instance

For information about the parameters in the following SDK code, such as their definitions and value ranges, see [CreateInstance](https://docs.byteplus.com/en/docs/cloudsearch/CreateInstance).

```Go
package main

import (
        "fmt"
        "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus"
        "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/credentials"
        "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/session"
        "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/escloud"
        "net/http"
        "time"
)

func main() {
        //创建实例
        var (
                ak     string
                sk     string
                region string
                config *byteplus.Config
                sess   *session.Session
                client *escloud.ESCLOUD
                err    error
        )

        ak = "Your AK"
        sk = "Your SK"
        region = "cn-beijing"
        config = byteplus.NewConfig().
                WithRegion(region).
                WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
                WithHTTPClient(&http.Client{Timeout: 3 * time.Second}).
                WithEndpoint("escloud.cn-beijing.byteplusapi.com")

        sess, err = session.NewSession(config)
        if err != nil {
                panic(err)
        }
        client = escloud.New(sess)

        createInstanceReq := &escloud.CreateInstanceInOneStepInput{}
        tagKey, tagValue := "k66", "v66"
        createInstanceReq.Tags = []*escloud.TagForCreateInstanceInOneStepInput{
                {Key: &tagKey, Value: &tagValue},
        }

        instanceName := "test-create-instance-golang"
        adminPwd := "sdk@es"
        version := "V7_10"
        chargeType := "PostPaid"
        regionId, zoneId := "cn-beijing", "cn-beijing-a"
        vpcName, vpcId := "es-vpc", "test-vpc-id"
        subnetName, subnetId := "es-subnet", "test-subnet-id"
        enableHttps := true
        instanceConfig := &escloud.InstanceConfigurationForCreateInstanceInOneStepInput{
                InstanceName:  &instanceName,
                AdminPassword: &adminPwd,
                Version:       &version,
                ChargeType:    &chargeType,
                RegionId:      &regionId,
                ZoneId:        &zoneId,
                EnableHttps:   &enableHttps,
                VPC: &escloud.VPCForCreateInstanceInOneStepInput{
                        VpcName: &vpcName,
                        VpcId:   &vpcId,
                },
                Subnet: &escloud.SubnetForCreateInstanceInOneStepInput{
                        SubnetName: &subnetName,
                        SubnetId:   &subnetId,
                },
        }
        hotNodeType, hotNum := "Hot", int32(3)
        resourceSpecName := "es.x2.medium"
        storageSpecName, storageSize := "es.volume.essd.pl0", int32(50)
        instanceConfig.NodeSpecsAssigns = []*escloud.NodeSpecsAssignForCreateInstanceInOneStepInput{
                {
                        Type:             &hotNodeType,
                        Number:           &hotNum,
                        ResourceSpecName: &resourceSpecName,
                        StorageSpecName:  &storageSpecName,
                        StorageSize:      &storageSize,
                },
        }
        createInstanceReq.InstanceConfiguration = instanceConfig

        resp, err := client.CreateInstanceInOneStep(createInstanceReq)
        if err != nil {
                panic(err)
        }
        fmt.Println(resp)
}
```


<span id="TwdYWWWw"></span>
## Query instance information

For the definitions, value ranges, and other information about the parameters used in the following SDK request, refer to DescribeInstance.

```Go
package main

import (
        "fmt"
        "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus"
        "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/credentials"
        "github.com/byteplus-sdk/byteplus-go-sdk-v2/byteplus/session"
        "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/escloud"
        "net/http"
        "time"
)

func describeInstance() {
        //Query instance information
        var (
                ak     string
                sk     string
                region string
                config *byteplus.Config
                sess   *session.Session
                client *escloud.ESCLOUD
                err    error
        )

        ak = "Your AK"
        sk = "Your SK"
        region = "cn-beijing"
        config = byteplus.NewConfig().
                WithRegion(region).
                WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
                WithHTTPClient(&http.Client{Timeout: 10 * time.Second}).
                WithEndpoint("escloud.cn-beijing.byteplusapi.com")

        sess, err = session.NewSession(config)
        if err != nil {
                panic(err)
        }

        client = escloud.New(sess)

        id := "o-xxx"
        describeInstanceInput := &escloud.DescribeInstanceInput{InstanceId: &id}
        resp, err := client.DescribeInstance(describeInstanceInput)

        if err != nil {
                panic(err)
        }

        fmt.Println(resp)
}
```
