---
title: "Saving processed files"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-image-storage"
---

TOS does not save processed images or video frames by default. This section describes how to save these files in a specified bucket by adding a storage parameter to the end of the URL. The following table lists the parameters and examples.

<span id="36ad6e6b"></span>
## **Note**


* To save a processed image or video frame, you must have the read permission on the source bucket and write permission on the target bucket.

* Images and video frames processed by an anonymous user must be saved in a publicly writable bucket.

* The source and target buckets must be in the same region.

* By default, the processed images and video frames are set to Private and saved in Standard Storage.


<span id="9201a111"></span>
## **Parameters**


|**Parameter** |**Description** |Value |**Required** |
|---|---|---|---|
|x\-tos\-save\-object |Specifies the name of the processed image or video frame in the target bucket. The name must be encoded in URL\-safe Base64. |A Base64\-encoded string. |Yes |
|x\-tos\-save\-bucket |Specifies the name of the bucket for saving the processed image or video frame. The name must be encoded in URL\-safe Base64. |A Base64\-encoded string. By default, it is the bucket of the original image or video frame. |No |


<span id="0d949bed"></span>
## **Examples**

You can save a processed image using either of the following methods:


* Use image processing and storage parameters to generate a presigned URL, and then use the URL to store the image. For more information on how to generate a presigned URL through the SDK, see the presignature mechanism document of the corresponding programming language.

* Add a storage parameter to the URL for accessing and processing an image to store the image in a specified bucket. When this method is used, the bucket is accessed in anonymous mode. Therefore, you must assign the Public Write permission to the bucket; otherwise, storage will fail.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The following provides the sample URLs with storage parameters. If you do not have the write permission on the buckets of the sample URLs but try to access the sample URLs, <code>AccessDenied</code> will be returned.</div>


<span id="1895dc13"></span>
### **Saving a resized image**

Processed image URL: [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_100](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_100)


* Name the processed image "abc.png" and store it in the bucket of the original image. The following is the sample URL:

   `https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_100&x-tos-save-object=YWJjLnBuZw==`

* Name the processed image "abc.png" and store it in bucket "arctic". The following is the sample URL:

   `https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/sample.png?x-tos-process=image/resize,w_100&x-tos-save-object=YWJjLnBuZw==&x-tos-save-bucket=YXJjdGlj`


<span id="1442db71"></span>
### **Saving a video fram**

Video frame URL: [https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/misc_video.mp4?x-tos-process=video/snapshot,t_26000,w_400,h_200,f_jpg](https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/misc_video.mp4?x-tos-process=video/snapshot,t_26000,w_400,h_200,f_jpg)


* Save the video frame as "abc.jpg" in the same bucket as the original image:

   `https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/misc_video.mp4?x-tos-process=video/snapshot,t_26000,w_400,h_200,f_jpg&x-tos-save-object=YWJjLnBuZw==`

* Save the video frame as "abc.jpg" in a bucket named "arctic":

   `https://tos-tools.tos-ap-southeast-1.bytepluses.com/misc/misc_video.mp4?x-tos-process=video/snapshot,t_26000,w_400,h_200,f_jpg&x-tos-save-object=YWJjLnBuZw==&x-tos-save-bucket=YXJjdGlj`
