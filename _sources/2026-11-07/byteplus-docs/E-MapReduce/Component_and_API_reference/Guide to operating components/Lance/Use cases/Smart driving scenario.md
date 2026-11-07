---
title: "Smart driving scenario"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Smart_driving_scenario"
---

<span id="d4996b4d"></span>
## Scenario description

This is a training scenario for a smart driving customer. The core issue the customer wants to address is the horizontal scalability of the training dataset in ultra\-large\-scale scenarios.

The customer's dataset is extremely large. Each piece of data is referred to as a "frame," and a frame contains several hundred columns, typically including camera (images), lidar, and sensor\-reported data. The size of a single frame is about 20 MB, and there are usually several frames per second. The customer currently stores data in Volcano Engine's vePFS and has already encountered bottlenecks. vePFS frequently requires horizontal expansion to meet the ever\-growing data storage demands. In the future, the customer plans to store 2 billion frames of data, with the storage scale approaching 40 PB. For vePFS to accommodate such a scale of data, the cost will be extremely high.

<span id="2bb94816"></span>
## Current solution

The customer currently uses a storage solution based on LMDB and pickle. Each frame's Python object data is serialized into a key\-value pair using pickle, then stored in LMDB. At the same time, the LMDB database files are stored on vePFS. When access is needed, the corresponding database file is first opened via LMDB, then the serialized frame data is read based on a specific key, and finally deserialized back into a Python object using pickle.

This solution is mature and lightweight for small\-scale datasets.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11e5f1e3777e42ecbf4486cb7f0520bf~tplv-goo7wpa0wc-image.image) </span>

<span id="97dd50d8"></span>
## Lance solution

The Volcano Engine EMR engine has proposed a multi\-modal data lake solution based on the Lance Format. Compared to the customer's current embedded storage solution using LMDB, this solution can support ultra\-large\-scale storage while providing better performance for various data access scenarios, including random access and full scans. Additionally, the storage of Lance data has very low coupling with the underlying storage service. Users can choose according to their scenario:


* To pursue high performance during training: Lance on vePFS can be selected.

* To pursue ultra\-large\-scale horizontal expansion: Lance on ToS can be selected.


Meanwhile, Lance supports ZSTD compression encoding, providing a high compression ratio for binary data. This feature can further compress storage space usage and also reduce network bandwidth usage.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c5055de27d24f1ea0f367f8a9dd0e8e~tplv-goo7wpa0wc-image.image) </span>

<span id="aad084d2"></span>
## Solution comparison

<span id="8fd1b7a2"></span>
### Data preprocessing

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13a4ea068cbc43329e6b8ccb83d51362~tplv-goo7wpa0wc-image.image) </span>


|Dimension |Current solution |Lance solution |
|---|---|---|
|Storage method |* LMDB + pickle: Embedded in\-memory database with a serialization mechanism tightly bound to the Python language;<br><br>* Dataset fragmentation, which makes management and mining difficult |* Columnar storage format, lightweight, decoupled from specific storage, can be stored on TOS or VEPFS;<br><br>* Can provide a complete view of the entire dataset and can scale horizontally with storage without limitation; |
|Schema changes<br><br>(Add column) |* Schema changes are very troublesome and almost require reprocessing all historical data;<br><br>* Another option is to split tables, but splitting tables requires all data and the cost of merging is very high; |* Lightweight schema evolution, generally does not require modifying old data files; |
|Distributed computing friendly |* The business needs to manually implement distributed ETL or data mining and analysis |* There are ready\-made connectors for RAY and Spark, making distributed ETL, data mining, and analysis very convenient; |
|Compression |* Needs to be implemented by business code and requires explicit handling by the business |* Transparent compression, with a compression ratio close to 3x, and transparent to the business; |
|Management cost |* High management cost: many fragmented LMDB files and no version management mechanism; |* Supports ACID transaction semantics and data version management mechanism (processing new version data does not interfere with training on old version data); |


