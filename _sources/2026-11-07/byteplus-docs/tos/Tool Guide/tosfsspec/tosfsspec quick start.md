---
title: "tosfsspec quick start"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/tosfsspec_quick_start"
---

This article guides you through quickly getting started with tosfsspec, including environment setup, authentication, authorization, and basic file operations.

<span id="6d6135b1"></span>
## Dependency description

`tosfsspec `depends on the following core components to run properly. `pip` will automatically handle the installation of these dependencies for you:


* Python: `>=3.8, <3.14`.

* fsspec: `>=2023.5.0`, providing the base class for file system specification.

* tos: `>=2.8.0`, the official TOS Python SDK provided by BytePlus.

* tosnativeclient: `>=1.1.13`, providing the underlying high\-performance core for tosfsspec, responsible for network requests, concurrency control, CRC checks, and other core functions.


<span id="6417842b"></span>
## Operating system

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you require support for a specific operating system, <a href="https://console.byteplus.com/workorder/create?step=1">submit a ticket</a> to contact us.</div>


Supports only Linux x86_64 and MacOS arm64 systems.

<span id="7adc674a"></span>
## Steps


1. If you have installed Python and the corresponding pip tool. Make sure the installed version meets tosfsspec dependency requirements.

   ```Shell
   python --version
   pip --version
   ```
   

2. Install tosfsspec directly using `pip`.

   ```Bash
   pip install tosfsspec
   ```
   

3. Obtain AKSK information.

* Region: the region where your TOS bucket is located, such as `cn-beijing`.

* Access Key: includes Access Key ID (AK) and Secret Access Key (SK), which serve as credentials for accessing the BytePlus API.

* Endpoint: optional parameter. If left empty, tosfsspec will auto\-generate it based on the `region` you provide.

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For a detailed list of regions and access domains, see <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Region and access domain (Endpoint)</a>.   </div>
   

4. Configure long\-term access credentials.

   Before initializing the SDK, you need to configure long\-term access credentials. The steps to configure these credentials vary by operating system.

   
   <Tabs>
   <Tab zoneid="eezKKifbQd" title="macOS">
   <TabTitle>macOS</TabTitle>
   
   1. Open Terminal and run this command to open the file.
   
   
   ```Shell
   nano ~/.bash_profile
   ```
   
   
   
   2. Add your access key ID and secret access key at the end of the file.
   
   
   ```Shell
   export TOS_ACCESS_KEY=AKTPYmI1Z****
   export TOS_SECRET_KEY=T1dJM01UU****
   ```
   
   
   
   3. Save the file and exit.
   
   4. Run this command to apply the configuration.
   
   
   ```Shell
   source ~/.bash_profile
   ```
   
   
   
   5. Run this command to verify the configuration.
   
   
   ```Shell
   echo $TOS_ACCESS_KEY
   echo $TOS_SECRET_KEY
   ```
   
   
   If configured successfully, the following example will be returned:
   
   ```Shell
   AKTPYmI1Z****
   T1dJM01UU****
   ```
   
   
   
   </Tab>
   <Tab zoneid="Yhynxbv3AQ" title="Linux">
   <TabTitle>Linux</TabTitle>
   
   1. Open Terminal and run this command to open the file.
   
   
   ```Shell
   sudo vim /etc/profile
   ```
   
   
   
   2. Add your access key ID and secret access key at the end of the file.
   
   
   ```Shell
   export TOS_ACCESS_KEY=AKTPYmI1Z****
   export TOS_SECRET_KEY=T1dJM01UU****
   ```
   
   
   
   3. Save the file and exit.
   
   4. Run this command to apply the configuration.
   
   
   ```Shell
   source /etc/profile
   ```
   
   
   
   5. Run this command to verify the configuration.
   
   
   ```Shell
   echo $TOS_ACCESS_KEY
   echo $TOS_SECRET_KEY
   ```
   
   
   The following output confirms a successful configuration.
   
   
   ```Shell
   AKTPYmI1Z****
   T1dJM01UU****
   ```
   
   
   
   </Tab>
   </Tabs>
   

5. Initialize the file system. The following code initializes it using the TOS domain name.

   ```Python
   import tosfsspec
   import os
   import tos
   
   # Get AKSK information from environment variables
   key = os.getenv('TOS_ACCESS_KEY')
   secret = os.getenv('TOS_SECRET_KEY')
   # Initialize TosFileSystem
   fs = tosfsspec.TosFileSystem(
       key，secret，
       endpoint = "your endpoint"，
       region = "your region"
   )
   ```
   


<span id="4b7e490a"></span>
## Basic operation examples

<span id="3711617f"></span>
### File read and write operations

You can use the `fs.open()` method to read and write objects on TOS just like working with local files. It returns a file\-like object that supports standard methods such as `read()` and `write()`.

<span id="aaef3c33"></span>
#### Write to a file

Open a path in binary write mode (`wb`). After the `with` code block completes, the data automatically uploads to TOS.

```Python
# Define the Bucket and object Key to write
bucket = 'your-bucket'
key = 'path/to/your/file.txt'
full_path = f'tos://{bucket}/{key}'

# Write data
data_to_write = b'Hello, tosfsspec!'
with fs.open(full_path, 'wb') as f:
    f.write(data_to_write)

print(f'The file has been successfully written.: {full_path}')
```


<span id="b66b46f4"></span>
#### Read object

