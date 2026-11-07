---
title: "Lake format conversion: Ray reads WebDataset and writes to Lance"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/lake_format_conversion"
---

<span id="bf1a6ea2"></span>
## Background

WebDataset makes dataset management and usage more efficient and flexible by packaging datasets into tar files and providing access through simple URLs.

Lance is an efficient columnar storage format based on Apache Arrow, designed to provide fast data storage and retrieval. It is particularly suitable for large\-scale data analysis and machine learning tasks. Lance leverages the advantages of columnar storage to deliver efficient read and write performance and compression when handling large\-scale data.

Because WebDataset uses a fixed compressed format, it is not possible to directly flatten JSON information and other data contained in the WebDataset, making it difficult to quickly filter, select, or query the dataset.

Therefore, this article provides a paradigm for reading WebDataset with Ray and writing to Lance. And operate on Lance datasets using Ray.

<span id="9b2a4677"></span>
## Data architecture

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c4c095b92324758911c0a6d51165b75~tplv-goo7wpa0wc-image.image) </span>

<span id="14c41fa1"></span>
## Code example

```Python
import ray
import logging
from lance.ray.sink import LanceDatasink
from tosfs.core import TosFileSystem
import pyarrow as pa
import numpy as np
from ray.data.dataset import Schema
from ray.data._internal.pandas_block import PandasBlockSchema
from PIL import Image
import io
import json

# Convert dict read from WEBDATASET to the schema required by Lance (PyArrow)

class TypeConverter:

    def __init__(self,
                 dataset_schema: Schema,
                 required_schema: pa.lib.Schema = None,) -> None:
        self.field_names = dataset_schema.names
        if required_schema is not None:
            self.schema = required_schema
        elif isinstance(dataset_schema.base_schema, pa.lib.Schema):
            self.schema = required_schema
        elif isinstance(dataset_schema.base_schema, PandasBlockSchema):
            self.schema = self.speculation_type(dataset_schema)
        else:
            raise ValueError(
                f"Unsupported schema type: {type(dataset_schema.base_schema)}")

    def __call__(self, batches) -> pa.Table:
        columns = {}
        for field_name in self.field_names:
            column_data = batches[field_name]
            if (field_name == "json"):
                parsed_json = json.loads(column_data[0].decode("utf-8"))
                for key in parsed_json.keys():
                    if key in self.schema.names:
                        columns[key] = [json.loads(item.decode(
                            "utf-8"))[key] for item in column_data]
            else:
                columns[field_name] = column_data
        return pa.Table.from_pydict(columns, schema=self.schema)

# TOS AK
ENV_AK = ''
# TOS SK
ENV_SK = 'xx=='
# REGION
ENV_REGION = 'cn-beijing'

# Only for lance REGION
S3_ENV_REGION = 'beijing'

# TOS ENDPOINT
TOS_ENV_ENDPOINT = "https://tos-" + ENV_REGION + ".ivolces.com"
# Name of the bucket for storing data
ENV_BUCKET = "test"
# Endpoint for S3 protocol
S3_ENV_ENDPOINT = "https://" + ENV_BUCKET + \
    ".tos-s3-" + ENV_REGION + ".ivolces.com"
# Directory for storing data
ENV_BASEDIR = ENV_BUCKET + "/datasource/"
# File types downloaded from WEBDATASET
FILE_TYPES = ["json", "jpg"]

# Convert to the schema required by LANCE; check the implementation of TypeConverter here
REQUIRED_SCHEMA = [pa.field("SAMPLE_ID", pa.float64()),
                   pa.field("HEIGHT", pa.float32()),
                   pa.field("WIDTH", pa.float32()),
                   pa.field("jpg", pa.binary()),
                   pa.field("URL", pa.string()),
                   pa.field("TEXT", pa.string()),
                   pa.field("LICENSE", pa.string()),
                   pa.field("NSFW", pa.string()),
                   pa.field("similarity", pa.float64()),
                   ]

TOS_ROOT_DIR = "tos://" + ENV_BASEDIR
S3_ROOT_DIR = "s3://" + ENV_BASEDIR
# Directory where the data is located
input_dir = TOS_ROOT_DIR + "webdataset/"
# The goal is to use the Lance AWS SDK directly, so the format must not include the TOS protocol and should follow the S3 protocol
output_dir = S3_ROOT_DIR + "lance/"

# Ray environment initialization
ray.init(runtime_env={
    "env_vars": {"TOSFS_LOGGING_LEVEL": "INFO", "LANCE_LOG": "INFO"},
    "pip": ["pylance", "tosfs"]
})
# Involves backpressure; adjust as needed when used together
data_context = ray.data.context.DataContext()
data_context.op_resource_reservation_enabled = False
logging.basicConfig(level=logging.INFO)

# Custom parsing function
# Data source: https://huggingface.co/datasets/laion/clevr-webdataset/tree/main/train
# Data format: https://huggingface.co/datasets/laion/clevr-webdataset
# Detailed settings: https://tosfs.readthedocs.io/en/latest/api.html
print(TOS_ENV_ENDPOINT)
print(TOS_ROOT_DIR)

TOS_FS = TosFileSystem(
    key=ENV_AK,
    secret=ENV_SK,
    endpoint_url=TOS_ENV_ENDPOINT,
    region='cn-beijing',
    socket_timeout=60,
    connection_timeout=60,
    max_retry_num=30

)

# Write to Lance
storage_options = {
    "access_key_id": ENV_AK,
    "secret_access_key": ENV_SK,
    "aws_region": S3_ENV_REGION,
    "aws_endpoint": S3_ENV_ENDPOINT,
    "virtual_hosted_style_request": "true"
}

# Read WebDataset
ds = ray.data.read_webdataset(
    paths=input_dir,
    filesystem=TOS_FS,
    override_num_blocks=100,
    suffixes=FILE_TYPES,
    concurrency=100,
    decoder=None,
)

# Convert according to type requirements
# Original types
# <class 'object'>  -->  pa.string()
# dict key --> pa.int()
# dict --> pa.int()
# <numpy.ndarray(shape=(320, 480, 3), dtype=uint8)> --> pa.binary()

required_schema = pa.schema(REQUIRED_SCHEMA)

# Type conversion
ds = ds.map_batches(TypeConverter,  fn_constructor_args=(
    ds.schema(), required_schema), batch_size=10, num_cpus=1, concurrency=30)

# Data writing to Lance
sink = LanceDatasink(
    output_dir,
    schema=required_schema,
    max_rows_per_file=100,
    storage_options=storage_options,
    mode="overwrite")
ds.write_datasink(sink)
```
