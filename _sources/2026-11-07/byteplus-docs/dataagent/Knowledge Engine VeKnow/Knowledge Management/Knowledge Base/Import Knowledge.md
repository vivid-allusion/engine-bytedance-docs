---
title: "Import Knowledge"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Import_Knowledge"
---

After creating a new knowledge base, you need to import the relevant knowledge content. Enterprise knowledge engine supports a variety of import methods according to different types of knowledge bases. This article introduces the operation steps for importing knowledge from different types of knowledge bases.

# Prerequisite

You have created a new knowledge base, please refer to the specific operation steps [Create a New Knowledge Base](https://docs.byteplus.com/docs/dataagent/Create_a_New_Knowledge_Base).

# Common Type Knowledge Base

## Step 1: Select the import method

1. Go to the new Common Type Knowledge Base, and on the right side of the **Knowledge Management** page, click **Import Knowledge**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30f844f11fb4495b8ae9b0e2f0c969cc~tplv-goo7wpa0wc-image.image)

2. Select the import method. Support for importing local files/folders, cloud documents & online links, object storage.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69c871d42bc745de9dcbe74df58b4502~tplv-goo7wpa0wc-image.image)

## Step 2: Import knowledge data

### Method 1: Import local files

1. After selecting **Local Files**, go to the **Import Files, Local Upload** page.

2. In the **Save to** dropdown list, select Folder as the save path.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/137a68406be54f9ca75ca16340d403e4~tplv-goo7wpa0wc-image.image)

   The system will automatically create a folder named after the knowledge base name based on the knowledge base you created as the default save path. If you need to save in another folder, you can create a new folder on the **Knowledge Management** page of the **Knowledge Base**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f9f2887c9744595940cd094f70d0047~tplv-goo7wpa0wc-image.image)

3. Upload the file.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4100f29bb16240f582974c14fdee19f5~tplv-goo7wpa0wc-image.image)

   You can upload up to 100 files at a time. The supported file formats and size limits are described below.

   |**Document type** |**Supported formats** |**Single file size** |
   |---|---|---|
   |Generic document |docx/doc/wps/txt/md |Docx, doc, wps do not exceed 450MB, txt, md do not exceed 45MB. |
   |PDF document |pdf/ofd |No more than 900MB. |
   |PowerPoint |ppt/pptx |No more than 500MB. |
   |Tabel |xlsx/et/csv |* A single file does not exceed 20MB, the number of lines does not exceed 20,000 lines, and the number of columns does not exceed 200 columns<br><br>* The et file will be automatically converted to xlsx before parsing and then enter the knowledge base processing link. |
   |Image |jpg/jpeg/png |No more than 50MB. |
   |Audio |mp3/wav |No more than 512MB, recommended duration no more than 5 hours. |
   |Video |avi/mov/mp4 |No more than 1024MB, recommended duration no more than 3 hours. |
   |Compressed file |zip |No more than 10240MB and no more than 100 subfiles in a compressed file. Subfiles in the compressed file are limited according to the size limit for system single\-type files. |
   |Other |html/jsom |No more than 20MB. |

4. Select the knowledge segmentation method.

   * **Default configuration:**  Adopt the system automatic segmentation strategy, automatically slice according to the document chapter intelligently, and do not configure knowledge quality parameters and knowledge labels.

   * **Custom configuration:**  support custom segmentation policy, knowledge quality parameters, knowledge labels.

5. At the bottom of the page, select turn on or off the **skip duplicate documents** switch.

   After turning off, all duplicate documents can continue to be imported, resulting in duplicate knowledge in the base.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e393a1ab63942fb89be8f7b72c697a7~tplv-goo7wpa0wc-image.image)

6. If \*\*\*\* select the **default configuration** for the **knowledge segmentation**, click **Finish** to complete the knowledge upload. If \*\*\*\* select **custom configuration** for the **knowledge segmenttation**, click **Next**.

### Method 2: Import the local folder

1. After selecting **a local folder**, go to the **Import Folder** page.

2. In the **Save to** dropdown list, select Folder as the save path.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a093dfeaa4a0413bbf3c414ee57feb2a~tplv-goo7wpa0wc-image.image)

