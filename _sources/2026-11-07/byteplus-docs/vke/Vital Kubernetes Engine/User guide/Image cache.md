---
title: "Image cache"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Image-Cache"
---

The image cache feature allows you to pre\-download images to data disks, create cache snapshots, and then create pod instances based on these snapshots. VKE supports displaying a list of image caches in the console.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

The image cache feature is supported only for VCI scenarios.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- Apply for Trial</strong></a>]: On the VCI side, the image cache feature is in the <strong>beta</strong> phase.</div>


<span id=".5Yib5bu66ZWc5YOP57yT5a2Y"></span>
## Creating image caches

For detailed instructions on creating an image cache, see [VCI image cache](https://docs.byteplus.com/en/docs/vke/VCI-Image-Cache).

<span id=".5p-l55yL6ZWc5YOP57yT5a2Y"></span>
## Viewing image caches


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Vital Container Instance** \> **Image Cache**.

3. On the **Image Cache** page, view information about generated image caches, including the image name/ID, status, image information, last usage time, and creation time.

   Click the name of an image cache to view its details, such as its basic information, warm\-up configuration, and events.


<span id=".566h55CG6ZWc5YOP57yT5a2Y"></span>
## Managing image caches


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Elastic Container Instance** \> **Image Cache**.

3. On the **Image Cache** page, find the target image cache and click the desired button in the **Actions** column to manage the image cache.

   
   |Actions |Description |
   |---|---|
   |Update |Update the image cache configuration. For detailed parameter settings, see [Creating VCI instances by using a manually created image cache](https://docs.byteplus.com/en/docs/vke/Creating-a-VCI-instance-using-Manual-Image-Cache). |
   |Delete |Delete the image cache.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Image cache deletion is irreversible. Proceed with caution.</div><br> |
   

4. Click **Confirm** to save the configuration.
