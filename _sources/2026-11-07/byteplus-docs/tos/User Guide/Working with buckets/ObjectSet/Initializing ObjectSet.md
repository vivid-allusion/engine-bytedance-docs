---
title: "Initializing ObjectSet"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Initializing-ObjectSet"
---

Before using the ObjectSet feature, enable it in the bucket. This includes completing the basic configurations. This topic explains how to initialize the ObjectSet feature.

<span id="m7ze4NfI"></span>
## Notes

Once the ObjectSet hierarchy depth and custom delimiter are set, they can only be modified if there are no ObjectSets in the bucket. Proceed with caution.

<span id="KNie3fp6"></span>
## Steps


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, select **ObjectSet \> ObjectSet management**.

6. Click **Initialize ObjectSet immediately** and complete the basic configurations.

   
   |Parameter |Description |
   |---|---|
   |ObjectSet Hierarchy Depth |Specify the number of directory levels for each ObjectSet.<br><br>The path prefix of every new ObjectSet must match this depth exactly. For example, if the depth is set to two, then `user/123/` is a valid prefix, but `user/` or `user/123/data/` is not.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can only modify this depth when there are no ObjectSets in the bucket.</div><br> |
   |Custom delimiter |An ObjectSet uses a delimiter to define levels of hierarchy.<br><br>The delimiter is a single character. Supported delimiters include `/`, `#`, `-`, and `_`. The default delimiter is the forward slash (`/`), and we recommend using it.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Once set, the delimiter can only be modified when there are no ObjectSets in the bucket.</div><br> |
   |Configuration Default ObjectSet QoS and storage quotas |Select this option to configure the default throttling limits and capacity limit for each ObjectSet.<br><br><br>* **Default QoS throttling limits**:<br><br>   * **ReadsQps**: QPS limit for read requests. Enter a positive integer between 0 and 100,000,000. A value of 0 means there is no limit.<br><br>   * **WritesQps**: QPS limit for write requests. Enter a positive integer between 0 and 100,000,000. A value of 0 means there is no limit.<br><br>   * **ListQps**: QPS limit for list requests. Enter a positive integer between 0 and 100,000,000. A value of 0 means there is no limit.<br><br>   * **ReadsRate (Mb/s)** : Download bandwidth in Mb **/** s. Enter a positive integer between 0 and 100,000,000. A value of 0 means there is no limit.<br><br>   * **WritesRate (Mb/s)** : Upload bandwidth in Mb **/** s. Enter a positive integer between 0 and 100,000,000. A value of 0 means there is no limit.<br><br>* **Default capacity limit**:<br><br>   Specify the **capacity limit** for each ObjectSet. The valid range is from 0 to 100 PiB. A value of 0 means there is no limit. |
   

7. Click **Save settings**.

   The ObjectSet initialization process takes about 1 minute. Thank you for your patience.


<span id="tqs0ohUp"></span>
## Other operations

On the **ObjectSet management** page, you can modify the basic ObjectSet configurations, including **ObjectSet Hierarchy Depth**, **Custom delimiter**, and **Configuration Default ObjectSet QoS and storage quotas**.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once the ObjectSet hierarchy depth and custom delimiter are set, they can only be modified if there are no ObjectSets in the bucket.</div>
