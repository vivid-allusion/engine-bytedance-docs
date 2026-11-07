---
title: "Distributed cache"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/distributed-cache"
---

Distributed cache is a cache sharing solution provided by ByteHouse Cloud Data Warehouse. Based on distributed cache technology, it can effectively improve data query performance and meet your requirements for high\-performance queries. This tutorial introduces the methods for enabling and using the distributed cache feature.

<span id="574e0425"></span>
# Background

<span id="3e8ef411"></span>
## Function overview

ByteHouse cloud data warehouse edition adopts a storage\-compute separation architecture. In real\-time data warehouse scenarios, the use of local disk caching in virtual warehouses still has certain limitations:


* When relying on object storage and other systems, first\-byte latency can affect query response speed;

* The shared storage layer is susceptible to resource contention in multi\-tenant scenarios, resulting in performance fluctuations.

* In a storage\-compute separation architecture, if there is a cache miss, data must be read directly from remote storage, which significantly increases query time.


Distributed cache can be deployed across **distributed computing nodes** to enable globally shared cache resources, specifically addressing the issues mentioned above and further enhancing performance and stability:


* **Data timeliness assurance**: Enables real\-time data warehouse business writes to be visible within seconds, ensuring data timeliness;

* **Tenant\-level resource isolation**: Provides tenant\-level compute and I/O acceleration capabilities;

* **Adapting to business growth**: Independent scaling of cache nodes enables linear expansion of IO throughput, flexibly addressing the growth of business traffic.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65c03dda823b435e8d7ad31eb4425e68~tplv-goo7wpa0wc-image.image) </span>

After enabling distributed cache, ByteHouse will automatically distribute cache configurations to the virtual warehouses in the current environment:


* When querying, data will be automatically loaded to the distributed cache;

* Subsequent identical queries will preferentially read data from the distributed cache, eliminating the need to repeatedly access remote storage and significantly improving query efficiency.


<span id="c1445255"></span>
## Applicable scenarios

This option will apply in the following situations:


* **High\-performance query scenarios**: Suitable for data analysis queries that require fast response (such as real\-time reports and instant data analysis), especially for frequently accessed data, where caching can accelerate and reduce query latency.

* **Large\-scale data processing**: In environments with large data volumes (such as PB\-level data storage), distributed caching reduces reliance on remote storage, avoids performance bottlenecks caused by repeated remote data reads, and improves overall query efficiency.


<span id="8878f042"></span>
## Billing


* **Pricing and billing**:

   * Distributed cache supports unified purchase and management of dedicated cache at the tenant\-environment level, with all virtual warehouses sharing cache resources. Each environment can enable a distributed cache only once, and once enabled, the cache is shared by all users.

   * The minimum order capacity for distributed cache is 10500 GiB and supports the **annual/monthly subscription** billing mode. For more details, please refer to [Specifications and pricing](https://docs.byteplus.com/docs/bytehouse/specifications-and-pricing).

* **Settlement**, **Renewal**, **Arrears**, and **Unsubscription**: The logic for settlement, renewal period, and other logic of distributed cache is independent of the corresponding logic of the public virtual warehouse group, though the logical framework is similar. For details, refer to the [billing](https://docs.byteplus.com/en/docs/bytehouse/billing) document.


<span id="3a575d4c"></span>
# Limitations

This feature is a Beta feature. To use it, please submit a ticket or contact the ByteHouse team to obtain allowlist permission.

<span id="7f7ba5ad"></span>
# Prerequisites


* To enable the distributed cache feature in the Console, only a user with the AccountAdmin or SystemAdmin role can perform this action.

* All sub\-users can view and use distributed cache.

* For more information about roles and users, please refer to [Role management](https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration).


<span id="6a5e2ed5"></span>
# Use distributed cache

<span id="2cf5cd9a"></span>
## Enable distributed cache


1. Log in to the ByteHouse cloud data warehouse console. Click **Tenant management** at the top. Then, click the **Basic information** tab. In the **Distributed Cache** module, click **Open now**. You will be redirected to the activation page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1c7726c3b7441b988ea5e3318d64d7e~tplv-goo7wpa0wc-image.image) </span>

2. On the activation page, set the required cache size, My Plan duration, and whether to enable auto\-renewal.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae259b8462e648ebafda67976cbbbdf0~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter items |Configuration description |
   |---|---|
   |Cache size |Cache size determines the resource capacity of distributed cache and affects the ability to cache frequently accessed data. The minimum order size is 10500 GiB and cannot be reduced; the adjustment increment is 10500 GiB, and cache specifications can be adjusted as needed. |
   |Purchase duration |You can select the validity period of the service as needed. |
   |Automatic renewal |Once enabled, the Platform will, by default, auto purchase each month without the need for Manual Purchase. You can adjust renewal settings at any time. For more information about automatic renewal, see [Automatic Renewal](https://docs.byteplus.com/docs/bytehouse/settlement-and-renewal-description#fd704ba9). |
   

3. After configuration is complete, click **confirm the order**. ByteHouse will create a distributed cache and redirect to the Cost Center, where you can review the costs again. Then click **Next step** to confirm and pay the related costs.

4. After the payment is complete, click **Go to Console**. The system will redirect to the ByteHouse Cloud Data Warehouse Console tenant management page, where you can view the initialization status of the distributed cache on the Basic Information tab. The enabled distributed cache will begin initialization, and its status will be "Configuring". The entire initialization takes approximately 5 minutes. Please wait patiently.

5. After distributed cache initialization is complete, the status changes to "**Running**".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e49117624d68494db0b2492f3007a24a~tplv-goo7wpa0wc-image.image) </span>

6. Optional: Edit project or flight tag, manage sub\-account information. ByteHouse cloud data warehouse edition supports managing split billing by project or tag. For details about the operation, please refer to [Manage cost allocation](https://docs.byteplus.com/docs/bytehouse/manage-cost-allocation).


<span id="0e888a7f"></span>
## Scale up distributed cache

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The minimum specification of the distributed cache is 10500 GiB. After activation, only scaling up and unsubscribing are supported; scaling down is not allowed.</div>


* <div data-tips="true" data-tips-type="warning">Scaling up takes effect immediately, and after the adjustment, billing will be based on the actual specifications.</div>


1. In the ByteHouse Cloud Data Warehouse Console, click the **Tenant management** at the top; click the **Basic information** tab; in the **Distributed Cache** module, click **Edit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59b009fdaa424fbeb29e6434bcfb4031~tplv-goo7wpa0wc-image.image) </span>

2. On the edit page, adjust the cache size, set the step size to 10500 GiB, and click **Confirm Change**. The platform will redirect to the order confirmation page, where you can confirm the specifications and costs again. After ensuring that everything is correct, click **Next step**. After purchase success, the Platform will automatically scale up.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99617d5e1fbb45f6a911a18f6d85e652~tplv-goo7wpa0wc-image.image) </span>

