---
title: "Metadata for AI-generated content"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/metadata_for_ai-generated_content"
---


|Parameter |Name |Data Type |Description |
|---|---|---|---|
|Label |Generate composite label |string |* `1` : The content is AI\-generated<br><br>* `2` : The content is potentially AI\-generated<br><br>* `3` : The content is suspected to be AI\-generated |
|ContentProducer |Synthetic service provider |string |The name or code of the synthetic service provider |
|ProduceID |Content production ID |string |The unique identifier assigned to the content by the synthetic service provider |
|ReservedCode1 |Reserved field 1 |string |Reserved for synthetic service providers to implement their own security measures and ensure the integrity of the content and identifier |
|ContentPropagator |Content propagation service provider |string |The name or code of the content propagation service provider |
|PropagateID |Content propagation ID |string |The unique identifier assigned to the content by the content propagation service provider |
|ReservedCode2 |Reserved field 2 |string |Reserved for content propagation service providers to implement their own security measures and ensure the integrity of the content and identifier |
