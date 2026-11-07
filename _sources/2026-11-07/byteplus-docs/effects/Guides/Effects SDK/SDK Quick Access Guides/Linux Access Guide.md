---
title: "Linux Access Guide"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-linux-access-guide"
---

<span id="Development Environment"></span>
# Development Environment

<span id="Recommended operating environments:"></span>
## Recommended operating environments:


1. Interface library：qt5

2. gcc/g++

3. Cmake 3.19

4. Opencv enironment


```Plain
sudo apt-get install libdc1394-22-dev libtbb2 libavcodec-dev libavformat-dev libswscale-dev liblapacke-dev libatlas-base-dev libhdf5-dev libtesseract-dev libtesseract-dev libomp5
```



5. System: Ubuntu 18.04 LTS


**Environment Values:** 


* export QT5_PATH=/usr/local/Qt/Qt5.13.2/5.13.2/gcc_64 #qt envrionment

* export EFFECT_SDK=/home/code/sdk/effect\-sdk #effect\-sdk path

* export HEIDI_SDK=/home/code/sdk/heidi\-sdk #heidi\-sdk path


Effect module catalog is as follow:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/0f07a7c-Linux1.png) </span>

Algorithm module catalog is as follow:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/a6b0df1-Linux2.png) </span>

<span id="Sample Operation Guide"></span>
## Sample Operation Guide


1. Install the building environment.


```Plain
apt-get install build-essential  #Install C++ building tool
```



2. Decompress the sample, enter the path of sample.

3. Build.


```Plain
sh build.sh Debug
```



4. After building, the executable file is generated under the path: ./build/Debug/Debug (release version is under the path: "build/Release/Release").


Do the command ./EffectDemo to run the sample.


5. Can use qt creator or vs code to open CMakeLists.txt to develop or debug.


<span id="SDK Integration Guide"></span>
# SDK Integration Guide

The complete process of using the SDK is done in ESSDKProcessor::process(), which includes the initialization and processing.

<span id="Use the SDK in three steps"></span>
## Use the SDK in three steps


6. Initializing the SDK.

7. Using the SDK for Image Processing.

8. Set SDK parameters related to beautification effects, stickers, and filters.


<span id="Initializing the SDK"></span>
### Initializing the SDK

OpenGL

The use of the SDK relies on the opengl environment, using dynamic loading of the angle library


1. First, you need to dynamically load the angle library in the main function and set the function address to libeffect.so, see the code in sample for details:


main.cpp:97


2. The contextual operations of the angle library in the sample are encapsulated in BEF::BEFEffectGLContext


SDK initializing

The initialization of the SDK is performed when the ESSDKProcessor::process() function is first entered, because the use of our SDK needs to be done in the same thread. You can add the debugging point in ESSDKProcessor::initializeProcessor() function to help understand.

<span id="Using the SDK for Image Processing"></span>
### Using the SDK for Image Processing

Interface of image processing is：

```C
EffectHandle::process(GLint texture, GLint textureSticker, int width, int height, bool imageMode, int timeStamp)
```


**Parameters：** 


|**Name** |**Description** |
|---|---|
|texture |Input texture to be processed |
|textureSticker |Output texture |
|width |Width of output texture |
|height |Height of output texture |
|imageMode |Whether image mode is |
|timeStamp |Current time |


<span id="Setting SDK Parameters (Related to Beautification Effects, Stickers, and Filters)"></span>
### Setting SDK Parameters (Related to Beautification Effects, Stickers, and Filters)

 **(1) Face beautification, body shaping, and makeup effects**

Use the same API to configure face beautification, body shaping, and makeup effects. Generally, two steps are required to make a beautification take effect.


1. Set the material path.

2. Set the effect's intensity. The default value is 0, meaning no effect, and it will be used if you do not configure this setting.


**The enter function of setting material path:** 

```C
ESVideoFilterRunnable::updateComposerNode(int subId, int updateStatus, float value)
```


**Parameters：** 


|**Name** |**Description** |
|---|---|
|subId |The type of the effect you want to set, locate the path of the material by this value, and register the type and path in EffectHandle::registerComposerNode |
|updateStatus |0:disable, 1: enable, 2: update the intensity |
|value |Intensity of effect |


 **(2) Setting the sticker**

E**nter function:** 

```C
ESVideoFilterRunnable::setSticker(const QString &stickerPath)
```


**Parameters:** 

stickerPath is the path of sticker.

 **(3) Setting the filter**

**Enter function:** 

```C
ESVideoFilterRunnable::setFilter(const QString &filterPath)
```


**Parameters:** 

filterPath is the path of filter.
