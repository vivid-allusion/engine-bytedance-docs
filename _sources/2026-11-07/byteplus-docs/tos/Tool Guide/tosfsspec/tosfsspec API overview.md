---
title: "tosfsspec API overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/tosfsspec_API_overview"
---

This article mainly introduces common methods and parameter summaries of the two core classes: `TosFileSystem` and `TosFile`.

<span id="f055e24b"></span>
## `tosfsspec.TosFileSystem`

`TosFileSystem` is the main entry point for interacting with TOS, providing all top\-level file system operations.

<span id="0211d374"></span>
### Constructor

```Python
__init__(self, region, endpoint='', key='', secret='', part_size=8388608, max_retry_count=3, shared_prefetch_tasks=32, shared_upload_part_tasks=32, shared_upload_part_copy_tasks=32, enable_crc=True, **kwargs)
```


<span id="511418b8"></span>
### Common methods

<span id="3d9ea67f"></span>
#### **Constructor parameter table**


|**Parameter** |**Item** |**Default value** |**Description** |
|---|---|---|---|
|region |str |Yes |Region where the target Bucket is located, for example, `'cn-beijing'`. |
|endpoint |str |'' |TOS external access domain name. If empty, the default Endpoint will be used based on `region`; specify explicitly here for intranet access or custom domain. |
|key |str |'' |Access Key ID for accessing TOS. Explicit configuration is recommended. |
|secret |str |'' |Secret Access Key for accessing TOS. |
|part_size |int |8 \* 1024 \* 1024 |Base part size (bytes) for multipart upload and multipart copy.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><code>part_size</code> must be greater than or equal to <code>4 * 1024 * 1024</code>, or a <code>ValueError</code> will be raised.</div><br> |
|max_retry_count |int |3 |Maximum number of retries for a failed request. |
|shared_prefetch_tasks |int |32 |Number of concurrent prefetch tasks during read. |
|shared_upload_part_tasks |int |32 |Number of concurrent tasks during multipart upload. |
|shared_upload_part_copy_tasks |int |32 |Number of concurrent tasks during multipart copy. |
|enable_crc |bool |True |Enable CRC64 checksum. Enabled for data integrity verification after upload and download. |


<span id="149ec8e4"></span>
#### **Common methods**

The following lists common methods of `TosFileSystem`, key parameters, and corresponding simple examples. All examples assume instance initialization is complete:

```Python
import tosfsspec
import os
import tos
 
# Set AK/SK via environment variables
key = os.getenv('TOS_ACCESS_KEY')
secret = os.getenv('TOS_SECRET_KEY')

fs = tosfsspec.TosFileSystem(
    key,secret,
    region='cn-beijing',
)
bucket = 'your-bucket'
```



* `open(self, path, mode='rb', block_size=None, autocommit=True, **kwargs)`


Purpose: open an object in TOS and return a `TosFile` file object.

Key parameters:


   * `path`: can be in the form of `'tos://bucket/key'` or `'bucket/key'`; using the protocol form is recommended.

   * `mode`: supports binary modes only: `'rb'`, `'wb'`, `'ab'`.

   * `block_size`: block size (bytes) used for reading and writing. Must be at least 4MB in write mode; if not explicitly set, it falls back to `part_size`.

   * Other common keyword parameters: In write mode, you can explicitly specify the object's `ContentType` using `Content-Type`.


Code examples:

```Python
path = f'tos://{bucket}/api-demo/open-example.txt'
with fs.open(path, 'wb', block_size=8 * 1024 * 1024, ContentType='text/plain') as f:
    f.write(b'hello from tosfsspec')

with fs.open(path, 'rb') as f:
    data = f.read()
    print(data.decode('utf-8'))
```




* `ls(path, detail=True, sort_names=True)`


Purpose: List files and directories under the specified path.

Key parameters:


   * `path`: Lists all Buckets when `'/'` or `''` is used; lists the prefixes under the Bucket when `'tos://bucket/prefix/'` is used.

   * `detail`: Returns a list of dictionaries with metadata if `True`; otherwise returns a list of string paths.


Code examples:

