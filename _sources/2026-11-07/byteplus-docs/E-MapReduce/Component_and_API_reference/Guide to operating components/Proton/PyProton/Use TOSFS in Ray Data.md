---
title: "Use TOSFS in Ray Data"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Use_TOSFS_in_Ray_Data"
---

With the increasing prevalence of large language models, the importance of the RAY engine is becoming more prominent. As a powerful technical foundation, the RAY engine plays a key role in the ecosystem of large language models. It offers outstanding computational acceleration capabilities, efficiently handling large\-scale data processing tasks, greatly reducing the time required for training and inference of large language models, and significantly improving the efficiency of model development and application. When processing complex language logic and massive text data, the RAY engine, thanks to its advanced architectural design, can flexibly allocate computing resources to ensure stable operation and accurate output of models across different scenarios. Whether in intelligent customer service, content generation, language translation, or other fields, the RAY engine provides a solid and reliable foundation for running large language models, helping them break through performance bottlenecks, achieve broader and deeper commercial and social value, and become one of the core driving forces for the continuous advancement and widespread adoption of large language model technology.

Volcano Engine offers a variety of products to meet different users' needs for the RAY engine. For details, refer to [RAY service related articles](https://docs.byteplus.com/docs/undefined/69aa38e4949de0056969b411). TOS is a low\-cost object storage service launched by Volcano Engine that supports massive amounts of data. The combination of the two is a mainstream choice for many AI users. TOSFS is a lightweight Python SDK for accessing TOS. It allows users to read and write TOS in the Ray Data module.

Install the latest version of TOSFS and the RAY\-related dependencies using the following command:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to use Python 3.9 or above.</div>


```Shell
pip install tosfs
pip install "ray[data]"
```


The following code demonstrates how to use the Ray Data API together with the common APIs of TosFileSystem to read and write TOS:

```Python
import ray
import logging
from tosfs.core import TosFileSystem

# csv file path
input_csv_path = "tos://{your-bucket}/input.csv"
output_csv_path = "tos://{your-bucket}/output.csv"

# TOS AK
ENV_AK = '{Access Key}'
# TOS SK
ENV_SK = '{Secret Key}'
# TOS ENDPOINT Please fill in according to actual conditions
TOS_ENV_ENDPOINT = 'https://tos-cn-beijing.volces.com'

ray.init(runtime_env={
    "env_vars": {"RAY_LOGGING_LEVEL": "INFO"},
    "pip": ["pyarrow", "tosfs"]
})

logging.basicConfig(level=logging.INFO)
# region in TosFileSystem Please fill in according to actual conditions
tos_fs = TosFileSystem(
    key=ENV_AK,
    secret=ENV_SK,
    endpoint_url=TOS_ENV_ENDPOINT,
    region='cn-beijing',
    socket_timeout=60,
    connection_timeout=60,
    max_retry_num=30
)


if __name__ == "__main__":
    # init: write a file to tos
    with tos_fs.open(input_csv_path, 'w') as f:
        f.write("id,name,age\n1,John Doe,30\n2,Jane Smith,25\n3,Bob Johnson,40\n")

    ds = ray.data.read_csv(input_csv_path, filesystem=tos_fs)

    # processing data
    #ds = ds.map_batches(your_processing_function)

    ds.repartition(1).write_csv(output_csv_path, filesystem=tos_fs)
```
