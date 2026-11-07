---
title: "Model labeling"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Model_labeling"
---

<span id="0a9dda5f"></span>
## Scenario description

In AI data lake scenarios, Schema Evolution (模式演进) is a critical capability that enables efficient handling and maintenance of changes in data structures without requiring downtime or rebuilding existing datasets. As business requirements become increasingly complex and data volumes continue to grow, changes in data structures have become the norm. This may involve adding new fields to meet emerging business needs, such as recording more customer information or product features, or even removing fields that are no longer needed to optimize data storage and processing efficiency.

The strength of Schema Evolution lies in its ability to allow data architectures to be flexibly adjusted and expanded at any time, thereby better adapting to business development and changes. At the same time, it maintains access to and compatibility with historical data, ensuring that previous data analysis and processing tasks are not affected, which provides significant convenience and assurance for enterprise data management and utilization.

In image\-centric scenarios, AI models are often used to perform a round of labeling operations on images. For example, aesthetic scoring models can be used to determine the aesthetic score of images in a dataset, assessing image quality. For such scenarios, datasets need to support adding columns. This is because, during image analysis and processing, new features or attributes may need to be recorded, and adding columns makes it easy to integrate this new information into the dataset, providing more comprehensive and accurate data support for subsequent analysis and applications.

<span id="125b7f8a"></span>
## Current solution

Currently, mainstream AI scenarios use WebDataset. WebDataset packages datasets into tar files and provides access via simple URLs, making dataset management and usage more efficient and flexible.

Lance is an efficient columnar storage format based on Apache Arrow, designed to provide fast data storage and retrieval. It is particularly suitable for large\-scale data analytics and machine learning tasks. By leveraging the advantages of columnar storage, Lance delivers high\-performance read and write operations and effective compression when handling large\-scale data.

However, since WebDataset uses a fixed compression format, it is not possible to directly flatten the JSON information contained in the webdataset, making it difficult to quickly filter, select, or query the dataset.

Therefore, Ray can be used to read WebDataset and write it in the Lance format. Ray can also be used to operate on the Lance dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/359757d43eaf4ba983cfec1dfb15c07a~tplv-goo7wpa0wc-image.image) </span>

After adopting the Lance format, model labeling becomes very convenient.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78cb423998f744d4b2bd1d3135a2370c~tplv-goo7wpa0wc-image.image) </span>

Image data is generally stored in the WebDataset format, and computation is performed by reading and processing with Ray.


1. When a Ray task is started, it reads WebDataset data line by line.

2. The model is loaded, inference is performed on the image column, and the predicted label values are obtained.

3. The label values are inserted into the JSON of the Label field.

4. The entire dataset is then written into a new dataset.


<span id="977b4b36"></span>
## Lance solution

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed2da388a555470ba0ea1234a54594e0~tplv-goo7wpa0wc-image.image) </span>

Data is stored in the Lance format, and computation uses either the Ray or Spark engine.

The Image field is directly extracted from the Lance dataset, and a new Lance file containing labels is generated.

Finally, the newly generated Lance file is submitted, completing the labeling process.

<span id="0a84d60d"></span>
## Solution comparison


|**Dimension** |**Current solution** |**Lance solution** |
|---|---|---|
|Data reading |* All WebDataset data must be read, resulting in severe I/O overhead<br><br>* If filtered reading is required, the I/O overhead becomes even more severe |* Columnar storage only reads the image column.<br><br>* If filtered reading is performed, it can skip the filtered columns. |
|Write data |* Write all data, especially, the image field needs to be rewritten. |* Only write the new Label column; the column is small. |


<span id="6cee426f"></span>
## Code example

This code implements distributed aesthetic scoring for images stored in the Lance dataset and writes the results back to the dataset. The main features include:


1. **Image aesthetic scoring**: Uses a pre\-trained vision model to score the aesthetics of images

2. **Distributed processing**: Utilizes the Ray framework to enable multi\-node parallel computation

3. **Data version management**: Ensures data consistency through Lance dataset transaction mechanisms


