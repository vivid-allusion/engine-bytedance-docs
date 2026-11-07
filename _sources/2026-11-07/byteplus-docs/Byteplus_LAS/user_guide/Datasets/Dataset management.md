---
title: "Dataset management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Dataset_management"
---

# Dataset feature description

## Feature overview

A dataset is a collection of data organized according to a specific structure and format, and can be used for analysis, research, training, and testing. AI datasets can be used to organize and visualize text or multimodal data samples, as well as for batch cleaning, data annotation, and exploration. Before model training, evaluation, and AI data workflows, you need to create specific datasets based on the business type. You can create Common dataset and Inference dataset.

* Common dataset: Multimodal data collections designed for AI developers, providing data support for scenarios such as model training, evaluation, or research.

## Core advantages

* **Wide scenario coverage**: End\-to\-end data processing and training pipeline. Data from each node and in various formats can be organized and managed as datasets. Supports both unimodal datasets and construction of multimodal datasets.

* **High usage efficiency**: Datasets and data processing modules are seamlessly integrated, enabling online visualization and exploration of data at each stage of processing. For Lance format datasets, provides efficient online capabilities for adding, deleting, updating, querying, and SQL queries. In annotation scenarios, manual verification is more efficient.

* **Superior multimodal storage performance**: Lance format datasets support mixed storage of multimodal data. row_id row\-level indexing and scalar, vector, and full\-text secondary indexing mechanisms support efficient random access and hybrid retrieval. Supports zero\-cost column addition, making it well\-suited for machine learning training scenarios.

* **Open ecosystem:**  Datasets can manage various types of data stored on TOS and seamlessly integrate with ByteplusModelArk, supporting feedback of model inference data. Support exporting high\-quality datasets processed on the LAS platform to ModelArk, enabling scenarios such as model training and fine\-tuning.

# Create a dataset

## General datasets

### General dataset description

**General dataset:**  Used for aligning model behavior with human preference data and adjusting model outputs through methods such as SFT.

### Steps

1. Log in to [LAS console](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home?), and select the region at the top left corner as needed.

2. In the left navigation pane, select Datasets \> Common dataset to enter the dataset list page.

