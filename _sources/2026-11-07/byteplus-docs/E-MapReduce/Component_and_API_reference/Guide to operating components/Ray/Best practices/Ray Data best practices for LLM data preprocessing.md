---
title: "Ray Data best practices for LLM data preprocessing"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Ray_Data_best_practices_for_LLM_data_preprocessing"
---

<span id="c735d4e8"></span>
## Scenario introduction

This article uses the end\-to\-end data preprocessing process as an example, combining open\-source Hugging Face datasets and Ray engine capabilities to preprocess data.

For an overview of the reasons for using Ray Data for offline batch preprocessing operations, as well as a comparison with other alternative solutions, please refer to [Ray Data overview](https://docs.ray.io/en/latest/data/overview.html#data-overview).

<span id="2bcca992"></span>
## Ray preprocessing workflow

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ddff4a594084ab595747a991f0109d1~tplv-goo7wpa0wc-image.image) </span>

Currently, many data preprocessing tasks involve small models for labeling and classification. The model inference module utilizes GPU/CPU resources, but the two ends of data processing are load and store, which are IO\-intensive operations. If these operations cannot be executed in a pipeline, backpressure may occur, resulting in reduced utilization of intermediate computing resources, including GPU/CPU, and ultimately increasing processing costs. Therefore, a Ray Data\-based solution is provided here.

<span id="df9aa32c"></span>
## Data preparation

Download the dataset from [Hugging Face](https://huggingface.co/datasets/bertram-gilfoyle/CC-MAIN-2021-17-raw/tree/main) and upload it to Volcano Engine Object Storage Service (TOS). The sample dataset used here is [bertram-gilfoyle/CC-MAIN-2021-17-raw](https://huggingface.co/datasets/bertram-gilfoyle/CC-MAIN-2021-17-raw/tree/main).

<span id="1a67c7f9"></span>
## Data loading


1. Configure the TOS read options. If you are using a Volcano Engine Ray cluster, our tosfs optimizes TOS read and write operations. You can use the self\-developed TosFileSystem. For the detailed installation process of tosfs, please refer to [official documentation](https://github.com/fsspec/tosfs).


```Python
TOS_FS = TosFileSystem(
    key=ENV_AK,
    secret=ENV_SK,
    endpoint_url=TOS_ENV_ENDPOINT,
    region='cn-beijing',
    socket_timeout=60,
    connection_timeout=60,
    max_retry_num=30
)
```


If pyproton is not integrated, you can use the open\-source s3fs. The configuration is as follows.

```Python
import s3fs
 
 # The configuration methods differ between versions, so both approaches are included here
s3fs.S3FileSystem.read_timeout = 300
s3fs.S3FileSystem.connect_timeout = 30
s3fs.S3FileSystem.retries = 100

def get_fs(s3_fs=True):
    return s3fs.S3FileSystem(anon=False,
                             key='xx',
                             secret='xxx==',
                             endpoint_url='https://tos-s3-cn-beijing.ivolces.com',
                             config_kwargs={'s3': {'addressing_style': 'virtual'},
                                            'read_timeout': 300,
                                            'connect_timeout': 30, })
```



2. Read files from the TOS folder.


```Python
# Retrieve all parquet files
    file_paths = TOS_FS.ls(input_dir, detail=False)

    # Only files with the parquet suffix are needed; you can replace this with other conditions, such as files containing a specific keyword in the name
    file_names = [
        file_name for file_name in file_paths if 'parquet' in file_name.split('/')[-1]][:2]
```



3. Set input and output directories.


```Bash
input_dir = '{bucket-name}/ray/raw/'
output_dir = '{bucket-name}/ray/output/'
```



4. Read parquet files.


```Bash
# Read all files
    # Read parquet files and retrieve only specific columns
    # schema
    # url              text
    # --------------------
    # https://www.volcengine.com/docs          Official link to Volcano Engine documentation
    ds = ray.data.read_parquet(
        file_names, filesystem=fs, concurrency=10, columns=['url', 'text'])
```


<span id="57ba1a44"></span>
## Data processing


1. Perform sensitive URL filtering on the data. Details are as follows.


```Bash
from typing import Dict
from datatrove.pipeline.filters import URLFilter
from datatrove.data import Document
from tldextract import TLDExtract

class CustomeURLFilter(URLFilter):
    """
    自定义URL过滤器
    过滤掉不安全的URL
    过滤掉没有uri的URL
    """

    name = "😈 CustomeURLFilter-filter"

    def __init__(
        self
    ):
        super().__init__

    def __call__(self, batch: Dict[str, str]):
        data = {}
        for (url, text) in batch.items():
            # Skip title
            if url == "url":
                continue

            # Skip keyword
            if "not safe" in url:
                continue

            # pseudo code
            # metadata = {"url": url}
            # document = Document(
            #     text="fake_text", id="fake_id", metadata=metadata)
            # print(f"------------{document.metadata['url']}")
            # filtered = super().filter(document)
            # if filtered:
            #     continue

            data[url] = text

        return data
```



2. Batch invocation in the main Ray Data workflow.


```Bash
 # Filter out unsafe URLs
    ds = ds.map_batches(CustomeURLFilter, batch_size=100,
                        num_cpus=1, concurrency=10)
```


<span id="131564e0"></span>
## Data archiving

```Bash
    # Write regression file to a fixed directory
    ds.write_parquet(output_dir, filesystem=fs, compression='snappy')
```


<span id="17954952"></span>
## Source code example

For more examples, refer to [official documentation](https://github.com/volcengine/emr-tutorial/tree/master/emr-on-vke/ai-ml/ray-examples).
