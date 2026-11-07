---
title: "Upload SDK overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-upload-sdk-overview"
---

The BytePlus VOD Upload SDK is a comprehensive toolset for uploading media assets to BytePlus VOD. It offers a wide range of features, including upload control, acceleration, and metadata extraction. By seamlessly integrating the Upload SDK into your Android, iOS, or Web applications, you can efficiently handle both user\-generated content (UGC) and professionally generated content (PGC) scenarios.

<span id="bd33ad30"></span>
## Highlights


* **Extensive file format support**: The Upload SDK supports a diverse range of file formats, including audio, video, image, subtitle, and font files.

* **Easy integration**: Integrating the Upload SDK into your apps is straightforward and requires only a few API calls. Additionally, minimal interaction between the Upload SDK and servers significantly reduces upload time.

* **Upload acceleration**: When uploading large files, network fluctuations can lead to retries or incomplete uploads if the entire file is uploaded at once. To address this, the Upload SDK segments large files, mitigating the impact of network fluctuations and enhancing upload speed.

* **Resumable upload**: Network disconnections or interruptions can halt the upload process. However, with the ability to resume uploading from where it left off, you can confidently restart the upload without worrying about external factors affecting the process.

* **Detailed error reporting**: The Upload SDK provides a detailed list of specific errors that may occur during the upload process. Each error is assigned a unique error code, enabling precise identification of the failed step and facilitating accurate error handling.
