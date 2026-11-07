---
title: "About Metal Rendering"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-about-metal-rendering"
---

As a graphics API officially supported by Apple, Metal has better adaptability and performance on Apple devices. During iOS development, some developers will expect to support Metal to process textures processed by CVSDK.

<span id="813766a9"></span>
# Solution Introduction

An example of a Metal\-enabled rendering environment is written in the 4.4.0 demo, and customers can use Metal rendering instructions to process textures through the SDK .

When creating CVPixelBuffer, Metal and OpenGL compatibility options are supported.

By binding CVPixelBuffer to MTLTexture, a cache area operated by GL and Metal can be created. Therefore, MTLTexture can be set as a property of BEPixelBufferGLTexture to directly access its bound Metal texture from pixelbuffer.

BEMTLView is responsible for the creation of the Metal environment and the execution of rendering on screen(rendering the textures processed by the SDK to the screen).

<span id="d717116e"></span>
# Sample code

Since the metal rendering environment is the logic of implements layer, this document only describes the related code provided in the sample.

This example code can be use as a reference, developers can check how we achieve the metal rendering with our SDK, and write your own logic.

<span id="2ecfa85f"></span>
## Tools function

This part describes the utility code in the sample, involving utility functions such as texture transformation.

<span id="282c2af0"></span>
### 1.CVPixelBuffer convert MTLTexture

The location of the sample code in the sample: **Core/Core/Utils/BEImageUtils.h [.m]** 

Add the utility function of CVPixelBuffer to MTLTexture, directly copy the memory area of pixelbuffer, and create a new mtltexture;

if you use BEPixelBufferGLTexture, you do not need to call this interface, and directly access the mtltexture corresponding to pixelbuffer.

```objectivec
// New interface:
///@Briefing CVPixelBuffer to metal texture
/// @param pixelBuffer CVPixelBuffer 
- (id<MTLTexture>)transformCVPixelBufferToMTLTexture:(CVPixelBufferRef)pixelBuffer;
```


<span id="2d17b894"></span>
### 2. Extensions to define BEPixelBufferGLTexture

The location of the sample code in the sample: **Core/Core/Utils/BEGLTexture.h [.m]** 

Extensions to define BEPixelBufferGLTexture

```objectivec
// Class definition extension: (only the new part is written)
//{en} /Internally completed the binding of CVPixelBuffer to gl texture and mtl texture. After the texture is processed,
//{en} /Call pixelBuffer directly to get the processed CVPixelBuffer
@interface BEPixelBufferGLTexture : NSObject <BEGLTexture>

@property (nonatomic) id<MTLTexture> mtlTexture;

//{en} CVMetalTextureCacheRef initialization according to CVMetalTextureCacheRef
- (instancetype)initWithMTKTextureCache:(CVMetalTextureCacheRef)textureCache;

//{en} CVMetalTextureCacheRef initialization based on width, height
- (instancetype)initWithWidth:(int)width height:(int)height mtlTextureCache:(CVMetalTextureCacheRef)textureCache;

//{en} /@Briefing initialization based on CVPixelBuffer 
- (instancetype)initWithCVPixelBuffer:(CVPixelBufferRef)pixelBuffer mtlTextureCache:(CVMetalTextureCacheRef)textureCache;

@end
```


<span id="cf0c9ee6"></span>
### 3.Data types and buffer indexes in MSL (Metal Shader Language)

The location of the sample code in the sample: **Core/Core/Utils/BEShaderTypes.h**

Contains data such as data types and buffer indexes in MSL (Metal Shader Language).

<span id="603ef4a2"></span>
## Implementation part

This part of the doc is the location of the drawing, screen and UI implementation code in the sample, which can be checked and referenced to write your own logic, according to the actual situation of your project.

<span id="db84c073"></span>
### 1. Draw

Location of sample code in sample: Common/Common/ui/view/content/BEMTLView.h [.m]

Responsible for the creation of the Metal environment, and Metal\-related rendering instructions, are completed in the (void) drawRect:(CGRect)rect.

```objectivec
//New interface:
//Called when the screen width and height are updated
- (void)resetWidthAndHeight;
//draw mtltexture to this view
- (void)renderWithTexture:(id<MTLTexture>)texture
                     size:(CGSize)size
      applyingOrientation:(int)orientation
                  fitType:(int)fitType;
```


<span id="18a15ee6"></span>
### 2. On the screen

Location of sample code in sample: Common/Common/ ui / vc /BEBaseVC.h [.m]

Add the BEMTLView property object and drawTextureOnScreen function to the VC base class.

```objectivec
//Newly added interface:
//Draw to BaseVC's property member mtlView with metal texture as input

//{en}/@param rotation angle
- (void)drawMTLTextureOnScreen:(id<BEGLTexture>)texture rotation:(int)rotation;
```


<span id="a5bf2ef1"></span>
### 3. Save

The location of the sample code in the sample: Common/Common/ui/vc/BEBaseBarVC.m

Complete the logic of saving the sdk processing result to the local.

<span id="06c1cb51"></span>
### 4. Beauty body shaper module UI supports metal


* Location of sample code in sample: Effect/Effect/ ui /base/ vc /BEEffectVC.h [.m]

   This version update only adds the functions supported by metal to the effects module, so the metal environment and business logic are completed in this VC . Responsible for adding UI options supported by Metal rendering.

* The position of the sample code in the sample: Effect/Effect/ ui /effect/ vc /BEBeautyEffectVC.m

   Added metal rendering support for the beauty & face reshaping module.


<span id="a8417d09"></span>
### 5. shader file for metal in sample

The position of the example in the sample: app/app/metal/fundamental.metal

This is the shader file of metal, because it directly participates in the compilation, needs to be placed in the non\-static library directory (in the demo, that is, under the app project).

This part of the shader file is a demo example, which can be set according to your own project environment, it is not necessary to use the examples provided in the sample.