<span id="d1ff660c"></span>
### Model training

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17c13b1b58cc440e8d6dbd2f20d9a08d~tplv-goo7wpa0wc-image.image) </span>


|Dimension |Current solution |Lance solution |
|---|---|---|
|Data shuffle |* Requires manual construction of index files, which is rather cumbersome;<br><br>* The pickle mechanism causes data to be merged for object storage, but when only some field information is needed, increased IO occurs; |* Lightweight shuffle mechanism based on row index;<br><br>* Schema can be expanded: only necessary data is read, without increased IO; |
|Stability |* Requires caching multiple LMDB file handles; over time, memory bloat and other stability issues may occur; |* No memory bloat issue; file\-level handles are not required. |


<span id="918881ce"></span>
## Code sample

The following is an example of the customer's schema:

```Thrift
schema = pa.schema([
    pa.field("dat_name", pa.string()),
    pa.field("frame_key", pa.string()),
    pa.field("label", pa.binary(), metadata={"lance-encoding:compression": "zstd"}),
    pa.field("sensor", pa.binary(), metadata={"lance-encoding:compression": "zstd"}),
    pa.field("src_label", pa.binary(), metadata={"lance-encoding:compression": "zstd"}),
])
```


LMDB to Lance:

```Python
import lmdb
import os
import lance
import pyarrow as pa
import ray
from tosfs.core import TosFileSystem

ENV_AK = ""
ENV_SK = ""
fs = TosFileSystem(
    endpoint_url="https://tos-cn-beijing.ivolces.com",
    key=ENV_AK,
    secret=ENV_SK,
    region="cn-beijing"
)

root_path = ""

sensor_path = root_path + 'sensor/'
label_path  = root_path + 'label/'
local_tmp_path = "/tmp/"
LANCE_PATH=""

dat_names = []
for path in fs.ls(label_path):
    dat_names.append(path.split("/")[-1].replace("_label.lmdb", ""))


schema = pa.schema([
    pa.field("label", pa.large_binary()),
    pa.field("sensor", pa.large_binary()),
])

LANCE_AK = ""
LANCE_SK = ""
storage_options = {
    "access_key_id": LANCE_AK,
    "secret_access_key": LANCE_SK,
    "aws_region": "cn-beijing",
    "aws_endpoint": "https://emrtest.tos-s3-cn-beijing.ivolces.com",
    "virtual_hosted_style_request": "true",
    "timeout": "600s"
}

ds = ray.data.from_items(dat_names, override_num_blocks=100)

def gen_pa_table_by_dat_name(parent_dir:str, dat_name: str):
    label_lmdb = parent_dir + "/" + dat_name + '_label.lmdb'
    sensor_lmdb = parent_dir + "/" + dat_name + '.lmdb'
    label_env = lmdb.open(label_lmdb, readonly=True, lock=False)
    label_ctx = label_env.begin(write=False)
    sensor_env = lmdb.open(sensor_lmdb, readonly=True, lock=False)
    sensor_ctx = sensor_env.begin(write=False)
    frame_keys = []
    for key, _ in label_ctx.cursor():
        if key.startswith("CD".encode()):
            frame_keys.append(key)
    schema = pa.schema([
            pa.field("label", pa.large_binary()),
            pa.field("sensor", pa.large_binary()),
        ])
    data = {
        "label": [],
        "sensor": [],
    }
    for frame_key in frame_keys:
        label_key = frame_key.decode('utf-8')
        sensor_key = frame_key.decode('utf-8')
        src_label_key = "src_" + label_key
        label_data = label_ctx.get(frame_key)
        sensor_data = sensor_ctx.get(frame_key)
        src_label_data = label_ctx.get(src_label_key.encode())
        data['label'].append(label_data)
        data['sensor'].append(sensor_data)
    table = pa.Table.from_arrays(
        [
            pa.array(data['label'], type=pa.large_binary()),
            pa.array(data['sensor'], type=pa.large_binary()),
        ],
        schema=schema
    )
    label_env.close()
    sensor_env.close()
    return table

def duplicate_row(row: dict[str, any]):
    dat_name = row["item"]
    import os
    local_dat_dir = local_tmp_path + dat_name
    local_label_dat_dir = local_dat_dir + "/" + dat_name + "_label.lmdb"
    local_sensor_dat_dir = local_dat_dir + "/" + dat_name + ".lmdb"
    label_tos_lmdb = label_path + dat_name + "_label.lmdb/"
    sensor_tos_lmdb = sensor_path + dat_name + "/" + dat_name+ ".lmdb/"

    print(f'local label  = {local_label_dat_dir}')
    print(f'local sensor = {local_sensor_dat_dir}')
    print(f'tos   label  = {label_tos_lmdb}')
    print(f'tos   sensor = {sensor_tos_lmdb}')

    os.makedirs(os.path.dirname(local_dat_dir), exist_ok=True)
    os.makedirs(os.path.dirname(local_label_dat_dir), exist_ok=True)
    os.makedirs(os.path.dirname(local_label_dat_dir), exist_ok=True)

    from tosfs.core import TosFileSystem
    fs = TosFileSystem(
        endpoint_url="https://tos-cn-beijing.ivolces.com",
        key=ENV_AK,
        secret=ENV_SK,
        region="cn-beijing"
    )
    fs.get(label_tos_lmdb, local_label_dat_dir, recursive=True)
    print(f"Downloaded {label_tos_lmdb} from tos to {local_label_dat_dir}")
    fs.get(sensor_tos_lmdb, local_sensor_dat_dir, recursive=True)
    print(f"Downloaded {sensor_tos_lmdb} from tos to {local_sensor_dat_dir}")
    
    table = gen_pa_table_by_dat_name(local_dat_dir, dat_name)
    fragment = lance.fragment.LanceFragment.create(LANCE_PATH, table, storage_options=storage_options)
    import shutil
    if os.path.exists(local_dat_dir):
        try:
            # Recursively delete folders and handle read-only permissions
            print(f"准备删除文件夹 {local_dat_dir}。")
            shutil.rmtree(local_dat_dir)
            print(f"文件夹 {local_dat_dir} 已成功删除。")
        except Exception as e:
            print(f"删除文件夹 {local_dat_dir} 时出错: {e}")
    else:
        print(f"文件夹 {local_dat_dir} 不存在。")
    return {"fragment": fragment}

fragments = ds.map(duplicate_row).take_all()

operation = lance.LanceOperation.Append([fragment['fragment'] for fragment in fragments])
dataset = lance.dataset(LANCE_PATH, storage_options=storage_options)
dataset = lance.LanceDataset.commit(LANCE_PATH, operation, read_version=dataset.latest_version, storage_options=storage_options)
```


Data shuffling during training:


* Based on rowid:


```Python
columns=["dat_name", "frame_key"]
rowids = []
index = 0
for fragment in ds.get_fragments():
    rowids.append(index)
    index += fragment.count_rows()
ds.take(rowids, columns=columns)
```



* Based on FragmentId:


```Python
columns=["dat_name", "frame_key"]
rowids = []
fragids = []
for fragment in ds.get_fragments():
    fragids.append(fragment.fragment_id)
    rowids.append(fragment.fragment_id << 32)

table = ds._take_rows(rowids, columns=columns)

# Write Fragment id to a new column
new_column_data = pa.array(fragids)
new_table = table.append_column('frag_id', new_column_data)

import pyarrow as pa
import pyarrow.compute as pc

filter_values = ["tag13_seq29_CD701_LS6C3E191PA250083_2024-12-06_10-22-32","tag13_seq30_CD701_LS6C3E191PA250083_2024-12-06_10-22-32","tag13_seq31_CD701_LS6C3E191PA250083_2024-12-06_10-22-32"]
# Filter by dat_name
filter_fn = pc.is_in(new_table.column('dat_name'), pa.array(filter_values))

filtered_table = pc.filter(new_table, filter_fn)

print(filtered_table.to_pandas())
```
