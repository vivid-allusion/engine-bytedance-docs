---
title: "What is Lake AI Service"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/What_is_AI_data_lake_service"
---

## Product overview

LAS (Lake AI Service) is a new\-generation multimodal data lake service, incubated in ByteDance's large model training scenarios. It helps customers quickly build multimodal data lakes, providing unified management of multimodal metadata, AI operator processing, enterprise\-level permission control, and seamless integration with ModelArk. It supports a wide range of AI scenarios such as machine learning, model training, and model fine\-tuning, breaking down data silos and fully unlocking the value of data.

## Product features

* Data ingestion into the lake

   * Supports unified ingestion of various types of multimodal data (images, text, audio, video, and more) and data from multiple engines into the lake.

* Lake storage optimization

   * Supports multiple data lake formats and automatically performs small file merging, fragment cleanup, and expired file removal.

* Unified metadata

   * Provides unified management of structured, semi\-structured, and unstructured metadata in the data lake, as well as unified permission management.

* Dataset management

   * Offers dataset management capabilities, including data querying, data editing, version management, and data export.

* Data processing

   * Provides workflow orchestration capabilities for built\-in unstructured data processing operators, accelerating the data cleansing process.

* Integration with the AI ecosystem

   * Datasets can be directly retrieved in BytePlus's vector database or used for training in ModelArk and machine learning platforms.

## Product advantages

* Data infrastructure designed specifically for AI

   * Compatible with mainstream AI frameworks such as PyTorch and TensorFlow.

   * Datasets seamlessly integrate with multiple AI training platforms of BytePlus.

   * Dataset management and processing designed for AI scenarios.

* Rapid construction of multimodal data lakes

   * Supports unified storage of multimodal data.

   * Supports storing and retrieving vectors in lake files.

   * Specially optimized lake formats for faster file read and write speeds.

* One\-stop inference\-data collection, processing, and training

   * Supports seamless collection of inference data from ModelArk and machine learning platforms into LAS.

   * Provides one\-stop dataset querying, analysis, and cleansing.

   * Datasets can be retrained on ModelArk and machine learning platforms.

## Product architecture

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6759390b3504d239a1689a552f1e958~tplv-goo7wpa0wc-topic.webp)

## Application scenarios

### Multimodal data lake

Enterprises' structured and unstructured data are unified into the lake and managed together, breaking down data silos, reducing data movement, lowering data usage costs, and improving data utilization efficiency.

#### Architecture diagram

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f05eca80223747fdb659b8c38e30efd9~tplv-goo7wpa0wc-topic.webp)

#### Architecture advantages

* Unified storage for multimodal data

   Supports unified lake format storage for tables and files

* Open lake format

   The lake format is open and supports conversion with Parquet and WebDataset

* Friendly to AI and big data ecosystems

   Compatible with mainstream engines such as PyTorch, TensorFlow, Ray, and Spark

#### Recommended related products

* Object storage

* EMR Severless

### AI data management

Helps AI teams manage datasets, accelerate the data cleaning process, improve data preprocessing efficiency, speed up model training, reduce workforce requirements, and achieve cost reduction and efficiency improvement.

#### Architecture diagram

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/290776b4-c014-46d7-ac10-f98f781380b6.svg)

#### Architecture advantages

* Convenient data management

   Provides dataset creation, query and analysis, multi\-version management, and other management functions

* Provides efficient data cleaning tools

   Offers workflows with built\-in open\-source operators to accelerate data cleaning

* Quick integration with training platforms

   Supports one\-click registration of cleaned data to the BytePlus training platform

#### Recommended related products

* BytePlus ModelArk

* Machine learning platform

* VikingDB

* Object storage

### AI model distillation

Helps enterprises build a closed loop of inference\-data collection, algorithm training, and human feedback, enabling efficient model distillation and accelerating model performance improvement.

#### Architecture diagram

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/da4c7162-1d2e-48da-9baa-711b49569f36.svg)

#### Architecture advantages

* Collect inference data with one click

   Collect inference data from BytePlus ModelArk into LAS

* Query and analyze feedback data

   Query and analyze collected feedback data on LAS

* Select usable data and initiate fine\-tuning for the model

   Mine training sets from feedback data, then perform fine\-tuning on the BytePlus ModelArk platform

#### Recommended related products

* [BytePlus ModelArk](https://www.byteplus.com/en/product/modelark)

* [Object Storage](https://www.byteplus.com/en/product/tos)
