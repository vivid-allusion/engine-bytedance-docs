---
title: "Image detection overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Image_Detection_Overview"
---

Image detection is a feature provided by the  platform for checking custom image specifications. You can use the feature to check image specifications when you import or create a custom image.

<span id=".5L2_55So5Zy65pmv"></span>
## Applicable scenarios

If you use an image that has not previously run on the  platform to create a  ECS instance, the instance may not work as expected due to compatibility issues with drivers, kernels, and tools. We recommend that you enable the image detection feature when you import or create a custom image. This way, the validity of the image can be verified and issues can be fixed in advance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* The image detection process starts after a custom image is created. Interrupted checks or failed checks do not block the creation or import process of the custom image.

* The image detection feature supports most Linux and Windows Server operating systems. For more information, see [Image release notes](https://docs.byteplus.com/en/docs/ecs/Image-release-notes).

* You need to enable the [snapshot](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots) feature before you can use this feature.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You are charged based on the number and storage duration of snapshots. <a href="https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots">Learn more</a>.   </div>