```Python
root = f'tos://{bucket}/data/'
entries = fs.ls(root, detail=True)
for entry in entries:
    print(entry['name'], entry['type'], entry['size'])
```




* `info(path, **kwargs) / stat(path)`


Purpose: Retrieve detailed metadata of a single file or directory.



* `exists(path, **kwargs)`


Purpose: determine whether the given path exists.



* `checksum(path)`


Purpose: get the checksum of the current object version. File types use the object's ETag, and directory types use the directory information hash.

Code example:

```Python
path = f'tos://{bucket}/data/file.txt'
if fs.exists(path):
    info = fs.info(path)
    print('size:', info['size'])
    print('checksum:', fs.checksum(path))
```




* `isdir(path) / isfile(path)`


Purpose: determine whether the path is a directory or a file.

Code example:

```Python
path_dir = f'tos://{bucket}/data/'
path_file = f'tos://{bucket}/data/file.txt'
print('isdir:', fs.isdir(path_dir))
print('isfile:', fs.isfile(path_file))
```




* `glob(path, maxdepth=None, **kwargs)`


Purpose: Use wildcard patterns to match paths and return a list of matched files.



* `find(path, maxdepth=None, withdirs=False, detail=False, **kwargs)`


Purpose: List all files (and optionally directories) under a path, usually to implement custom traversal logic.



* `walk(path, maxdepth=None, detail=False, **kwargs)`


Purpose: Recursively traverse the directory tree, returning a `(root, dirs, files)` generator.

Code examples:

```Python
pattern = f'tos://{bucket}/logs/**/*.log'
matched = fs.glob(pattern)
print('matched logs:', matched)

for root, dirs, files in fs.walk(f'tos://{bucket}/logs/'):
    print('root:', root, 'files:', [f['name'] for f in files])

found = fs.find(f'tos://{bucket}/logs/', maxdepth=2)
print('found paths:', found)
```




* `put_file(lpath, rpath, callback=None, **kwargs)`


Purpose: Upload a local file to the specified path in TOS.

Key parameters:


   * `lpath`: Local file path.

   * `rpath`: target TOS path, usually `'tos://bucket/key'`.

   * `callback`: optional progress callback implementing the `set_size()` and `relative_update()` interfaces.

   * Other common keyword arguments: explicitly specify the object's `Content-Type` via `ContentType`. If not specified, it will be automatically inferred based on the local file extension.


Code examples:

```Python
local_path = 'local-demo.txt'
with open(local_path, 'w', encoding='utf-8') as f:
    f.write('local to TOS')

remote_path = f'tos://{bucket}/upload/local-demo.txt'
fs.put_file(local_path, remote_path, ContentType='text/plain')
```




* `get_file(rpath, lpath, callback=None, **kwargs)`


Purpose: download remote objects to a local file.

Key parameters:


   * `rpath`: source TOS path.

   * `lpath`: local save path; intermediate directories will be automatically created if not existing.

   * `callback`: optional progress callback.


Code examples:

```Python
download_path = 'download-from-tos.txt'
fs.get_file(remote_path, download_path)
with open(download_path, 'r', encoding='utf-8') as f:
    print(f.read())
```




* `cp_file(path1, path2, reserve_metadata=False, **kwargs)`


Purpose: copy a single object within TOS.

Key parameters:


   * `path1`: source object path.

   * `path2`: destination object path.

   * `reserve_metadata`: if `True`, preserves source object's metadata as much as possible.



* `copy(path1, path2, recursive=False, maxdepth=None, on_error=None, reserve_metadata=False, **kwargs)`


Purpose: copy one or more paths within TOS, supporting recursive directory copying and wildcards.



* `mv(path1, path2, recursive=False, maxdepth=None, reserve_metadata=False, **kwargs)`


Purpose: Move (rename) objects or directories within TOS. For HNS Buckets, directory moves are usually atomic; for FNS Buckets, the operation may involve copy and delete.

