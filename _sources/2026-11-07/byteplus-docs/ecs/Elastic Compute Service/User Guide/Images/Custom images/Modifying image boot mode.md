---
title: "Modifying image boot mode"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Modifying-custom-image-information"
---

If the boot mode is specified incorrectly when you create a custom image, or if you have manually changed the actual boot mode of the image, you need to set the boot mode displayed in the console to the correct mode. This helps ensure that the image works as expected.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To change the boot mode of an image from <code>BIOS</code> to <code>UEFI</code>, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Changing-the-boot-mode-of-Linux">Changing boot mode from BIOS to UEFI for Linux custom images</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Image console](https://console.byteplus.com/image/images). 

2. In the top menu bar, select the region and project where the target custom image is located.

3. Select the "Custom Image" tab.

4. Click the name of the target custom image, and select the "Overview" tab.

5. Click the edit button next to "Startup mode".

6. In the "Modify the startup method" pop\-up window, click the drop\-down list and select a new boot mode.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c2c0706c7fc123fa65502b808a84d871.png) </span>

7. Click the "OK" button to complete the modification.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[ModifyImageAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyImageAttribute)
