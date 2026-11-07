---
title: "Read and write LAS datasets"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Read_and_write_LAS_datasets"
---

<span id="988a90e7"></span>
## Introduction

The LAS platform provides dataset hosting functionality. Users can host their own data on the platform and use the tools provided by the platform to preview and analyze the data.

LAS dataset hosting uses a semi\-hosted model. In this model, users do not need to upload data to the LAS platform; they only need to keep the data maintained in their own TOS/vePFS system. This model effectively ensures data security and eliminates users' concerns about the risk of data leakage.

In addition, datasets hosted by LAS can be directly processed at scale using the tools provided by the platform, meeting users' needs for data computation.

By using tools such as ve\-daft, development environments, and workflows provided by the LAS platform, users can build a complete data processing pipeline. For more information on this topic, refer to [LAS job development](https://docs.byteplus.com/docs/Byteplus_LAS/92525). This article focuses on how to use ve\-daft to read and write LAS datasets.

<span id="efa70c78"></span>
## Data types

Currently, LAS datasets support the following types:


* Table types

   * CSV

   * JSON

   * Lance

   * Parquet

* Multimodal Folder types

   * Image Folder

   * Audio Folder

   * Video Folder


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, reading and writing JSON is only supported by daft's native engine and does not yet support distributed processing with ray.</div>


* <div data-tips="true" data-tips-type="tip">Iceberg and Text are still under development.</div>



<span id="cb271962"></span>
### Table types

For table types, LAS recommends using Lance as the data storage format. This format offers several advantages:


1. Storage efficiency is higher than typical text formats.

2. For typical AI scenarios such as adding columns, operational efficiency is higher.

3. Supports storage of multimodal data.

4. Supports efficient training directly based on the Lance format.


For more information about the Lance format, refer to [Lance documentation](https://www.volcengine.com/docs/6491/1544094).

<span id="436247ac"></span>
### Folder types

This section provides a brief explanation of the multimodal Folder format.

<span id="daf1fe52"></span>
#### Read a folder

Take a Folder as an example; its directory structure is as follows:

```Python
my_data/
    metadata.jsonl # Optional
    sub_folder/
        pic3.png
        pic4.png
        ...
    pic1.png
    pic2.png
    audio1.mp3
    audio2.mp3
    ...
```


When it is read as an Image Folder:


1. If metadata.csv, metadata.jsonl, or metadata.parquet exists, this metadata will be read as an image dataframe. That is, this metadata describes the files within the entire folder. Typically, each line in metadata.jsonl describes a file and records the file's features, such as file link, size, label, and so on.

2. If there is no metadata, then

   1. The file list will be read as a dataframe. The file list is processed recursively and filtered according to the extension types supported by Image. For example, files in .txt format will not be included as elements of the Image dataframe. If the file list is read as Audio format, then audio1.mp3 and audio2.mp3 will be read, while others will not be read.

   2. The data returned from reading the file list has a fixed schema:


```Python
bytes：If you choose to read the contents of the file and read the file as binary data, this column is not available by default
base64: If you choose to read the contents of the file and read the file as a base64 string. This column is not available by default
path: File Path 
size: file size
rows: If the file is in parquet format, the number of lines in the parquet file
```


<span id="c85f7073"></span>
#### Write folder

Write folder consists of two stages:


1. Write raw Image/Audio/Video data

2. Write metadata (optional)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, daft does not support saving in\-memory data as image, audio, or video files; that is, daft only supports writing metadata.</div>


To save one or more columns containing image, audio, or video content data as files and then as a LAS dataset, use a UDF:


1. Define a UDF that saves in\-memory data as local files and then uploads them to TOS.

2. Delete the column.

3. Save the remaining columns as an Image/Audio/Video type LAS dataset.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When writing metadata, pay special attention to ensuring that the metadata dataset is not too large and does not exceed 80% of the driver's available memory. Otherwise, the driver node may experience OOM. This is because the data must be collected to the driver node before it can be saved as a TOS metadata file. If the dataframe contains content data such as Image, Audio, or Video, you can drop these columns before writing.</div>


<span id="ded6ddde"></span>
## Read and write LAS datasets

<span id="b4273bec"></span>
### Read operation

<span id="e88498b6"></span>
#### Method signature

The API signature for reading a LAS dataset is as follows:

```Python
def read_las_dataset(name: str, read_options: ReadOptions | None = None) -> DataFrame:
    """Create a DataFrame from a las dataset.

    Args:
        name: Name of the dataset.
        read_options: The format specified read options. These options will be passed to correspond read functions.

    Returns:
        DataFrame: a DataFrame with the schema converted from the dataset.
            For audio/image/video folder, if there's a metadata.csv/metadata.jsonl/metadata.parquet,
            this will return the content the metadata file as dataframe, otherwise, this will return
            a dataframe whose content is the file list, with the following schema:

            1. bytes/base64: the content of the file, bytes or base64 according to the reading options,
                and if only read url, this column does not exist.
            2. path: the path to the file/directory
            3. size: size of the object in bytes
            4. rows: number of rows if the file is parquet
    """
```


Among them, `ReadOptions` corresponds to the configuration for reading various formats, which differs depending on the data type:


* CSV


```Python
@dataclass
class CsvReadOptions(ReadOptions):
    infer_schema: bool = True
    schema: dict[str, DataType] | None = None
    has_headers: bool = True
    delimiter: str | None = None
    double_quote: bool = True
    quote: str | None = None
    escape_char: str | None = None
    comment: str | None = None
    allow_variable_columns: bool = False
    file_path_column: str | None = None
    hive_partitioning: bool = False
    schema_hints: dict[str, DataType] | None = None
    _buffer_size: int | None = None
    _chunk_size: int | None = None
```



* JSON


```Python
@dataclass
class JsonReadOptions(ReadOptions):
    infer_schema: bool = True
    schema: dict[str, DataType] | None = None
    file_path_column: str | None = None
    hive_partitioning: bool = False
    schema_hints: dict[str, DataType] | None = None
    _buffer_size: int | None = None
    _chunk_size: int | None = None
```



* Parquet


```Python
@dataclass
class ParquetReadOptions(ReadOptions):
    row_groups: list[list[int]] | None = None
    infer_schema: bool = True
    schema: dict[str, DataType] | None = None
    file_path_column: str | None = None
    hive_partitioning: bool = False
    coerce_int96_timestamp_unit: str | TimeUnit | None = None
    schema_hints: dict[str, DataType] | None = None
    _multithreaded_io: bool | None = None
    _chunk_size: int | None = None
```



* Lance


```Python
@dataclass
class LanceReadOptions(ReadOptions):
    version: str | int | None = None
    asof: str | None = None
    block_size: int | None = None
    commit_lock: object | None = None
    index_cache_size: int | None = None
    default_scan_options: dict[str, str] | None = None
    metadata_cache_size_bytes: int | None = None
```



* Image/Audio/Video Folder


```Python
@dataclass
class FolderReadOptions(ReadOptions):
    metadata_options: ReadOptions = field(
        default_factory=lambda: ReadOptions(io_config=IOConfig(s3=TOSConfig.from_env().to_s3_config()))
    )
    file_types: list[str] = field(default_factory=list)
    read_type: Literal["url", "binary", "base64", "ndarray"] = "url"

@dataclass
class ImageFolderReadOptions(FolderReadOptions):
    file_types: list[str] = field(
        default_factory=lambda: [".blp", ".dib", ".bmp", ".bufr", ".cur", ".pcx", ".dcx", ".dds", ".ps", ".eps", ".fit", ".fits", ".fli", ".flc", ".ftc", ".ftu", ".gbr", ".gif", ".grib", ".apng", ".jp2", ".j2k", ".jpc", ".jpf", ".jpx", ".j2c", ".icns", ".ico", ".im", ".iim", ".tif", ".tiff", ".jfif", ".jpe", ".jpg", ".jpeg", ".mpg", ".mpeg", ".msp", ".pcd", ".pxr", ".pbm", ".pgm", ".ppm", ".pnm", ".psd", ".bw", ".rgb", ".rgba", ".sgi", ".ras", ".tga", ".icb", ".vda", ".vst", ".webp", ".wmf", ".emf", ".xbm", ".xpm"]
    )

@dataclass
class AudioFolderReadOptions(FolderReadOptions):
    file_types: list[str] = field(
        default_factory=lambda: [".aiff", ".au", ".avr", ".caf", ".flac", ".htk", ".svx", ".mat4", ".mat5", ".mpc2k", ".m4a", ".ogg", ".paf", ".pvf", ".raw", ".rf64", ".sd2", ".sds", ".ircam", ".voc", ".w64", ".wav", ".nist", ".wavex", ".wve", ".xi", ".mp3", ".opus"]
    )
    
@dataclass
class VideoFolderReadOptions(FolderReadOptions):
    file_types: list[str] = field(
        default_factory=lambda: [".mkv", ".mp4", ".avi", ".mpeg", ".mov"]
    )
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The <code>ReadOptions</code> for CSV, JSON, Parquet, and Lance actually correspond to the parameters of the methods <code>daft.read_csv</code>, <code>daft.read_json</code>, <code>daft.read_parquet</code>, and <code>daft.read_lance</code>. Their meaning can be found in daft's API documentation.</div>


<span id="a098505b"></span>
#### Read data example

Export the necessary environment variables:

```Python
export ACCESS_KEY=xxx
export SECRET_KEY=xxx
export TOS_ENDPOINT=https://tos-cn-beijing.volces.com  # If it is an intranet, change volces to ivolces
export TOS_REGION=cn-beijing
```



1. Read a LAS dataset in CSV format


```Python
import daft
import ray
from daft.io import CsvReadOptions, IOConfig
from daft.las.io import TOSConfig

ray.init()  # If in a distributed ray environment

io_config = IOConfig(s3=TOSConfig.from_env().to_s3_config())
dataset_name = "my_dataset"
read_options = CsvReadOptions(io_config=io_config)

df = daft.read_las_dataset(name=dataset_name, read_options=read_options)
df.show()

# Output
╭─────────────────┬───────╮                                                                                                                                                                                                                                               
│ file_name       ┆ size  │
│ ---             ┆ ---   │
│ Utf8            ┆ Int64 │
╞═════════════════╪═══════╡
│ subfolder/1.png ┆ 234   │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 2.png           ┆ 256   │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 3.jpg           ┆ 300   │
╰─────────────────┴───────╯

(Showing first 3 of 3 rows)
```



2. Read a dataset of the Image folder type (Audio/Video are similar).

* Example with metadata


Assume the user's directory structure is as follows:

```Python
image_dataset
    /subfolder/1.png
    /2.png
    /3.jpg
    /4.txt   # Note that there is a non-image file here
    /metadata.jsonl
```


The contents of metadata.jsonl are as follows.

```JSON
{"file_name":"subfolder/1.png","size":1705}
{"file_name":"2.png","size":1899}
{"file_name":"3.jgp","size":929}
```


**Example code**

```Python
import daft
import ray
from daft.io._las_dataset import FolderReadOptions, IOConfig
from daft.las.io import TOSConfig

ray.init()  # If in a distributed ray environment

dataset_name = "my_dataset"

io_config = IOConfig(s3=TOSConfig.from_env().to_s3_config())
read_options = FolderReadOptions(io_config=io_config)

df = daft.read_las_dataset(name=dataset_name, read_options=read_options)
df.show()

# Output
╭─────────────────┬───────╮                                                                                                                                                                                                                                               
│ file_name       ┆ size  │
│ ---             ┆ ---   │
│ Utf8            ┆ Int64 │
╞═════════════════╪═══════╡
│ subfolder/1.png ┆ 1705  │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 2.png           ┆ 1899  │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┤
│ 3.jpg           ┆ 929   │
╰─────────────────┴───────╯

(Showing first 3 of 3 rows)
```



* No metadata


**Example code**

```Python
import daft
import ray
from daft.io import ImageFolderReadOptions, IOConfig
from daft.las.io import TOSConfig

ray.init()  # If in a distributed ray environment

dataset_name = "my_dataset"

io_config = IOConfig(s3=TOSConfig.from_env().to_s3_config())
read_options = ImageFolderReadOptions(io_config=io_config, read_type="url") # Audio/Video is similar

df = daft.read_las_dataset(name=dataset_name, read_options=read_options)
df.show()

# Output
╭────────────────────────────────┬───────┬──────────╮                                                                                                                                                                                                                     
│ image                          ┆ size  ┆ num_rows │                                                                                                                                                                                                                     
│ ---                            ┆ ---   ┆ ---      │
│ Utf8                           ┆ Int64 ┆ Int64    │
╞════════════════════════════════╪═══════╪══════════╡
│ s3://las-ci/daft/dataset/imag… ┆ 1899  ┆ None     │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ s3://las-ci/daft/dataset/imag… ┆ 929   ┆ None     │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
│ s3://las-ci/daft/dataset/imag… ┆ 1705  ┆ None     │
╰────────────────────────────────┴───────┴──────────╯

(Showing first 3 of 3 rows)
```


<span id="844a7454"></span>
### Write operation

<span id="640dbbca"></span>
#### Method signature

The API signature for writing a LAS dataset is as follows:

```Python
def write_las_dataset(  # type: ignore[no-untyped-def]
    self,
    name: str,
    format: str | None = None,
    write_options: WriteOptions | None = None,
    create_ds_options: CreateLasDatasetOptions | None = None,
) -> DataFrame:
    """Writes the DataFrame to LAS dataset, returning a new DataFrame with paths to the files that were written.

    The dataset will be created if it was not exist.
    Files may be written to `<root_dir>/*` with randomly generated UUIDs as the file names.

    Args:
        name: Name of the dataset to be created.
        format: Format of the dataset (CSV, Parquet, Lance, Jsonl or Iceberg).
        write_options: The format specified write options. These options will be passed to correspond writing functions.
        create_ds_options: The options used to create the dataset.

    Returns:
        DataFrame: A new DataFrame containing paths to the written files.

    Raises:
        ValueError: If the format is unsupported or if required arguments are missing.
        Exception: If dataset creation fails in the LAS service.
    """
```


Among them, `WriteOptions` corresponds to the configuration for writing various formats, which differs depending on the data type.


* CSV


```Python
@dataclass
class CsvWriteOptions(WriteOptions):
    root_dir: str | pathlib.Path | None = None
    write_mode: Literal["append", "overwrite", "overwrite-partitions"] = "append"
    partition_cols: list[ColumnInputType] | None = None
```



* JSON


```Python
@dataclass
class JsonWriteOptions(WriteOptions):
    root_dir: str | pathlib.Path | None = None
    write_mode: Literal["append", "overwrite", "overwrite-partitions"] = "append"
    partition_cols: list[ColumnInputType] | None = None
```



* Parquet


```Python
@dataclass
class ParquetWriteOptions(WriteOptions):
    root_dir: str | pathlib.Path | None = None
    compression: str = "snappy"
    write_mode: Literal["append", "overwrite", "overwrite-partitions"] = "append"
    partition_cols: list[ColumnInputType] | None = None
```



* Lance


```Python
@dataclass
class LanceWriteOptions(WriteOptions):
    uri: str | pathlib.Path | None = None
    mode: Literal["create", "append", "overwrite"] = "create"
    schema: Schema | None = None
```



* Image/Audio/Video


```Python
@dataclass
class FolderWriteOptions(WriteOptions):
    root_dir: str | None = None
    write_mode: Literal["append", "overwrite", "overwrite-partitions"] = "append"
    metadata_format: Literal["csv", "jsonl", "parquet"] = "jsonl"
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The <code>WriteOptions</code> for CSV, JSON, Parquet, and Lance actually correspond to the parameters of the methods <code>dataframe.write_csv</code>, <code>dataframe.write_json</code>, <code>dataframe.write_parquet</code>, and <code>dataframe.write_lance</code>. Their meaning can be found in daft's API documentation.</div>


* <div data-tips="true" data-tips-type="warning">Image/Audio/Video Folder: There may be a metadata file. <code>metadata_options</code> corresponds to the <code>WriteOptions</code> for metadata files (which can be in CSV, JSONL, or Parquet format).</div>



<span id="bc261d84"></span>
#### Write mode

Currently, the write modes and default write mode support for several formats are as follows:


|Format |Mode |Default mode |Description |
|---|---|---|---|
|CSV |["append", "overwrite", "overwrite\-partitions"] |"append" |Currently, only "append" is supported |
|JSONL |["append", "overwrite", "overwrite\-partitions"] |"append" |Currently, only "append" is supported |
|Parquet |["append", "overwrite", "overwrite\-partitions"] |"append" |Currently, only "append" is supported |
|Lance |["create", "append", "overwrite"] |"create" |Caution: Use "create" for the first write, and "append" or "overwrite" for subsequent writes |
|Folder（Image/Audio/Video） |["append", "overwrite", "overwrite\-partitions"] |"append" |* This refers to writing metadata<br><br>* Currently, only "append" is supported |


<span id="6765219e"></span>
#### Write dataset example

As above, first export the necessary environment variables:

```Python
export ACCESS_KEY=xxx
export SECRET_KEY=xxx
export TOS_ENDPOINT=https://tos-cn-beijing.volces.com  # If it is an intranet, change volces to ivolces
export TOS_REGION=cn-beijing
```



1. Write CSV format data and create a new LAS dataset


```Python
import daft
import ray
from daft.io import CreateLasDatasetOptions, CsvWriteOptions, IOConfig
from daft.las.io import TOSConfig

ray.init()  # If in a distributed ray environment

dataset_name = "my_dataset"
format = "csv"
root_dir = "tos://bucket/path/to/my/dataset"

io_config = IOConfig(s3=TOSConfig.from_env().to_s3_config())
write_options = CsvWriteOptions(io_config=io_config, root_dir=root_dir)
create_ds_options = CreateLasDatasetOptions(
    nick_name="daft_test_csv_write",
    privacy="public",
    description="This is my dataset"
)

df = daft.from_pydict({
    "file_name": ["subfolder/1.png", "2.png", "3.jpg"],
    "size": [1705, 1899, 929]
})

df.write_las_dataset(name=dataset_name, format=format, write_options=write_options, create_ds_options=create_ds_options)
```


After writing, you can view the created dataset on the LAS platform. You can also use ve\-daft to read and view the dataset, as you would when reading a dataset.


2. Append data


By default, for CSV/JSONL/Parquet and Image/Audio/Video types, the default behavior for metadata is "append", which actually means "create" and "append". For Lance, "append" needs to be explicitly set:

```Python
write_options = LanceWriteReadOptions(io_config=io_config, uri=root_dir, mode="append")
```



3. Overwrite write


Currently, except for Lance, other formats do not support overwrite writing. In this case, the user needs to delete the dataset or directly delete the TOS data before writing new data.


4. Write Image Folder type dataset


```Python
import daft
import ray
from daft.io import CreateLasDatasetOptions, ImageFolderWriteOptions, IOConfig
from daft.las.io import TOSConfig

ray.init()  # If in a distributed ray environment

dataset_name = "my_dataset"
format = "image"
root_dir = "tos://bucket/path/to/my/dataset"

io_config = IOConfig(s3=TOSConfig.from_env().to_s3_config())
write_options = ImageFolderWriteOptions(io_config=io_config, root_dir=root_dir)
create_ds_options = CreateLasDatasetOptions(
    nick_name="my_dataset",
    privacy="private",
    description="This is my dataset"
)

df = daft.from_pydict({
    "file_name": ["subfolder/1.png", "2.png", "3.jpg"],
    "size": [1705, 1899, 929]
})

df.write_las_dataset(name=dataset_name, format=format, write_options=write_options, create_ds_options=create_ds_options)
```


After writing, you can use the reading method introduced above to read the dataset.