```Python
src = f'tos://{bucket}/api-demo/src.txt'
dst_copy = f'tos://{bucket}/api-demo/src-copy.txt'
dst_mv = f'tos://{bucket}/api-demo/src-moved.txt'

fs.cp_file(src, dst_copy, reserve_metadata=True)
fs.copy(dst_copy, f'tos://{bucket}/api-demo/copy-dir/', recursive=False)
fs.mv(dst_copy, dst_mv)
```




* `rm(path, recursive=False, maxdepth=None)`


Purpose: Delete a single path or a group of paths. `path` can be a string or a list of strings.



* `rmdir(path, **kwargs)`


Purpose: Delete an empty directory; when `delete_bucket=True` is passed, the entire Bucket can be deleted.



* `mkdir(path, create_parents=True, create_bucket=False, **kwargs)`


Purpose: Create a directory; when `create_bucket=True` and the path contains only the Bucket name, a Bucket creation is attempted.



* `makedirs(path, exist_ok=False)`


Purpose: recursively create directory structure; no error if directory exists when `exist_ok=True`.



* `touch(path, truncate=True, **kwargs)`


Purpose: create a zero\-byte object or truncate an existing object.

Key parameters:


   * `truncate`: raises an exception if set to `False` and the object exists.

   * `content_type`: optional; explicitly specify `Content-Type`. If not specified, inferred automatically based on the key suffix.


Code examples:

```Python
bucket_root = f'tos://{bucket}'
fs.mkdir(f'{bucket_root}/tmp/', create_parents=True)
fs.makedirs(f'{bucket_root}/tmp/api-demo/', exist_ok=True)
temp_file = f'{bucket_root}/tmp/api-demo/file.tmp'
fs.touch(temp_file)
fs.rm(temp_file)
fs.rmdir(f'{bucket_root}/tmp/api-demo/')
```




* close()


Purpose: close the underlying client connection and release resources. Usually called automatically when the process exits; call explicitly to release resources early.

Code examples:

```Python
fs.close()
```



<span id="12170911"></span>
## `tosfsspec.TosFile`

`TosFile` is a file class object returned by `fs.open()`, providing standard I/O methods.

<span id="06bd919e"></span>
### Constructor

```Python
__init__(self, fs, path, mode='rb', block_size='default', autocommit=True, **kwargs)
```


<span id="fc027213"></span>
### Common methods


|**Method/Attribute** |**Description** |
|---|---|
|`read(size=-1)` |Read the specified number of bytes from the current position. `size=-1` means read until the end of the file. |
|`readinto(buf)` |Read data directly into the writable buffer object `buf` and return the actual number of bytes read, avoiding extra memory copying. |
|`readuntil(char=b'\n', blocks=None)` |Continuously read data until the specified delimiter `char` (including the delimiter) or the end of the file is reached. |
|`write(data)` |Write the byte data `data` into the file buffer. |
|`seek(loc, whence=0)` |Move the file pointer to the specified position. `whence` can be `0` (beginning), `1` (current position), or `2` (end of file). |
|`tell()` |Return the current position of the file pointer. |
|`flush(force=False)` |Flushes the accumulated data in the buffer to the underlying write stream. Usually called automatically by `commit()` or when closing the file. |
|`commit()` |Commits all data in the current buffer. Explicit calls are generally unnecessary for write modes with auto\-commit enabled. |
|`discard()` |Abandons the current write session, terminates the underlying shard upload, and discards uncommitted data. |
|`close()` |Closes the file and ensures all data is written. Automatically called when exiting the `with` statement block. |
|`readable()` / `writable()` / `seekable()` |Return boolean values indicating whether the file supports reading, writing, or random access. |
|`closed` |Indicates whether the file is closed. |
|`bucket` |Name of the bucket to which the current file belongs. |
|`key` |Object key of the current file within the bucket. |


<span id="bffd46ad"></span>
### Code examples

```Python
path = 'tos://your-bucket/api-demo/line-data.txt'
with fs.open(path, 'wb') as f:
    f.write(b'first line\nsecond line\n')
    
with fs.open(path, 'rb') as f:
    first = f.readuntil(b'\n')
    print('first line:', first)
    print('bucket:', f.bucket, 'key:', f.key)
```
