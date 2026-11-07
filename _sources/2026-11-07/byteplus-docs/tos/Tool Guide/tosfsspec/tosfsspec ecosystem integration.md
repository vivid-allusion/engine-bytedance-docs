---
title: "tosfsspec ecosystem integration"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/tosfsspec_ecosystem_integration"
---

tosfsspec fully implements the `fsspec` specification. It can be used directly in Python and seamlessly integrates with major data analysis and AI frameworks such as `Pandas`, `Dask`, `Ray`, `PyArrow`, and `PyTorch`.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You need to configure long\-term access credentials before passing constructor parameters; please refer to <a href="https://docs.byteplus.com/docs/6349/2275445">Steps</a> for detailed instructions.</div>


<span id="AoQuxnxb"></span>
## Using with fsspec

<div data-tips="true" data-tips-type="warning">warning</div>


<div data-tips="true" data-tips-type="warning">The reason to use <code>tos-new://</code> instead of <code>tos://</code> is that the current unofficial <a href="https://github.com/fsspec/tosfs"><code>tosfs</code></a> has registered <code>fsspec</code> open\-source library and occupied the <code>tos://</code> protocol.</div>


You can access TOS resources directly through `fsspec.open()` by using the `tos-new://` protocol in the URL and passing the required constructor parameters via `storage_options`.


Code examples

```Python
import fsspec
import os
import tos

fsspec.register_implementation('tos-new', 'tosfsspec.TosFileSystem')
url = 'tos-new://your-bucket/path/to/data.csv'

# Get AKSK information from environment variables
key = os.getenv('TOS_ACCESS_KEY')
secret = os.getenv('TOS_SECRET_KEY')

storage_options = {
    'key','secret',
    'region': 'cn-beijing',
}

with fsspec.open(url, 'rb', **storage_options) as f:
    head = f.read(1024)
    print(head)
```



When using `fsspec.register_implementation`, `fsspec` will automatically select `TosFileSystem` as the underlying file system implementation.

<span id="03ad2128"></span>
## Using in Python

You can read and write TOS directly in Python through the common APIs of tosfsspec, similar to using a local file system.


Code examples

```Python
import os
import tosfsspec
import tos

# Get AKSK information from environment variables
key = os.getenv('TOS_ACCESS_KEY')
secret = os.getenv('TOS_SECRET_KEY')

fs = tosfsspec.TosFileSystem(
    key,secret,
    region='cn-beijing'
)

bucket = 'your-bucket'
local_file_path = 'localfile.txt'
remote_file_path = f'tos://{bucket}/remote_file.txt'

# create a local file to upload
with open(local_file_path, 'w') as f:
    f.write('Hello TOSFS.')

# upload to tos
fs.put_file(local_file_path, remote_file_path)
print(f'Uploaded {local_file_path} to {remote_file_path}')

# download from tos
downloaded_file_path = 'downloaded_file.txt'
fs.get_file(remote_file_path, downloaded_file_path)
print(f'Downloaded {remote_file_path} to {downloaded_file_path}')

# read content from downloaded local file
with open(downloaded_file_path, 'r') as f:
    content = f.read()
    print(f'Content of {downloaded_file_path}: {content}')

# delete tos file
fs.rm(remote_file_path)

# write to tos
with fs.open(remote_file_path, 'w') as f:
    f.write('Hello TOSFS.')

# read from tos
with fs.open(remote_file_path, 'r') as f:
    tos_content = f.read()
    print(f'Content of {remote_file_path}: {tos_content}')

# clean local files
os.remove(local_file_path)
os.remove(downloaded_file_path)
```



<span id="bd4aa69f"></span>
## Using in a multiprocessing environment

tosfsspec supports multi\-process scenarios and can be used in multi\-process environments; however, it is still recommended to start subprocesses in `spawn` mode.


Code examples