3. Upload a local folder.

   * Support uploading parent and child folders, which add up to no more than 5 layers with the original directory of the knowledge base.

   * You can upload up to 100 files at a time, and the file size limits for each type are described below.

      |**Document type** |**Supported formats** |**Single file size** |
      |---|---|---|
      |Generic document |docx/doc/wps/txt/md |Docx, doc, wps do not exceed 450MB, txt, md do not exceed 45MB. |
      |PDF document |pdf/ofd |No more than 900MB. |
      |PowerPoint |ppt/pptx |No more than 500MB. |
      |Tabel |xlsx/et/csv |* A single file does not exceed 20MB, the number of lines does not exceed 20,000 lines, and the number of columns does not exceed 200 columns.<br><br>* The et file will be automatically converted to xlsx before parsing and then enter the knowledge base processing link. |
      |Image |jpg/jpeg/png |No more than 50MB. |
      |Audio |mp3/wav |No more than 512MB, recommended duration no more than 5 hours. |
      |Video |avi/mov/mp4 |No more than 1024MB, recommended duration no more than 3 hours. D |
      |Compressed file |zip |No more than 10240MB and no more than 100 subfiles in a compressed file. Subfiles in a compressed file are limited according to the size limit for system single\-type files. |
      |Other |html/jsom |No more than 20MB. |

   * Excess number of files, folder level, document type, the system will automatically filter.

4. Select the knowledge segmentation method.

   * **Default configuration:**  Adopt the system automatic segmentation strategy, automatically slice according to the document chapter intelligently, and do not configure knowledge quality parameters and knowledge labels.

   * **Custom configuration:**  support custom segmentation policy, knowledge quality parameters, knowledge labels.

5. At the bottom of the page, select turn on or off the **skip duplicate documents** switch.

   After turning off, all duplicate documents can continue to be imported, resulting in duplicate knowledge in the base.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a108685124e647459aaf2e61ab81a090~tplv-goo7wpa0wc-image.image)

6. If \*\*\*\* select the **default configuration** for the **knowledge segmentation**, click **Finish** to complete the knowledge upload. If \*\*\*\* select **custom configuration** for the **knowledge segmenttation**, click **Next**.

### Method 3: Import from cloud documents

1. Select **Lark Cloud Documents**, **WeCom Documents**, **DingTalk Cloud Documents**

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b5997e612504b9ebd66d388e40a4d6f~tplv-goo7wpa0wc-image.image)

2. Once selected, follow the instructions on the **Import File** page to complete the configuration.

   1. Select **Save Path**.

      The system will automatically create a folder named after the knowledge base name based on the knowledge base you created as the default save path. If you need to save in another folder, you can create a new folder on the **Knowledge Management** page of the **Knowledge Base**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbc6248b2df44d3e85b4df49a084aa1e~tplv-goo7wpa0wc-image.image)

   2. Customize the **import task name**.

   3. Select whether to enable **automatic knowledge update**. After turning on, you need to configure the automatic update frequency(**day\-level**, **weekly level**, **monthly level**) on demand, and set the **time**. The knowledge will be automatically updated when the update frequency is met.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bd887b41e8a4f05822d7a592f3d8102~tplv-goo7wpa0wc-image.image)

   4. In the **import knowledge selection** area, the first import needs to complete the authorization of Lark, WeCom, and DingTalk. After the authorization is completed, the cloud document can be imported.

      > **注意**

      * > Enterprise administrators need to complete the cloud document access configuration (for details, see [Access Cloud Documents](https://docs.byteplus.com/docs/dataagent/Access_Cloud_Documents)), and then complete user authorization or selection knowledge according to the guidelines on the current page.

      * > After authorization, you can only import cloud documents that authorized users have permissions to (specific permissions follow the permission management logic of Lark, WeCom, and DingTalk cloud documents).

      |**Import channel** |**Configuration instructions** |
      |---|---|
      |Lark Cloud Documentation |* **Add Quickly:**  After the authorization is completed, you can get the Lark cloud document with permission, and then tick the document that needs to be imported.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea74e8a7cf9e4659a2c2973f8900f9b6~tplv-goo7wpa0wc-image.image)<br><br>* **Link Add:**  Enter a cloud document link with permissions to import the document, and support adding multiple links.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67fca0a00cd443358ec917be26f54819~tplv-goo7wpa0wc-image.image)<br><br><br>> **注意**<br><br><br>> At present, Lark native forms, native PPT, and knowledge access of audio, video, and compressed file types for file uploads are not supported, and will continue to iterate.<br> |
      |WeCom Documentation |Enter the WeCom document link to import, and support adding multiple links.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f88a4b29ce854f519b3de2c7207d16ac~tplv-goo7wpa0wc-image.image) |
      |DingTalk Cloud Documentation |Support for selecting files from **team files**, **My Documents**, **Knowledge Base**.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7723c8e3df4f43568f0fbef5c9229723~tplv-goo7wpa0wc-image.image) |

