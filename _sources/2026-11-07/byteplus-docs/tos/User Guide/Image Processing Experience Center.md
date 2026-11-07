---
title: "Image Processing Experience Center"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Image-processing-experience-center"
---

The TOS console integrates functions such as image cropping and watermarking, enabling visual configuration of image processing for quick feature experience. This article explains the usage limits and operation steps of image cropping and watermarking functions in the TOS console.

<span id="6d38671f"></span>
## Feature introduction

Previously, TOS only supported image cropping and watermarking by sending related parameters through the GetObject interface request; for details, see [Image Processing Overview](https://docs.byteplus.com/docs/tos/docs-overview_2).

To enhance user experience, the TOS console now integrates image cropping and watermarking features, providing visual management of image processing through a graphical interface. You can crop stored images or adjust brightness in the TOS console. After processing, you can directly download the processed image or store it in a specified bucket. The TOS console supports the following image processing operations:


|Category |Image processing operations |
|---|---|
|Crop |Custom cropping |
||Incircle crop |
||Rounded rectangle |
|Effect |Image brightness |
||Image contrast |
||Image rotation |
||Image sharpening |
||Image blur |
|Watermark |Image watermark |
||Text watermark |


<span id="99e9dbbd"></span>
## Usage limits


|**Category** |**Usage limits** |
|---|---|
|Format |Image processing operations only support original images in jpg/jpeg, png, bmp, gif, webp, and tiff formats. |
|Size |* The source image can be up to 20 MB.<br><br>* The source image can have up to 30,000 pixels in width and height, with a total of up to 250 million pixels. The width and height cannot exceed 4,096 pixels for rotation operations. |
|QPS |The QPS limit for image processing operations in each region is 50.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you have a compute\-intensive workload or usage that exceeds these limits, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001170">submit a ticket</a> to consult with our technical team or your designated account manager.</div><br> |
|Concurrency |The default concurrency limits for processing images are as follows:<br><br><br>* China (Beijing): 20<br><br>* Other regions: 10<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you have a compute\-intensive workload or usage that exceeds these limits, submit a ticket to consult with our technical team or your designated account manager.</div><br> |
|Server\-side encryption |Supports processing images encrypted with SSE\-TOS, SSE\-C, and SSE\-KMS. Usage restrictions are as follows:<br><br><br>* SSE\-C encryption<br><br>   * When processing images encrypted with SSE\-C, you must include the SSE\-C headers `x-tos-server-side-encryption-customer-algorithm`, `x-tos-server-side-encryption-customer-key`, and `x-tos-server-side-encryption-customer-key-MD5`. For detailed information on SSE\-C headers, see [Server-side encryption with customer-provided keys (SSE-C)](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).<br><br>   * Adding image watermarks to images encrypted with SSE\-C is supported, but using SSE\-C encrypted images as watermarks on other images is not supported. For example, if images aaa and bbb are encrypted with SSE\-C and image ccc is not encrypted with SSE\-C, you can add image ccc as a watermark on image bbb, but you cannot add image aaa as a watermark on image bbb.<br><br>* SSE\-KMS encryption<br><br>   Anonymous processing of images encrypted with SSE\-KMS is not supported. You must enable the KMS service and have permission to access the master key to process SSE\-KMS encrypted images with a valid signature. |


<span id="5963aa23"></span>
## Image cropping


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, select **Multimedia Experience Center** \> **Image Processing**.

3. In the top navigation bar of the **Image Processing Experience Center** page, select the bucket storing the images.

4. In the image upload area, click **Select image**.

5. In the **Select file** dialog, choose the image and click **OK**.

6. In the left operation bar, click **Crop**, select the cropping method, and configure the parameters accordingly.

   * Standard cut

      Standard cropping requires specifying any point on the original image as the starting coordinate to crop an area with the specified width and height.

      
      |**Parameter** |**Note** |
      |---|---|
      |Crop start position |Origin of coordinates for cropping. |
      |Abscissa of starting point |X\-axis offset to the origin.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">On the x\-axis, positive values indicate offset to the right, and negative values indicate offset to the left.</div><br> |
      |Starting ordinate |Y\-axis offset to the origin for the starting point of cropping.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">On the y\-axis, positive values indicate offset downward, and negative values indicate offset upward.</div><br> |
      |Width |Clipping width, unit in px. |
      |Height |Clipping height, unit in px. |
      |Crop shape |Crop the image into a **rectangle**, **rounded rectangle**, or **round** as follows:<br><br><br>* **rectangle**: Crop the image into a rectangle using the width and height set previously.<br><br>* **rounded rectangle**: Specify the corner radius to crop the image into a rounded rectangle.<br><br>* **round**: Specify the radius; crop the image into a circle centered on the image with the given radius. |
      

   * Free cropping

      Free cropping requires specifying the crop ratio first. The system will generate an adjustable area on the image according to the ratio. You can drag and resize this area freely, and TOS will crop the image based on the selected range.

      
      |**Parameter** |**Note** |
      |---|---|
      |Select crop ratio |Create a resizable area proportionally. You can drag and scale the area freely. TOS will crop the image based on the selected range. Steps:<br><br>Click **Start cropping**, choose the crop ratio, then drag to adjust the crop area. After selecting the area, click **Confirm crop**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only original images support cropping.</div><br> |
      |Crop shape |Crop the image into a **rectangle**, **rounded rectangle**, or **round**. Details are as follows:<br><br><br>* **rectangle**: crop the image into a rectangle according to the selected area above.<br><br>* **rounded rectangle**: specify the corner radius to crop the image into a rounded rectangle.<br><br>* **round**: specify the radius. The image will be cropped into a circle centered on the image center based on the specified radius. |
      

      After setting the parameters, TOS automatically crops the image according to the configuration. You can view the cropped image in the image upload area.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">On the <strong>Image Processing Experience Center</strong> page top navigation bar, press and hold the compare icon to view the image before processing; release to restore the processed image; click the reset icon to revert the image to its original state.      </div>
      

7. Export the processed image.

   * Download the processed image

      On the top right of the **Image Processing Experience Center** page, click **Download** to download the processed image locally.

   * Share the processed image

      On the top right of the **Image Processing Experience Center** page, click **Copy Link** to share this pre\-signed link with others, allowing them to access the processed image via the link.

   * Save the processed image to a specified bucket

      At the bottom of the **Image Processing Experience Center** page, click the copy button to obtain the image crop parameters, append these parameters to the image URL, then add persistence parameters to save the processed image to the specified bucket. For detailed information, see [image processing persistence](https://docs.byteplus.com/docs/tos/docs-image-storage).


<span id="a2744e76"></span>
## Image effects


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, select **Multimedia Experience Center** \> **Image Processing**.

3. In the top navigation bar of the **Image Processing Experience Center** page, select the bucket storing the images.

4. In the image upload area, click **Select image**.

5. In the **Select file** dialog, choose the image and click **OK**.

6. In the left action pane, click **Effects** and configure the corresponding parameters.

   
   |**Parameter** |**Note** |
   |---|---|
   |Brightness |Adjust the image brightness within the range [\-100, 100]. The parameters are described below:<br><br><br>* A negative value decreases brightness.<br><br>* The value 0 indicates no brightness adjustment.<br><br>* A positive value increases brightness. |
   |Contrast Ratio |Adjust the image contrast with a value range of [\-100, 100]. Details are as follows:<br><br><br>* A negative value decreases the contrast.<br><br>* The value 0 indicates no contrast adjustment.<br><br>* A positive value increases the contrast. |
   |Spin |Rotate the image clockwise; you need to set the clockwise rotation angle.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If the rotation angle is not 90°, 180°, 270°, or 360°, the processed image will be larger in size.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The rotation function limits the image size; the width or height cannot exceed 4096 px.</div><br> |
   |Sharpen |Adjust the image sharpening effect, with a range of [50,399].<br><br>The larger the value, the clearer the image. A larger value may distort the image. The recommended value is 100 for the optimal effect. |
   |Blurry |Apply a blur effect to the image, described as follows:<br><br><br>* **Blur Radius**: Range is [1,50]; the higher the value, the more blurred the image.<br><br>* **Standard Deviation in Gaussian Blur**: Range is [1,50]; the higher the value, the more blurred the image. |
   

   After setting the parameters, TOS automatically processes the images according to the configuration. You can view the processed images in the image upload area.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the <strong>Image Processing Experience Center</strong> top navigation bar, long press the compare icon to view the image before processing; release to revert to the processed image. Click the reset icon to restore the image to its original state.   </div>
   

7. Export the processed image.

   * Download the processed image

      At the top right of the **Image Processing Experience Center** page, click **Download** to save the processed image locally.

   * Share the processed image

      At the top right of the **Image Processing Experience Center** page, click **Copy Link** to share the pre\-signed link with others, allowing them to access the processed image via this link.

   * Save the processed image to the specified storage bucket

      At the bottom of the **Image Processing Experience Center** page, click the copy button to obtain the image processing parameters. Append these parameters to the image URL, add persistence parameters, and save the processed image to the specified storage bucket. For details, refer to [Image Processing Persistence](https://docs.byteplus.com/docs/6349/762921).


<span id="c066607e"></span>
## Image watermark


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, select **Multimedia Experience Center** \> **Image Processing**.

3. In the top navigation bar of the **Image Processing Experience Center** page, select the bucket storing the images.

4. In the image upload area, click **Select image**.

5. In the **Select file** dialog, choose the image and click **OK**.

6. In the left action pane, click **Watermark**, select **Watermark method**, then configure the corresponding parameters.

   * Image watermark

      
      |**Parameter** |**Description** |
      |---|---|
      |Watermark image |Select the watermark image.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The watermark image must be in the same storage bucket as the original image.</div><br> |
      |Scale |Resize the watermark image by percentage. |
      |Watermark Location |Select the watermark position on the image and set the vertical and horizontal margins for the watermark.<br><br><br>* Vertical margin: the vertical distance from the image edge. This parameter applies only when the watermark is positioned at upper left, upper middle, upper right, lower left, lower middle, or lower right.<br><br>* Horizontal margin: the horizontal distance from the image edge. This parameter is valid only when the watermark is on the upper left, middle left, lower left, upper right, middle right, or lower right of the image. |
      |Opacity |Opacity of the watermark image; the higher the value, the higher the opacity. |
      

   * Text watermark

      
      |**Parameter** |**Note** |
      |---|---|
      |Text content |Text watermark content.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The text watermark feature does not currently support Traditional Chinese.</div><br> |
      |Text Font |Font of the text watermark. |
      |Text size |Font size of the text watermark. |
      |Text Rotation |Degree of the clockwise rotation of the text watermark. |
      |Text Color |Font color of the text watermark. Hexadecimal color code, ranging from 000000 to FFFFFF. |
      |Text Filling the Space |Fill the original image with watermark text. |
      |Text Shadow |Text watermark shadow.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Text shadow function does not work after text rotation.</div><br> |
      |Watermark Location |Select the watermark placement on the image and set the vertical and horizontal margins.<br><br><br>* Vertical margin: the vertical distance from the edge of the image. This parameter is valid only when the watermark is positioned at the upper left, upper center, upper right, lower left, lower center, or lower right of the image.<br><br>* Horizontal margin: the horizontal distance from the edge of the image. This parameter is valid only when the watermark is on the upper left, middle left, lower left, upper right, middle right, or lower right of the image. |
      |Opacity |The opacity of the watermark text; the higher the value, the more opaque it is. |
      

   After setting the parameters, TOS automatically processes the images based on the configuration. You can view the processed images in the image upload area.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the top navigation bar of the <strong>Image Processing Experience Center</strong> page, long\-press the comparison icon to view the image before processing; release to restore the processed image. Click the reset icon to revert the image to its original state.   </div>
   

7. Export the processed image.

   * Download the processed image

      In the top right corner of the **Image Processing Experience Center** page, click **Download** to save the processed image locally.

   * Share the processed image

      In the top right corner of the **Image Processing Experience Center** page, click **Copy link** to share the pre\-signed link with others. Users can access the processed image via this link.

   * Save the processed image to a specified bucket

      At the bottom of the **Image Processing Experience Center** page, click the copy button to obtain the image processing parameters, append them to the image URL, add persistence parameters, and then save the processed image to the specified bucket. For details, see [Image Processing Persistence](https://docs.byteplus.com/docs/6349/762921).