3. Click Create dataset. The page will redirect to the dataset parameter configuration page. Configure the parameters as described, and then click **Create** when finished.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea7fd55200f84ca3925ea9e15b49b592~tplv-goo7wpa0wc-topic.webp)

   |Parameter |Description |
   |---|---|
   |Dataset English name |The unique identifier of the dataset.<br><br>Length: 1–100 characters<br><br>Only supports Chinese, uppercase and lowercase letters, or numbers as the first character<br><br>Only hyphen '\-' and underscore '_' symbols are supported; special characters are not allowed |
   |Dataset Chinese name |The alias of the dataset.<br><br><br>* Length: 1–100 characters<br><br>* Only supports **Chinese**, uppercase and lowercase letters, or numbers as the first character<br><br>* Only hyphen '\-' and underscore '_' symbols are supported; special characters are not allowed. |
   |Dataset formats |The reading method of the dataset.<br><br><br>* Lance: A data lake format. Supports advanced features such as editing and deleting data items, and full\-text search.<br><br>* Iceberg: A data lake format.<br><br>* CSV: When this format is selected, files with .csv or .tsv extensions will be read from the **data source** path<br><br>* JSONL: When this format is selected, files with .jsonl or .json extensions will be read from the **data source** path<br><br>* Parquet: When this format is selected, files with .parquet extensions will be read from the **data source** path<br><br>* Image/Audio/ Video/Text：<br><br>   * For the four formats Image, Audio, Video, and Text, if there is a file named metadata with a json, jsonl, csv, or parquet extension in the first\-level directory of the **data source**, this file is designated as the **description file** for the dataset. In the **description file**, **file_name** is specified as the path to the corresponding file. Files with the specified extension are then read from the corresponding path. For details, please refer to the following [Data reading rules: Image/Audio/Video/Text](https://docs.byteplus.com/docs/Byteplus_LAS/Dataset_management#ed8c8f2d).<br><br>   * If there is no descriptor file:<br><br>      * Image: When this format is selected, files with the extensions .png, .jpg, .jpeg, .gif, .tiff, and .bmp will be read from the **data source** path.<br><br>      * Audio: When this format is selected, files with the extensions .mp3, .wav, .flac, .ogg, .m4a, .aac, .pcm, .aiff, and .aif will be read from the **data source** path.<br><br>      * Video: When this format is selected, files with the extensions .mp4, .mkv, .avi, .mov, and .webm will be read from the **data source** path.<br><br>      * Text: When this format is selected, files with the extension .txt will be read from the **data source** path.<br><br>* Lerobot: An open\-source robotics toolkit from Huggingface. The LAS dataset supports reading lerobot datasets in version v3.0 and provides capabilities for pagination, SQL queries, and loading by extracting video frames. |
   |Data source |You can currently read data from object storage TOS and metadata Catalog to create datasets.<br><br><br>* Object storage TOS: Select the storage path in TOS where the data you want to use to create a dataset is located.<br><br>   > **说明**<br>   <br><br>   > Currently, only data in TOS within the same region is supported for reading.<br>   <br><br>* For data in Lance and Iceberg formats, you can directly use Catalog as the basis for dataset creation. |
   |Metadata storage<br><br>(Supported for some data formats) |When creating datasets in Lance or Iceberg format, you can simultaneously register the dataset's related metadata as a table in Catalog, making it easier for users to manage metadata and optimize storage.<br><br>> **说明**<br><br><br><br>* > To perform this operation, you must have permission to create tables in the corresponding Catalog.<br><br><br>* > If you later delete the corresponding dataset, the tables registered in the corresponding Catalog will also be deleted automatically.<br> |

### Data reading rules: Image/Audio/Video/Text

For the Image, Audio, Video, and Text formats, if there is a file named metadata with the extension json, jsonl, csv, or parquet in the root directory of the **data source**, this file is designated as the **description file** for the dataset. In the **description file**, **file_name** is specified as the path to the corresponding file.

Taking the audio format as an example, suppose the data source path is: tos://dataset/audio, and the directory structure is as follows:

```SQL
.
└── dataset
    └── audio
        ├── audio_1.mp3
        ├── audio_2.mp3
        ├── audio_3.mp3
        ├── desc
        │   └── metadata.csv -- Only descriptor files in the first-level directory will be read, so this file will not be recognized as a descriptor file.
        └── metadata.jsonl -- Only description files in the first-level directory are read, so this file will be recognized as a description file.
```

In the description file, you can use **file_name** to indicate the file path (which must be a relative path), and use other columns to represent metadata for this file path, for example:

```JSON
{"file_name":"audio_1.mp3","size":1000,"length":11}
{"file_name":"audio_2.mp3","size":1000,"length":29}
{"file_name":"audio_3.mp3","size":1000,"length":99}
```

### Data reading rules: JSONL, CSV, Parquet

For datasets in JSONL, CSV, or Parquet format, LAS currently supports recursively searching directories for files that match the required extensions. The following is a logical example.

|Example 1: Consistent data directory hierarchy |Example 2: Inconsistent data directory hierarchy |
|---|---|
|* When creating a dataset, Data sourcethe TOS path is set to: `tos://a/`<br><br>* The actual path where data is stored in TOS can be read normally as long as it is at the same directory level. For example:<br><br>   * `tos://a/b/1.parquet`<br><br>   * `tos://a/b/2.parquet`<br><br>   * `tos://a/b/3.parquet`<br><br>   * `tos://a/c/4.parquet`<br><br>   * `tos://a/c/5.parquet`<br><br><br>— Although the second level of the data path in TOS may be "b" or "c", all data ultimately resides at the third level. Therefore, the dataset can read all data from 1.parquet to 5.parquet. |* When creating a dataset, Data sourcethe TOS path is set to: `tos://a/`<br><br>* The actual path where data is stored in TOS can be read normally as long as it is at the same directory level. For example:<br><br>   * `tos://a/b/1.parquet`<br><br>   * `tos://a/b/2.parquet`<br><br>   * `tos://a/b/c/3.parquet`<br><br>   * `tos://a/4.parquet`<br><br><br>— When data is actually stored in TOS, if the directory hierarchy is inconsistent, only data under the Data sourceconfigured path can be read normally. In this example, only `4.parquet` can be read normally. |

# Manage datasets

## Data query

After the dataset is created, you can click the dataset name to view basic information in the data details. You can also preview and query data content online.

### Data details

1. Click the target dataset name to enter the **data details** page, and click the icon to the right of the column name to expand the filter options.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96dc23382e3c429681ccea46d29c9b5e~tplv-goo7wpa0wc-topic.webp)