3. Click **Go to Console**, and the system will navigate to the ByteHouse Cloud Data Warehouse console's **Tenant Management** page. You can view the status of the distributed cache under the **Basic information** tab. During scaling up, the status of the distributed cache will be shown as **updating**. The entire configuration process takes approximately 5 minutes, so please wait patiently.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/284222fa30304afdb0948fc029fead6b~tplv-goo7wpa0wc-image.image) </span>

4. After scaling up is complete, the status changes to **Running**, and the cache size is also adjusted to your configured cache size.


<span id="b8d4ae1f"></span>
## Manage renewal


1. In the ByteHouse Cloud Data Warehouse Console, click the top **Tenant management**. Click the **Basic information** tab. In the **Distributed Cache** module, click **Renew**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df7ab21c8a024231960ca983c42647c7~tplv-goo7wpa0wc-image.image) </span>

2. Copy the ID from the prompt box. In the next steps, use this ID to search in the BytePlus Cost Center and complete the renewal. After copying, click **Apply**, and the platform will jump to the renewal management page in the BytePlus Cost Center.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f47ed46e77364c9bb2a310f6484378ec~tplv-goo7wpa0wc-image.image) </span>

3. In the search box after Instance ID, enter the ID copied in Step 2 and press Enter to search. Click the **Renew** button in the Operation column of the row where the instance is located. You will be redirected to the renewal information confirmation page. For renewal operations, refer to the [manual renewal rule description](https://www.volcengine.com/docs/6269/1134224). To enable automatic renewal, refer to the [Automatic renewal rules](https://www.volcengine.com/docs/6269/1134227).

4. After the renewal is complete, you can return to the ByteHouse Cloud Data Warehouse Console and refresh the page. The expiration time will be updated according to your configured renewal period. To address any questions regarding the renewal period, please submit a ticket and contact the after\-sales team for assistance.


<span id="aa653a71"></span>
# Unsubscribe distributed cache


1. In the ByteHouse Cloud Data Warehouse Console, click **Tenant management** at the top. Then, click the **Basic information** tab. In the **Distributed Cache** module, click **Unsubscribe**, and finally click **Apply**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d67484261e9149b994bf6b48d4a5140b~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After unsubscribing is complete, any existing distributed cache will be cleared. Please proceed with caution.   </div>
   

2. The system will jump to the **Unsubscribe management** page of the BytePlus Cost Center. Click **Submit Order**, then click **Apply** to unsubscribe the current resource. After a successful unsubscription, the refund amount will be returned to the account balance.

3. After the unsubscription is complete, you can return to the **Tenant management** page in the ByteHouse cloud data warehouse edition Console, where you can view the status of the distributed cache on the **Basic information** tab. At this time, the status of the distributed cache will be "Deleting". The entire deletion process takes approximately 5 minutes.
