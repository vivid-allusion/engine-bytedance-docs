---
title: "Perform multimodal vector data retrieval using the Lance data format"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Perform_multimodal_vector_data_retrieval_using_the_Lance_data_format"
---

This article describes how to use LanceDB to perform vector retrieval on multimodal data stored in Lance.

<span id="e00b05b2"></span>
# Dataset and package preparation

This example uses an ImageNet dataset with 100,000 images as an example.


1. Download the dataset:


```YAML
wget https://lance-poc.tos-cn-shanghai.volces.com/public/imagenet.tar
```



2. Install the required Python packages:


```YAML
pip install daft pylance lancedb
```


<span id="f4a5831c"></span>
# Convert images to a Lance dataset using Daft


1. Unzip the dataset:


```YAML
tar -zxvf ./imagenet.tar
```



2. Upload the unzipped data to the TOS path.

3. Use the Daft engine to convert the demo dataset into a Lance dataset:


```Python
import daft
from daft import col
from daft.datatype import DataType
import lance
from PIL import Image
from io import BytesIO
from daft.io import IOConfig, S3Config

ak = "your_ak"
sk = "your_sk"
endpoint = "https://tos-s3-cn-beijing.ivolces.com"


io_config  =IOConfig (
    s3 = S3Config(
        endpoint_url = endpoint,
        key_id = ak,
        access_key= sk,
        region_name="cn-beijing",
        force_virtual_addressing=True,
        verify_ssl=True,
    )
)

IMAGE_DIR = "s3://your_bucket_name/image_original/"
OUTPUT_DATASET_PATH = "s3://your_bucket_name/new_converted_imagenet.lance"

def build_daft_dataframe(image_dir: str) -> daft.DataFrame:
    pattern = f"{image_dir.rstrip('/')}/*.JPEG"
    df = daft.from_glob_path(pattern, io_config=io_config)
    # Download binary data directly via Daft's URL mode
    df = df.with_column("image", df["path"].url.download(io_config=io_config))
    # Explicitly set as binary type
    df = df.with_column("image", col("image").cast(DataType.binary()))
    # You can retain the path for debugging, or keep only the image
    df = df.select(df["path"], df["image"])
    return df

def main():
    df = build_daft_dataframe(IMAGE_DIR)
    # Only one image folder, directly overwrite or create the dataset
    df.write_lance(OUTPUT_DATASET_PATH, io_config=io_config, mode="overwrite")

if __name__ == "__main__":
    main()
```


<span id="cbf1b9f7"></span>
# Generate embeddings for the dataset using LanceDB

To support subsequent vector\-based semantic image retrieval, we first need to convert images into **vectorized** representations. This process is called **embedding**. Generating embeddings depends on an embedding model. We choose the open\-source open\-clip model. To support semantic retrieval, we select a multimodal model that supports both **image encoder** and **text encoder** for embedding, with both outputs residing in the same semantic vector space.

```Python
import lance
import lancedb
from lancedb.embeddings import EmbeddingFunctionConfig, EmbeddingFunctionRegistry

registry = EmbeddingFunctionRegistry.get_instance()
clip = registry.get("open-clip").create(device="cuda", batch_size=8192)
conf = EmbeddingFunctionConfig(source_column="image", vector_column="vector", function=clip)

storage_options = {
    "access_key_id": "your_ak",
    "secret_access_key": "your_sk",
    "aws_endpoint": "https://{your_bucket_name}.tos-s3-cn-beijing.volces.com",
    "virtual_hosted_style_request": "true"
}

uri = "s3://your_bucket_name/image_original/image_vector_demo/"
ds=lance.dataset("s3://your_bucket_name/image_original/image_vector_demo/imagenet.lance", storage_options=storage_options)
db = lancedb.connect(uri)
table = db.create_table("image_with_vector", data=ds, embedding_functions=[conf])
```


<span id="951030ba"></span>
# Perform semantic retrieval on the dataset using LanceDB

LanceDB supports direct semantic retrieval on embeddings without relying on the creation of a vector index. However, in production environments, we strongly recommend creating a vector index before performing retrieval.

For demonstration purposes, we use LanceDB's semantic retrieval API here. In daily use, we can also perform retrieval directly with Pylance, but we need to embed the query text first. The following is a code snippet based on Jupyter that displays the retrieval recall results after decoding with base64:

```Python
# tool for display binary
def display_subset_images(data):
    html_output = "<div style='display:flex; flex-wrap:wrap; gap:20px;'>"
    
    for idx, row in data.iterrows():
        path = row["path"]
        image_data = row["image"]
        
        if isinstance(image_data, bytes):
            b64_str = base64.b64encode(image_data).decode("utf-8")
        else:
            b64_str = image_data
        
        html_output += f"""
        <div style='border: 1px solid #ddd; padding: 10px; border-radius: 5px;'>
            <p><b>路径:</b> {path}</p>
            <img src='data:image/png;base64,{b64_str}' 
                 style='max-width: 300px; max-height: 200px; object-fit: contain;'/>
        </div>
        """
    
    html_output += "</div>"
    display(HTML(html_output))
    
result=table.search("a house").to_pandas()
display_subset_images(result)
```


The result is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3d6b119508543cfacb6878803374bbf~tplv-goo7wpa0wc-image.image) </span>
