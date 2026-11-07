---
title: "Process screenshots on Web"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1323361"
---

After calling [takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-104478#takelocalsnapshot) / [takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-104478#takeremotesnapshot) to capture a local/remote video frame, usually, you need to process the returned `ImageData` by converting it into formats such as Blob or JPEG for further use. You can refer to the following best practices to achieve this.

<span id="step-1-obtain-imagedata-and-convert-it-to-canvas"></span>
## Step 1: Obtain ImageData and convert it to Canvas

```javascript
// Extract the ImageData object
var imageData = await engine.takeLocalSnapshot(StreamIndex.STREAM_INDEX_MAIN);

// Create a Canvas element and get the context
var canvas = document.createElement('canvas');
var context = canvas.getContext('2d');
canvas.width = imageData.width;
canvas.height = imageData.height;
context.putImageData(imageData, 0, 0);
```


<span id="step-2-convert-canvas-to-other-formats"></span>
## Step 2: Convert Canvas to other formats

<span id="convert-to-blob"></span>
### Convert to Blob

```javascript
// canvas to Blob
canvas.toBlob((blob) => {// Obtain Blob and proceed with further operations
const file = new File([blob], "view.png", { type: "image/png" });
const imgUrl = URL.createObjectURL(file);
const imgElement = document.createElement('img');
    imgElement.src = imgUrl;
    document.body.appendChild(imgElement);
});
```


<span id="convert-to-jpeg"></span>
### Convert to JPEG

```javascript
// canvas to JPEG
const url = canvas.toDataURL('image/jpeg');
const a = document.createElement('a');
a.href = url;
a.download = 'Screenshot-' + Date.now();
a.click();
```


<span id="convert-to-png"></span>
### Convert to PNG

```javascript
// canvas to PNG
const url = canvas.toDataURL('image/png');
const a = document.createElement('a');
a.href = url;
a.download = 'Screenshot-' + Date.now();
a.click();
```