3. Select the knowledge segmentation method.

   * **Default configuration:**  Adopt the system automatic segmentation strategy, automatically slice according to the document chapter intelligently, and do not configure knowledge quality parameters and knowledge labels.

   * **Custom configuration:**  support custom segmentation policy, knowledge quality parameters, knowledge labels.

4. At the bottom of the page, select turn on or off the **skip duplicate documents** switch.

   After turning off, all duplicate documents can continue to be imported, resulting in duplicate knowledge in the base.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98517c2a4314417386d0c2d58f8f62c0~tplv-goo7wpa0wc-image.image)

5. If select the **default configuration** for the **knowledge segmentation**, click **Finish** to complete the knowledge upload. If select **custom configuration** for the **knowledge segmenttation**, click **Next**.

### Method 4: Online link

1. On the **Knowledge Management** page of the Common Knowledge Base, click **Import Knowledge** and select the **Public link**.

2. In the **Online Links** area of the **Select Import Method** interface, select **Public Links** to support importing publicly accessible document links.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/152bbb4abacb4501b24d20e1e4a12890~tplv-goo7wpa0wc-image.image)

3. On the **Import File • Public Links** page, complete the following configuration.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67dbdbb9718d49a3ae149bf2163e00cf~tplv-goo7wpa0wc-image.image)

   1. Select **Save Path**.

      The system will automatically create a folder named after the knowledge base name based on the knowledge base you created as the default save path. If you need to save in another folder, you can create a new folder on the **Knowledge Management** page of the **Knowledge Base**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f96856437104a11881d2b6b27e09239~tplv-goo7wpa0wc-image.image)

   2. Select whether to enable **automatic knowledge update**. After opening, you need to configure the automatic update frequency(**day\-level, weekly level, monthly level**) on demand, and set the **time**. The knowledge will be automatically updated when the update frequency is met.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3f07a5aae08408bba99f6d0ed9c0297~tplv-goo7wpa0wc-image.image)

   3. In the **Import Knowledge selection** area, enter a public link to download without authorization and set the **page resolution depth**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1873bde398a5498988b2c7fdd1ae15cb~tplv-goo7wpa0wc-image.image)

      * Enter up to 20 URLs at a time, one for each line in the input box.

      * Page parsing depth selection:

         * **Current link only**, parses only the content of the current URL.

         * **Drill down a layer:**  The child URLs contained in the current URL are also parsed.

   4. After the configuration is completed, click Add and Parse, wait for the system to complete the parsing, and you can view the parsing results.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c429b9888dde41bc8c4f2f3d4c44d064~tplv-goo7wpa0wc-image.image)

   5. In the **Knowledge Segmentation** area, select Segmentation Configuration.

      * **Default configuration:**  Adopt the system automatic segmentation strategy, automatically slice according to the document chapter intelligently, and do not configure knowledge quality parameters and knowledge labels.

      * **Custom configuration:**  support custom segmentation policy, knowledge quality parameters, knowledge labels.

4. At the bottom of the page, select turn on or off the **skip duplicate documents** switch.ments switch.

   After turning off, all duplicate documents can continue to be imported, resulting in duplicate knowledge in the base.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a1887f64a4c46028ecc3eea4328aa9a~tplv-goo7wpa0wc-image.image)

