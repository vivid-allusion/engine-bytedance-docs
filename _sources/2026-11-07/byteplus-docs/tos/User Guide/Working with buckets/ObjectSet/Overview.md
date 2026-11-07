---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/-Overview"
---

In business scenarios involving AI agents and multi\-tenant SaaS services, developers often need to provide logically isolated data management units for a large number of end users within a single storage space. TOS addresses this need with the ObjectSet feature.

An ObjectSet is a virtual resource management unit created within a bucket. It expands the TOS data model from two layers (bucket\-object) to three layers (bucket\-objectset\-object), providing a scalable, native, multi\-tenant isolation solution for upper\-layer applications. Each ObjectSet has its own permissions, traffic throttling, and usage metering. This enables you to build robust applications that can support billions of tenants on TOS in a convenient and cost\-effective manner.

<span id="nLhWGA5Z"></span>
## Introduction

An ObjectSet provides a lightweight isolation layer within a bucket, offering management capabilities similar to those of a native bucket. It eliminates the need for complex middleware services to manage multi\-tenant data.


|Core features |Description |
|---|---|
|Independent resource unit |An ObjectSet is an independent resource entity that enables you to manage objects throughout their lifecycle, including their creation, modification, and deletion.<br><br>You can create an ObjectSet for each end user or business unit to achieve fine\-grained resource management. |
|Performance isolation |Each ObjectSet offers comprehensive isolation capabilities to ensure that the data and access behaviors of different users do not interfere with each other.<br><br>You can set independent QPS (queries per second) and bandwidth limits for each ObjectSet. This prevents burst traffic from a single user from affecting others and helps maintain overall service stability. |
|Protocol compatibility |Accessing an ObjectSet is identical to accessing a standard TOS object. ObjectSet is also compatible with the S3 protocol. |
|Advanced features |An ObjectSet can be used with various advanced TOS features.<br><br>For example, you can add tags to an ObjectSet and configure lifecycle rules to migrate or archive objects in bulk within all ObjectSets with a specific tag. |


<span id="fUmqGJwC"></span>
## Benefits


|Benefit |Description |
|---|---|
|Hundreds of millions of ObjectSets |You can create hundreds of millions of ObjectSets within a single bucket. This solves the problem of the limited number of buckets found in traditional solutions and provides a solid foundation for building large\-scale, multi\-tenant applications. |
|Simplified architecture |The ObjectSet feature extends multi\-tenant isolation to the storage layer. It natively isolates permissions, performance, and metering.<br><br>By eliminating the need for complex middleware gateways or proxies, it greatly reduces architectural complexity and development costs. |
|Refined management |With per\-ObjectSet metering and billing, you can accurately track the resource consumption of each tenant. |
|Flexible performance |To achieve differentiated quality of service (QoS), you can assign different QPS and bandwidth quotas to tenants based on their business tier or payment model. This prevents unpaid or low\-value tenants from abusing resources while ensuring service quality for core tenants. |


<span id="MGUKSwVK"></span>
## Use cases


|Use case |Description |
|---|---|
|AI agents and sandbox environments |In applications such as AI agents, MaaS platforms, and Coze, each end user or session may require independent, secure file storage (a sandbox).<br><br>Creating an ObjectSet for each user allows you to easily achieve file isolation, manage resource quotas, and track usage statistics, thereby ensuring data privacy and service fairness. |
|Multi\-tenant SaaS applications |Enterprise SaaS services, such as online collaboration platforms, project management tools, and cloud storage services, require logically isolated storage space for each customer.<br><br>With ObjectSet, you can assign a dedicated ObjectSet to each customer, enabling data isolation, per\-customer metering, and customized feature configurations. |
|Content creation and sharing platforms |On video, image, or document\-sharing platforms, each content creator can have their own ObjectSet to store and manage their work.<br><br>These platforms can use ObjectSet metrics to track each creator's storage usage and outbound traffic for cost accounting or revenue sharing purposes. |
|IoT device data management |In IoT scenarios, massive numbers of devices continuously upload data. To achieve logical data isolation, access control, and traffic monitoring, as well as to simplify subsequent data analysis and management, you can create an ObjectSet for each device or group of devices. |


<span id="9AiCaXzD"></span>
## How it works

The introduction of ObjectSet changes the TOS data model from a two\-layer structure (Bucket\-Object) to a three\-layer structure (Bucket\-ObjectSet\-Object). The following explains how data is accessed and managed under this new architecture.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5d8e4e4ac6f1ad7e5951997fff20c662.jpg) </span>