Open an existing object in binary read mode (`rb`)

```Python
# Read the recently written file from TOS
with fs.open(full_path, 'rb') as f:
    content = f.read()

print(f'Content read from the file: {content.decode()}')
# Output: Content read from file: Hello, tosfsspec!
```


<span id="b21d2d78"></span>
### Basic operations

`TosFileSystem` offers a variety of file system operation methods.

<span id="5e391b23"></span>
#### List Buckets

When the path is the root directory `/` or an empty string `''`, `fs.ls()` lists all storage buckets in your account.

```Python
# List all buckets
buckets = fs.ls('/')
for b in buckets:
    print(b['name'])
```


<span id="d301b6fc"></span>
#### List Objects

The `fs.ls()` method lists files and directories at the specified path.

```Python
# Create some files and directories for demonstration
fs.touch(f'tos://{bucket}/data/file1.txt')
fs.touch(f'tos://{bucket}/data/file2.csv')
fs.makedirs(f'tos://{bucket}/data/images/')
fs.touch(f'tos://{bucket}/data/images/photo.jpg')

# List contents under the 'data/' directory
print(f'--- ls tos://{bucket}/data/ ---')
file_list = fs.ls(f'tos://{bucket}/data/')
for item in file_list:
    print(f"- {item['name']} (type: {item['type']}, size: {item['size']})")
```


Output example:

```Plain Text
--- ls tos://your-bucket/data/ ---
- your-bucket/data/file1.txt (type: file, size: 0)
- your-bucket/data/file2.csv (type: file, size: 0)
- your-bucket/data/images (type: directory, size: 0)
```


<span id="b176b1fc"></span>
#### Upload and download (`put`/`get`)

Use `fs.put()` and `fs.get()` to transfer complete files between the local file system and TOS.

```Python
# create a local file
local_file_path = 'local_example.txt'
with open(local_file_path, 'w') as f:
    f.write('This is a local file.')

# uploading local files to TOS
remote_path_for_put = f'tos://{bucket}/uploads/uploaded_file.txt'
fs.put(local_file_path, remote_path_for_put)
print(f'{local_file_path} Uploaded to {remote_path_for_put}')

# download file from TOS to local
local_download_path = 'downloaded_from_tos.txt'
fs.get(remote_path_for_put, local_download_path)
print(f'{remote_path_for_put} Downloaded to {local_download_path}')

# verify download content
with open(local_download_path, 'r') as f:
    print(f'Downloaded file content: {f.read()}')

# clean up local files
import os
os.remove(local_file_path)
os.remove(local_download_path)
```


<span id="76c34ef4"></span>
#### Copy, move, and delete (`cp`/`mv`/`rm`)

These operations manage objects within TOS.


* `fs.cp()`: copy objects.

* `fs.mv()`: move or rename objects.

* `fs.rm()`: delete objects or directories.


```Python
# copying objects
src_path = f'tos://{bucket}/data/file1.txt'
dst_path = f'tos://{bucket}/data/file1_copy.txt'
fs.cp(src_path, dst_path)
print(f'The file has been copied.: {fs.exists(dst_path)}') # output: True

# move (rename) file
mv_src = dst_path
mv_dst = f'tos://{bucket}/data/file1_renamed.txt'
fs.mv(mv_src, mv_dst)
print(f'Does the original file exist?: {fs.exists(mv_src)}') # output: False
print(f'Does the new file exist?: {fs.exists(mv_dst)}') # output: True

Deleting objects
fs.rm(mv_dst)
exists = fs.exists(mv_dst)
print(f'Does the renamed file exist: {exists}') Output: False

Recursively delete directories
fs.rm(f'tos://{bucket}/data/', recursive=True)
exists = fs.exists(f'tos://{bucket}/data/')
print(f'Does the data directory exist?: {exists}') Output: False
```


<span id="eb93ac0a"></span>
#### Directories and wildcards (`walk`/`glob`)

Use `fs.walk()` and `fs.glob()` to perform advanced object searches.


* `fs.walk()`: recursively traverse all objects and subdirectories in a specified directory.

* `fs.glob()`: find matching objects using wildcard patterns like `*` and `**`.


```Python
Prepare directory structure
fs.makedirs(f'tos://{bucket}/glob_test/a/b/')
fs.touch(f'tos://{bucket}/glob_test/a/file.txt')
fs.touch(f'tos://{bucket}/glob_test/a/b/file.log')

Use walk to traverse
print('--- walk ---')
for root, dirs, files in fs.walk(f'tos://{bucket}/glob_test/'):
    print(f'Root: {root}, Dirs: {dirs}, Files: {files}')

Use glob to search
print('\n--- glob ---')
log_files = fs.glob(f'tos://{bucket}/glob_test/**/*.log')
print(f'Found .log file: {log_files}')
```


<span id="5646ab5e"></span>
#### Get metadata and check existence (`info`/`exists`)


* `info()` or `stat()`: Get detailed information of files or directories.

* `exists()`: Check if a path exists.


```Python
path_to_check = f'tos://{bucket}/data/file1.txt'
fs.touch(path_to_check)

Check existence
if fs.exists(path_to_check):
    print(f'{path_to_check} exist.')
    Get metadata
    info = fs.info(path_to_check)
    print(f'{info}')
else:
    print(f'{path_to_check} It does not exist.')
```