5. If select the **default configuration** for the **knowledge segmentation**, click **Finish** to complete the knowledge upload. If select **custom configuration** for the **knowledge segmenttation**, click **Next**.

### Method 5: Import from Object Store

1. Support importing knowledge from Object Storage Service or system that supports S3 protocol, such as Volcano Cloud TOS, Tencent Cloud COS, Alibaba Cloud OSS, etc.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51d59fa6a54544839705c3ae930e1e70~tplv-goo7wpa0wc-image.image)

2. On the **Import File** page, complete the following configuration.

   1. Select **Save Path**.

      The system will automatically create a folder named after the knowledge base name based on the knowledge base you created as the default save path. If you need to save in another folder, you can create a new folder on the **Knowledge Management** page of the **Knowledge Base**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/530d4d705c8240339d39dc5b2d381b90~tplv-goo7wpa0wc-image.image)

   2. Customize the **import task name**.

   3. Select whether to enable **automatic knowledge update**. After opening, you need to configure the automatic update frequency(**day\-level, weekly level, monthly level**) on demand, and set the **time**. The knowledge will be automatically updated when the update frequency is met.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7af270e2dc074cf2a0b83c1fb8fed679~tplv-goo7wpa0wc-image.image)

   4. In the **Import knowledge selection** area, select the data connection for the specified object storage. If there is no data connection that meets the requirements, you can click **New** to go to Create and then select.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4edfcd6a4fe14a358590ca2ebb530f7a~tplv-goo7wpa0wc-image.image)

      For each object storage data connection method, see:

      * [Volcano Engine Clouds TOS_ Unstructured](https://docs.byteplus.com/docs/dataagent/Volcano_Engine_Clouds_TOS__Unstructured)

      * [Alibaba Cloud OSS_ Unstructured](https://docs.byteplus.com/docs/dataagent/Alibaba_Cloud_OSS__Unstructured)

      * [Tencent Cloud COS_ Unstructured](https://docs.byteplus.com/docs/dataagent/Tencent_Cloud_COS__Unstructured)

      * [Huawei Cloud OBS_ Unstructured](https://docs.byteplus.com/docs/dataagent/Huawei_Cloud_OBS__Unstructured)

      * [SCHEMA_LESS S3](https://docs.byteplus.com/docs/dataagent/SCHEMA_LESS_S3)

3. After selecting a data connection, set the import scope to support **partial import** or **full import**.

   > **说明**

   * > If the amount of data is large, it may take a long time to import and parse all the data.

   * > At present, knowledge access of compressed file types is not supported.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd86aa13d4df40ed8799523926c9c83c~tplv-goo7wpa0wc-image.image)

4. Select the knowledge segmentation method.

   * **Default configuration:**  Adopt the system automatic segmentation strategy, automatically slice according to the document chapter intelligently, and do not configure knowledge quality parameters and knowledge labels.

   * **Custom configuration:**  support custom segmentation policy, knowledge quality parameters, knowledge labels.

5. At the bottom of the page, select turn on or off the **skip duplicate documents** switch.

   After turning off, all duplicate documents can continue to be imported, resulting in duplicate knowledge in the base.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d068392fd27a415d80b6e5bfe08d7d8a~tplv-goo7wpa0wc-image.image)

6. If select the **default configuration** for the **knowledge segmentation**, click **Finish** to complete the knowledge upload. If select **custom configuration** for the **knowledge segmenttation**, click **Next**.

## Step 3: Configure the knowledge segmentation method

Knowledge segmentation is the process of dividing long documents into smaller units that are easier to process and retrieve models. Reasonable configuration helps to improve the accuracy and efficiency of retrieval.

1. Configure segmentation parameters.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f58feb0ddcfb4098b7b452b2083f9c1a~tplv-goo7wpa0wc-image.image)

   * Support selection of **automatic segmentation**, **custom segmentation**, **model summary segmentation**, and **context\-aware segmentation**.

      * Automatic segmentation: Adopts a general slicing strategy, and the model automatically recognizes the document according to the document structure for slicing.

      * Custom segmentation: You need to manually define **segmentation rules**, **segmentation related information**, and **merge small segmentation** configuration items.

      * Model summary segmentation: through model summary summary, key information extraction, segmentation of document fragments.

      * Context\-aware segmentation: Intelligent segmentation of document fragments through model analysis of context information.

   * You need to configure the **parsing strategy** and the **maximum length of the segment** according to the page prompt information.

   > **说明**

   > The configuration items of different import methods may be different, please refer to the actual page information for configuration.

2. Configure intelligent summary parameters.

   Invoking the large model to extract richer knowledge points for each segment to build an index can improve the effect of segment recall, but it will increase the processing time and resource consumption.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe73606d497b4a89a1cbd05e8158a61a~tplv-goo7wpa0wc-image.image)

   |**Parameter** |**Parameter description** |**Default configuration** |
   |---|---|---|
   |Document summary |A paragraph summarizes the document's themes and core conclusions for document\-level coarse screening. |Open |
   |Document guide |A detailed summary of the core points of the document, such as background, findings, and conclusions, makes it easy to quickly grasp the content of the document, and is mainly used by users to browse the key information of the document. |Close |
   |Segmented summary |One sentence condenses the slice core, which is used for fast and accurate retrieval of slices, which can improve the accuracy of retrieval recall. |Close |
   |Segmented key issues |The high\-frequency questions that can be answered by slicing can enhance the semantic distance between Query and chunk, and improve the accuracy of retrieval recall. |Close |
   |Segmented keywords |Easy\-to\-retrieve labelsls for keyword filtering can enhance the accuracy of retrieval recalls. |Close |

3. Set knowledge quality measurement parameters.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6293bc0e7b47447ca07c5322bd59deef~tplv-goo7wpa0wc-image.image)

   |**Parameter** |**Parameter description** |**Default configuration** |
   |---|---|---|
   |**Document deduplicate** |After opening, the system will verify whether the content of the uploaded file is duplicate with the existing file in the knowledge base. If there is a duplicate, it cannot be uploaded. By verifying file MD5, only fully duplicated files are considered duplicates. |Close |
   |**Typo detection** |After opening, the system will detect whether there are typos in the content of the uploaded file. |Close |
   |**Incomplete statement detection** |After opening, the system will detect whether the uploaded statement is incomplete. |Close |
   |**Sensitive word detection** |After opening, the system will detect whether the uploaded content has sensitive words. |Close |

