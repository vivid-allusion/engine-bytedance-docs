---
title: "Common concepts"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/76491"
---

<span id="主账号"></span>
# Main account

The main account is an account registered through the [Byteplus official website ](https://www.byteplus.com/en). The account has access rights to all services under Byteplus and can create sub\-accounts under the account and assign specific permissions. At the same time, the main account is the billing subject of the user on Byteplus. All sub\-accounts under the main account also belong to the main account.

<span id="子账号（子用户）"></span>
# Sub\-account (sub\-user)

The account created by the main account in the Byteplus [Access control (IAM) ] system does not have any access rights to Byteplus services by default when the account is created. After the main account assigns a specific permission policy, ordinary users log in and use the machine learning platform and other services of Byteplus through the sub\-account password assigned by the main account.

<span id="ak-sk"></span>
# AK / SK

The AccessKey ID (AK) and AccessKey Secret (SK) are your keys to access the Byteplus API, have all the permissions of the account, and can only create a maximum of two keys. Please keep and change the key regularly to ensure account Security. The relevant management entry is in [Key Management ](https://console.byteplus.com/iam/keymanage/). For specific actions, please refer to [Key Management - Help Documentation ](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). Users accessing private TOS data using need to configure AK/SK in advance for authentication.

<span id="iam"></span>
# IAM

[Access control (Identity Access Management, IAM) ](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3)is a set of rights management system provided by Byteplus for customers. In this system, users can create several identities under the account and grant specific permissions to achieve on\-demand allocation management of permissions. In some enterprise scenarios, the enterprise assigns access to different resources to different IAM users for each employee to use, allowing team members to perform their duties and collaborate on a project, while also reducing Security risks. Common permission configurations on machine learning platforms can be found in [Rights management](https://docs.byteplus.com/docs/mlp/rights_management).

<span id="tos"></span>
# TOS

[Object Storage (Tinder Object Storage, TOS) ](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos)is a massive, secure, low\-cost, easy\-to\-use, highly reliable and highly available distributed cloud storage service provided by Byteplus. Users can use Byteplus TOS through its RESTful API interface, SDK, and other forms. Through the network, you can manage and access data on Byteplus TOS from any application, anytime, anywhere. TOS is one of the cloud services that machine learning platforms rely on. The data and models registered by users on the machine learning platform are actually stored on TOS. For common data upload methods, please refer to [Upload data to TOS](https://docs.byteplus.com/docs/mlp/Upload_data_to_TOS)[ ](https://docs.byteplus.com/en/docs/186/73643).

<span id="vpc"></span>
# VPC

[Private Network (VPC, Virtual Private Cloud) ](https://docs.byteplus.com/en/docs/vpc/What-is-VPC)Build an isolated, self\-configured and managed virtual network environment for resources on the cloud. You can customize Internet Protocol Address segments, Security groups, routing policies and other network characteristics in the private network, and easily manage and configure the network on the cloud. Security quickly makes network changes. In the machine learning platform, you need to complete the global VPC configuration before you can use the private network log in of the developer computer, mount NAS/vePFS shared file system and other functions.

<span id="nas"></span>
# NAS

Byteplus NAS (Network Attached Storage) is a shared access, scalable, highly reliable and high\-performance distributed file system based on POSIX file interface, which is widely used in large\-scale data sharing, big data analytics, machine learning and other scenarios. Users of machine learning platforms mount NAS onto developer computers, custom training tasks, or online services for efficient and convenient data access.

<span id="vepfs"></span>
# vePFS

[vePFS ](https://docs.byteplus.com/en/docs/pfs/What-is-PFS)(Volc Engine Paralleled File System) is a high\-performance and scalable parallel file system, which is widely used in machine learning, genetic computing, autonomous driving and other application scenarios that require ultra\-high throughput. Like NAS and TOS, users who want to access large amounts of training data during training can mount vePFS as a data disk in the training container.


* Fileset: a small dataset of vePFS, with independent inode space and management capabilities. You can use Fileset as the smallest unit, set the corresponding permission policy and Quota, QoS configuration, and count the usage information of Fileset.


<span id="cr"></span>
# CR

[Image Repository (Container Registry, CR) ](https://docs.byteplus.com/en/docs/cr/what-is-cr)is a high\-availability container image, Helm Chart and other OCI\-compliant cloud\-native product hosting services provided by Byteplus, which is convenient for users to manage the full lifecycle of OCI\-compliant cloud\-native products. CR is one of the Cloud Services that machine learning platforms rely on. The pre\-set images of the machine learning platform and the custom images registered by users are actually stored on CR.

<span id="vmp"></span>
# VMP

[The Volcengine Managed Service for Prometheus (VMP) ](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus)is a Monitoring Product that fully inherits and connects to the open source Prometheus ecosystem and is hosted on the Byteplus cloud. The machine learning platform supports pushing the user's Monitoring data to the user's VMP for free use.

<span id="region"></span>
# Region

Region refers to the different geographical regions where the physical data center is located, and the internal network between different regions is completely isolated to ensure maximum stability and fault tolerance between different regions. At present, the machine learning platform supports North China 2 (Beijing), East China 2 (Shanghai) and other regions.

<span id="az"></span>
# AZ

Availability Zone (AZ) refers to a physical area where power and network are independent of each other within the same region.


* In the same region, within the same private network, different availability zones can communicate with each other.

* Fault isolation between Availability Zones means that a failure in one Availability Zone will not affect the normal use of other Availability Zones, ensuring that your business remains online.


<span id="tensor-配置"></span>
# Tensor configuration

Tensor configuration refers to the name, accuracy, and size of the input and output Tensor of a model on a machine learning platform, with the help of these information platforms to correctly deploy the model, complete performance evaluation, and model transformation.

<span id="tensorboard"></span>
# TensorBoard

TensorBoard is a tool for visualizing machine learning experiments. When the user creates the training task, turn on the TensorBoard function and write the corresponding log file to the specified path (environment variables `TENSORBOARD_LOG_PATH`path) in the code, the machine learning platform can track and visualize the loss, accuracy, network structure, weight changes and other training information for the user.

<span id="tensorflowps"></span>
# TensorFlowPS

TensorFlow Parameter Server is one of the most common distributed training paradigms. Support for parameter server (PS) training on multiple machines. In each round of training, the parameter server (ps) distributes the latest model parameters to the worker process (worker). After the worker completes the calculation, the layer is returned to ps. After ps updates the parameters, it enters the next round of training until the training is completed. For the method of initiating TensorFlowPS distributed training on the machine learning platform, please refer to [Initiate TensorFlowPS distributed training](https://docs.byteplus.com/docs/mlp/Initiate_TensorFlowPS_distributed_training).

<span id="pytorchddp"></span>
# PyTorchDDP

PyTorch DistributedDataParallel (DDP) is one of the most common distributed training paradigms. DDP creates multiple processes for model training and assigns different training data to each model copy. Process communication is done through ring\-all\-reduce method to complete layer exchange and parameter update. For the method of initiating DDP distributed training on the machine learning platform, see [Initiate PyTorchDDP distributed training](https://docs.byteplus.com/docs/mlp/Initiate_PyTorchDDP_distributed_training).

<span id="mpi"></span>
# MPI

MPI is a parallel programming technique based on information transfer and is a set of standards for multi\-node data communication. The machine learning platform supports users to initiate distributed training tasks of MPI on the platform, and also supports users to initiate tasks through training frameworks based on MPI encapsulation such as Horovod and DeepSpeed. For details, see [Initiate MPI distributed training](https://docs.byteplus.com/docs/mlp/Initiate_MPI_distributed_training).


* Horovod: Horovod is a distributed training framework that encapsulates the underlying communication libraries (MPI, NCCL, Gloo, etc.) to support TensorFlow, PyTorch, MXNet, and other deep learning frameworks. Its distributed training performance is high and there are few changes to the training code.

* DeepSpeed: Similar to Horovod, DeepSpeed is also dedicated to large\-scale distributed training scenarios, supporting the training of very large models, with high memory usage efficiency, long sequence length (used in attention mechanisms), and other characteristics.


<span id="byteps"></span>
# BytePS

BytePS is a distributed training framework developed by ByteDance and is currently open\-sourced on [GitHub ](https://github.com/bytedance/byteps). Like Horovod, it also supports deep learning frameworks such as TensorFlow, PyTorch, and MXNet. The performance of BytePS for communication\-intensive tasks significantly exceeds that of Horovod and PyTorch DDP under the same conditions. The current implementation scenarios include large\-scale training such as BERT and GAN. For the method of initiating BytePS distributed training on the machine learning platform, please refer to [Initiate BytePS distributed training](https://docs.byteplus.com/docs/mlp/Initiate_BytePS_distributed_training).

<span id="nccl"></span>
# NCCL

[NCCL (The NVIDIA Collective Communications Library) ](https://docs.nvidia.com/deeplearning/nccl/user-guide/docs/overview.html)is a collection communication library released by NVIDIA, which supports communication primitives such as AllReduce, Broadcast, Reduce, AllGather, ReduceScatter, etc. The underlying communication of the commonly used Horovod distributed training framework is also based on NCCL.

<span id="预付费"></span>
# Prepaid

A payment model. The user determines the required amount of resources in advance and pays for it in the form of **Subscription** , and can use it arbitrarily before the Purchase duration expires. For example, if you buy a **prepaid resource group** containing 8Core + 32GiB + 1 Tesla\-V100 GPU on the machine learning platform, the Purchase duration is 12 months, and the user performs tasks in the queue under the resource group within these 12 months. No longer charge for this part of the resource.

<span id="后付费"></span>
# Postpaid

A payment model. The user can not determine the length of use of the resource in advance, then you can use the first payment, the amount of payment is determined by the length of use and the corresponding resource unit price. For example, a training task containing 8Core + 32GiB + 1 Tesla\-V100 GPU was executed in the queue under the **Postpaid resource group** on the machine learning platform, and the running time of the task was 1 hour. The final total cost was the unit price of this part of the resource x 1 hour.
