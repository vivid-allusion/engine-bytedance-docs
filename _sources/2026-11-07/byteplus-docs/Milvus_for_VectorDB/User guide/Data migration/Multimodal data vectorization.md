---
title: "Multimodal data vectorization"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Multimodal_data_vectorization"
---

The embedding node in the data migration workflow supports the configuration of the doubao multimodal vectorization model (doubao\-embedding\-vision\-250615), which can perform mixed multimodal vectorization on multiple data types including text, pictures, and videos, then write the vectors into a Milvus for VectorDB instance.

The doubao multimodal vectorization model API supports accessing data via URL and also accepts Base64\-encoded pictures or video data in the request body, but the request body size has certain limits. See [Multimodal vectorization API](https://docs.byteplus.com/en/docs/ModelArk/1523520) for details.

<span id="oQgbKitL"></span>
## Multimodal data storage and retrieval

<span id="a1Y5F6Ok"></span>
### File storage

Picture and video files are usually large and are generally stored in TOS. Only the corresponding address needs to be recorded in the data row; the files can be read and downloaded from TOS at runtime.

<span id="ko1DDu1w"></span>
### Model Retrieval

The model needs to download pictures or video files to be vectorized before vectorization. TOS’s [pre-signed mechanism](https://docs.byteplus.com/en/docs/tos/Pre-signature-mechanism3) can directly issue URLs to download objects without requiring additional authentication information. Input pictures and videos require a pre\-signed mechanism; the model can download these resources directly during vectorization.

<span id="ZyLJ1xAe"></span>
### Sample data

The sample data is as follows. The pictures and videos involved in the data are all stored in TOS, with only the pre\-signed URLs of the file objects saved in the fields.

```JSON
{
  "description": "多模态数据测试",
  "text": "图片和视频分别是什么",
  "image": "https://xxx-project.tos-cn-beijing.volces.com/doc_image/tower.png?${pre_signature}",
  "video": "https://xxx-project.tos-cn-beijing.volces.com/doc_video/ark_vlm_video_input.mp4?${pre_signature}"
}
```


<span id="mXexxhSz"></span>
## Multimodal data vectorization

The Embedding node configuration in the data migration workflow is as follows. It supports vectorizing single text, picture, or video as well as vectorizing multiple texts, pictures, or videos in the same or different modalities. For detailed operations, see [Create a workflow](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_workflow).

<span id="2JRXQVfj"></span>
### Configuration specification

Multimodal data requires specifying `field`, `modality` (default `text`), and `format` (default `text`).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The Embedding node supports automatic modality detection. When <code>modality</code> is not explicitly specified and <code>format</code> is not <code>binary</code>, the system automatically detects the modality type based on the file extension of the field value.</div>



|configuration key |Description |Value range |
|---|---|---|
|field |Data source. |upstream node output fields |
|modality |Modality type. |* Pictures: jpeg (jpg, jpeg), png (png, apng), gif, webp, bmp (bmp, dib), tiff (tiff, tif), ico, icns, sgi, jpeg2000 (j2c, j2k, jp2, jpc, jpf, jpx).<br><br>* Videos: mp4, avi, mov.<br><br>* Text: text (default). |
|format |Data format. |* text: text format (default).<br><br>* url: URL format.<br><br>* binary: binary data format. |


<span id="AZi2ZSrV"></span>
### Configuration example

```JSON
{
  # 指定 Embedding 模型 API 地址
  "api_path": "https://ark.cn-beijing.volces.com/api/v3/embeddings/multimodal",
  "vectorization_fields": {
    # 单个文本字段 Embedding
    "text_vector": "text",
    # 单个图片字段 Embedding（显示指定模态类型）
    "image_vector": {
      "field": "image",
      "modality": "png",
      "format": "url"
    },
    # 单个视频字段 Embedding
    "video_vector": {
      "field": "video",
      "modality": "mp4",
      "format": "url"
    },
    # 多个同模态字段 Embedding
    "multi_field_text_vector": [
      "text",
      "description"
    ],
    # 多个多模态字段 Embedding
    "multi_field_mix_vector": [
      "text",
      {
        "field": "image",
        "modality": "png",
        "format": "url"
      },
      {
        "field": "video",
        "modality": "mp4",
        "format": "url"
      }
    ]
  }
}
```