4. Configure knowledge labels.

   Knowledge is classified by knowledge marking, please refer to the specific configuration operation [Knowledge classification](https://docs.byteplus.com/docs/dataagent/Manage_Knowledge#3ef7126a).

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/129611a083f54eda826531e15abc49fe~tplv-goo7wpa0wc-image.image)

# Query Cache Type Knowledge Base

1. Click on the new knowledge base to enter the knowledge base details page.

2. Click **Upload**, upload the content file cached by Query, and then click **Finish**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6930b2f6dae640aaa248371f29c22d76~tplv-goo7wpa0wc-image.image)

   Files support xlsx, et, csv and other formats, and can upload up to 10 files at a time, a single file does not exceed 10 MB, and the number of lines does not exceed 10,000 lines.

   > **说明**

   > It is recommended that you click **Download Template** and fill in the Query name and description according to the requirements of the template.

3. Click **Cache Query** to create a new Query cache.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41153ebc19a34cd09b09b2f5a575ac0b~tplv-goo7wpa0wc-image.image)

4. In the **New Query Cache** panel, fill in the relevant parameters and click **Save**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8780cda394ae479c976fc0de969f1779~tplv-goo7wpa0wc-image.image)

# QA Q & A Knowledge Base

1. Click on the new knowledge base to enter the knowledge base details page.

2. Click **Upload**, upload the QA content file, and then click **Finish**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4225bb8c149a47ffa8d2bf0bf3f42d3c~tplv-goo7wpa0wc-image.image)

   Files support xlsx, et, csv and other formats, and can upload up to 10 files at a time, a single file does not exceed 10 MB, and the number of lines does not exceed 10,000 lines.

   > **说明**

   > It is recommended that you click **Download Template** and fill in the Query name and description according to the requirements of the template.