* This page displays specific data items within the dataset. Different formats support varying levels of features:

   * Lance: Supports pagination, insight statistics, search and filter, SQL query, edit/delete, and save as.

   * Iceberg: Supports pagination, insight statistics, search and filter, SQL query, and save as.

   * JSONL/CSV/Parquet: Supports pagination and SQL query.

   * Text/Image/Audio/Video: Only supports previewing ten items.

   * Lerobot: Supports pagination and SQL query.

   > **说明**

   * > **Lance format dataset multimodal data loading rules**: Data modality is defined by column name, and there are corresponding data type requirements as follows:

      * > Image column: The column name must use "image" as a prefix or suffix, and the type written to Lance must be the binary data type.

      * > Audio column: The column name must use "audio" as a prefix or suffix, and the type written to Lance must be the binary data type in blob format.

   * > **Viewing rules for Image/Audio/Video/Text format datasets**:

      * > No description file: Images can be viewed directly, audio can be previewed, videos can be watched, or text can be previewed.

      * > With description file: In addition to the above viewing operations, metadata for the corresponding data will also be displayed.

* LAS currently supports filtering table content by **text** and **character count**. Filter relationships can be set to **equals**/**does not equal**, **is empty**/**is not empty**, **contains**/**does not contain**, and **matches regular expression**.

### Save as dataset

Currently, datasets can be saved via "Save as" allowing data to be returned to ByteplusModelArk or saved as a new LAS dataset.

#### Scenario 1: Dataset returned to ModelArk

When returning data to ModelArk via "Save as", the following restrictions apply.

|Dataset types |ModelArk dataset return requirements |
|---|---|
|General datasets |* Format restrictions: Currently, only Lance and Iceberg formats are supported.<br><br>* Return method: Implemented via the "Save As" operation.<br><br>* Additional features: Columns that meet ModelArk fine\-tuning requirements can be filtered as needed and converted to a recognizable format. |

The operation and core configuration parameters are described below.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fd152a98dd4498b9ed44226b9e1023e~tplv-goo7wpa0wc-topic.webp)

|Parameter |Description |
|---|---|
|Dataset name |When saving as a ModelArk dataset, you can specify the dataset name. |
|Save to |The destination for saving the dataset. |
|Save formats |The format for saving the dataset; currently, only jsonl is supported. |
|Select fields：System |Select a column as the "system role". |
|Select fields： User |Select a column as the "prompt". |
|Select fields： Assistant |Select a column as the "model response". |
|Select fields： Loss_weight |Select a column as the "training weight". |

#### Scenario 2: Save dataset as LAS dataset

Currently, only datasets that are directly accessible and shared are supported. The recipient can save the dataset as a LAS dataset in their own account, and the corresponding data is stored on their own TOS.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8b01be8a1cf482fb5da513e2f9834ad~tplv-goo7wpa0wc-topic.webp)

|Parameter |Configuration instructions |
|---|---|
|Dataset English name &Dataset Chinese name |Customize the English and Chinese names of the new LAS dataset. |
|Storage address |Select the TOS address for storing the dataset data.<br><br>Selecting the root directory of the TOS Bucket is not supported. |
|Metadata storage |Select the metadata Catalog path associated with the new dataset. |
|Administrative authority &Read\-only permission |Select the permission scope for the new dataset. |
|Project affiliation |Select the project to which the new dataset belongs. |

## SQLquery

1. Click the target dataset name to enter the details page, then select SQL queries to filter data.

2. Write SQL statements in the left console, click the Start query button to execute the retrieval task, and the query results are displayed on the right. To reset the SQL statement, click the Reset button.

> **说明**

* > You can review Historical query in the lower left corner, or select **SQL template** for quick queries. Simply select the appropriate template and run the query to easily obtain accurate results. Additionally, click **Full Screen Preview** in the upper right corner of the page to enter immersive browsing mode.

* > For datasets in Lance/Iceberg format, the SQL query engine is Datafusion. Your SQL must comply with Datafusion standards.

* > For datasets in JSONL/CSV/Parquet/Lerobot format, the SQL query engine is DuckDB. Your SQL must comply with DuckDB specifications.

* > For security reasons, all IO\-related functions are currently disabled.

## File management

On this tab, you can view all files in this path, upload, preview, delete, and download files, as well as create new folders.

### Operation records

This tab records modifications to the dataset.

## Data addition

You can add data to the dataset, but the format of the new data must match the current dataset format.

1. Select **Add** in the action items on the right side of the target dataset to enter the **Add data** page.

2. Parameters are automatically configured based on the current dataset's **dataset name, data type, and format**. You only need to add the TOS path for the new data to complete the addition.

## Data export

Supports dataset export capabilities, allowing export to object storage, ModelArk, and datasets of new versions for subsequent model training.

LAS AI currently supports the following two methods for exporting data.

* On the **LAS Console \> Dataset \>**  Data details page, click Export data to export the specified dataset.

* On the **LAS Console \> Dataset \> SQL Query** page, export the **SQL query results**.

## Dataset logs

After the dataset is created, you can view all operation records. These can be found in Dataset \- Operation Records.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1261f30a9f2746b784ca6515f4d0e422~tplv-goo7wpa0wc-topic.webp)

## Dataset permissions

The dataset permission system is primarily defined based on **account roles** and **visibility settings**. Permissions are divided into **No permission**, **Read\-only permission**, and **Management permission**.

1. Click Permission in the upper right corner of the dataset details page to access the permission management page for the current dataset.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f87c973a13c4bf2828e7c0000fcb649~tplv-goo7wpa0wc-topic.webp)

2. Configure **management permissions** and **read\-only permissions**.

   |**Permission name** |**Description** |
   |---|---|
   |No permission |No permissions; can only view the dataset list and dataset summary information. |
   |Read\-only permission |Allows reading data in the dataset |
   |Management permission |Grants the ability to read and write the dataset, as well as grant permissions to other users<br><br>The creator of the dataset is granted management permission for the dataset by default<br><br>In dataset sharing scenarios, the primary account and the first sub\-user to accept the shared dataset become the Owner of the dataset and have irrevocable management permission for the dataset |

   > **说明**

   * > There are two types of authorized entities: **specified users** and **all members within the organization**. Specified users can include individual users or user groups, and fuzzy search is available. All members within the organization refers to granting permissions to all users within the current tenant; newly added or deleted users will continue to be included.

   * > You can grant permissions to specified users in batch operations. You can add or remove multiple authorized entities at the same time: To add authorization, check the box in front of the entity; to remove authorization, uncheck the box in front of the entity.

   * > The dataset creator and the primary account have management permissions for the dataset, which cannot be revoked, so neither requires authorization.
