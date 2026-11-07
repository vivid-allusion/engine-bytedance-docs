---
title: "Accessing and storing TOS data in PyTorch jobs"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Accessing-and-storing-tos-data-in-Pytorch-tasks"
---

This article explains how to access and store TOS data in Pytorch tasks.

<span id="76d4175a"></span>
## Prerequisites


1. Before using TOS, ensure you have registered a BytePlus account and completed identity verification. For details, see [Signing up for BytePlus accounts](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account).

2. Make sure you have activated the TOS service and created a TOS bucket. For details, see [Quick Start](https://docs.byteplus.com/docs/tos/docs-quick-start_1#step-1-activating-tos).

3. The Linux x86\-64 operating system must be used.

4. Python 3.8 or later is installed.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Versions 3.12 and above are not recommended because PyTorch does not support them.   </div>
   

<span id="2e78c221"></span>
## Environment preparation

Before integrating TOS, install Pytorch in the Python 3.8+ environment. For details, see [Pytorch](https://pytorch.org/get-started/locally/).

```Python
# Install basic torch dependencies
pip3 install torch torchvision

# Install torch lighting
pip3 install lightning

# Install torchdata
pip3 install torchdata==0.9.0
```


After installation, you can verify the success by using the following example.

```Python
import torch
import torchvision

# Save checkpoint as a local file
if __name__ == '__main__':
    model = torchvision.models.resnet18()
     
    with open('test.pt', 'wb') as writer:
        torch.save(model.state_dict(), writer)


    with open('test.pt', 'rb') as reader:
        stat_dict = torch.load(reader)

    model.load_state_dict(stat_dict)
    print(model)
```


<span id="fab39175"></span>
## Integration method description


|Integration method |Description |
|---|---|
|Use fsspec integration |* By implementing the fsspec standard with tosfs, the BytePlus TOS is wrapped as Python’s standard read/write interface, and torchdata is used to directly read and write local paths for integration.<br><br>* Supports TOS FNS buckets and HNS buckets. |
|Use FSX integration |* FSX supports mounting buckets to Linux systems as local file systems, suitable for scenarios that require accessing data in buckets with file system semantics, such as training model data in AI machine learning scenarios.<br><br>* Supports TOS FNS buckets and HNS buckets. |
|Connect using S3 Connector |* S3 Connector is a PyTorch connector provided by AWS that enhances the S3\-related access capabilities offered by [torchdata](https://pytorch.org/data/0.8/). It supports map\-style datasets, iterable\-style datasets, and checkpointing interfaces. For details, see [S3-connector-for-pytorch](https://github.com/awslabs/s3-connector-for-pytorch).<br><br>* Currently, only TOS FNS buckets are supported. |
|Connect using tosutil |* Use the tosutil tool to mount BytePlus  TOS as a local path, then use torchdata to read and write directly to this local path for integration.<br><br>* Supports TOS FNS buckets and HNS buckets. |


<span id="746acf18"></span>
## Procedure

The steps for different integration methods are as follows.


<Tabs>
<Tab zoneid="cyyklkOQ8G" title="Connect using fsspec">
<TabTitle>Connect using fsspec</TabTitle>

Using tosfs, which implements the fsspec specification, wraps BytePlus  TOS as Python's standard read\-write interface, and then uses torchdata to read and write local paths directly for integration. For more information, see [tosfs](https://github.com/volcengine/tosfs).

<span id="h0qgjNKY"></span>
### Notes

Supports TOS FNS buckets and HNS buckets.

<span id="8r5INSGe"></span>
### Procedure


1. Run the following command to install tosfs.


```Bash
# Install tosfs for fsspec
pip install tosfs
```



2. Run the following command to initialize the client.


```Python
from tosfs.core import TosFileSystem

# Configure access keys and other info if __name__ == '__main__':
    tosfs = TosFileSystem(
        key='<Your AK>',
        secret='<Your  SK>',
        endpoint_url='http://tos-cn-beijing.bytepluses.com.cn',
        region='cn-beijing',
    )
```



3. Run the following code to use iterable\-style datasets.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This article uses a bucketname bucket in the Beijing region as an example; it is recommended to modify the code based on your business needs.</div>


```Python
from torchdata.datapipes.iter import FSSpecFileLister, FSSpecFileOpener

if __name__ == '__main__':
    kwargs = {
        'key' : '<Your  AK>',
        'secret' : '<Your  SK>',
        'endpoint_url' : 'https://tos-cn-beijing.bytepluses.com.cn',
        'region' :'cn-beijing'
    }
    
    bucket = 'bucketname'print('test iterable-style datasets')
    file_lister = FSSpecFileLister(root='tos://'+ bucket+'/shard-data/', **kwargs)
    iterable_dataset = FSSpecFileOpener(file_lister, mode='rb', **kwargs)
# iterate and read objects in Dataset. for _, item in iterable_dataset:
        print(item.bucket, item.key)
        data = item.read()
        print(len(data))
```



4. Run the following code to save or load a checkpoint.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This article uses a bucketname bucket in the Beijing region as an example; it is recommended to modify the code based on your business needs.</div>


```Python
import torch
import torchvision
from tosfs.core import TosFileSystem

if __name__ == '__main__':
    tosfs = TosFileSystem(
        key='<Your AK>',
        secret='<Your SK>',
        endpoint_url='http://tos-cn-beijing.bytepluses.com.cn',
        region='cn-beijing',
    )

    bucket = 'bucketname'print('test checkpointing')
    model = torchvision.models.resnet18()
    
# wrap tos as python standard read-write interface with tosfs.open(bucket + '/checkpoint/epoch1.ckpt', 'wb') as writer:
        torch.save(model.state_dict(), writer)
    
    with tosfs.open(bucket+'/checkpoint/epoch1.ckpt', 'rb') as reader:
        stat_dict = torch.load(reader)
    
    model.load_state_dict(stat_dict)
    print(model)
```





</Tab>
<Tab zoneid="M15gAfeGfe" title="Connect using FSX">
<TabTitle>Connect using FSX</TabTitle>

FSX is a client used to mount buckets. With this client, you can mount a TOS bucket to a Linux system, allowing the bucket to function as a local file system for data storage and management.

<span id="tWybLiwv"></span>
### Precautions


* FSX is currently in closed beta. For a trial, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001170).

* For details on supported environments and constraints, see [FSX overview](https://docs.byteplus.com/docs/tos/Overview).


<span id="Grm4xIKV"></span>
### Procedure

This article uses the veLinux environment as an example to explain FSX client installation and steps to mount the entire bucket. For more environment and parameter details, see the documents below:


* [Install FSX](https://docs.byteplus.com/en/docs/tos/Install-fsx)

* [FSX configuration and mounting](https://docs.byteplus.com/en/docs/tos/FSX-configuration-and-mounting)

* [FSX mounting parameter explanation](https://docs.byteplus.com/en/docs/tos/FSX-mount-parameter-description)

1. Install the FSX client.

   1. Depending on your operating system, please  [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001170) to contact the technical team for the latest installation package.

   2. Run this command to install the client.

      ```Bash
      dpkg -i fsx_amd64.deb
      ```
      

   3. Run this command to check the client version.

      ```Bash
      fsx -v
      ```
      

      The following version information indicates a successful installation.

      ```Bash
      Version: 1.1.0.400
      ```
      

2. Configure mount permissions.

   When IAM users mount buckets, ListBucket and HeadBucket permissions are required. Reading objects inside the mounted bucket requires GetObject permission, and writing files requires PutObject and AbortMultipartUpload permissions.

   Below is a minimal permission example. For more information, see [permission configuration](https://docs.byteplus.com/en/docs/tos/FSX-configuration-and-mounting#a6e1a909).

   ```Bash
   {
           "Statement": [{
                   "Effect": "Allow",
                   "Action": [
                           "tos:GetObject",
                           "tos:PutObject",
                           "tos:DeleteObject",
                           "tos:AbortMultipartUpload",
                           "tos:ListBucket",
                           "tos:HeadBucket"
                   ],
                   "Resource": [
                           "*"
                   ]
           }]
   }
   ```
   

3. Mount the TOS bucket.

   For mount parameter details, see [FSX configuration and mounts](https://docs.byteplus.com/en/docs/tos/FSX-configuration-and-mounting).

   1. Access the Linux operating system and run the following command to create the mount point.

      ```Bash
      mkdir /mnt/point
      ```
      

   2. Run the following command to mount the bucket.

      ```Bash
      mount -t fsx /tos/&lt;mounted_bucket_name&gt; &lt;mount_point&gt; -o region="&lt;region&gt;",endpoint="&lt;endpoint&gt;",access_key_id="AK",secret_access_key="SK",no_writeback_cache
      ```
      

      **Example:** 

      ```Bash
      mount -t fsx /tos/bucketname /mnt/point -o region="cn-beijing",endpoint="http://tos-cn-beijing.bytepluses.com.cn",access_key_id="AKAKAK****",secret_access_key="SKSKSK****",no_writeback_cache
      ```
      

   3. Run the following command to check the bucket mount status.

      ```Bash
      df -h
      ```
      

      If the returned content shows the mount point and bucket name, the mount is successful.

      ```Bash
      Filesystem                  Size   Used Avail Use% Mounted on
      BFA281845F:tos-fuse-test    8.0E      0  8.0E   0% /mnt/fuse_shm
      ```
      

4. Run the following code to build iterable\-style datasets.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This article uses shard\-data/ directory as an example; modify the code according to your business needs.   </div>
   

   ```Python
   from torchdata.datapipes.iter import FileLister, FileOpener
   
   if __name__ == '__main__':
       dataset_uri = './root/shard-data/'print('Test iterable-style datasets')
       file_lister = FileLister(root=dataset_uri)
       iterable_dataset = FileOpener(file_lister, mode='rb')
   # Iterate through and read objects in the dataset. for _, item in iterable_dataset:
           print(item.bucket, item.key)
           data = item.read()
           print(len(data))
   ```
   

5. Run the following code to save or load the checkpoint.

   This article uses checkpoint/ directory as an example; modify the code according to your business needs.

   ```Python
   import torch
   import torchvision
   
   if __name__ == '__main__':
       print('Test checkpointing')
       model = torchvision.models.resnet18()
       
   # Handle tos as a local file directly with open('./root/checkpoint/epoch0.ckpt', 'wb') as writer:
           torch.save(model.state_dict(), writer)
   
   
       with open('./root/checkpoint/epoch0.ckpt', 'rb') as reader:
           stat_dict = torch.load(reader)
   
       model.load_state_dict(stat_dict)
       print(model)
   ```
   





</Tab>
<Tab zoneid="j5tuCNMpQp" title="Connect using S3 Connector">
<TabTitle>Connect using S3 Connector</TabTitle>

The S3 Connector is an AWS\-provided PyTorch connector designed to enhance [torchdata](https://pytorch.org/data/0.8/)'s S3 access capabilities, supporting map\-style datasets, iterable\-style datasets, and checkpointing interfaces. For details, see [S3-connector-for-pytorch](https://github.com/awslabs/s3-connector-for-pytorch).

<span id="Kc6t0xZq"></span>
### Note

Currently, only TOS FNS buckets are supported.

<span id="nEEDGjq7"></span>
### Procedure


1. Install the S3 connector.

   1. Run the following command to install the S3 connector core library.

      ```JSON
      pip install s3torchconnector
      ```
      

   2. (Optional) Run the following command to install the S3 connector for lightning.

      ```JSON
      pip install s3torchconnector[lightning]
      ```
      

2. Configure the environment.

   1. Run the following command to edit the key configuration file.

      ```JSON
      vim ~/.aws/credentials
      ```
      

   2. Run the following command to configure access keys.

      ```JSON
      [default]
      aws_access_key_id = <Your AK>
      aws_secret_access_key = <Your SK>
      ```
      

   3. Run the following command to save the configuration.

      ```JSON
      :wq
      ```
      

3. Run the following code to use iterable\-style datasets.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This article uses the bucketname bucket in the Beijing region with the shard\-data/ directory as an example; it is recommended to modify the code according to your business needs.   </div>
   

   ```Python
   from s3torchconnector import S3IterableDataset, S3ClientConfig
   
   if __name__ == '__main__':
       dataset_uri = 's3://bucketname/shard-data/'
       region = 'cn-beijing'
       endpoint = 'http://tos-s3-cn-beijing.bytepluses.com.cn'
       s3_config = S3ClientConfig(force_path_style=False)
   
       print('Test iterable-style datasets')
       iterable_dataset = S3IterableDataset.from_prefix(dataset_uri,
                                                        region=region,
                                                        endpoint=endpoint,
                                                        s3client_config=s3_config)
   # Iterate and read objects in the Dataset. for item in iterable_dataset:
           print(item.bucket, item.key)
           data = item.read()
           print(len(data))
   ```
   

4. Run the following code to use map\-style datasets.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This article uses the bucketname bucket in the Beijing region with the shard\-data/ directory as an example; it is recommended to modify the code according to your business needs.   </div>
   

   ```Python
   from s3torchconnector import S3IterableDataset, S3ClientConfig
   
   if __name__ == '__main__':
       dataset_uri = 's3://bucketname/shard-data/'
       region = 'cn-beijing'
       endpoint = 'http://tos-s3-cn-beijing.bytepluses.com.cn'
       s3_config = S3ClientConfig(force_path_style=False)
       
       print('test map-style datasets')
       map_dataset = S3MapDataset.from_prefix(dataset_uri,
                                              region=region,
                                              endpoint=endpoint,
                                              s3client_config=s3_config)
   # Iterate and read objects from the Dataset. for item in map_dataset:
           print(item.bucket, item.key)
           data = item.read()
           print(len(data))
           
   # Read an object from the Dataset by index.
       item = map_dataset[0]
       bucket = item.bucket
       key = item.key
       print(bucket, key)
       data = item.read()
       print(len(data))
   ```
   

5. Run the following code to save or load a checkpoint.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This article uses the bucketname bucket in the Beijing region with the checkpoint/ directory as an example; it is recommended to modify the code according to your business needs.   </div>
   

   ```Python
   import torch
   import torchvision
   from s3torchconnector import S3Checkpoint, S3ClientConfig
   
   if __name__ == '__main__':
       checkpoint_uri = 's3://bucketname/checkpoint/'
       region = 'cn-beijing'
       endpoint = 'http://tos-s3-cn-beijing.bytepluses.com.cn'
       s3_config = S3ClientConfig(force_path_style=False)
   
       print('test checkpointing')
       checkpoint = S3Checkpoint(region=region,
                                 endpoint=endpoint,
                                 s3client_config=s3_config)
   
       model = torchvision.models.resnet18()
   
       with checkpoint.writer(checkpoint_uri + 'epoch0.ckpt') as writer:
           torch.save(model.state_dict(), writer)
   
       with checkpoint.reader(checkpoint_uri + 'epoch0.ckpt') as reader:
           state_dict = torch.load(reader)
   
       model.load_state_dict(state_dict)
   ```
   





</Tab>
<Tab zoneid="r0MqxigSI1" title="Connect using tosutil">
<TabTitle>Connect using tosutil</TabTitle>

Use the tosutil tool to mount BytePlus  TOS as a local path, then use torchdata to read and write the local path directly for integration. This article uses tosutil as the Fuse mounting tool, but you may choose other tools to mount the bucket depending on your situation.

<span id="fHmeNkJ4"></span>
### Procedure


1. Install the tosutil tool. For detailed steps, refer to [download and installation](https://docs.byteplus.com/en/docs/tos/Download-and-install).

2. Configure the tosutil tool and check its version and connectivity. For detailed steps, refer to [quick start](https://docs.byteplus.com/en/docs/tos/Quick-start).

3. Use the mount command to mount the bucket and verify the mount result. For detailed steps, refer to [mount bucket as local file system directory (mount)](https://docs.byteplus.com/en/docs/tos/The-mount-bucket-is-a-local-file-system-directory-mount).

   This article uses mounting the bucketname bucket to the ./root directory as an example.

   ```Python
   ./tosutil mount tos://bucketname ./root -aow -ar -ao
   ```
   

4. After mounting, run the following command to verify the mount result.

   ```Python
   ls ./root
   ```
   

5. Run the following code to build iterable\-style datasets.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This article uses shard\-data/ as an example; you are advised to modify the code according to your business needs.   </div>
   

   ```Python
   from torchdata.datapipes.iter import FileLister, FileOpener
   
   if __name__ == '__main__':
       dataset_uri = './root/shard-data/'print('test iterable-style datasets')
       file_lister = FileLister(root=dataset_uri)
       iterable_dataset = FileOpener(file_lister, mode='rb')
   # iterate and read objects in the Dataset. for _, item in iterable_dataset:
           print(item.bucket, item.key)
           data = item.read()
           print(len(data))
   ```
   

6. Run the following code to save or load a checkpoint.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This article uses checkpoint/ as an example; you are advised to modify the code according to your business needs.   </div>
   

   ```Python
   import torch
   import torchvision
   
   if __name__ == '__main__':
       print('test checkpointing')
       model = torchvision.models.resnet18()
       
   # Directly treat tos as a local file with open('./root/checkpoint/epoch0.ckpt', 'wb') as writer:
           torch.save(model.state_dict(), writer)
   
   
       with open('./root/checkpoint/epoch0.ckpt', 'rb') as reader:
           stat_dict = torch.load(reader)
   
       model.load_state_dict(stat_dict)
       print(model)
   ```
   





</Tab>
</Tabs>
