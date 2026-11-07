---
title: "Creating TOS accelerators"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Creating-tos-accelerators"
---

This topic provides notes and steps for creating, modifying, and deleting TOS accelerators.

<span id="acb3b7d3"></span>
## Notes


|**Category** |**Considerations** |
|---|---|
|Acceleration mode |* Read\-only cache mode:<br><br>   * Both FNS and HNS buckets are supported.<br><br>   * Both single\-AZ and multi\-AZ buckets are supported.<br><br>* Read/write cache mode:<br><br>   * Only FNS buckets are supported. HNS buckets are not supported.<br><br>   * Only single\-AZ buckets are supported. Multi\-AZ buckets are not supported.<br><br>   * Append\-only writes are not supported.<br><br>   * This feature is currently in closed beta. Please contact your account manager for access. |
|Region |Each account can only have one accelerator per availability zone. |
|Others |* TOS accelerators only support binding to single\-region access points. They do not support binding to multi\-region access points.<br><br>* A single\-region access point can only be bound to one TOS accelerator. |


<span id="NS8ayGZd"></span>
## Steps


1. Create an accelerated domain name.

   1. Log in to the [TOS console](https://console.byteplus.com/tos).

   2. In the left navigation pane, select **Access point** \> **Single\-Region Access Point**.

   3. On the **Single\-Region Access Point** page, click **Create a Single\-Region Access Point**.

   4. On the **Create a Single\-Region Access Point** page, enter a name for your access point, select a bucket, and click **Select**.

2. Create an accelerator.

   1. In the left navigation pane, click **TOS accelerator**.

   2. On the **TOS accelerator** page, click **Create a TOS accelerator**.

   3. On the **Create a TOS accelerator** page, configure the following parameters:

      
      |Section |**Parameter** |Description |
      |---|---|---|
      |Basic information |TOS accelerator name |Enter a name for your TOS accelerator. |
      ||Region |Choose a region for your accelerator.<br><br>Currently, you can only create TOS accelerators in China (Beijing), China (Beijing2), China (Shanghai), China (Guangzhou), China (Wuhu), and Asia Pacific (Johor). |
      ||Availability zone |Choose an availability zone for your accelerator.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, you can create TOS accelerators in the following availability zones:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">China (Beijing) Availability Zone C/D/E</div><br><br><br>* <div data-tips="true" data-tips-type="tip">China (Shanghai) Availability Zone E</div><br><br><br>* <div data-tips="true" data-tips-type="tip">China (Guangzhou) Availability Zone C</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Asia Pacific (Johor) Availability Zone B</div><br><br><br><br><div data-tips="true" data-tips-type="tip">For more information, see <a href="https://docs.byteplus.com/en/docs/tos/Overview11?lang=en#aOhDsm2C">Supported regions</a>.</div><br> |
      |Instance configuration |Acceleration mode |Select an acceleration mode for your accelerator. The default is **Read\-only cache**.<br><br><br>* **Read\-only cache**: Suitable for read\-intensive workloads. It caches hot data to significantly improve read performance. However, write acceleration is not supported, and write requests pass through to the backend storage.<br><br>* **Read/write cache**: Suitable for mixed read/write or write\-intensive workloads. Written data goes directly into the high\-speed cache and is asynchronously flushed to the backend, achieving acceleration for both reads and writes. |
      ||Acceleration range |* **Accelerated Domain Name**: Select one or more accelerated domain names.<br><br>* **Acceleration strategy**: Select an acceleration strategy. The options are:<br><br>   * **Accelerate the entire access point**: The accelerator speeds up access to all the resources in the bucket. All requests to the bucket via accelerated domain names are forwarded to the accelerator.<br><br>   * **Accelerated specified prefix**: The accelerator speeds up access to objects with the specified prefix in the bucket. After selecting this option, enter the **Acceleration path**.<br><br>* **Acceleration path**: Enter the cache path. You can add up to ten paths.<br><br>   For example, if the acceleration path is set to image/, only requests to the image/ path via accelerated domain names will be accelerated. Requests to any other paths will not be accelerated.<br><br>   * **Synchronous warm\-up:** <br><br>      Select whether to enable synchronous warm\-up.<br><br>      When this option is enabled, data will be written to both the accelerator cache and TOS simultaneously after a client requests to read in\-scope resources.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">This parameter only applies when <strong>Acceleration mode</strong> is set to <strong>Read\-only cache</strong>.      </div><br>      <br><br>   * **Exclude subpath:** <br><br>      Select whether to exclude subpaths.<br><br>      When this option is enabled, your accelerator can exclude specific subpaths under an accelerated path when caching data.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For each accelerated path, you can exclude up to ten subpaths<strong>.</strong>      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">An excluded path cannot be empty or the same as its accelerated path.      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Excluded paths must be unique and cannot contain each other.      </div><br>      <br><br>   * **Cache elimination:** <br><br>      Select whether to evict data from the cache space.<br><br>      When this option is enabled, the accelerator removes expired data from the cache based on the configured expiration time. This time must be at least one hour. |
      |Capacity configuration |Accelerator capacity |Enter the desired capacity for your accelerator. The range is from 50 GiB to 200 TiB, in increments of 1 GiB.<br><br>**Estimated performance**: Adjusting the value for **accelerator capacity** will display the corresponding values for **Instance bandwidth** and **Current storage capacity**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter only applies when <strong>Acceleration mode</strong> is set to <strong>Read\-only cache</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The bandwidth of an accelerator grows linearly with capacity. As cache capacity increases, accelerator bandwidth improves proportionally. For more information, see <a href="https://docs.byteplus.com/docs/tos/Overview11#d8399dce">Performance metrics</a>.</div><br> |
      |Broadband configuration |Broadband mode |Select a bandwidth mode for your accelerator. The default is **Broadband provision**.<br><br><br>* **Broadband provision**: This mode is ideal for predictable workloads. Configure the provisioned bandwidth according to your needs. Once you have selected this option, you will only be charged for bandwidth that exceeds the baseline bandwidth. This mode supports up to 120,000 MB/s of read bandwidth and 900,000 QPS. To ensure optimal performance when you begin using this service, we recommend configuring a higher initial bandwidth in this mode.<br><br>* **Baseline Broadband Model**: This mode provides scalable bandwidth based on storage capacity for workloads with basic performance requirements. It supports up to 30,000 MB/s of bandwidth and 900,000 IOPS.<br><br>   **Estimated performance**: Adjusting the value for **Estimated Capacity** will display the corresponding values for **100% read**, **100% write**, and **Current storage capacity**.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Estimated Capacity</strong> is for estimation only and will not be applied to create the accelerator.   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Current storage capacity</strong> is an estimate provided for reference purposes only.   </div><br>   <br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e3aae95fac3af35e8750b8a615eef33f.png) </span><br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter only applies when <strong>Acceleration mode</strong> is set to <strong>Read/write cache</strong>.</div><br> |
      ||Provision of bandwidth |Select whether to enable provisioned bandwidth for your accelerator. If so, enter a limit for the bandwidth.<br><br>The valid range is 600 to 120,000 MB/s.<br><br><br>* **Estimated performance:**  Adjusting the value for **Provision of bandwidth** or **Estimated Capacity** will display the corresponding values for **100% read**, **100% write**, **Current storage capacity**, and **Billing provision bandwidth**.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Both <strong>Current storage capacity</strong> and <strong>Billing provision bandwidth</strong> are estimates provided for reference purposes only.   </div><br>   <br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_22b171b8fc43e3c8d0e51d7f6b61df59.png) </span><br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter only applies when <strong>Acceleration mode</strong> is set to <strong>Read/write cache</strong> and <strong>broadband mode</strong> is set to <strong>Broadband provision</strong>.</div><br> |
      

   4. Once you have finished configuring, click **Select**.

      After creating the accelerator successfully, you can use it for cache acceleration. For more information, see [Using TOS accelerators](https://docs.byteplus.com/docs/tos/Using-tos-accelerators).


<span id="d1552cb6"></span>
## Related operations

<span id="b80b39f8"></span>
### Editing an accelerator


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **TOS accelerator**.

3. On the **TOS accelerator** page, click **Edit** in the **Actions** column of the accelerator you want to manage.

4. On the **Edit TOS accelerator** page, modify the following settings as necessary: **Acceleration mode**, **Accelerator capacity**, **Broadband configuration**, **Accelerated Domain Name**, **Acceleration strategy**, **Acceleration path**, **Synchronous warm\-up**, **Exclude subpath**, and **Cache elimination**. Then, click **Select** to save the changes.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Changes take effect immediately after you modify the accelerator capacity or provisioned bandwidth. However, you can only reduce the capacity or bandwidth once per hour.   </div>
   

5. In the box that appears, verify the changes and click **OK edit**.


<span id="eTv8ckBS"></span>
### Deleting an accelerator

Before deleting an accelerator, make sure to clear any warm\-up tasks and dissociate all accelerated domain names from it. Otherwise, the accelerator cannot be deleted.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **TOS accelerator**.

3. On the **TOS accelerator** page, click **Delete** in the **Actions** column of the accelerator you want to remove.

4. In the box that appears, verify that all warm\-up tasks have been cleared. Then, click **Click Unbind** to unbind all accelerated domain names. Next, confirm the deletion by entering the accelerator name and clicking **OK**.
