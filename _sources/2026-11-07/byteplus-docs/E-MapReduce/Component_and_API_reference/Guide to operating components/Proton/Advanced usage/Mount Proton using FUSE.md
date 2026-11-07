---
title: "Mount Proton using FUSE"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Mount_Proton_using_FUSE"
---

You can use Hadoop's built\-in fuse_dfs to mount Proton files to the local file system, allowing you to operate files on Proton as if they were on the local file system.

<span id="30a3f8fc"></span>
## Mount


1. Install fuse


```Shell
apt-get install fuse
```



2. Create a mount point


```Shell
mkdir -p /mnt/proton_mount
```



3. Mount


```Shell
export OS_ARCH=amd64
export LD_LIBRARY_PATH=${JAVA_HOME}/jre/lib/${OS_ARCH}/server:${HADOOP_HOME}/lib/native
export CLASSPATH=$CLASSPATH:`${HADOOP_HOME}/bin/hadoop classpath --glob`
export LIBHDFS_OPTS="-Xmx1024m"
export PROTON_ENABLE_FUSE=true

# 在这里修改 bucket
export BUCKET_NAME=<your bucket name>

${HADOOP_HOME}/bin/fuse_dfs -ordbuffer=1024 -oattribute_timeout=0 tos://${BUCKET_NAME}/ /mnt/proton_mount
```


<span id="d6b27537"></span>
## Unmount

```Shell
fusermount -u /mnt/proton_mount
# 必须删掉该目录，保证下次能正常挂载
rm -rf /mnt/proton_mount
```


<span id="8b90e575"></span>
## Feature support


|**Feature** |**Note** |**Supported** |
|---|---|---|
|getattr() |Query file attributes |Supported |
|mkdir() |Create directory |Supported |
|rmdir() |Delete directory |Supported |
|unlink() |Delete file |Supported |
|rename() |Rename file |Supported |
|read() |Sequential read |Supported |
|pread() |Random read |Supported |
|write() |Sequential write |Supported |
|pwrite() |Random write |Not supported |
|flush() |Flush memory to kernel buffer |Supported |
|fsync() |Flush memory to disk |Not supported |
|release() |Close file |Supported |
|readdir() |Read directory |Supported |
|create() |Create file |Supported |
|open() O_APPEND |Open file in append mode |Not supported |
|open() O_TRUNC |Open file in overwrite mode |Supported |
|ftruncate() |Truncate an open file |Not supported |
|truncate() |Truncate a closed file |Supported |
|lseek() |Specify the read/write position in an open file |Not supported |
|chmod() |Modify file permissions |Supported |
|access() |Query file permissions |Supported |
|utimes() |Modify file access and modification times |Not supported |
|setxattr() |Modify file xattr attributes |Not supported |
|getxattr() |Get file xattr attributes |Not supported |
|listxattr() |List file xattr attributes |Not supported |
|removexattr() |Remove file xattr attributes |Not supported |
|lock() |Support POSIX locks |Not supported |
|fallocate() |Pre\-allocate physical space for a file |Not supported |
|symlink() |Create symbolic link |Not supported |
|readlink() |Read symbolic link |Not supported |


<span id="bdc87d8a"></span>
## Performance \- non\-cached mode

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before performing operations, you must install fio. Installation command: <code>apt-get install fio</code>.</div>


<span id="6de98177"></span>
### Write

Test command

```Shell
fio -filename=/mnt/proton_mount/fio.txt --ioengine=posixaio --name=write_iops --directory=`pwd` --size=30G \
--time_based --runtime=20s --ramp_time=2s  --direct=0 \
--verify=0 --bs=4K --iodepth=256 --rw=write --group_reporting=1 \
--iodepth_batch_submit=256  --iodepth_batch_complete_max=256
```


Test result


|bs=4K |write: IOPS=45.3k, BW=177MiB/s |
|---|---|
|bs=16K |write: IOPS=25.6k, BW=400MiB/s |
|bs=64k |write: IOPS=9491, BW=594MiB/s |
|bs=1M |write: IOPS=654, BW=667MiB/s |


<span id="54a8802a"></span>
### Sequential read

Test command

```Shell
fio -filename=/mnt/proton_mount/fio.txt --ioengine=posixaio --name=read_iops --directory=`pwd` --size=30G \
--time_based --runtime=20s --ramp_time=2s  --direct=0 \
--verify=0 --bs=4K --iodepth=256 --rw=read --group_reporting=1 \
--iodepth_batch_submit=256  --iodepth_batch_complete_max=256
```


Test result


|bs=4K |read: IOPS=18.8k, BW=73.6MiB/s |
|---|---|
|bs=16K |read: IOPS=4685, BW=73.4MiB/ |
|bs=64k |read: IOPS=1168, BW=73.8MiB/s |
|bs=1M |read: IOPS=73, BW=85.4MiB/s |


<span id="2f51eab2"></span>
### Random read

Test command

```Shell
fio -filename=/mnt/proton_mount/fio.txt --ioengine=posixaio --name=rand_read_iops --directory=`pwd` --size=30G \
--time_based --runtime=20s --ramp_time=2s  --direct=0 \
--verify=0 --bs=4K --iodepth=256 --rw=randread --group_reporting=1 \
--iodepth_batch_submit=256  --iodepth_batch_complete_max=256
```


Test result


|bs=4K |read: IOPS=136, BW=595KiB/s |
|---|---|
|bs=16K |read: IOPS=117, BW=2067KiB/s |
|bs=64k |read: IOPS=113, BW=8064KiB/s |
|bs=1M |read: IOPS=18, BW=27.8MiB/s |
