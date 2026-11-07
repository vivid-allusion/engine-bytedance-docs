---
title: "Creating live rooms"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/creating-live-rooms"
---

Before you can start streaming, you need to create a live room. This guide provides step\-by\-step instructions for creating a single live room or multiple rooms in bulk using the BytePlus Live console.

<span id="0c4271f3"></span>
## Prerequisite

A BytePlus account or an IAM user. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

<span id="b99e36a4"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. Click **Create live room** on the **Live rooms** page.

   You will be directed to the **Create live room** page. On the **Create live room** page, you can create a single live room or multiple rooms at once.

   * **Create a live room**: On the **Create a live room** tab, configure your live room and click **Save**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a71a04ec8c024d54b94b2a8286fadc82~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">We recommend using a live template. BytePlus Live system templates include typical configurations for scenarios like E\-commerce, Live Marketing, and Online Education.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can also view the configurations of these templates by navigating to <strong>Account center</strong> \><strong>Live templates</strong> in the console.      </div>
      

   * To create multiple live rooms at once: On the **Create multiple live rooms** tab, click **Add live** or click **Add recording**. Complete the configurations as instructed, and then click **Save**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19115025e17647af9a0434aadeae4dfc~tplv-goo7wpa0wc-image.image) </span>

      You can also click **Download template**, edit the file according to the instructions within it and then click **Import** to upload the updated template.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After clicking <strong>Add recording</strong>, you must upload a local video for the live room. After the live room is created, the uploaded video is automatically made available for playback on the viewing page and stored in the <strong>Media library</strong> \> <strong>Videos</strong> \> <strong>Temporary storage</strong>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The time zone for the live stream is UTC+08:00. To change the time zone, go to the <strong>Producer</strong> \> <strong>Basic information</strong> page of the live room.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Before you can select a tag, you must create category tags. For instructions on creating category tags, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tagging-live-streams">Tagging live rooms</a>.      </div>
      


<span id="e59975a0"></span>
## Next step

After creating a live room, you can start a live stream. BytePlus Live provides four methods for livestreaming. The following table describes the available methods for starting a live stream.


|**Broadcast method** |**Description** |
|---|---|
|Web browser |On the live streaming page in a web browser, you can perform operations such as sharing the screen, interacting with viewers, and sending interactive content. For more information, see [Live streaming from your web browser](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser). |
|Pull stream |Pull a live stream from an external source to synchronize it with your BytePlus Live room. Supported pull protocols include RTMP, HLS, and FLV. You can use this method if you want to live stream on multiple platforms at the same time. For more information, see [Pulling streams](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pulling-streams). |
|Prerecorded video |Continuously loop one or more videos for your live stream. You can use this method for marketing live streams or scheduling pre\-recorded videos to be broadcast as a live stream. For more information, see [Starting prerecorded videos](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-the-carousel). |
|Push stream |Get the server URL and stream key to push the live stream to the live room of BytePlus Live. Use this method to allow external providers or hosts using third\-party tools (such as OBS) to push streams to BytePlus Live. For more information, see [Pushing streams (Using OBS as an example)](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pushing-streams). |
