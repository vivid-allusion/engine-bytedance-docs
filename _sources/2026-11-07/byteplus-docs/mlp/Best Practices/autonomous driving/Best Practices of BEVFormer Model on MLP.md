---
title: "Best Practices of BEVFormer Model on MLP"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Best_Practices_of_BEVFormer_Model_on_MLP"
---

Machine Learning Platform is a set of services for professional algorithm engineers, integrating cloud\-native tools + computing power (GPU, CPU Cloud as a Service), for one\-stop AI algorithm development and iteration platform. This program will introduce you to how to use BEVFormer models for training in MLP.

<span id="使用前提"></span>
# Premise of use

This solution takes the BEVFormer model as an example. Before starting the operation, please confirm that you have completed the following preparations:


* The network/PFS has been activated. For details, please refer to [Change the load network of the Prepaid resource group VPC -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Change_the_load_network_VPC_of_a_prepaid_resource_group), [File Storage PFS](https://docs.byteplus.com/docs/mlp/File_Storage_PFS)[ ](https://www.volcengine.com/docs/6459/145549).

* Purchased MLP resources, see [Create Resource Group -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_a_resource_queue). For resource pricing details, see [Instance Specifications and Pricing -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing).

* Created Dev boxes instance with key parameters configured as follows. For details, see [Create Dev boxes -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_Dev_boxes).

   * Resource Specifications: Configure the following resource specifications.

      * CPU instance: 8C/64G/20GB cloud disk.

      * GPU card count: at least 8 cards, best practice is to use a ml.pni3l.

   * Mount Configuration: When you are a multi\-machine training task, the Mount PFS parallel file system is required. For more configuration information, please visit [File Storage PFS](https://docs.byteplus.com/docs/mlp/File_Storage_PFS)

   * Mirror address: Configure the mirror below in the custom mirror and fill in the SSH key. Creating Dev boxes for the first time is expected to take 20 minutes due to the large mirror being pulled.

      ```bash
        vemlp-cn-beijing.cr.volces.com/preset-images/bevformer:0.0.1
      ```
      


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BEVFormer code has been prefabricated in the mirror, the default directory is <code>/root/code/BEVFormer</code>, do not need to re\-download.</div>


<span id="步骤一：准备数据集"></span>
# Step 1: Prepare the dataset


1. Enter the Dev boxes.

   1. Login [Account Login - BytePlus ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/dashboard).

   2. Click Dev boxes in the left navigation bar, and click the name of the Dev boxes to be operated on the Dev boxes list page to enter the corresponding Dev boxes.

   3. Remote login Dev boxes through SSH, for details, see [Remote connection through SSH Dev boxes -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Remote_connection_to_Dev_boxes_via_SSH).

2. Configure volc configure. For details, please refer to [the usage documentation -- Machine Learning Platform - BytePlus](https://www.volcengine.com/docs/6459/72394)[ ](https://www.volcengine.com/docs/6459/72394).

3. The nuScenes V1.0 mini dataset is already prefabricated in the mirror in the `/root/code/BEVFormer/data`directory, you can use it directly for subsequent training and skip the steps later in this chapter.

4. If you want to use the V1.0 full dataset for training, you can follow the steps below to download and configure the corresponding dataset.


```bash
wget https://d36yt3mvayqw5m.cloudfront.net/public/v1.0/v1.0-trainval_meta.tgz 
wget https://motional-nuscenes.s3.amazonaws.com/public/v1.0/v1.0-trainval01_blobs.tgz
#If you need to continue downloading the remaining 9 parts, you can continue to execute the following command
# for part_num in {2..10}; do
#   if [ $part_num -lt 10 ]; then
#     wget https://motional-nuscenes.s3.amazonaws.com/public/v1.0/v1.0-trainval0${part_num}_blobs.tgz
#   else
#     wget https://motional-nuscenes.s3.amazonaws.com/public/v1.0/v1.0-trainval${part_num}_blobs.tgz
#   fi
# done


tar -xzvf v1.0-trainval_meta.tgz -C /root/code/BEVFormer/data
tar -xzvf v1.0-trainval01_blobs.tgz -C /root/code/BEVFormer/data
#Continue to unpack the remaining 9 parts
# for part_num in {2..10}; do
#   if [ $part_num -lt 10 ]; then
#     tar -xzvf v1.0-trainval0${part_num}_blobs.tgz -C /root/code/test
#   else
#     tar -xzvf v1.0-trainval${part_num}_blobs.tgz -C /root/code/test
#   fi
# done

cd /root/code/BEVFormer/
#Data preprocessing
python tools/create_data.py nuscenes --root-path ./data/nuscenes --out-dir ./data/nuscenes --extra-tag nuscenes --version v1.0 --canbus ./data
```


<span id="步骤二：模型训练"></span>
# Step 2: Model training

<span id="_2-1-在开发机中进行训练调试"></span>
## 2.1 **Training and debugging in Dev boxes**

If you are using GPU Dev boxes, you can directly enter the Dev boxes for training. The Start training command is as follows. The last parameter of the command is the number of GPU cards used.

```bash
cd /root/code/BEVFormer && sh ./tools/train.sh ./projects/configs/bevformer/bevformer_base.py 8
```


<span id="_2-2-自定义任务分布式训练（指令微调）"></span>
## 2.2 Distributed training for custom tasks (instruction fine\-tuning)

The best practices document provides instructions for both the console and the command line.

<span id="方式一：控制台"></span>
### Method 1: Console


1. Enter custom tasks [console](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/customTask/create)

2. configuration environment

   1. Configure mirrors at Custom mirrors.

   ```bash
   vemlp-cn-beijing.cr.volces.com/preset-images/bevformer:0.0.1
   ```
   

   2. Fill in the entry commands and define environment variables. Please note that the path of the PFS mount on the development machine is inconsistent with the path of the mount in custom tasks. When filling in the model path in the entry command to fill in the dataset path environment variables, you need to ensure that it is the path of the mount in custom tasks.

   ```bash
   cd /root/code/BEVFormer && export PYTHONPATH=/root/code/BEVFormer &&  ./tools/dist_train.sh ./projects/configs/bevformer/bevformer_base.py
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae9896f283f64f64bcfb5d5e9d42314e~tplv-goo7wpa0wc-image.image) </span>

3. Allocate resources

   1. Select the appropriate resources, and the best practice is to use a stand\-alone 8\-card ml.pni3l.

   2. Mount PFS. Note: If it is a multi\-machine training task, you need to configure shared storage to the `/root/code/BEVFormer/work_dirs`directory.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Here, the shared storage access path of Mount PFS is the storage path of the trained model. You can modify the path yourself and modify it synchronously in the model code.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0f23218daee46698677a10d5dea30c4~tplv-goo7wpa0wc-image.image) </span>

<span id="方式二：命令行"></span>
### Method 2: Command Line

In the Terminal, use the following command to train BEVFormer. The specific operation steps are as follows.


1. Create a **demo\-bevformer\-train .yaml** file.

2. Edit the YAML file and fill in the mirror, resource specifications, environment variables, and entry commands.

3. Run the task command. If the operation is successful, the words " **Create task was successful, task_id** " will appear in the Terminal. The full training time using the nuScenes v1.0 mini dataset is expected to be around 30 minutes.

4. You can also further customize hyperparameters such as learning rate and number of training steps (epochs). The relevant configuration is in the `projects/configs/bevformer/bevformer_base.py`directory.


```bash
volc ml_task submit --conf=demo-bevformer-train.yaml
```


**demo\-bevformer\-train .yaml** file example:

```bash
TaskName:  "BEVformer-demo-train"
Description:  ""
Tags: []

ImageUrl:  "vemlp-cn-beijing.cr.volces.com/preset-images/bevformer:0.0.1"
ResourceQueueID:  "q-**************" #Please replace with your own queue ID
# DL framework, support: TensorFlow PS,PyTorch DDP,Horovod,BytePS
Framework:  "PyTorchDDP"
#Flavor represents the model, go to https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing
TaskRoleSpecs:
        - RoleName:  "worker"
            RoleReplicas: 1                                                   
            Flavor:  "custom"
            ResourceSpec:
                    Family:  "ml.pni3l"
                    CPU: 165.000
                    Memory: 1765.000
                    GPUNum: 8

AccessType:  "Queue"
Storages:
        - Type:  "Vepfs"                     
            MountPath:  "/root/code/BEVFormer/work_dirs" The path can be modified
            ReadOnly:  "False"
            VepfsHostPath:  "/mnt/vepfs-**************" #Please replace with your own file system ID
            VepfsId:  "vepfs-**************" #Please replace with your own file system ID
            VepfsName:  "demo-huabei2" Please replace it with your own file system name
Entrypoint: |
  cd  /root/code/BEVFormer &&  export  PYTHONPATH=/root/code/BEVFormer &&  ./tools/dist_train.sh ./projects/configs/bevformer/bevformer_base.py
```



5. After training is complete, you can view the training log information in the task log.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b845c817acd24f31bd8c38eef05861a0~tplv-goo7wpa0wc-image.image) </span>