1. **Enabling and configuring ObjectSet**: When enabling the ObjectSet feature, you can define the directory hierarchy and delimiter of the ObjectSet path prefix, establishing a unified standard for subsequent ObjectSet creation and management.

2. **Creating an ObjectSet**: You can create a dedicated ObjectSet for a tenant (e.g., an end user) and assign a unique path prefix. This prefix serves as the unified namespace entry for all objects in that ObjectSet.

3. **Policy execution for object reads and writes**: When an end user reads or writes an object, the TOS gateway matches the object's full path (i.e., key) against its ObjectSet. Once a match is found, the system automatically enforces the configured policies of that ObjectSet. These policies include:

   * **Quality of Service (QoS) check**: Determines whether the request exceeds the ObjectSet's QPS or bandwidth quota. If so, throttling is applied.

   * **Permission check**: Verifies that the requester has permission to access the ObjectSet and its objects.

   * **Metering and monitoring**: Attributes metrics, such as traffic and request count, to the corresponding ObjectSet for statistical purposes.

4. **Data flow**: If all policy checks are passed, the data I/O process is the same as standard TOS object access. Ultimately, it writes to or reads from the underlying storage medium. This process is transparent to upper\-layer applications.


<span id="VLXRWIBr"></span>
## Constraints and limitations

To ensure the stability, performance, and future scalability of the ObjectSet feature, observe the following constraints.


|Category |Description |
|---|---|
|Number of buckets with ObjectSet enabled |You can create up to 100 buckets with ObjectSet enabled for each account and its sub\-account(s). |
|Number of ObjectSets per bucket |By default, you can create up to 10 million ObjectSets for each bucket. To request a higher limit, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245). |
|Lifecycle |Deleting an ObjectSet only removes its metadata. The data belonging to that ObjectSet is not deleted. Whether or not to clean up that data is based on your business requirements. |
|Hierarchy |* You cannot create an ObjectSet with the root directory (`/`) as its path prefix. Doing so would place all objects under a single ObjectSet, which defeats the purpose of isolation.<br><br>* When enabling the ObjectSet feature for a bucket, you must specify a fixed directory hierarchy of one to five levels. The path prefix of every new ObjectSet must match this depth exactly. You can only modify this depth when there are no ObjectSets in the bucket.<br><br>   For example, if the depth is set to two, then `user/123/` is a valid prefix, but `user/` or `user/123/data/` is not.<br><br>* An ObjectSet uses a delimiter to define levels of hierarchy. The default delimiter is the forward slash (`/`). It is set at the bucket level and can only be modified when there are no ObjectSets in the bucket. |
|Naming conventions |The path prefix of an ObjectSet must be between 3 and 256 characters long. |
|Usage statistics |Usage statistics obtained through APIs such as GetObjectSetStorage are not precise, real\-time values. There is usually a 10\-minute calculation and synchronization delay. |
|Enablement and compatibility |* Before using the ObjectSet feature, enable it in the bucket. For more information, see [Initializing ObjectSet](https://docs.byteplus.com/en/docs/tos/Initializing-ObjectSet).<br><br>* In a bucket where ObjectSet is enabled, any existing objects whose path prefix does not match a newly created ObjectSet become orphaned objects. These objects continue to follow the bucket\-level management policies. |


<span id="4fGjRkOx"></span>
## Billing notes

The ObjectSet feature is currently free.

<span id="97TB3tvl"></span>
## FAQ

**Q1: Can I enable the ObjectSet feature on a bucket that already contains a large number of objects?** 

**A1**: Yes. Once enabled, all objects whose path prefix does not match any newly created ObjectSet become orphaned objects. These objects continue to follow the bucket\-level management policies.

**Q2: After I delete an ObjectSet, are the data inside it deleted immediately?** 

**A2**: No. Deleting an ObjectSet only removes the logical resource unit and its associated configurations, such as QoS and tags. The objects stored under that ObjectSet are not deleted. Instead, they become orphaned objects. Based on your business needs, you need to decide whether to clean up these data through batch deletion or other methods.

**Q3: Are the QPS and bandwidth quotas of ObjectSet hard or soft limits?** 

**A3**: They are hard limits. When an ObjectSet's access traffic or request rate reaches its configured quota limit, TOS throttles subsequent requests and returns a 429 (Too Many Requests) error code. This ensures that the service quality of other ObjectSets is not affected.

<span id="9DK9Q0WK"></span>
## Related documentation


* [Initializing ObjectSet](https://docs.byteplus.com/en/docs/tos/Initializing-ObjectSet)

* [Creating an ObjectSet](https://docs.byteplus.com/en/docs/tos/Creating-an-ObjectSet)


&nbsp;