3. Click on **QA Q & A** to create a new QA Q & A.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0882bc5f86df4efb9c9b75678b8889b8~tplv-goo7wpa0wc-image.image)

4. In the **New QA Q & A** panel, fill in the questions and answers (answers support adding pictures), and then click **Save**. Add up to 20 questions and answers at a time.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79cb219cc51e4734a601cc479e2e5422~tplv-goo7wpa0wc-image.image)

# Term Type Knowledge Base

1. Click on the new knowledge base to enter the knowledge base details page.

2. Click **Upload**, upload the QA content file, and then click **Finish**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f280abd631224f39baf2b48192731cbc~tplv-goo7wpa0wc-image.image)

   Files support xlsx, et, csv and other formats, and can upload up to 10 files at a time, a single file does not exceed 10 MB, and the number of lines does not exceed 10,000 lines.

   > **说明**

   > It is recommended that you click **Download Template** and fill in the term name and term definition according to the requirements of the template.

3. Click **Terms** to create a new term.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4f5f111f33f4afbb52ece78b47f38f8~tplv-goo7wpa0wc-image.image)

4. In the **New Term** panel, fill in the **term name** and **definition**, or click **Add**, add synonyms, and then click **Save**. Add up to 20 terms at a time.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6bc4d173efa4cb383a1100654e4e051~tplv-goo7wpa0wc-image.image)

# Structured Data Types Knowledge Base

1. Click to enter the newly created Structured Data Type Knowledge Base.

2. On the **Knowledge Management** page, in the **All Knowledge** area, click **Import Knowledge**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76eda22e5daf4059a402dcc4eba971c6~tplv-goo7wpa0wc-image.image)

3. On the **Import Knowledge** page, complete the following configuration and click **Save** at the bottom of the page.

   \*\*Import method \*\*Select **local file** or **dataset**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e332bd87faf04669acd7b3329dfd7c62~tplv-goo7wpa0wc-image.image)

   You need to upload files locally, support uploading 1 xlsx/csv format file at a time, the size does not exceed 20 MB, and the recommended number of lines does not exceed 50,000 lines.

   * **Save to:**  Path to save the current knowledge file.

      The system will automatically create a folder named after the knowledge base name based on the knowledge base you created as the default save path. If you need to save in another folder, you can create a new folder on the **Knowledge Management** page of the **Knowledge Base**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7ed2205b52d4fde9c18e66b829c1f75~tplv-goo7wpa0wc-image.image)

   * **Table field configuration:**  You need to select the **import Sheet**, **the row where the table header is located,**  and the **data starting row**. The system will automatically identify the table column name according to the settings, and generate the column name after import and the display name after import. You can customize the column name, display name, data type, and description according to your actual needs, and configure the following switches:

      * **Participate in vector retrieval:**  When enabled, this field will generate a vector through the Embedding model for semantic similarity retrieval. It is recommended to enable the core text field.

      * **Participation Criteria Filtering:**  After opening, this field can be used as an accurate filter condition for retrieval, such as filtering by date, category, channel, etc.

      * **Unique identification field:**  used to generate stable row_key. After the first configuration, the asset supports subsequent append, overwrite, and manual addition.

      * **Whether to import:**  When turned on, the field participates in the recall and results are returned to the configuration.

   * At the bottom of the **table field configuration**, add new fields manually.

# Operation result

After the knowledge segmentation configuration is completed and submitted, the knowledge import task begins to execute. The Knowledge Base Management list page displays the knowledge processing status, such as processing in progress, processing success, and so on.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2d99e0428644172ae59342e10cf46a7~tplv-goo7wpa0wc-image.image)

In the **processing status** column field supports filtering knowledge information for each state.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a7b0f14288a408a9c62117494821040~tplv-goo7wpa0wc-image.image)

# **Test import results**

1. On the Knowledge Base page, click **Knowledge Recall Test** to enter the Knowledge Base Test page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c47a439c9d9463894d86d19ceb33c60~tplv-goo7wpa0wc-image.image)