```Python
import multiprocessing
import tosfsspec
import os
import tos

bucket = 'your-bucket'

# set AK/SK via environment variables
key = os.getenv('TOS_ACCESS_KEY')
secret = os.getenv('TOS_SECRET_KEY')

def action(fs):
    result = fs.ls(f'tos://{bucket}/')
    print(result)

if __name__ == '__main__':
    # spawn mode is recommended
    multiprocessing.set_start_method('spawn', force=True)
    fs = tosfsspec.TosFileSystem(
        key,secret,
        region='cn-beijing'
    )
    processes = [multiprocessing.Process(target=action, args=(fs,)) for i in range(4)]
    for p in processes:
        p.start()
    for p in processes:
        p.join()
```



<span id="5a4474b7"></span>
## Integrate with Pandas

tosfsspec follows the `fsspec` specification, allowing Pandas to read or write various data formats such as CSV and Parquet directly from TOS via tosfsspec, without downloading locally first.


* Read CSV files from TOS



Code examples

```Python
import fsspec
import pandas as pd
import tosfsspec
import os
import tos

fsspec.register_implementation('tos-new', 'tosfsspec.TosFileSystem')
# Set AK/SK via environment variables
key = os.getenv('TOS_ACCESS_KEY')
secret = os.getenv('TOS_SECRET_KEY')

# Prepare a CSV file on TOS
fs = tosfsspec.TosFileSystem(
    key,secret,
    region='cn-beijing'
)
bucket = 'your-bucket'
csv_path = f'tos-new://{bucket}/datasets/iris.csv'
csv_content = 'sepal_length,sepal_width,petal_length,petal_width,species\n5.1,3.5,1.4,0.2,setosa\n'
with fs.open(csv_path, 'wb') as f:
    f.write(csv_content.encode())

# Configure storage_options
storage_options = {
    'key','secret',
    'region': 'cn-beijing'
}

# Read directly using pandas
df = pd.read_csv(csv_path, storage_options=storage_options)

print('Successfully read data from TOS:')
print(df)
```




* Write DataFrame to Parquet files in TOS



Code examples

```Python
import fsspec
import pandas as pd
import os
import tos

fsspec.register_implementation('tos-new', 'tosfsspec.TosFileSystem')

bucket = 'your-bucket'
# Set AK/SK via environment variables
key = os.getenv('TOS_ACCESS_KEY')
secret = os.getenv('TOS_SECRET_KEY')

# Create a DataFrame
data = {'col1': [1, 2], 'col2': [3, 4]}
df_to_write = pd.DataFrame(data=data)

# Define the Parquet file path to write
parquet_path = f'tos-new://{bucket}/output/data.parquet'

# Configure storage_options
storage_options = {
    'key','secret',
    'region': 'cn-beijing'
}

# Write directly to TOS; pyarrow or fastparquet required
df_to_write.to_parquet(parquet_path, storage_options=storage_options, index=False)

print(f'DataFrame Successfully written to: {parquet_path}')
```



<span id="a9ec4236"></span>
## Integrate with Dask

Dask is a flexible parallel computing library that natively supports `fsspec`\-compatible file systems. With `tosfsspec`, you can use `dask.dataframe` to read multiple CSV files on TOS concurrently and build a distributed DataFrame.


* Assume your TOS Bucket contains multiple CSV files with the following structure:



Code examples

```Python
your-bucket/
└── stock_data/
    ├── part.0.csv
    ├── part.1.csv
    └── part.2.csv
```




* You can use `dask` to load them all at once:



Code examples

```Python
import dask.dataframe as dd
import fsspec
import os
import tos

fsspec.register_implementation('tos-new', 'tosfsspec.TosFileSystem')

bucket = 'your-bucket'
# Set AK/SK via environment variables
key = os.getenv('TOS_ACCESS_KEY')
secret = os.getenv('TOS_SECRET_KEY')

# configure storage_options
storage_options = {
    'key','secret',
    'region': 'cn-beijing'
}

# file paths support wildcards
dask_path = f'tos-new://{bucket}/stock_data/part.*.csv'

# read data with Dask; Dask automatically handles wildcards and loads data in parallel
ddf = dd.read_csv(dask_path, storage_options=storage_options)

# Dask uses lazy evaluation; data is not yet loaded at this point
print('Number of partitions in a Dask DataFrame:', ddf.npartitions)

# execute computations, such as calculating the average; this triggers actual I/O operations
mean_value = ddf.some_column.mean().compute()

print('Calculated average:', mean_value)
```



