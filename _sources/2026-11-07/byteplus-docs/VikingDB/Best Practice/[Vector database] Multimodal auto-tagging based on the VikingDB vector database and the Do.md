---
title: "[Vector database] Multimodal auto-tagging based on the VikingDB vector database and the Doubao LLM"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Multimodal_auto-tagging"
---

<span id="[Vector database] Multimodal auto-tagging based on the VikingDB vector database and the Doubao LLM"></span>
# [Vector database] Multimodal auto\-tagging based on the VikingDB vector database and the Doubao LLM

<span id="02496d47"></span>
# 1. Background

<span id="ed3b211b"></span>
## 1.1 Requirements and scenarios

When you need to automatically classify massive amounts of multimodal data with high accuracy, especially in scenarios with complex tagging systems, this guide provides a complete solution. It walks you through combining the VikingDB vector database with the Doubao large language model (LLM). By following the steps, you will learn how to use VikingDB's fast semantic retrieval to narrow the classification scope, which significantly improves the LLM's tagging accuracy and efficiency. After accumulating massive multimodal data such as text, images, and videos, enterprises need to classify and tag the data for subsequent analysis, retrieval, and use.

**Scenarios:** 

**Customer feedback classification**: Tag customer feedback with categories such as product issues or shipping delays for quick resolution.

**Content moderation and recommendation**: Tag user\-uploaded text or images with categories such as sensitive content or trending topics for content moderation and recommendation.

**E\-commerce product classification**: Tag product images or descriptions with categories such as home appliances or clothing for efficient listing.

<span id="ed1e91f3"></span>
## 1.2 Solution

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/131dd1d256514681afaa8bce95174c6a~tplv-goo7wpa0wc-image.image" width="650px" /></div>


> **The solution is devised based on the following considerations:** 

> **Question**: Why do we combine the VikingDB vector database with the Doubao large language model (LLM)?

> **Answer**: The VikingDB vector database quickly identifies the tags of the historical data that are semantically similar to the new data, narrowing the classification scope and significantly reducing the inference complexity of the Doubao LLM.

> **Question**: When should we combine the VikingDB vector database with the Doubao LLM?

> **Answer**: When the tagging system is highly complex, with hundreds or thousands of tags or overlapping hierarchies, relying solely on the Doubao LLM for classification becomes challenging and error\-prone. In this case, combining the VikingDB vector database with the Doubao LLM for tagging can narrow the classification scope and reduce the inference complexity.


<span id="0c15e1f1"></span>
## 1.3 Advantages of the solution

**Accurate classification**: This solution provides reference tags based on vector retrieval, improving the classification accuracy of the LLM.

**Multimodal tagging**: This solution supports the classification and tagging of multiple types of data, such as text, images, videos, and audio.

<span id="5a36b855"></span>
# 2. Procedure

<span id="ec3af5f1"></span>
## 2.1 Determine a scenario and prepare data

This section demonstrates how to automatically tag and classify text using the VikingDB vector database and the Doubao LLM in the event of a large number of tags.

First, we obtain WOS_Data_1000.xlsx, **the tagged abstracts** to be stored in the VikingDB vector database.

> This dataset was released by Kamran Kowsari et al. For more information, refer to *HDLTex: Hierarchical Deep Learning for Text Classification* (ICMLA 2017).


As shown in the following table, the Excel file contains 7 first\-level tags in the domain field, 126 second\-level tags in the area field, and 1,000 tagged abstracts in the abstract field.

| | | | \


|domain |area |abstract | |
|---|---|---|---|
| | | |\ |
|CS |Symbolic computation |(2 + 1)\-dimensional non\-linear optical waves through the coherently…… | |
| | | |\ |
|Medical |Alzheimer's Disease |(beta\-amyloid (A beta) and tau pathology become …… | |
| | | |\ |
|…… |…… |…… | |


Then, we obtain WOS_Data_Untagged_20.xlsx, the abstracts **not to be stored** in the VikingDB vector database.

Next, we implement the solution to automatically tag and classify these abstracts. By comparing the tags from this solution with the original ones, we can verify the effectiveness of searches in this scenario.

<span id="638217cb"></span>
## 2.2 Prepare an access key and an environment

