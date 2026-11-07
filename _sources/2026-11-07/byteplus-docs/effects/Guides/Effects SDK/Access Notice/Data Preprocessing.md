---
title: "Data Preprocessing"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-data-preprocessing"
---

<span id="Abstract"></span>
## Abstract

Before we input the original image into our algorithm module, we often need to perform multiple preprocessing tasks on the image, such as size compression, angle rotation, and format conversion.

<span id="Input Image Format Selection"></span>
## Input Image Format Selection

For image detection algorithm functions, such as human keypoints, portrait keypoints, and gestures, the input formats supported by our interface input are shown in the following table:


|**Format** |
|---|
|RGBA8888 |
|RGBA8888 |
|BGR888 (Portrait, Gesture) |
|RGB888 (Portrait, Gesture) |
|NV21 |
|NV12 |
|YUV420P |


RGB data can be directly inputted into our SDK, and YUV data can be converted through our YUV2RGB conversion interface.

For the image special effects functions, such as face beautification and stickers, the input and output formats supported by our interface are shown in the following table:


|**Format** |
|---|
|glTexture2D |
|RGBA8888 |
|BGRA8888 (for input only) |
|NV21 |
|NV12 |
|YUV420P |


Because the image special effects algorithms mainly complete image processing and rendering processes using the GPU, we recommend using glTexture2D as input to reduce the time loss caused by the data going through the CPU memory and video memory. If you use YUV format data as input, we will use Shader at the bottom to convert YUV to RGBA format, and then generate textures for special effect processing. In this case, you can also convert the YUV data to RGBA8888 format externally, and then input it into the special effects processing interface. The difference between the two solutions is that the former is to complete the YUV to RGB format conversion in the GPU, and the latter is in the CPU. The solution chosen depends on the actual operating environment.

<span id="Input Image Size Settings"></span>
## Input Image Size Settings

The size of the input image affects the performance and results of the algorithm \- size that is too large decreases the algorithm's running speed, and a size that is too small leads to reduced result prediction accuracy. The following table contains our suggested input sizes for different algorithm modules.

When the portraits output by the camera are straight, we recommend the following minimum input size for portrait image orientation (width < height):


|**Algorithm** |**Width (pixels)**  |**Height (pixels)**  |
|---|---|---|
|106\-Point Portrait |128 |224 |
|280\-Point Portrait |360 |640 |
|Portrait attributes |360 |640 |
|Gesture keypoints and detection |360 |640 |
|Bone detection |128 |224 |
|Body segmentation |128 |224 |
|Hair segmentation |128 |224 |
|Portrait comparison |128 |224 |


When the portraits output by the camera are straight, we recommend the following minimum input size for landscape image orientation (height < width):


|**Algorithm** |**Width (pixels)**  |**Height (pixels)**  |
|---|---|---|
|106\-Point Portrait |224 |128 |
|280\-Point Portrait |640 |360 |
|Portrait attributes |640 |360 |
|Gesture keypoints and detection |640 |360 |
|Bone detection |224 |392 |
|Body segmentation |224 |128 |
|Hair segmentation |224 |128 |
|Portrait comparison |224 |128 |


The above sizes are recommended for mobile phones. If the device is not a mobile phone, the input size may be different.

<span id="Input Image Orientation Settings"></span>
## Input Image Orientation Settings

The detection angle needs to be input into all our algorithm interfaces. The detection angle n means that the face is in an upright position after rotating n degrees clockwise. Because the mobile phone itself may also rotate in space, we rotate the texture to an upright position in the texture preprocessing stage in the demo, thus the angle obtained by the mobile phone sensor is directly used as the detection angle. If the face in the source image is not at the upright position, such as the YUV data outputted from the Android camera, the rotation angle of the phone gesture needs to be superimposed on the basis of the YUV rotation angle.

In addition, our SDK provides an interface for data conversion between YUV format and RGBA format. This interface supports rotating, scaling, and flipping (required for the front\-facing camera) while converting the YUV data format.

Generally, the output of the Android rear\-facing camera needs to be rotated 90 degrees clockwise, and 270 degrees clockwise for the front\-facing camera. To ensure that the visual effects work, we usually perform a horizontal mirror operation on the front\-facing camera output to achieve the effect of how we see ourselves in a mirror. The output of the iOS native camera is in portrait orientation, with no need to rotate.

<span id="Explanation of the algorithm input image parameter "stride""\>

<span id="explanation-of-the-algorithm-input-image-parameter-stride"></span>
## Explanation of the algorithm input image parameter "stride"

It can be understood as the number of bytes occupied by each line of the image. However, the conventional input interface does not accept byte\-aligned image data. Taking RGBA data as an example: stride can default to image_width\*4
