---
title: "Image management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Image_management"
---

The AI Data Lake Service LAS product provides official built\-in images based on different frameworks and versions, and also supports flexible custom image functionality, such as the ability to build images on the platform using development machines. You can directly select the appropriate image when using a development machine or submitting a task, enabling rapid construction of AI development environments or data processing tasks.

# Background information

LAS internal image management is built on the BytePlus Container Registry. Container Registry (CR) is a secure and highly available cloud\-native artifact hosting service provided by BytePlus, supporting container images, Helm Charts, and other OCI\-compliant artifacts. It enables users to manage the full lifecycle of OCI\-compliant cloud\-native artifacts. Both LAS official built\-in images and user custom images are actually stored in the Container Registry.

# Prerequisites

1. There must be at least one CR Standard Edition instance under the current account.

   > **说明**

   > If no standard edition instance has been created under the account, you may need to contact a user with the required permissions, such as the `CRFullAccess` IAM policy, to go to the CR console page and create a standard edition instance.

2. The image list provided by the LAS service, due to network restrictions, is by default only accessible on BytePlus ECS machines, including Pod services or other services deployed on ECS machines.

3. Custom images only support selecting the Standard Edition Container Registry when being created.

# Built\-in images

|Image name/ID |Image description |Framework |Instance type |Image size |Image repository address |
|---|---|---|---|---|---|
|ve\-daft |ve\-Daft is a customized version of Daft launched by the BytePlus LAS team. It includes Daft, as well as dependencies and runtime environments related to multimodal operators, such as CUDA, Conda, Ray, and more. |Daft |CPU、GPU |11.87 GB |las\-ai\-bp\-online\-ap\-southeast\-1.cr.bytepluses.com/las/ve\-daft:0.7.2.post4\-cu12.9.1\-py3.11\-ubuntu24.04 |
|ray |Ray is a customized Ray Runtime launched by the BytePlus EMR team. It includes the Ray image and its required dependencies, with built\-in Conda, Java 8, and Hadoop services. |RAY |CPU、GPU |7.12 GB |las\-ai\-bp\-online\-ap\-southeast\-1.cr.bytepluses.com/las/ray:2.56.0.0\-cu13.0.0\-py3.12\-ubuntu24.04\-1040 |
|ray\-ml ||RAY |CPU、GPU |7.12 GB |las\-ai\-bp\-online\-ap\-southeast\-1.cr.bytepluses.com/las/ray\-ml:2.56.0.0\-cu13.0.0\-py3.12\-ubuntu24.04\-1040 |
|spark |Spark is a customized version of Spark launched by the BytePlus EMR team. It includes the Spark image and its required dependencies, with built\-in Java 8, Hadoop, and other services. |SPARK |CPU、GPU |1.56 GB |las\-ai\-bp\-online\-ap\-southeast\-1.cr.bytepluses.com/las/spark:3.5.1\-py3.12\-ubuntu20.04\-358\-1 |
|las\-opensource\-lib |This is an open\-source pre\-integrated image designed for data processing and machine learning tasks. It provides a ready\-to\-use toolchain (including Python 3.10, CUDA 12.6, and Ubuntu 22.04), covering scenarios such as data cleaning for basic model pre\-training, audio feature engineering, NLP/CV model fine\-tuning and deployment, with optimized CUDA acceleration and distributed computing performance. |— |CPU、GPU |9.27 GB |las\-ai\-bp\-online\-ap\-southeast\-1.cr.bytepluses.com/las\-ai/las\-opensource\-lib:0.2.1\-py3.10\-12.6.1\-cudnn\-devel\-ubuntu22.04\-18 |

# Custom images

LAS image management provides flexible custom image functionality, supporting the creation of new images on the platform using development machines to meet data processing needs, improve production efficiency, and enhance operational convenience.

## Create custom images

1. Log in to **the LAS console**, select the target region and project, then sequentially select Resource management \> Image management. After entering the image management page, click Create custom image on the custom images tab to enter the custom image creation page.

2. Configure custom image parameters on the custom image creation page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/261e80a0ab9b4dee9e376f903b4e3f36~tplv-goo7wpa0wc-topic.webp)

   1. Configure basic information.

      |Configuration item |Description |
      |---|---|
      |Namespace |Select the namespace within the standard edition instance. A namespace is a collection that manages multiple OCI artifact repositories with related attributes. The name of the namespace is typically the name of an internal organizational team, a product project, or a custom name defined by an individual. |
      |Image name |Enter the image name. For the namespace, create a corresponding OCI artifact repository to store container images and OCI (Open Container Initiative) artifacts that comply with open container standards. |
      |Version |Enter the image version. This is the suffix of the image address, used to distinguish images with the same base image but different build layers. |
      |Description |Enter an appropriate description for the image. |

   2. Configure build settings.

      |Configuration item |Note |
      |---|---|
      |Build method & development machine |* Currently, custom images can be built based on development machines.<br><br>* Select the development machine that needs to be built as an image. |
      |exclusion list |Set the development machine directories that do not need to be included in the image build. |

3. After completing the configuration, click 'Create' at the bottom to start creating the custom image.

## View image details and logs

You can view all custom images you have created on the custom image page. Click "View details" on the corresponding custom image card to view the details of the image in the sidebar that appears.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d28167c0bdf24699928a23a93ebbf8fa~tplv-goo7wpa0wc-topic.webp)

* You can view the version history, status of each version, image size, source, and more for the corresponding image.

* You can click "View logs" to view detailed log information about the creation of the custom image.

## Add a custom image version

To add a custom image version, click "Add version" in the custom image details sidebar and configure the custom image parameters on the new version page.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec2e8d2bb76b4e9c9773ad8b94efa596~tplv-goo7wpa0wc-topic.webp)

## Use a custom image

After a custom image is created, you can use it to create a development machine or task.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d140c0c1a784217b1dd5cd729a2b966~tplv-goo7wpa0wc-topic.webp)
