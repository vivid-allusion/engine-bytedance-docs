---
title: "Application practice- Usage instructions for datasets based on veDaft"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Daft-dataset-usage"
---

After creating a dataset in LAS, you can perform read and write operations on the data within the dataset during data processing. This article introduces the general workflow and key points for using datasets with Daft on the LAS development machine.

# Note and prerequisites

* The LAS dataset has already been created. For details, see [Dataset management](https://docs.byteplus.com/docs/Byteplus_LAS/91363).

* Note: Currently, veDaft does not support direct reading of Iceberg or Text\-type datasets. The following provides guidance for operating other types of datasets.

# Preparation

## Prepare the development environment

Before using a dataset, you need to prepare the development environment for data processing. It is recommended to use the LAS development machine, which comes with multiple official images pre\-installed, such as images for relevant Daft versions. Therefore, you can quickly prepare the development environment based on the LAS development machine and official images .

## Configure environment variables

1. Before using a dataset, you need to obtain the API Key, region, and Endpoint information of the dataset, which will be used for configuration when using the dataset later.

   * You can create or view your API Key in "Access Control" \-\> "API Access Key" .

   * You can view the region and Endpoint of the TOS Bucket for the current dataset in the corresponding dataset's TOS console.

2. It is recommended to configure the information obtained above as environment variables to avoid plain\-text configuration when using the dataset and to improve security.

   ```Bash
   export LAS_TOS_ACCESS_KEY=xxx
   export LAS_TOS_SECRET_KEY=xxx
   export TOS_ENDPOINT=https://tos-ap-southeast-1.bytepluses.com
   export TOS_REGION=ap-southeast-1
   ```

# Using the dataset

## Read data

```Python
import daft

dataset_name = "your_dataset_name"
df = daft.read_las_dataset(name=dataset_name)
df.show()
```

## Convert to Lance dataset

You can convert datasets in CSV, JSONL, Parquet, Image, Audio, Video, and Lerobot formats to Lance format. The specific operation instructions are as follows

```Python
import daft
from daft.io import CreateLasDatasetOptions, IOConfig, LanceWriteOptions
from daft.las.io import TOSConfig

# You can customize the path for your new dataset
dataset_name = "your_dataset_name"
lance_tos_dir = f"tos://{tos_bueckt_dir}/{dataset_name}.lance"
LANCE_DATASET_FORMAT = "lance"

# Create the relevant configuration
io_config = IOConfig(s3=TOSConfig.from_env().to_s3_config())
write_options = LanceWriteOptions(io_config=io_config, uri=lance_tos_dir)
create_ds_options = CreateLasDatasetOptions(
    nick_name="daft_test_lance_write",
    privacy="public",
    description="This is my dataset",
)

# Read the original data
df = daft.read_las_dataset(name=dataset_name)

# Create here
new_dataset_name = dataset_name + "_lance"
df.write_las_dataset(
    name=new_dataset_name,
    format=LANCE_DATASET_FORMAT,
    write_options=write_options,
    create_ds_options=create_ds_options,
)

# Read the newly converted dataset
df = daft.read_las_dataset(name=new_dataset_name)
print("\n\nnew dataset:")
df.show()
```

## Add columns

To use the full functionality available on the LAS dataset page, you can add a __data_item_id column as a logical primary key. Refer to the following code:

> **警告**

> Before performing the add columns operation, you need to convert the dataset to a Lance dataset. Currently, only Lance datasets support the add columns operation.

```Python
import random
import pyarrow as pa
from daft.io.lance import merge_columns
from daft.io import IOConfig
from daft.las.io import TOSConfig

def create_assign_uuid(batch: pa.RecordBatch) -> pa.RecordBatch:
    num_rows = batch.num_rows

    uuid_list = [random.getrandbits(63) for _ in range(num_rows)]
    uuid_array = pa.array(uuid_list, type=pa.int64())

    return pa.RecordBatch.from_arrays([uuid_array], names=["__data_item_id"])


print("Generating business primary keys...")

dataset_name = "your_dataset_name"
lance_tos_dir = f"tos://{tos_bueckt_dir}/{dataset_name}.lance"
io_config = IOConfig(s3=TOSConfig.from_env().to_s3_config())
merge_columns(
    url=lance_tos_dir.replace("tos://", "s3://"),
    io_config=io_config,
    transform=create_assign_uuid,
)

print("Business primary key generation completed...")
```

For image, audio, and video data, it is usually desirable to write the original data into the Lance dataset as well. The following example uses image data to demonstrate sample code for adding columns and writing data:

```Python
import os
import pyarrow as pa
import tos
from daft.io.lance import merge_columns
from daft.io import IOConfig
from daft.las.io import TOSConfig

ak = os.environ["LAS_TOS_ACCESS_KEY"]
sk = os.environ["LAS_TOS_SECRET_KEY"]
endpoint = os.environ["TOS_ENDPOINT"]
region = os.environ["TOS_REGION"]

dataset_name = "doctest_image"

# Read image data from the tos path
def read_tos_path(path: str, tos_client: tos.TosClientV2):
    if (not path) or path.strip() == "":
        return None

    if path.startswith("tos://"):
        path = path[len("tos://") :]

    if path.startswith("s3://"):
        path = path[len("s3://") :]

    bucket, path = path.split("/", 1)
    obj = tos_client.get_object(bucket=bucket, key=path)
    return obj.read()


def get_create_assign_raw_image_func(input_col: str, output_col: str):
    def create_assign_raw_image(batch: pa.RecordBatch) -> pa.RecordBatch:
        paths = batch.column(input_col).to_pylist()
        tos_client = tos.TosClientV2(ak, sk, endpoint, region)

        image_data_list = []
        for path in paths:
            data = read_tos_path(path, tos_client)
            image_data_list.append(data)

        image_data_array = pa.array(image_data_list, type=pa.binary())
        new_batch = pa.RecordBatch.from_arrays([image_data_array], names=[output_col])

        # Only return the new columns
        return new_batch

    return create_assign_raw_image


print("Saving image original data source into lance dataset...")

io_config = IOConfig(s3=TOSConfig.from_env().to_s3_config())
lance_tos_dir = f"tos://ycs-test/las/lance/{dataset_name}.lance"
merge_columns(
    url=lance_tos_dir.replace("tos://", "s3://"),
    io_config=io_config,
    transform=get_create_assign_raw_image_func("image", "raw_image"),
)

print("Image original data source has been saved into the lance dataset")
```