2. Complete the following configuration for recall testing.

   |**Knowledge base type** |**Configuration item description** |
   |---|---|
   |GenerIc Content/QA/Term/Query Cache |* Search keywords: Enter keywords to search.<br><br>* Specify the scope of knowledge: Select the scope of documents participating in the recall test, and default to all documents.<br><br>* Filter labels: Filter recall results by knowledge labels.<br><br>* Vector search weight: Adjust the proportion of keyword matching and semantic understanding. The lower the value, the more attention is paid to accurate word and sentence hits, and the higher the value, the more attention is paid to the overall semantic relevance.<br><br>* Mixed similarity threshold: the lower bound of relevance score for synthetic semantic matching and keyword matching. It will only be recalled if the mixed similarity of the candidate documents exceeds this threshold. The higher the value, the more accurate the recall result but the smaller the quantity; the lower the value, the wider the recall range but may introduce noise.<br><br>* Sorting strategy: support selection **not sorting**, **semantic model sorting**, **large model sorting**.<br><br>   * Semantic model ranking: Use a dedicated semantic ranking model to re\-rank initial shardings by relevance. Fast and cost\-effective, it is suitable for most scenarios.<br><br>   * Large model sorting: Call the large language model to evaluate the matching degree of sharding to the problem one by one, and the sorting quality is higher, but the speed is slightly slower. It is suitable for scenarios where there are high requirements for answer quality.<br><br>* Number of initial shardings: The number of candidate shardings retrieved from the knowledge base and returned. The higher the value, the wider the coverage of the recall, but it will increase the processing time. This value should be ≥ the number of selected shardings.<br><br>* Sorting score threshold: When the threshold is set, only recall shardings with scores ≥ this threshold are retained, and results below the threshold will be filtered directly and will not participate in the final display. The higher the threshold, the more accurate the results, but the number of recalls may decrease; the lower the threshold, the richer the results, but the less relevant content may be mixed in.<br><br>* Recall segment count: The number of shardings that were finally displayed in the search list and fed to the large model after reordering. The higher the value, the more reference information the model can obtain, but it may introduce noise. |
   |Structured data |* Specify the scope of knowledge:<br><br>   * Data table: Candidate for the data table (table or dataset) that has been successfully processed in the current structured knowledge base.<br><br>   * Filter criteria: Set the exact filter criteria by the filterable fields of the current data table.<br><br>   * Semantic recall field (vector column): Candidate contains only the fields with vector index enabled in the current data table, which is not selected by default; it takes effect in mixed retrieval and vector retrieval modes.<br><br>   * Result return fields: The candidates are all fields of the current data table, which are used to crop the columns displayed on the recall result card. By default, the fields that are opened when importing are selected "whether to enable".<br><br>* Semantic search keywords: Enter search keywords for semantic recall, up to 200 words.<br><br>* Vector search parameters:<br><br>   * Vector search weight: Adjust the proportion of keyword matching and semantic understanding. The lower the value, the more attention is paid to accurate word and sentence hits, and the higher the value, the more attention is paid to the overall semantic relevance.<br><br>   * Mixed similarity threshold: the lower bound of relevance score for synthetic semantic matching and keyword matching. Only when the mixed similarity of the candidate data reaches this threshold will it be recalled.<br><br>   * Sorting strategy: When not sorted, it will be returned in the default order of the search engine; semantic model sorting will reorder the results of the initial screening.<br><br>   * Recall Records (Rows): The number of rows of structured data finally displayed on the recall result card after reordering. The higher the value, the more reference information is obtained, but it may introduce noise. |

3. The recall accuracy is evaluated based on the index of recall paragraph ranking, reordering score, mixture similarity and so on.

   * Generic Content/QA/Term/Query Cache

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/924c2a97ea07410eae7cb54618308893~tplv-goo7wpa0wc-image.image)

   * Structured data

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9d34a33f8024cb3bb062b2245c132e8~tplv-goo7wpa0wc-image.image)

# Next step

