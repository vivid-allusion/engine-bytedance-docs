---
title: "Best practices for data recovery when spot instances are reclaimed"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Data_Recovery_When_Spot_Instances_Are_Reclaimed_Best_Practices"
---

Spot instances have an [interrupt reclamation mechanism](https://docs.byteplus.com/en/docs/ecs/Reclaiming_spot_instance). Before being fully reclaimed, the instance enters a locked state and triggers an interruption event. When you receive an interruption notification for a spot instance, you can follow steps below to create a custom image for the instance. Then you can launch a new spot instance with this image to recover data stored on the instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After a spot instance is released, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances#.5Yig6Zmk5ZCO5a6e5L6L55u45YWz6LWE5rqQ5oOF5Ya1">Status of instance resources after an ECS instance is deleted</a> for details on retained data.</div>


<span id=".5rWB56iL6K-05piO"></span>
## Process description

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6fa3f3614124df4870e9e32c25c9ad45.png) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The platform sends a notification of interrupting a spot instance in advance (1 hour in advance for GPU instances and 5 minutes in advance for non\-GPU instances). When the reclaim time is reached, the instance is officially reclaimed. However, the specific time taken for data recovery depends on factors such as the image type of your instance and the file size of system volume. For example, the larger the system volume, the longer the recovery time. Make sure that you assess and verify example codes provided in this document before you use them.</div>


* <div data-tips="true" data-tips-type="warning">Practice provided in this topic is for reference only. There is no guarantee that the image can be created and data recovered successfully before your instance is reclaimed. We recommend that you regularly <a href="https://docs.byteplus.com/en/docs/ecs/Spot_instances_overview#.5rOo5oSP5LqL6aG5">back up data</a> for better user experience.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65oqi5Y2g5byP5a6e5L6L"></span>
### Step 1: Create a spot instance

This document takes calling [RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) operation to create and automatically start a spot instance as an example.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also refer to <a href="https://docs.byteplus.com/en/docs/ecs/Buying_spot_instance">Purchasing spot instances</a> and create a spot instance in the ECS console.</div>


**Sample request**

The following code is applicable if you want to create a General\-purpose g2i spot instance with the billing method of pay\-as\-you\-go `PostPaid` and the spot strategy of automatic bid `SpotAsPriceGo`.

```Plain Text
GET /?Action=RunInstances&Version=2020-04-01&ZoneId=cn-beijing-a&ImageId=image3tgt71djf14bwbh7****&InstanceTypeId=ecs.g2i.xlarge&InstanceName=instance-test&InstanceChargeType=PostPaid&SpotStrategy=SpotAsPriceGo&Count=1&Password=password@123&NetworkInterfaces.1.SubnetId=subnet-3thbjdy3rh4bwbh8****&NetworkInterfaces.1.SecurityGroupIds.1=sg3thbinrkp94bwbha****&Volumes.1.VolumeType=PTSSD&Volumes.1.Size=40 HTTP/1.1
Host: open.volcengineapi.com
Region: cn-beijing
Service: ecs
```


**Sample response**

The return of `InstanceIds` indicates the spot instance is created successfully.

```Plain Text
    "Result": {
        "InstanceIds": [
            "i-3tigy72q3u3vj0******"
        ]
    }
```


<span id=".5q2l6aqk5LqM77ya5o6l5pS25oqi5Y2g5byP5a6e5L6L5Lit5pat5raI5oGv"></span>
### Step 2: Receive the interruption message of spot instance

Except for notifications, the system also generates corresponding system events for you. This article introduces how to call [DescribeSystemEvents](https://docs.byteplus.com/en/docs/ecs/DescribeSystemEvents) operation to view the spot instance's event information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also refer to <a href="https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications">Configuring event monitoring notifications</a> to subscribe to the "spot instance interruption, instance release" event message notifications through the ECS console.</div>


**Sample request**

```Plain Text
GET /?Action=DescribeSystemEvents&Version=2020-04-01&ResourceIds.1=i-3tigy72q3u3vj0****** HTTP/1.1
Host: open.volcengineapi.com
Region: cn-beijing
ServiceName: ecs
```


**Sample response**

The response of `Scheduled` status `SpotInstanceInterruption.Delete` event indicates that spot instance is about to be interrupted.

```Plain Text
    "Result": {
        "SystemEvents": [
            {
                "Id": "t-3ti9101aju3vj0******",
                "CreatedAt": "2022-06-15T16:34:34+08:00",
                "UpdatedAt": "2022-06-15T16:34:49+08:00",
                "ResourceId": "i-3tigy72q3u3vj0******",
                "Type": "SpotInstanceInterruption.Delete",
                "Status": "Scheduled",
                "OperatedEndAt":"2021-07-10T18:11:46+08:00"
            }
        ],
        "NextToken": "bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******"
    }
```


<span id=".5q2l6aqk5LiJ77ya5Li65Y2z5bCG6KKr5Zue5pS255qE5oqi5Y2g5byP5a6e5L6L5Yib5bu66Ieq5a6a5LmJ6ZWc5YOP"></span>
### Step 3: Create a custom image for the spot instance to be reclaimed

After you receive the instance interruption message, call [CreateImage](https://docs.byteplus.com/en/docs/ecs/CreateImage) operation to create a custom Image for the current instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also refer to <a href="https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance">Creating custom images from a Linux instance </a> to create a custom image in the ECS console.</div>


**Sample request**

```Plain Text
GET /?Action=CreateImage&Version=2020-04-01&InstanceId=i-3tigy72q3u3vj0******&ImageName=image-1 HTTP/1.1
Host: open.volcengineapi.com
Region: cn-beijing
ServiceName: ecs
```


**Sample response**

The return of `ImageId` indicates that the custom image is created.

```Plain Text
{
    "Result": {
        "ImageId": "image-3teco18f1w5a71******"
    }
}
```


After you create the custom image, you can call the [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) operation to view the image status. When the image status becomes available, proceed to the next step.

```Plain Text
GET /?Action=DescribeImages&Version=2020-04-01&ImageIds.1=image-3teco18f1w5a71******  HTTP/1.1
Host: open.volcengineapi.com
Region: cn-beijing
Service: ecs
```


<span id=".5q2l6aqk5Zub77ya5L2_55So6Ieq5a6a5LmJ6ZWc5YOP5paw5bu65oqi5Y2g5byP5a6e5L6L5a6e546w5pWw5o2u5oGi5aSN"></span>
### Step 4: Use the custom image to create a new spot instance to recover data.

Call the [RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) operation to use the custom image obtained in Step 3 to recreate a spot instance. For detailed parameters, refer to Step 1, where:


* You need to replace `ImageId` with the new image ID.

* We recommend that the availability zone of the new instance, `ZoneId`, remains the same as the original instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also refer to <a href="https://docs.byteplus.com/en/docs/ecs/Buying_spot_instance">Purchasing spot instances</a> and recreate a spot instance in the ECS console.</div>
