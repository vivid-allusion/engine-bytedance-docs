---
title: "tosfsspec advanced usage"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/tosfsspec_advanced_usage"
---

This article mainly introduces the advanced capabilities of tosfsspec, focusing on high performance, data consistency, and practical needs for specific business scenarios.

<span id="bed8e695"></span>
## Multipart upload and download

When handling large files, tosfsspec automatically enables the multipart mechanism, splitting the file into multiple parts for parallel transmission to improve speed and stability.

<span id="366a8a2b"></span>
### Part size (`part_size` and `block_size`)


* **`TosFileSystem(part_size=...)`** : The `part_size` set during `TosFileSystem` initialization serves as a global default, mainly affecting operations involving server\-side copy or multipart copy such as `cp_file`.

* **`fs.open(..., block_size=...)`** : The `block_size` parameter in the `open()` method is more commonly used and directly determines the buffer size for writing (`wb`, `ab`) or reading (`rb`) files.

   * Write modes (`wb`, `ab`):

      `block_size` determines the size of each part uploaded to TOS. To meet TOS requirements, this value must be at least 4MB; if not set explicitly, it defaults to `part_size` of `TosFileSystem`.

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For writing large files, it is recommended to set <code>block_size</code> between 8MB and 128MB, depending on network conditions and file size. Most scenarios can start from 8MB.      </div>
      

   * Read mode (`rb`):

      `block_size` determines the size of each data block downloaded from TOS, which is the amount of data pre\-fetched by the client when executing `file.read(size)`. A proper `block_size` can optimize random read performance.

   * Code examples:

   ```Python
   # Specify a 10MB slice size when writing
   with fs.open('tos://my-bucket/large_file.dat', 'wb', block_size=10 * 1024 * 1024) as f:
   # Writing 20MB of data will be split and uploaded in 2 slices
       f.write(b'a' * 20 * 1024 * 1024) 
   ```
   


<span id="181aa5d7"></span>
## Concurrent task control

tosfsspec uses a high\-performance kernel to execute high\-concurrency network requests and allows adjusting the concurrency pool size via initialization parameters.


* `shared_prefetch_tasks`: the number of concurrent prefetch tasks when reading data.

* `shared_upload_part_tasks`: the number of concurrent tasks for part uploads.

* `shared_upload_part_copy_tasks`: Number of concurrent part copy tasks.


Increasing concurrency improves parallelism and may speed up transfers under good network conditions but increases CPU and memory usage. Code example:

```Python
# increase upload concurrency to 64
fs = tosfsspec.TosFileSystem(
    ...,
    shared_upload_part_tasks=64
)
```


<span id="9061473d"></span>
## Append write (in `'ab'` mode)

tosfsspec supports opening objects in append mode (`ab`), suitable for continuous log writing, incremental updates, etc.; it relies on TOS's `AppendObject` feature. Code example:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Specify the requirement that the target object must be of Appendable type. When creating an object with <code>wb</code> mode for the first time in tosfsspec, a appendable object is created by default; appending to a non\-appendable object (such as a regular object uploaded by other tools) may fail.</div>


```Python
path = f'tos://{bucket}/logs/app.log'
# first write
with fs.open(path, 'wb') as f:
    f.write(b'Log entry 1\n')
# second append
with fs.open(path, 'ab') as f:
    f.write(b'Log entry 2\n')
# read verification
with fs.open(path, 'rb') as f:
    content = f.read()
print(content)
# output: b'Log entry 1\\nLog entry 2\\n'
```


<span id="ae1d11b7"></span>
## Content type (Content\-Type)

When uploading objects, tosfsspec tries to automatically infer the `Content-Type` (MIME type) to facilitate correct access by browsers and other clients.


* `put_file()`: Automatically inferred from the local file extension.

* `open(..., 'wb')` or `touch()`: Automatically inferred from the object key's extension.


To override automatic inference, explicitly specify it using the `ContentType` parameter in `open()`, `touch()`, or `put_file()`. The code example is shown below:

```Python
# auto-detect
fs.touch('tos://my-bucket/assets/style.css') # Content-Type is set to 'text/css' by default

# specify explicitly
# Set Content-Type to 'application/json' even if the file extension is .txt
with fs.open('tos://my-bucket/config.txt', 'wb', ContentType='application/json') as f:
    f.write(b'{"key": "value"}')
```


<span id="c603fa6a"></span>
## Data verification (`enable_crc`)

By default, `enable_crc=True`. `tosfsspec` uses CRC64 to verify data after transfer, ensuring consistency between local and remote data and providing strong data integrity protection. If extremely high performance is required and the risk of rare data corruption is acceptable, this verification can be disabled. The code example is shown below:

```Python
# Disable CRC check
fs_no_crc = tosfsspec.TosFileSystem(
    ...,
    enable_crc=False
)
```


<span id="1c4822a0"></span>
## HNS/FNS and `maxdepth` limitations

TOS Buckets mainly consist of two types:


* **FNS (Flat Namespace)** : a flat namespace where all objects exist at one level and the directory structure is simulated.

* **HNS (Hierarchical Namespace)** : a hierarchical namespace that offers a native directory structure, better performance, and an experience similar to HDFS.


tosfsspec supports both types but has operational differences:


* `mv()`: Moving directories within HNS buckets is an atomic and more efficient operation. Within FNS buckets, it requires copying and deleting each item individually.

* `walk()`, `find()`, `rm()`, `copy()`: The `maxdepth` parameter limits recursion depth during recursive operations. This parameter is only effective for FNS\-type buckets. Using `maxdepth` in HNS buckets raises a `ValueError` because the native directory traversal in HNS does not support this limit.


```Python
# In FNS Bucket, only traverse 2 levels of depth
# Assume bucket 'my-fns-bucket' is of FNS type
for root, dirs, files in fs.walk('tos://my-fns-bucket/deep/folder/', maxdepth=2):
    print(root)

# The following code will throw an error in HNS Bucket
# Assume bucket 'my-hns-bucket' is of HNS type
# fs.glob("tos://my-hns-bucket/data/**", maxdepth=1) # will raise ValueError
```
