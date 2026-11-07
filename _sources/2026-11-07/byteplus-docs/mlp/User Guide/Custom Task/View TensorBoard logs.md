---
title: "View TensorBoard logs"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/View_TensorBoard_logs"
---

You can create TensorBoard services for custom training tasks, and view model training results analysis reports more intuitively through TensorBoard's visual interface. This article shows you how to create a Tensorboard service.

<span id="操作步骤"></span>
# Procedure

<span id="控制台"></span>
## console


1. Log into the BytePlus console and open the Machine Learning Platform \- custom tasks page.

2. Click [Create Task] to enter the training task creation page.

   1. In the [Experiment Recording and Visualization Tools] module, open the TensorBoard service

   2. Specify the storage location of TensorBoard Logs. The platform currently supports both NAS and vePFS storage types. The platform will automatically


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b43d20ecf5541b49dd3975ed8a3673e~tplv-goo7wpa0wc-image.image) </span>


3. Click Submit Task.


<span id="volc-命令行"></span>
## Volc command line

If you need to create custom tasks from the command line, you can open them in the configuration file and specify the storage location of TensorBoard Logs.

```yaml
# Whether to enable TensorBoard
EnableTensorBoard: true
# Fill in after enabling TensorBoard. Write the logs to NAS or PFS, and whitelist access must be granted.
TensorBoardStorage:
    Type: "Nas/PFS"                     # Required. The type of the storage instance where TensorBoard logs are written. Can be filled with Nas or PFS.
    NasId: "replace with your NAS Id"     # NAS instance ID. Fill in when Type is Nas. At least one of NasId and NasAddr should be filled.
    NasAddr: "replace with your NAS Addr" # NAS instance mount point address. Fill in when Type is Nas. At least one of NasId and NasAddr should be filled.
    VepfsId: "replace with your VepfsId"  # When type is PFS: If two PFS instances are mounted on the platform, the corresponding PFS instance ID needs to be specified; if there is only one instance, it can be left empty.
    SubPath: "replace with NAS sub path"  # Required. The sub - directory of the storage instance where TensorBoard logs are written. When Type is PFS, you need to have the mount permission for this sub - directory. 
```


<span id="查看-tensorboard-服务日志"></span>
# View the TensorBoard service log


1. After the task runs successfully, you can select the task and click [Compare TensorBoard]. The platform will create a TensorBoard service for you and automatically mount the storage of TensorBoard Logs onto the service.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c519a70ca3ac49df9b9f71b319a51490~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2263657120880605dc10d7efbae70dc7.png) </span>

&nbsp;
