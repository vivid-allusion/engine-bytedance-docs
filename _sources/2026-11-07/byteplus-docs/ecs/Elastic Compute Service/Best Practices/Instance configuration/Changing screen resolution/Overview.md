---
title: "Overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview_05"
---

To improve compatibility, operating systems with a graphical user interface (GUI) use a low default screen resolution. If the default resolution does not meet your business requirements, you can change it as needed.

<span id="dX9FpTWv"></span>
## Scenarios


* **Model training/data science**

   * You need to view multiple windows side by side, such as TensorBoard, W&B, Jupyter Notebook, and system resource monitoring tools (for example, nvidia\-smi), to track training status in a timely manner.

   * You need to clearly view complex charts, feature maps, and 3D rendering results to analyze training performance.

* **Video editing/graphics rendering**

   * You need sufficient layout space for the timeline, effect controls, media library, and preview window in video editing software to prevent panel overlap.

   * You need to preview video clips at a resolution close to the target output (for example, 1080p) so that you can check video details.

* **Remote desktop and debugging**

   * Set the remote desktop screen resolution to the same as that of the local display so that you can perform full\-screen operations seamlessly and reduce scrolling.

   * Prevent graphical development tools (such as IDEs) and database management tools from having broken layouts caused by undersized windows.


<span id="5wZ7PtnN"></span>
## Changing the screen resolution


* [Setting Windows OS screen resolution](https://docs.byteplus.com/en/docs/ecs/Settings_Windows_screen_definition)

* [Changing Linux OS screen resolution](https://docs.byteplus.com/en/docs/ecs/Changing_Linux_OS_screen_resolution)


<span id="q18wWcgf"></span>
## More screen resolutions

If the common screen resolutions provided by BytePlus do not meet your business requirements, you can use the following screen resolutions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The screen resolutions shown in this section are in Beta. To request a trial,<a href="https://console.byteplus.com/workorder/create"> submit a ticket</a> or contact your account manager.</div>


* <div data-tips="true" data-tips-type="warning">Make sure that your instance and operating system meet the following requirements. Otherwise, you cannot use the screen resolutions shown in this section.</div>


   * <div data-tips="true" data-tips-type="warning">Instance: An ECS instance with a non\-DPU architecture. <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Learn more</a>.</div>


   * <div data-tips="true" data-tips-type="warning">Operating system:</div>


      * <div data-tips="true" data-tips-type="warning">Windows: Windows Server 2019 or later, with<a href="https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images?lang=en#.56ys5LqU5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFVmlydGlv6amx5Yqo"> the Virtio driver installed</a>.</div>


      * <div data-tips="true" data-tips-type="warning">Linux: Ubuntu 22.04 or later, with <a href="https://docs.byteplus.com/en/docs/ecs/Install-a-GUI-in-Linux">a graphical user interface (GUI) installed</a>.</div>




<Tabs>
<Tab zoneid="XiZd7v5lh1" title="4th-generation instances">
<TabTitle>4th-generation instances</TabTitle>

This section lists the screen resolutions supported by 4th\-generation instances. For more information, see [Instance generations](https://docs.byteplus.com/en/docs/ecs/Instance-type-selection-best-practice).


|Screen resolution |Windows Server |Ubuntu |
|---|---|---|
|3840 × 2160 |√ |√ |
|2560 × 1080 |√ |√ |
|2048 × 1280 |√ |× |
|2048 × 1152 |× |√ |
|1920 × 1440 |√ |√ |
|1920 × 1200 |√ |√ |
|1920 × 1080 |√ |√ |
|1856 × 1392 |× |√ |
|1792 × 1344 |× |√ |
|1680 × 1050 |√ |√ |
|1600 × 1200 |× |√ |
|1600 × 1000 |√ |× |
|1440 × 900 |√ |√ |
|1400 × 1050 |√ |√ |
|1360 × 768 |× |√ |
|1280 × 1024 |× |√ |
|1280 × 960 |× |√ |
|1280 × 800 |√ |× |
|1280 × 768 |× |√ |
|1280 × 720 |√ |× |
|1024 × 768 |√ |√ |
|800 × 600 |√ |√ |





</Tab>
<Tab zoneid="FKt9rafYLC" title="3rd-generation instances">
<TabTitle>3rd-generation instances</TabTitle>

This section lists the screen resolutions supported by 3rd\-generation instances. For more information, see[ Instance generations](https://docs.byteplus.com/en/docs/ecs/Instance-type-selection-best-practice).


|Screen resolution |Windows Server |Ubuntu |
|---|---|---|
|3840 × 2160 |√ |√ |
|2560 × 1080 |√ |√ |
|2048 × 1280 |√ |× |
|2048 × 1152 |× |√ |
|1920 × 1440 |√ |√ |
|1920 × 1200 |√ |√ |
|1920 × 1080 |√ |√ |
|1856 × 1392 |√ |√ |
|1792 × 1344 |√ |√ |
|1680 × 1050 |√ |√ |
|1600 × 1200 |√ |√ |
|1440 × 900 |√ |√ |
|1400 × 1050 |√ |√ |
|1360 × 768 |× |√ |
|1280×1024 |× |√ |
|1280 × 960 |× |√ |
|1280 × 768 |× |√ |
|1280 × 720 |√ |× |
|1024 × 768 |√ |√ |
|800 × 600 |√ |√ |





</Tab>
</Tabs>


&nbsp;

&nbsp;