<span id="f079862c"></span>
## Integrate with Ray distributed computing

Ray can use tosfsspec to directly read and process data on TOS in a distributed cluster.


Code examples

```Python
import ray
import tosfsspec
import os
import tos

# initialize Ray (usually already initialized in cluster environments)
ray.init()

bucket = 'your-bucket'
# set AK/SK via environment variables
key = os.getenv('TOS_ACCESS_KEY')
secret = os.getenv('TOS_SECRET_KEY')

fs = tosfsspec.TosFileSystem(
    key,secret,
    region='cn-beijing'
)

# csv file path
input_csv_path = f'tos://{bucket}/input.csv'
output_csv_path = f'tos://{bucket}/output.csv'

with fs.open(input_csv_path, 'w') as f:
    f.write('id,name,age\n1,John Doe,30\n2,Jane Smith,25\n3,Bob Johnson,40\n')

ds = ray.data.read_csv(input_csv_path, filesystem=fs)

# processing data
# ds = ds.map_batches(your_processing_function)

ds.repartition(1).write_csv(output_csv_path, filesystem=fs)
```



<span id="dafa064f"></span>
## Integrate with PyArrow

`pyarrow` can use tosfsspec through the `filesystem` parameter to efficiently read and write data in TOS.


Code examples

```Python
import pyarrow as pa
import pyarrow.dataset as ds
import pyarrow.parquet as pq
import tosfsspec
import os
import tos

bucket = 'your-bucket'
# Get AKSK information from environment variables
key = os.getenv('TOS_ACCESS_KEY')
secret = os.getenv('TOS_SECRET_KEY')

fs = tosfsspec.TosFileSystem(
    key,secret,
    region='cn-beijing'
)

# Generate Parquet dataset
table = pa.table({'year': [2020, 2022, 2021, 2022, 2019, 2021],
                  'n_legs': [2, 2, 4, 4, 5, 100],

                  'animal': ['Flamingo', 'Parrot', 'Dog', 'Horse',
                             'Brittle stars', 'Centipede']})
pq.write_table(table, f'tos://{bucket}/data.parquet', filesystem=fs)

# Read Parquet dataset
dataset = ds.dataset(f'tos://{bucket}/data.parquet', filesystem=fs)

# Output dataset information
print(f'Rows: {dataset.count_rows()}')
print(dataset.schema)

# Convert to Pandas DataFrame
df = dataset.to_table().to_pandas()
print(df.head())
```



<span id="596c2391"></span>
## Integrate with PyTorch

`PyTorch` can integrate tosfsspec for dataset loading and checkpoint read/write scenarios.


Code examples

```Python
import fsspec
import torch
import tosfsspec
from torchdata.datapipes.iter import FSSpecFileLister, FSSpecFileOpener
import os
import tos

bucket = 'your-bucket'
# Get AKSK information from environment variables
key = os.getenv('TOS_ACCESS_KEY')
secret = os.getenv('TOS_SECRET_KEY')

# Load dataset
fsspec.register_implementation('tos-new', 'tosfsspec.TosFileSystem', )
storage_options = {
    'key','secret',
    'region': 'cn-beijing'
}

file_lister = FSSpecFileLister(root=f'tos-new://{bucket}/dataset/', **storage_options)
iterable_dataset = FSSpecFileOpener(file_lister, mode='rb', **storage_options)

for _, item in iterable_dataset:
    data = item.read()

# Read and write checkpoint
fs = tosfsspec.TosFileSystem(
    key=,secret,
    region='cn-beijing'
)

model = torch.nn.Linear(10, 10)
with fs.open(f'tos://{bucket}/models/model.pt', 'wb') as f:
    torch.save(model.state_dict(), f)

with fs.open(f'tos://{bucket}/models/model.pt', 'rb') as f:
    state_dict = torch.load(f)
    # print(state_dict)
    model.load_state_dict(state_dict)
```
