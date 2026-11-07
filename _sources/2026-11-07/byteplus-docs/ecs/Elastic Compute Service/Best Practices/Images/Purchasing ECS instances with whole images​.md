---
title: "Purchasing ECS instances with whole images​"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-whole-images-to-buy-ECS"
---

This topic describes how to use BytePlus OpenAPI to quickly purchase an ECS instance by using a custom whole image (that is, a custom image containing both the system volume and data volumes).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also purchase an ECS instance in the console. <a href="https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-custom-images">Learn more</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

You can call the [RunInstances ](https://docs.byteplus.com/en/docs/ecs/RunInstances) operation and pass in the target whole image ID by using the `ImageId` parameter to create one or more ECS instances.

The following sections describe how to pass in parameters when you call the operation in scenarios in which you want to modify the volume attributes.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you create additional data volumes, make sure that the total number of volumes included in the whole image and the additional volumes does not exceed the maximum number of volumes that can be mounted to a single instance. The number of volumes that can be mounted to an instance varies based on the instance type. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types</a>.</div>


* <div data-tips="true" data-tips-type="tip">The capacity of a volume created from a snapshot must not be less than the capacity of the snapshot. If the specified volume capacity is less than the snapshot capacity, BytePlus  will use the snapshot capacity by default to create the volume.</div>



<span id=".5Zy65pmv5LiA77ya5peg6ZyA5L-u5pS56ZWc5YOP5YyF5ZCr55qE5LqR55uY5aSn5bCP44CB57G75Z6L562J5bGe5oCn"></span>
### Scenario 1: No need to modify the sizes, types, or other attributes of volumes included in the image

Do not pass in the `Volumes.N.xxx` parameter when you call the operation. In this case, BytePlus will create volumes of the corresponding sizes based on the snapshot information associated with the whole image. The default type of these volumes is ESSD_PL0, and they are deleted by default when the instance is deleted.

<span id=".5Zy65pmv5LqM77ya5L-u5pS55pW05py66ZWc5YOP5YyF5ZCr55qE5p-Q5Lqb5LqR55uY5aSn5bCP44CB57G75Z6L562J5bGe5oCn"></span>
### Scenario 2: Modify certain attributes such as the sizes and types of volumes included in the whole image


* Specify the system volume attribute by using the `Volumes.1.xxx` parameter.

   > By default, when you modify the attributes of a volume created from a system volume snapshot included in a whole image, you do not need to pass in the system volume snapshot ID by using the `Volumes.1.SnapshotId` parameter. Any value you specify for this parameter will be ignored.   
   

   For example, you can use the following configurations to change the system volume capacity to 100 GiB and specify that the volume is deleted when the instance is deleted:

   ```Plain Text
   Volumes.1.Size=100&Volumes.1.DeleteWithInstance=true
   ```
   

* Pass in the snapshot ID of the target data volume associated with the image by using the `Volumes.N(>1).SnapshotId` parameter, and specify the volume attribute by using the `Volumes.N.xxx` parameter.

   For example, you can use the following configurations to change the capacity of the data volume created from the `snap-hjdrwnbtxxxx` snapshot to 100 GiB and specify that the data volume is deleted when the instance is deleted:

   ```Plain Text
   Volumes.2.SnapshotId=snap-hjdrwnbtxxxx&Volumes.2.Size=100&Volumes.2.DeleteWithInstance=true
   ```
   


<span id=".5Zy65pmv5LiJ77ya5Yib5bu66aKd5aSW5pWw5o2u55uY"></span>
### Scenario 3: Create an additional data volume


* Specify attributes such as the size and type of an additional data volume by using the `Volumes.N(>1).xxx` parameter.

   For example, you can use the following configurations to create a data volume with a capacity of 100 GiB and specify that the data volume is deleted when the instance is deleted:

   ```Plain Text
     Volumes.3.Size=100&Volumes.3.DeleteWithInstance=true
   ```
   

* You can also pass in the ID of a snapshot that does not belong to the whole image by using the `Volumes.N(>1).SnapshotId` parameter to create a data volume based on an existing snapshot.

   For example, you can use the following configurations to create a data volume with a capacity of 100 GiB from the `snap-ulo8stsgxxxx` snapshot and specify that the data volume is deleted when the instance is deleted:

   ```Plain Text
     Volumes.4.SnapshotId=snap-ulo8stsgxxxx&Volumes.4.Size=100&Volumes.4.DeleteWithInstance=true
   ```
   


<span id=".5Zy65pmv5Zub77ya6YCa6L-H5pW05py66ZWc5YOP5YWz6IGU55qE5b-r54Wn5Yib5bu66aKd5aSW5pWw5o2u55uY"></span>
### Scenario 4: Create an additional data volume by using a snapshot associated with a whole image


* Pass in the ID of the target snapshot contained in the whole image by using the `Volumes.N(>1).SnapshotId` parameter, and pass in the `Volumes.N.xxx` parameter based on your needs to specify volume attributes.

* You can pass in the snapshot ID again by using the `Volumes.M(M>N).SnapshotId` parameter. You can also modify the attributes of the additional volume you create by using the `Volumes.M.xxx` parameter.

   For example, you can use the following configurations to create an additional data volume with a capacity of 150 GiB by using the `snap-hjdrwnbtxxxx` snapshot contained in the image, and specify that the data volume is deleted when the instance is deleted:

   ```Plain Text
   Volumes.5.SnapshotId=snap-hjdrwnbtxxxx&Volumes.6.SnapshotId=snap-hjdrwnbtxxxx&Volumes.6.Size=150&Volumes.6.DeleteWithInstance=true
   ```