```Python
import lance
import pyarrow as pa
import pandas as pd
import numpy as np
import torch
import ray
import time
from PIL import Image
import random
from aesthetic_predictor_v2_5 import convert_v2_5_from_siglip
from typing import List, Dict, Any
from io import BytesIO
# TOS configuration
ENV_AK = ''
ENV_SK = ''
storage_options = {}
lance_path = ""
REF_COLUMN_SCHEMA = pa.schema([
    pa.field("jpg", pa.binary())
])
SCORE_SCHEMA = pa.schema([
    pa.field("AESTHETIC_SCORE", pa.float32()),
    pa.field("AESTHETIC_TAG", pa.string())
])


class FragmentScoreColumns:
    def __init__(self, storage_options, lance_path):
        self.ds = lance.dataset(uri=lance_path,
                                storage_options=storage_options)
        self.model, self.preprocessor = convert_v2_5_from_siglip(
            predictor_name_or_path="aesthetic_predictor_v2_5.pth",
            encoder_model_name="siglip-so400m-patch14-384",
            low_cpu_mem_usage=True,
            trust_remote_code=True
        )
        self.model = self.model.to(torch.float32)

    def get_score_tag(self, score: float) -> str:
        if score > 7.1:
            return 'very aesthetic'
        elif 5.5 < score <= 7.1:
            return 'aesthetic'
        elif 3.7 < score <= 5.5:
            return 'displeasing'
        else:
            return 'very displeasing'

    def process_image(self, image_bytes: bytes) -> tuple[float, str]:
        try:
            # Create image from byte stream
            image = Image.open(BytesIO(image_bytes)).convert("RGB")
            pixel_values = self.preprocessor(
                images=image,
                return_tensors="pt"
            ).pixel_values
            with torch.inference_mode():
                score = float(self.model(
                    pixel_values).logits.squeeze().numpy())
            return score, self.get_score_tag(score)
        except Exception as e:
            print(f"Error processing image: {str(e)}")
            return None, "error"
        finally:
            if 'image' in locals():
                image.close()

    def __call__(self, batch):
        fragment_id = batch["item"]
        fragment = self.ds.get_fragment(fragment_id)
        new_fragment, new_schema = fragment.merge_columns(
            value_func=self.generate_aesthetic_scores,
            columns=REF_COLUMN_SCHEMA.names
        )
        return {"fragments": new_fragment, "schema": new_schema}

    ## Apply the model to the jpg column to calculate the score and tag columns
    def generate_aesthetic_scores(self, batch: pa.RecordBatch) -> pa.RecordBatch:
        i = random.randint(0, 10)
        # Retrieve image data column
        image_bytes = batch.column('jpg').to_pylist()
        scores = []
        tags = []
        for img in image_bytes:
            score, tag = self.process_image(img)
            scores.append(score if score is not None else float('nan'))
            tags.append(tag)
        # Create DataFrame and convert to RecordBatch
        df = pd.DataFrame({
            'AESTHETIC_SCORE': scores,
            'AESTHETIC_TAG': tags
        })
        return pa.RecordBatch.from_pandas(df, schema=SCORE_SCHEMA)


def process_lance_dataset(num_workers: int = 10):
    """处理Lance数据集并添加美学评分"""
    print("Loading Lance dataset...")
    lance_ds = lance.dataset(lance_path, storage_options=storage_options)
    print(f"Original schema: {lance_ds.schema}")
    # Retrieve all fragment IDs
    fragment_ids = [f.fragment_id for f in lance_ds.get_fragments()]
    print(f"Processing {len(fragment_ids)} fragments...")
    # Use Ray for distributed processing
    ray_ds = ray.data.from_items(fragment_ids).map(
        FragmentScoreColumns,
        fn_constructor_args=(storage_options, lance_path),
        concurrency=num_workers
    ).take_all()
    print("Committing results to Lance dataset...")
    # Submit to Lance
    merged_fragments = [item["fragments"] for item in ray_ds]
    schema = ray_ds[0]["schema"] if ray_ds else None
    operation = lance.LanceOperation.Merge(merged_fragments, schema)
    dataset = lance.LanceDataset.commit(
        lance_path,
        operation,
        read_version=lance_ds.version,
        storage_options=storage_options
    )
    print("Processing completed!")
    return dataset


if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(
        description="Process Lance dataset for aesthetic scoring")
    parser.add_argument("--num-workers", type=int,
                        default=10, help="Number of workers")
    args = parser.parse_args()
    start_time = time.time()
    ray.init()
    process_lance_dataset(args.num_workers)

    print(f"Total processing time: {time.time() - start_time:.2f} seconds")
```
