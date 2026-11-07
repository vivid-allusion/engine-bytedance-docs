---
title: "Quick start"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Daft_Quick_start"
---

<span id="2399d462"></span>
## Installation

The LAS development machine has ve\-daft installed by default, so users do not need to install it separately. To install ve\-daft on your own machine, follow these steps.


1. ve\-daft has not yet been released on the public PyPI repository. Users need to download the offline installation package for ve\-daft: [Click to download](https://las-ai-cn-beijing.tos-cn-beijing.volces.com/qa/whl/ve_daft-0.5.10.post7-cp39-abi3-manylinux_2_35_x86_64.whl).

2. Run the following command to install ve\-daft.


```Python
pip install ve_daft-0.5.10.post7-cp39-abi3-manylinux_2_35_x86_64.whl
```


By default, ve\-daft only provides read and write access to LAS datasets. To use the multimodal computation operators provided by LAS, you need to install the following two extras:

```Python
pip install ve_daft-0.5.10.post7-cp39-abi3-manylinux_2_35_x86_64.whl[las]
pip install ve_daft-0.5.10.post7-cp39-abi3-manylinux_2_35_x86_64.whl[flash-attn]
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Since the computation operator uses multiple model and algorithm libraries, the size may be relatively large. Please reserve sufficient space.</div>


<span id="cadbf1ae"></span>
## Basic usage

The following section introduces the basic operations of the daft dataframe.

<span id="0077c276"></span>
### Create a dataframe

You can instantiate a dataframe from a Python dict and display it:

```Python
import daft

df = daft.from_pydict({
    "A": [1, 2, 3, 4],
    "B": [1.5, 2.5, 3.5, 4.5],
    "C": [True, True, False, False],
    "D": [None, None, None, None],
}).show()

╭───────┬─────────┬─────────┬──────╮
│ A     ┆ B       ┆ C       ┆ D    │
│ ---   ┆ ---     ┆ ---     ┆ ---  │
│ Int64 ┆ Float64 ┆ Boolean ┆ Null │
╞═══════╪═════════╪═════════╪══════╡
│ 1     ┆ 1.5     ┆ true    ┆ None │
├╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌┤
│ 2     ┆ 2.5     ┆ true    ┆ None │
├╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌┤
│ 3     ┆ 3.5     ┆ false   ┆ None │
├╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌┤
│ 4     ┆ 4.5     ┆ false   ┆ None │
╰───────┴─────────┴─────────┴──────╯

(Showing first 4 of 4 rows)
```


Similarly, you can create a dataframe from a Python list.

```SQL
df = daft.from_pylist([
    {"A": 1, "B": 1.5, "C", True, "D": None},
    {"A": 2, "B": 2.5, "C", True, "D": None},
    {"A": 3, "B": 3.5, "C", False, "D": None},
    {"A": 4, "B": 4.5, "C", False, "D": None},
])
```


You can also create a dataframe from the following data structures:

```Python
from_pandas(data: Union["pd.DataFrame", list["pd.DataFrame"]])
from_arrow(data: Union["pa.Table", list["pa.Table"], Iterable["pa.Table"]])
from_ray_dataset(ds: "RayDataset")
from_dask_dataframe(ddf: "dask.DataFrame")
```


In addition, you can read data from a data source into a dataframe. For details, see Section 2 "Data source support".

<span id="421bcae7"></span>
### Operate on a dataframe

Using the ve\-daft dataframe is similar to using dataframes in other engines, such as Pandas or PySpark. The common operations are basically the same and easy to use, for example:

Select columns,

```Python
df.select("A", "B").show()

╭───────┬─────────╮
│ A     ┆ B       │
│ ---   ┆ ---     │
│ Int64 ┆ Float64 │
╞═══════╪═════════╡
│ 3     ┆ 3.5     │
├╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┤
│ 4     ┆ 4.5     │
╰───────┴─────────╯

(Showing first 2 of 2 rows)
```


or filter,

```SQL
df.filter(df["A"] > 2).show()

╭───────┬─────────┬─────────┬──────┬─────────╮
│ A     ┆ B       ┆ C       ┆ D    ┆ E       │
│ ---   ┆ ---     ┆ ---     ┆ ---  ┆ ---     │
│ Int64 ┆ Float64 ┆ Boolean ┆ Null ┆ Float64 │
╞═══════╪═════════╪═════════╪══════╪═════════╡
│ 3     ┆ 3.5     ┆ false   ┆ None ┆ 6.5     │
├╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┤
│ 4     ┆ 4.5     ┆ false   ┆ None ┆ 8.5     │
╰───────┴─────────┴─────────┴──────┴─────────╯

(Showing first 2 of 2 rows)
```


or perform calculations using standard expressions:

```Python
df = df.with_column("E", df["A"] + df["B"]).show()

╭───────┬─────────┬─────────┬──────┬─────────╮
│ A     ┆ B       ┆ C       ┆ D    ┆ E       │
│ ---   ┆ ---     ┆ ---     ┆ ---  ┆ ---     │
│ Int64 ┆ Float64 ┆ Boolean ┆ Null ┆ Float64 │
╞═══════╪═════════╪═════════╪══════╪═════════╡
│ 1     ┆ 1.5     ┆ true    ┆ None ┆ 2.5     │
├╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┤
│ 2     ┆ 2.5     ┆ true    ┆ None ┆ 4.5     │
├╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┤
│ 3     ┆ 3.5     ┆ false   ┆ None ┆ 6.5     │
├╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┤
│ 4     ┆ 4.5     ┆ false   ┆ None ┆ 8.5     │
╰───────┴─────────┴─────────┴──────┴─────────╯

(Showing first 4 of 4 rows)
```


and more.

Users can also use UDFs to operate on the dataframe. Daft's UDFs are unique compared to UDFs in engines like Pandas or PySpark, as they support classes. This type of UDF is very important for AI computation. For details, refer to Section 3 "User\-defined functions" below.

For more operations, refer to the official daft documentation.

<span id="93d661ca"></span>
### Multimodal support

One of daft's main features is its support for multimodal data. This multimodal support is reflected in two aspects:


1. Multimodal data types. These data types extend the traditional dataframe/SQL data types, adding support for types such as Image, URL, Text, and Json.

2. Direct operations (also called "operators") for these types are added. For example, for the URL type, you can use the `download()` method to download files; for the Image type, you can use the `decode()` method to decode images, and so on. The following is an example:


```SQL
df = daft.read_parquet("metadata.parquet") \
    .with_column("image_data", col("urls").url.download()) \
    .with_column("resized", col("image_data").image.resize(224, 224))
```


<span id="991a7971"></span>
### Data source support

<span id="b314db6b"></span>
#### Data source list

ve\-daft supports multiple data sources. In addition to common formats such as parquet, csv, and json, it also supports emerging data lake formats like lance, as well as reading and writing LAS datasets. The complete list is as follows:


* csv

* json

* parquet

* iceberg

* hudi

* lance

* deltalake

* clickhouse

* mcap

* las_dataset


Among them, clickhouse, mcap, and las_dataset are exclusively supported by ve\-daft.

<span id="5ab3bf28"></span>
#### Read and write TOS

Currently, ve\-daft does not yet support the TOS protocol, so users still need to use the S3\-compatible protocol when reading and writing data stored in TOS. The following demonstrates how to read csv data stored in TOS, as well as how to write csv data to TOS.


1. First, configure environment variables


```Python
export ACCESS_KEY=xxx
export SECRET_KEY=xxx
export TOS_ENDPOINT=https://tos-cn-beijing.volces.com
export TOS_REGION=cn-beijing
```



2. Read csv:


```Python
import daft
from daft.daft import IOConfig
from daft.las.io.tos import TOSConfig

s3_config = TOSConfig.from_env().to_s3_config()
df = daft.read_csv(path="s3://path/to/csv/dir", io_config=IOConfig(s3=s3_config))
```



3. Write csv:


```Python
import daft
from daft.daft import IOConfig
from daft.las.io.tos import TOSConfig


df = daft.from_pydict({
    "A": [1, 2, 3, 4],
    "B": [1.5, 2.5, 3.5, 4.5],
    "C": [True, True, False, False],
    "D": [None, None, None, None],
})

s3_config = TOSConfig.from_env().to_s3_config()
df = daft.write_csv(root_dir="s3://path/to/csv/dir", io_config=IOConfig(s3=s3_config))
```


For reading and writing other formats, refer to daft's [official documentation](https://docs.daft.ai/en/stable/).

<span id="60ea6cc1"></span>
## Advanced usage

<span id="dbf9f0c6"></span>
### Read and write LAS datasets

One major feature of ve\-daft is its support for reading and writing LAS datasets. For information on reading and writing LAS datasets, refer to the documentation [Read and write LAS datasets](https://docs.byteplus.com/docs/Byteplus_LAS/92523).

<span id="65cf2a45"></span>
### User\-defined functions (UDFs)

ve\-daft supports two types of UDFs: function type and class type. The class type is an important distinction between ve\-daft and other engines such as spark and hive. Function\-type UDFs can be further divided into lambda function UDFs and regular function UDFs.


1. Lambda\-type UDFs.


This type of UDF is generally used for in\-row computations and is suitable for simple scenarios. It is invoked via `.apply()`:

```Python
df.with_column(
    "flattened_image",
    df["image"].apply(lambda img: img.flatten(), return_dtype=daft.DataType.python())
).show(2)
```



2. Regular function\-type UDFs.


This type of UDF is the kind commonly seen in other engines. It is defined using the `@daft.udf()` decorator:

```Python
@daft.udf(return_dtype=daft.DataType.python())
def crop_images(images, crops, padding=0):
    cropped = []
    for img, crop in zip(images, crops):
        x1, x2, y1, y2 = crop
        cropped_img = img[x1:x2 + padding, y1:y2 + padding]
        cropped.append(cropped_img)
    return cropped

df = df.with_column(
    "cropped",
    crop_images(df["image"], df["crop"], padding=1),
)
df.show(2)
```



3. Class\-type UDFs.


These are also defined using `@daft.udf()`, but unlike function\-type UDFs, they are defined on a class:

```Python
@daft.udf(
    return_dtype=daft.DataType.int64(),
    concurrency=4,  # initialize 4 instances of the UDF to run across your data
)
class RunModel:
    def __init__(self, model_name = "meta-llama/Llama-4-Scout-17B-16E-Instruct"):
        # Perform expensive initializations
        self._model = create_model(model_name)
    def __call__(self, features_col):
        return self._model(features_col)
        
df = df.with_column("image_classifications", RunModel(df["image"]))
```


The advantage of class UDFs is that they can maintain "state" and be reused, which allows for heavier operations such as loading models. If function\-type UDFs are used, model loading must occur every time the UDF is called, which results in unimaginable time consumption.

<span id="97e49b9e"></span>
### ve\-daft operators

<span id="2b7925c6"></span>
#### Built\-in operators

"Operators" are functions provided by ve\-daft for multimodal data processing, such as removing special characters from text, filtering sensitive information, extracting audio from video, speaker recognition, and many more, covering a wide range of use cases. The essence of an operator is a class with a specific interface, which can be invoked as a UDF.

The following code is a real, runnable example:

```Python
import os

import daft
from daft import col
from daft.las.functions.audio import AudioDuration
from daft.las.functions.udf import las_udf

if __name__ == "__main__":
    sample_path = f"tos://tos_bucket/audio_duration/sample.mp3"

    df = daft.from_pydict({"audio_path": [sample_path]})
    df = df.with_column("duration_result", las_udf(AudioDuration)(col("audio_path")))
    df.show()
    # ╭────────────────────────────────┬─────────────────╮
    # │ audio_path                     ┆ duration_result │
    # │ ---                            ┆ ---             │
    # │ Utf8                           ┆ Float32         │
    # ╞════════════════════════════════╪═════════════════╡
    # │ tos://tos_bucket/audio_durati… ┆ 49.711          │
    # ╰────────────────────────────────┴─────────────────╯
```


In the code above, `AudioDuration` is a function (callable class) used to calculate audio duration, and `las_udf` is a wrapper method that encapsulates `AudioDuration` as a ve\-daft UDF.

`las_udf()` encapsulates multiple parameters:

```Python
las_udf(
    operator: type[Operator],
    construct_args: dict[str, Any] | None = None,
    num_cpus: float | None = None,
    num_gpus: float | None = None,
    memory_bytes: int | None = None,
    batch_size: int | None = None,
    concurrency: int | None = None,
)
```


**Parameter description**:


* operator: Refers to the operator class.

* construct_args: Initialization parameters for the operator, corresponding to the named parameters of the class's `__init__`.

* num_cpus: Number of CPUs used by a single operator in ray mode.

* num_gpus: Number of GPUs used by a single operator in ray mode.

* memory_bytes: Amount of memory used by a single operator in ray mode.

* batch_size: Number of records processed per batch.

* concurrency: Number of concurrent operators.


<span id="828cf342"></span>
#### Custom operator

Users can define custom operators by inheriting the following class and implementing the corresponding interfaces:

```Python
class Operator(ABC):
    """An operator that process the input data."""

    def transform(self, *args: Any, **kwargs: Any) -> pa.Array:
        raise NotImplementedError

    @staticmethod
    @abstractmethod
    def __return_column_type__() -> pa.DataType: ...
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the input is a dataframe column, its type should be py.Array, for example <code>transform(self, col: pa.Array) -> pa.Array</code>.</div>


* <div data-tips="true" data-tips-type="tip"><code>__return_column_type__</code> defines the return type as the type of the contents inside pa.Array. For example, if pa.Array contains float data, the return type should be <code>pa.float64()</code>.</div>



The following is a simple example that returns the value itself:

```Python
import daft
import pyarrow as pa

from daft import col
from daft.las.functions.types import Operator
from daft.las.functions.udf import las_udf

# 1. Define operator
class EchoUDF(Operator):
    @staticmethod
    def __return_column_type__() -> pa.DataType:
        return pa.int64()

    def transform(self, col_a: pa.Array, col_b: pa.Array | None = None, c: str | None = None) -> pa.Array:
        return col_a

# 2. Use operator
df = daft.from_pydict({
    "A": [1, 2, 3, 4],
    "B": [1.5, 2.5, 3.5, 4.5]
})

df = df.with_column("dup_a", las_udf(EchoUDF)(col("A")))

df.show()
```


Output:

```Python
╭───────┬─────────┬───────╮
│ A     ┆ B       ┆ dup_a │
│ ---   ┆ ---     ┆ ---   │
│ Int64 ┆ Float64 ┆ Int64 │
╞═══════╪═════════╪═══════╡
│ 1     ┆ 1.5     ┆ 1     │
├╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 2     ┆ 2.5     ┆ 2     │
├╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 3     ┆ 3.5     ┆ 3     │
├╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 4     ┆ 4.5     ┆ 4     │
╰───────┴─────────┴───────╯

(Showing first 4 of 4 rows)
```