Register a BytePlus account and enable the VikingDB service. For more information, refer to [Register an account and enable the service](https://www.volcengine.com/docs/84313/1254444).

Obtain an access key, which consists of an access key ID and a secret access key. For more information, refer to [Managing access keys](https://www.volcengine.com/docs/6291/65568).

Run the following commands in a terminal window to prepare an environment:

| | | | \


|**Python** |Version 3.7 or later | | |
|---|---|---|---|
| | | |\ |
|**SDK for Python** |pip3 install \-\-upgrade volcengine |Used for accessing VikingDB. | |
| | | |\ |
|**Ark** |pip3 install \-\-upgrade 'volcengine\-python\-sdk[ark]' |Used for accessing the Doubao LLM. | |
| | | |\ |
|**pandas** |pip3 install \-\-upgrade pandas |Used for preprocessing data. | |
| | | |\ |
|**openpyxl** |pip3 install \-\-upgrade openpyxl |Used for reading Excel data. | |
| | | |\ |
|**aiohttp** |pip3 install \-\-upgrade aiohttp |A framework for asynchronous HTTP communication. | |


<span id="3593dc44"></span>
## 2.3 Initialize the SDK for Python for the VikingDB vector database

This section describes how to initialize the SDK for Python for the VikingDB vector database.

Enter your access key ID after vikingdb_service.set_ak and your secret access key after vikingdb_service.set_sk.

For more information about how to obtain an access key ID and a secret access key, refer to [Managing access keys](https://www.volcengine.com/docs/6291/65568).

```Python
from volcengine.viking_db import *  # Make sure that you have installed volcengine by running the following command: pip3 install --upgrade volcengine. 

# Initialize the SDK. 
vikingdb_service = VikingDBService( 
    host="api-vikingdb.volces.com", # Do not include the protocol (like http:// or https://) in this parameter. 
    region="cn-beijing", # Configure this parameter as needed, such as cn-beijing for the North China region or cn-shanghai for the East China region. 
    scheme="https", # This parameter is optional. You can set it to http or https. However, we recommend that you set it to https. 
    connection_timeout=30, # This parameter defaults to 30 seconds. You can modify it as needed. 
    socket_timeout=30 # This parameter defaults to 30 seconds. You can modify it as needed. 
) 

vikingdb_service.set_ak("Enter your access key ID, with the double quotes retained.") 
vikingdb_service.set_sk("Enter your secret access key, with the double quotes retained.")
```


<span id="0b6ce0ab"></span>
## 2.4 (Optional) Preprocess the data

The VikingDB vector database supports the upload of JSON data. If your data is in the JSON format, preprocessing is unnecessary.

In the current scenario, ExcelWOS_Data_1000.xlsx must be preprocessed into the JSON format for upload.

Original data (Excel):

| | | | \


|domain |area |abstract | |
|---|---|---|---|
| | | |\ |
|CS |Symbolic computation |(2 + 1)\-dimensional non\-linear optical waves through the coherently…… | |
| | | |\ |
|Medical |Alzheimer's Disease |(beta\-amyloid (A beta) and tau pathology become …… | |
| | | |\ |
|…… |…… |…… | |


Preprocessed data (JSONL):

```Python
{"ID": 1, "domain": "CS", "area": "Symbolic computation", "abstract": "(2 + 1)-dimensional non-linear……"} 
{"ID": 2, "domain": "Medical", "area": "Alzheimer's Disease", "abstract": "(beta-amyloid (A beta) and……"} 
……
```


Code: **Note that the Excel file must be in the same directory as the code.** 

```Python
## Data preprocessing## 
# Specify the input and output file paths. 
file_path = "WOS_Data_1000.xlsx" 
output_file = "WOS_Data_1000.jsonl" 

def pre_processing(): 
    # Read the data from the three required fields in the Excel file. 
    df = pd.read_excel(file_path, usecols=["domain", "area", "abstract"]) 

    # Write all data to a JSONL file. 
    with open(output_file, 'w', encoding='utf-8') as f: 
        # Use enumerate() to generate doc_id values, which start from 1. 
        for idx, row in enumerate(df.itertuples(index=False), start=1): 
            record = { 
                "ID": idx,  # Use idx as doc_id. 
                "domain": row.domain, 
                "area": row.area, 
                "abstract": row.abstract 
            } 
            f.write(json.dumps(record, ensure_ascii=False) + '\n') 

    # Output the processing result. 
    print(f"{len(df)} rows of data are extracted and saved to {output_file}. ") 

# Start data preprocessing. 
pre_processing()
```


After the data preprocessing completes, the first 1,000 rows of data in the Excel file are converted into the JSON format and automatically saved to WOS_Data_1000.jsonl.

<span id="42858bf7"></span>
## 2.5 Configure fields to create a collection

You can configure fields to create a collection through the console or the SDK for Python.

After you run the preceding code, the tagging_best_practice collection appears on the Collection page of the VikingDB vector database.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3af0dfac466f460ba44487cb83fe4438~tplv-goo7wpa0wc-image.image" width="1457px" /></div>


`}\></Tabs.TabPane\>);

```Plain

###

<span id="e0792863"></span>

## 2.6 Upload data

In this example, the preprocessed data WOS_Data_1000.jsonl is uploaded.  <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ec94f6da4f045f4bc5fe4637f44220b~tplv-goo7wpa0wc-image.image" name="WOS_Data_1000.jsonl" ></Attachment>  <span style="color: #D83931"><strong>Note:</strong></span>  <span style="color: #D83931"><strong>Place the JSONL file and the code in the same directory.</strong></span>  <span style="color: #D83931"><strong>Enter your access key ID and secret access key at the beginning of the code.</strong></span>

```Python
from concurrent.futures import ThreadPoolExecutor, as_completed 
from volcengine.viking_db import *  # Make sure that you have installed volcengine by running the following command: pip install --upgrade volcengine. 

# Initialize the SDK. 
vikingdb_service = VikingDBService( 
    host="api-vikingdb.volces.com", # Do not include the protocol (like http:// or https://) in this parameter. 
    region="cn-beijing", # Configure this parameter as needed, such as cn-beijing for the North China region or cn-shanghai for the East China region. 
    scheme="https", # This parameter is optional. You can set it to http or https. However, we recommend that you set it to https. 
    connection_timeout=30, # This parameter defaults to 30 seconds. You can modify it as needed. 
    socket_timeout=30 # This parameter defaults to 30 seconds. You can modify it as needed. 
) 

vikingdb_service.set_ak("Enter your access key ID, with the double quotes retained.") 
vikingdb_service.set_sk("Enter your secret access key, with the double quotes retained.") 


## Data uploading ## 
# Specify the file path. 
file_path = "WOS_Data_1000.jsonl"  # The preprocessed JSONL file. 

# Initialize the VikingDB service and specify the collection. 
collection = vikingdb_service.get_collection("tagging_best_practice") 

def do_upsert(record, collection): 
    """ 
    Call upsert_data to upload one row of data to VikingDB. 
    """ 
    data = Data(record)  # Use the entire record. 
    collection.upsert_data([data]) 
    print(f"Record {record.get('ID', 'unknown')} is successfully uploaded. ") 

def concurrent_upload_jsonl(file_path, collection, max_workers=50): 
    """ 
    Use a thread pool to concurrently read rows of data from the JSONL file and write them to VikingDB. 
    :param file_path: the path of the JSONL file 
    :param collection: the initialized VikingDB collection 
    :param max_workers: the maximum number of worker threads, which defaults to 50 
    """ 
    with ThreadPoolExecutor(max_workers=max_workers) as executor: 
        futures = [] 
        with open(file_path, "r", encoding="utf-8") as f: 
            for line in f: 
                record = json.loads(line.strip()) 
                future = executor.submit(do_upsert, record, collection) 
                futures.append(future) 

        # Wait for all threads to complete their tasks. 
        for future in as_completed(futures): 
            try: 
                future.result() 
            except Exception as e: 
                print(f"An error occurred during the upload: {e}") 

    print("All data are uploaded. ") 

# Start uploading data. 
concurrent_upload_jsonl(file_path, collection, max_workers=50)
```


**After the upload, wait a moment for the data to synchronize**. The row count for the tagging_best_practice collection will update on the Collection page, but note that the value may be temporarily inaccurate due to synchronization delays.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2453b15a71b04fb8bc5eea5b1158fd85~tplv-goo7wpa0wc-image.image" width="706px" /></div>


<span id="7fcf5604"></span>
## 2.7 Create an index

You can create an index through the console or the SDK for Python.

After you run the preceding code, the number of indexes for the tagging_best_practice collection displayed on the Collection page of the VikingDB vector database becomes 1, which indicates that one index has been created.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02b449b62f7c45e4a19d16363af43385~tplv-goo7wpa0wc-image.image" width="781px" /></div>


On the Index page of the VikingDB vector database, the newly created index whose name is tagging_best_practice_abstract_index appears.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bdf890896cf14379b87b97b3281ed61b~tplv-goo7wpa0wc-image.image" width="1616px" /></div>


It takes a few minutes to initialize an index. Once the status of the index displayed in the Status column on the Index page of the VikingDB vector database becomes Ready, you can use the index to retrieve data.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8b90abd2a1e4542966ef6ae105c2e5b~tplv-goo7wpa0wc-image.image" width="1608px" /></div>


`}\></Tabs.TabPane\>);

```Plain

<span id="b9e8f683"></span>

###

<span id="cc427445"></span>

## 2.8 Test vector retrieval

You can test vector retrieval through the console or the SDK for Python.

```mixin-react
return (<Tabs> 
<Tabs.TabPane title="Console" key="UYYiWCVUU0"><RenderMd content={`After uploading the data and creating an index, you can test the effectiveness of vector retrieval. 
In this example, the abstract of the first row of data from the WOS_Data_Untagged_20.xlsx file, which was not uploaded, is used as the input. Its domain tag is CS and its area tag is Cryptography. 
<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec6b6e26dda14df499e1343bb9a32717~tplv-goo7wpa0wc-image.image" name="WOS_Data_Untagged_20.xlsx" ></Attachment> 
> **Retrieval principle and standard** 

> * **Retrieval principle**: The input abstract is embedded into a vector to represent its semantics. Then, the VikingDB vector database searches the stored data for the vector that is most similar to the vector of the input abstract and returns the retrieved vector. The abstract corresponding to the retrieved vector is the search result. A high vector similarity between the input and output abstracts indicates their strong similarity in semantics. 
> * **Retrieval standard**: The WOS_Data_Untagged_20.xlsx file is not uploaded to the VikingDB vector database. Therefore, if the retrieved abstract has the same tags as the input abstract, vector retrieval successfully found semantically similar data. 

On the Index page of the VikingDB vector database, click Retrieval test next to the newly created index. 
<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b034ba76d1274d209a740ab21a9c223f~tplv-goo7wpa0wc-image.image" width="2932px" /></div> 


In the Query text input box, enter the following data. The data is the abstract of the first row of data in the WOS_Data_Untagged_20.xlsx file. Its domain tag is CS and its area tag is Cryptography. 
```Python 
A three-party scheme for secure quantum communication, namely controlled quantum dialogue (CQD), is analyzed under the influence of non-Markovian channels. By comparing with the corresponding Markovian cases, it is seen that the average fidelity can be maintained for relatively longer periods of time. Interestingly, a number of facets of quantum cryptography, such as quantum secure direct communication, deterministic secure quantum communication and their controlled counterparts, quantum dialogue, quantum key distribution, quantum key agreement, can be reduced from the CQD scheme. Therefore, the CQD scheme is analyzed under the influence of damping, dephasing and depolarizing non-Markovian channels, and subsequently, the effect of these non-Markovian channels on the other schemes of secure quantum communication is deduced from the results obtained for CQD. The damped non-Markovian channel causes a periodic revival in the fidelity, while fidelity is observed to be sustained under the influence of the dephasing non-Markovian channel. 
```


Click Search at the bottom to view the search results on the right side.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1210c77ef61472992e0f45240ddae15~tplv-goo7wpa0wc-image.image" width="1459px" /></div>


The first search result has the same domain and area tags as the input data, which indicates that vector retrieval successfully found semantically similar data.

`}> <tabs.tabpane title="SDK for Python" key="fLNU4lAuzT"><rendermd content="{</span"><span data-node>After uploading the data and creating an index, you can test the effectiveness of vector retrieval. In this example, the abstract of the first row of data from the WOS_Data_Untagged_20.xlsx file, which was not uploaded, is used as the input. Its domain tag is CS and its area tag is Cryptography.`

> **Retrieval principle and standard**

> **Retrieval principle**: The input abstract is embedded into a vector to represent its semantics. Then, the VikingDB vector database searches the stored data for the vector that is most similar to the vector of the input abstract and returns the retrieved vector. The abstract corresponding to the retrieved vector is the search result. A high vector similarity between the input and output abstracts indicates their strong similarity in semantics.

> **Retrieval standard**: The WOS_Data_Untagged_20.xlsx file is not uploaded to the VikingDB vector database. Therefore, if the retrieved abstract has the same tags as the input abstract (the domain tag of CS and the area tag of Cryptography), this indicates that vector retrieval successfully found semantically similar data.


```Python
from volcengine.viking_db import *  # Make sure that you have installed volcengine by running the following command: pip install --upgrade volcengine. 

# Initialize the SDK. 
vikingdb_service = VikingDBService( 
    host="api-vikingdb.volces.com", # Do not include the protocol (like http:// or https://) in this parameter. 
    region="cn-beijing", # Configure this parameter as needed, such as cn-beijing for the North China region or cn-shanghai for the East China region. 
    scheme="https", # This parameter is optional. You can set it to http or https. However, we recommend that you set it to https. 
    connection_timeout=30, # This parameter defaults to 30 seconds. You can modify it as needed. 
    socket_timeout=30 # This parameter defaults to 30 seconds. You can modify it as needed. 
) 

vikingdb_service.set_ak("Enter your access key ID, with the double quotes retained.") 
vikingdb_service.set_sk("Enter your secret access key, with the double quotes retained.") 


## Retrieval test ## 
# Obtain the specified index. 
index = vikingdb_service.get_index( 
    "tagging_best_practice", # The name of the collection. 
    "tagging_best_practice_abstract_index" # The name of the index. 
) 

# Input the query text. 
# (Use the abstract of the first row of data in the WOS_Data_Untagged_20.xlsx file, whose domain tag is CS and whose area tag is Cryptography.) 
search_input = """ 
A three-party scheme for secure quantum communication, namely controlled quantum dialogue (CQD), is analyzed under the influence of non-Markovian channels. By comparing with the corresponding Markovian cases, it is seen that the average fidelity can be maintained for relatively longer periods of time. Interestingly, a number of facets of quantum cryptography, such as quantum secure direct communication, deterministic secure quantum communication and their controlled counterparts, quantum dialogue, quantum key distribution, quantum key agreement, can be reduced from the CQD scheme. Therefore, the CQD scheme is analyzed under the influence of damping, dephasing and depolarizing non-Markovian channels, and subsequently, the effect of these non-Markovian channels on the other schemes of secure quantum communication is deduced from the results obtained for CQD. The damped non-Markovian channel causes a periodic revival in the fidelity, while fidelity is observed to be sustained under the influence of the dephasing non-Markovian channel. 
""" 

# Call search_by_text to search the stored abstracts by text. 
res = index.search_by_text( 
    Text(text=search_input), # The query text. 
    limit=10, # The maximum number of search results. 
    output_fields=["ID", "domain", "area", "abstract"] # The fields to return. 
) 

# Print the results. 
for item in res: 
    print(item.fields) 
```


As shown in the following response, the first search result has the same domain and area tags as the input data, which indicates that vector retrieval successfully found semantically similar data.

```Python
{ 
'ID': 963, 
'abstract': 'A notion of asymmetric quantum dialogue (AQD) is introduced. Conventional protocols of quantum dialogue are essentially symmetric as the users (Alice and Bob) can encode the same amount of classical information. In contrast, the proposed scheme for AQD provides different amount of communication powers to Alice and Bob. The proposed scheme offers an architecture, where the entangled state to be used and the encoding scheme to be shared between Alice and Bob depend on the amount of classical information they want to exchange with each other. The general structure for the AQD scheme has been obtained using a group theoretic structure of the operators introduced in Shukla et al. (Phys Lett A 377: 518, 2013). The effect of different types of noises (e.g., amplitude damping and phase damping noise) on the proposed scheme is investigated, and it is shown that the proposed scheme for AQD is robust and it uses an optimized amount of quantum resources.', 
'area': 'Cryptography', 
'domain': 'CS' 
} 
```


If the following error occurs, the index has not been initialized. In this case, wait and try again later.

```Python
volcengine.viking_db.exception.IndexNotReadyException: message:failed to index_recall, index is not ready, code:1000023, 
```


`}\></Tabs.TabPane\>);

```Plain

<span id="e0e0cae6"></span>

###

<span id="a5f13a6c"></span>

## 2.9 Integrate a Doubao LLM for auto-tagging

Before integrating a Doubao LLM, you must obtain an API key and an inference endpoint for it.

1.  **Create and obtain an API key for integrating a Doubao LLM.**

Register a BytePlus account and log in to [ModelArk](https://console.volcengine.com/auth/login?redirectURI=%2Fark%2Fregion%3Aark%2Bcn-beijing%2FapiKey%3Fapikey%3D%257B%257D%26projectName%3Dundefined). On the API keys page, click Create API key.

<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39d297939a624997b67e05976fda32fd~tplv-goo7wpa0wc-image.image" width="2938px" /></div>

Enter a name for the API key and click Create.

<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2af658fd2684f32a4df25bce8c4e2cd~tplv-goo7wpa0wc-image.image" width="2940px" /></div>

Then, you can click the copy icon to obtain the API key.

<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4abe70d9874b4eca906031368555646c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>

2.  **Create an inference endpoint for a Doubao LLM.**

Register a BytePlus account and log in to [ModelArk](https://console.volcengine.com/auth/login?redirectURI=%2Fark%2Fregion%3Aark%2Bcn-beijing%2Fendpoint%3Fconfig%3D%257B%257D). On the Online inference page, click Create inference endpoint.

<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5103ab3dd272411b9efcd7109ea06b4f~tplv-goo7wpa0wc-image.image" width="2940px" /></div>

Enter a name and a description for the endpoint and click Add model.

<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22be35d7d7a24c198176eb8cd44621cd~tplv-goo7wpa0wc-image.image" width="2940px" /></div>

We recommend that you select Doubao-pro-256k.

<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2271137b9c644ff1bae5159b8e50f897~tplv-goo7wpa0wc-image.image" width="2940px" /></div>

Click Integrate.

<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5050584b3ffa41d599a038dde9f6b5ee~tplv-goo7wpa0wc-image.image" width="2940px" /></div>

Click API calling next to the newly created endpoint.

<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/292957686553452398274644708023a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>

Copy your inference endpoint, which is similar to ep-****** displayed in the following code.

<div style="text-align: center"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec3f9daa8f714a5a9d7f8acd1c47aedf~tplv-goo7wpa0wc-image.image" width="2940px" /></div>

In this example, the abstract of the seventh row of data in the WOS_Data_Untagged_20.xlsx file is used as the value of input_abstract for test purposes. For the abstract, its domain tag is Civil and its area tag is Water Pollution.  <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a88cb0363bc416e9adb2456cbffb03a~tplv-goo7wpa0wc-image.image" name="WOS_Data_Untagged_20.xlsx" ></Attachment> 
If the result is "domain": "Civil", "area": "Water Pollution," the solution is effective.  <span style="color: #D83931"><strong>Note:</strong></span>  <span style="color: #D83931"><strong>Enter your API key and inference endpoint at the beginning of the code.</strong></span>  <span style="color: #D83931"><strong>Enter your access key ID and secret access key at the beginning of the code.</strong></span>

```Python
from collections import Counter 
from volcengine.viking_db import *  # Make sure that you have installed volcengine by running the following command: pip install --upgrade volcengine. 
from volcenginesdkarkruntime import Ark  # Make sure that you have installed Ark by running the following command: pip install --upgrade 'volcengine-python-sdk[ark]'. 

## Integration of a Doubao LLM for auto-tagging ## 
# Specify the API key of the Doubao LLM. 
Doubao_API_key = "Enter your API key of the Doubao LLM, with the double quotes retained." 
# Specify the inference endpoint of the Doubao LLM. 
model_end_point = "Enter your inference endpoint, with the double quotes retained." 
# Specify an abstract from the WOS_Data_Untagged_20.xlsx file, which was not uploaded, to tag. 
input_abstract = "A total of 211 water samples were collected from 53 key sampling points from 5-10th July 2013 at four different depths (0 m, 2 m, 4 m, 8 m) and at different sites in the Huaihe River, Anhui, China. These points were monitored for 18 parameters (water temperature, pH, TN, TP, TOC, Cu, Pb, Zn, Ni, Co, Cr, Cd, Mn, B, Fe, Al, Mg, and Ba). The spatial variability, contamination sources and health risk of trace elements as well as the river water quality were investigated. Our results were compared with national (CSEPA) and international (WHO, USEPA) drinking water guidelines, revealing that Zn, Cd and Pb were the dominant pollutants in the water body. Application of different multivariate statistical approaches, including correlation matrix and factor/principal component analysis (FA/PCA), to assess the origins of the elements in the Huaihe River, identified three source types that accounted for 79.31% of the total variance. Anthropogenic activities were considered to contribute much of the Zn, Cd, Pb, Ni, Co, and Mn via industrial waste, coal combustion, and vehicle exhaust; Ba, B, Cr and Cu were controlled by mixed anthropogenic and natural sources, and Mg, Fe and Al had natural origins from weathered rocks and crustal materials. Cluster analysis (CA) was used to classify the 53 sample points into three groups of water pollution, high pollution, moderate pollution, and low pollution, reflecting influences from tributaries, power plants and vehicle exhaust, and agricultural activities, respectively. The results of the water quality index (WO) indicate that water in the Huaihe River is heavily polluted by trace elements, so approximately 96% of the water in the Huaihe River is unsuitable for drinking. A health risk assessment using the hazard quotient and index (HQ/HI) recommended by the USEPA suggests that Co, Cd and Pb in the river could cause non-carcinogenic harm to human health. (C) 2017 Elsevier B.V. All rights reserved." 

# Initialize the SDK. 
vikingdb_service = VikingDBService( 
    host="api-vikingdb.volces.com", # Do not include the protocol (like http:// or https://) in this parameter. 
    region="cn-beijing", # Configure this parameter as needed, such as cn-beijing for the North China region or cn-shanghai for the East China region. 
    scheme="https", # This parameter is optional. You can set it to http or https. However, we recommend that you set it to https. 
    connection_timeout=30, # This parameter defaults to 30 seconds. You can modify it as needed. 
    socket_timeout=30 # This parameter defaults to 30 seconds. You can modify it as needed. 
) 

vikingdb_service.set_ak("Enter your access key ID, with the double quotes retained.") 
vikingdb_service.set_sk("Enter your secret access key, with the double quotes retained.") 

# Initialize the Ark client. 
client = Ark( 
    base_url="https://ark.cn-beijing.volces.com/api/v3", # The API address of the ModelArk service. 
    api_key=Doubao_API_key # Your API key. 
) 

# Input a system prompt and a user query to get the output of the Doubao LLM. 
def ask_doubao(system_prompt,user_query): 
    # Call chat.completions to start a dialogue task. 
    completion = client.chat.completions.create( 
        model=model_end_point,  # The endpoint of the model. 
        messages=[ 
            {"role": "system", "content": system_prompt},  # system prompt 
            {"role": "user", "content": user_query},  # user query 
        ], 
    ) 
    return completion.choices[0].message.content 

# Obtain the specified index. 
index = vikingdb_service.get_index( 
    "tagging_best_practice", # The name of the collection. 
    "tagging_best_practice_abstract_index" # The name of the index. 
) 

# Retrieve from the vector database the 10 abstracts most similar to the input abstract, as well as their first-level domain tags and second-level area tags, for the Doubao LLM to use as a reference when tagging the input abstract. 
related_abstract_domain_area = index.search_by_text( 
    Text(text=input_abstract), # The query text. 
    limit=10, # The maximum number of search results to return. 
    output_fields=["domain", "area"] # The fields to return. 
) 

search_result = [] # The search results. 
# Add all search results to the list. 
for item in related_abstract_domain_area: 
    search_result.append(item.fields) 

# Calculate the frequency of each domain and area tag. 
domain_counter = Counter(item['domain'] for item in search_result) 
area_counter = Counter(item['area'] for item in search_result) 

# Sort tags by frequency and deduplicate them. 
unique_domains = [domain for domain, count in domain_counter.most_common()] 
unique_areas = [area for area, count in area_counter.most_common()] 

# Specify a system prompt for the Doubao LLM to tag the input abstract. 
recommond_tags_system_prompt = f""" 
## Role 
- You are a classifier capable of analyzing, classifying, and tagging user-input abstracts. 

## Task 
- Analyze and classify a user-input abstract to output a domain tag and an area tag for it. 

## All tags 
- All domain tags: ['CS', 'Medical', 'Civil', 'ECE', 'biochemistry', 'MAE', 'Psychology']; 
- All area tags: ['Symbolic computation', "Alzheimer's Disease", 'Green Building', 'Electric motor', "Parkinson's Disease", 'Computer vision', 'Molecular biology', 'Satellite radio', 'Fluid mechanics', 'Prenatal development', 'Sprains and Strains', 'Enzymology', 'Southern blotting', 'Cancer', 'Northern blotting', 'Sports Injuries', 'Senior Health', 'Computer graphics', 'Digital control', 'Human Metabolism', 'Polymerase chain reaction', 'Multiple Sclerosis', 'Operating systems', 'Microcontroller', 'Attention', 'Immunology', 'Genetics', 'Water Pollution', 'Hydraulics', 'Hepatitis C', 'Weight Loss', 'Machine learning', 'Low Testosterone', 'Fungal Infection', 'Diabetes', 'Data structures', 'Cell biology', 'Parenting', 'Birth Control', 'Smart Material', 'network security', 'Heart Disease', 'computer-aided design', 'Image processing', 'Parallel computing', 'Ambient Intelligence', 'Allergies', 'Menopause', 'Emergency Contraception', 'Electrical network', 'Construction Management', 'Distributed computing', 'Electrical generator', 'Electricity', 'Operational amplifier', 'Manufacturing engineering', 'Analog signal processing', 'Skin Care', 'Eating disorders', 'Myelofibrosis', 'Suspension Bridge', 'Machine design', 'Hypothyroidism', 'Headache', 'Overactive Bladder', 'Geotextile', 'Irritable Bowel Syndrome', 'Polycythemia Vera', 'Atrial Fibrillation', 'Smoking Cessation', 'Lymphoma', 'Thermodynamics', 'Asthma', 'State space representation', 'Bipolar Disorder', 'Materials Engineering', 'Stealth Technology', 'Solar Energy', 'Signal-flow graph', "Crohn's Disease", 'Borderline personality disorder', 'Prosocial behavior', 'False memories', 'Idiopathic Pulmonary Fibrosis', 'Electrical circuits', 'Algorithm design', 'Strength of materials', 'Problem-solving', 'Internal combustion engine', 'Lorentz force law', 'Prejudice', 'Antisocial personality disorder', 'System identification', 'Computer programming', 'Nonverbal communication', 'Relational databases', 'PID controller', 'Voltage law', 'Leadership', 'Child abuse', 'Mental Health', 'Dementia', 'Rheumatoid Arthritis', 'Osteoporosis', 'Software engineering', 'Bioinformatics', 'Medicare', 'Control engineering', 'Psoriatic Arthritis', 'Addiction', 'Atopic Dermatitis', 'Digestive Health', 'Remote Sensing', 'Gender roles', 'Rainwater Harvesting', 'Healthy Sleep', 'Depression', 'Social cognition', 'Anxiety', 'Cryptography', 'Psoriasis', 'Ankylosing Spondylitis', "Children's Health", 'Stress Management', 'Seasonal affective disorder', 'HIV/AIDS']; 

## Recommended tags 
- Recommended domain tags: {unique_domains}; 
- Recommended area tags: {unique_areas}; 

## Requirements 
- Break the user-input abstract down to analyze its content, domain, and area step by step. 
- Each abstract can have only one domain tag and one area tag. 
- Preferentially select recommended tags for the user-input abstract. 
- If none of the recommended tags is suitable after analysis, select other tags from the list of all tags for the user-input abstract. 
- Output the result in the following JSON format. 

## Output format 
{{"analysis": "analysis of what the abstract is about and how to tag the abstract", "domain": "a domain tag", "area": "an area tag"}} 
""" 

# Tag the input abstract. 
tagging_result = ask_doubao(recommond_tags_system_prompt,input_abstract) 
print(tagging_result)
```


The output is as follows:

```Python
{ 
"analysis": "The abstract focuses on the 211 water samples collected from 53 key sampling points at different sites in the Huaihe River, Anhui, China. These sampling points monitored 18 parameters to investigate the spatial variability, contamination sources, and health risks of trace elements, as well as river water quality. The abstract also includes the comparison of the results against the national and international drinking water standards, the analysis of the sources of the trace elements based on various statistical approaches, and the classification of the sampling points by water pollution level based on cluster analysis. All these are related to water pollution research. Therefore, from the recommended tags, Civil is selected as the domain tag and Water Pollution is selected as the area tag.", 
"domain": "Civil", 
"area": "Water Pollution" 
}
```


As shown in the preceding input and output, the correct tag combination of `"domain": "Civil", "area": "Water Pollution"` has been successfully selected from the 882 (7 × 126) possible tag combinations.