Carry out knowledge management operations such as knowledge marking and valid period, please refer to the specific operations [Knowledge Management](https://docs.byteplus.com/docs/dataagent/Manage_Knowledge).

# Reference: Knowledge segmentation configuration and tuning recommendations

### **Scenario 1: Evaluation from the text feature dimension**

* Based on the complexity evaluation, the following parameters can be used to configure the logic:

   |**Parameter** |**Complex text** |**Simple text** |
   |---|---|---|
   |**Explain** |Such as academic research papers and other professional content, involving multi\-disciplinary knowledge and complex logic. |Such as daily conversations, simple consultation records, etc., do not involve complex logic and knowledge analysis. |
   |**Automatic keywords** |It is recommended to configure 12\-20 to cover cross\-cutting concepts in multiple fields. |It is recommended to configure 8\-12 (or less) to focus on high\-frequency topics. |
   |**Automatic question** |It is recommended to configure 4\-6 to disassemble the complex logic chain. |It is recommended to configure 2\-3 to simplify interaction intent. |
   |**Split strategy** |Document tree/chapter, preserving directory structure. |Paragraph (divided into natural segments, such as question\-and\-answer rounds in customer service conversations). |
   |**Character length** |512\-1024 (or higher) (to accommodate long paragraph formula/chart descriptions). |128\-256 (suitable for short dialogues/single\-sentence instructions). |
   |**Whether to recognize PDF forms** |It is recommended to open (extract experimental data forms, regulatory schedules). |Optional on (off when text\-only to save resources). |
   |**Whether to use PDF Outline** |It is recommended to open (use the directory to locate chapters, such as "Chapter 3, Model Building → 3.1 Algorithm Principles"). |Optional shutdown (no need to enable without directory structure). |
   |**The maximum level of chapter expectations** |Level 3\-4. |Level 1\-2. |
   |**Number of block tokens** |It is recommended to configure 512\-1024 (or higher) to ensure semantic coherence in long paragraphs. |It is recommended to configure 128\-256 to avoid redundant calculations. |
   |**Segmentation identifier** |It is recommended to use strict symbols such as periods and semicolons to segment. |It is recommended to segment with regular symbols such as periods and commas. |
   |**Layout recognition** |It is recommended to open. |It is recommended to open. |
   |**Table to HTML** |It is recommended to open. |It is recommended to open. |

* Based on the text length evaluation, the following parameters can be used to configure the logic:

   |**Parameter** |**Long text** |**Short text** |
   |---|---|---|
   |**Explain** |For example, technical manuals, novels, etc. |For example, social media comments, text messages, etc. |
   |**Split strategy** |Document tree/chapter (split by "Chapter → Section → Subsection"). |Paragraph/custom separator (split by "\ n" or "."). |
   |**Character length** |1024 + (cross\-chapter semantic associations, such as "Chapter 5 Formulas → Chapter 6 Applications"). |128\-256 (single message processing independently). |
   |**Whether to merge small chunks** |Closing (preserving chapter independence, such as "Appendix A" separated from "Body"). |Open (merge adjacent sentences, such as "Hello → How can I help you?"). |
   |**PDF page limit** |500\-1000 (processing large documents in batches, such as "2000\-page regulations parsed in 4 times"). |No special restrictions (single page/small amount of content processed at one time). |
   |**Number of Block Tokens** |It is recommended to configure 512\-1024 (or higher) for long context dependencies. |It is recommended to configure 128\-256 to respond quickly to requirements. |
   |**Segmentation identifier** |It is recommended that line breaks, section headings, etc. be used as segment identifiers. |It is recommended to use a period or natural pause as the segmentation symbol. |
   |**Layout recognition** |It is recommended to open |It is recommended to open |
   |**Table to HTML** |It is recommended to open |It is recommended to open |

### **Scenario 2: Evaluation from the application scenario dimension**

* **High\-precision scenarios** (academic research, legal documents, etc.).

   * **Core objective:**  Maximize knowledge relevance and integrity.

   * **Configuration strategy:**  a large number of keywords are extracted, the problem is split carefully, the character length is long, strictly according to the text structure and logical segmentation, accurately identify the layout and process the table data.

* **High\-efficiency scenarios** (intelligent customer service, real\-time interaction, etc.)

   * **Core goal:**  Balance semantic understanding with responsiveness.

   * **Configuration strategy:**  on the basis of ensuring understanding of semantics, moderate number of keywords and questions, simple and easy\-to\-handle segmentation identifiers, layout recognition and table processing should be concise and efficient.
