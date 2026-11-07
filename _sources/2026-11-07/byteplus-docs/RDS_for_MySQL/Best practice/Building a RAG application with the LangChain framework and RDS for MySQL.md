---
title: "Building a RAG application with the LangChain framework and RDS for MySQL"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Building_a_RAG_application_with_the_LangChain_framework_and_RDS_for_MySQL"
---

<span id="xvOlUtzD"></span>
## Overview

This topic provides a step\-by\-step guide on how to build a complete Retrieval\-Augmented Generation (RAG) application using the LangChain framework with BytePlus RDS for MySQL as the vector storage. You will use the Embedding and LLM models provided by BytePlus Ark and simplify the operation by using the langchain\-volcengine\-mysql integration library.

After completing this topic, you will understand the entire process, from preparing the environment, ingesting data, and retrieving vectors, to building a complete question\-answering (QA) chain. You will also learn some best practices for production deployment.

<span id="RSlLLXBQ"></span>
### Architecture

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8d792090a0a82a70f92ad2ebadc92965.png) </span>

<span id="bhSnYk8j"></span>
## Procedure


1. ### Prepare the environment and install the dependencies <span id="3t88CJF7"></span>


Before you start, ensure that Python 3.8 or a later version is installed. Then, we need to install all the required dependencies. These libraries include LangChain core components, the BytePlus Ark SDK, and the LangChain integration library for MySQL.

Open your client and run the following command:

```Bash
pip install langchain langchain-core langchain-classic langchain-volcengine-mysql pymysql

pip install --upgrade "volcengine-python-sdk[ark]"
```


**Dependency descriptions**


* langchain, langchain\-core, langchain\-classic: The core LangChain framework that provides various tools for building RAG applications.

* volcengine\-python\-sdk[ark]\": The official Python SDK for the BytePlus Ark platform, used to call Embedding and LLM models.

* langchain\-volcengine\-mysql: The core of this tutorial, providing the ability to use RDS for MySQL as a LangChain vector storage and Retriever.

* pymysql: A Python driver for connecting to MySQL databases.

2. ### Security configuration: set the environment variables <span id="vzlTYUwG"></span>


To keep your keys and database credentials secure, it is highly recommended to manage this sensitive information with environment variables rather than hardcoding them in your code. This is not only more secure, but also makes it easier to switch configurations in different environments (development, test, and production).


1. #### Set up environmental variables <span id="bMDWco3b"></span>


Set the following environment variables in your development environment. You can add them to your .bashrc or .zshrc files, or export them manually before running the script.

```Bash
# BytePlus Ark API Key
export ARK_API_KEY="YOUR_ARK_API_KEY"

# RDS for MySQL database connection information
export MYSQL_HOST="YOUR_MYSQL_HOST"
export MYSQL_PORT="3306" # Usually 3306
export MYSQL_USER="YOUR_MYSQL_USER"
export MYSQL_PASSWORD="YOUR_MYSQL_PASSWORD"
export MYSQL_DATABASE="YOUR_MYSQL_DATABASE"

# BytePlus model configuration
export EMBEDDING_MODEL="YOUR_EMBEDDING_MODEL_ENDPOINT_ID"
export LLM_MODEL="YOUR_LLM_MODEL_ENDPOINT_ID"
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">ARK_API_KEY: Obtain it from the BytePlus Ark console.</div>


* <div data-tips="true" data-tips-type="default">MYSQL_\*: These are the connection information for your RDS for MySQL instance.</div>


* <div data-tips="true" data-tips-type="default">EMBEDDING_MODEL and LLM_MODEL: These are the endpoint IDs of the models you deployed on the Ark platform.</div>


2. #### Read environment variables in code <span id="kp5QhCOB"></span>


In Python scripts, you can use the `os` module to easily read these environment variables.

```Python
import os

# Read Ark API Key
ARK_API_KEY = os.getenv("ARK_API_KEY")

# Read Database configuration
MYSQL_CONFIG = {
    "host": os.getenv("MYSQL_HOST"),
    "port": int(os.getenv("MYSQL_PORT", 3306)),
    "user": os.getenv("MYSQL_USER"),
    "password": os.getenv("MYSQL_PASSWORD"),
    "database": os.getenv("MYSQL_DATABASE"),
}

# Read model configuration
EMBEDDING_MODEL = os.getenv("EMBEDDING_MODEL")
LLM_MODEL = os.getenv("LLM_MODEL")
```



3. ### Initialize the client and Embeddings <span id="MYkqDRer"></span>


Next, we need to initialize the connection to the BytePlus Ark service and create a custom Embedding class to handle rate limiting issues during vector generation.


1. #### Initialize the Ark client <span id="yxpnJKZH"></span>


```Python
from volcenginesdkarkruntime import Ark

# Initialize the Ark client
# The SDK automatically reads the secret key from the `ARK_API_KEY` environment variable
ark_client = Ark()
```



2. #### Customize the Embeddings class <span id="3LJg043W"></span>


Although LangChain provides an official BytePlus Embedding wrapper, you may be rate\-limited due to a high request frequency during actual calls. To make the application more robust, create a wrapper class that includes automatic retry and exponential backoff logic.

```Python
import time
from typing import List
from langchain_core.embeddings import Embeddings

class CustomArkEmbeddings(Embeddings):
    """带有限流重试逻辑的BytePlus Ark Embeddings 封装"""

    def __init__(self, client: Ark, model: str):
        self.client = client
        self.model = model

    def embed_documents(self, texts: List[str]) -> List[List[float]]:
        max_retries = 3
        retry_delay = 2  # seconds

        for attempt in range(max_retries):
            try:
                resp = self.client.embeddings.create(
                    model=self.model,
                    input=texts
                )
                return [data.embedding for data in resp.data]
            except Exception as e:
                if attempt == max_retries - 1:
                    raise
                print(f"请求被限流，将在 {retry_delay} 秒后重试... (尝试次数 {attempt + 1}/{max_retries})")
                time.sleep(retry_delay)
                retry_delay *= 2  # Exponential backoff

    def embed_query(self, text: str) -> List[float]:
        return self.embed_documents([text])[0]

# Instantiate our custom Embeddings
embeddings = CustomArkEmbeddings(client=ark_client, model=EMBEDDING_MODEL)
```



4. ### Configure the MySQL vector database <span id="pp5lzxe0"></span>


This is a key step in integrating MySQL into the LangChain ecosystem. The langchain\-volcengine\-mysql package provides a convenient mysql.configure function, allowing you to complete all configurations with just a few lines of code.


1. #### Use mysql.configure <span id="CbHD68Qw"></span>


This function automatically creates or connects to the specified table in the database based on your configuration, and prepares the vector_store and retriever objects.

```Python
from langchain_volcengine_mysql import mysql

# Configure the vector store
mysql.configure(
    host=MYSQL_CONFIG["host"],
    port=MYSQL_CONFIG["port"],
    user=MYSQL_CONFIG["user"],
    password=MYSQL_CONFIG["password"],
    database=MYSQL_CONFIG["database"],
    table_name="rag_tutorial_documents", # Custom table name
    embedding_function=embeddings, # Pass in the instantiated embedding object
    embedding_dim=1024 # **Important**: The dimension must be consistent with the selected Embedding model.
)

# Obtain vector_store and retriever from the mysql module
vector_store = mysql.vector_store
retriever = mysql.retriever

print("✓ RDS MySQL 向量库配置成功！")
print(f"使用的表名: {vector_store.table_name}")
```


**mysql.configure parameter details**


* host, port, user, password, database: Standard database connection parameters.

* table_name: The name of the table used for storing vectors and documents. If the table does not exist, the library creates it automatically.

* embedding_function: A LangChain Embeddings object used to convert text into vectors. Here, we pass in the previously created CustomArkEmbeddings instance.

* embedding_dim: The output dimension of the Embedding model. This is a very important parameter that must exactly match the model dimension specified in EMBEDDING_MODEL, or a database error will occur. For example, the dimension of the bge\-large\-zh model is 1024.

5. ### Preparing and writing document data <span id="om8WTlPi"></span>


After the vector database is configured, you can add documents to it. The data storage process involves constructing a list of Document objects and then calling the vector_store.add_documents method.


1. #### Construct a document list <span id="oYTewSb3"></span>


Each document object contains two parts: page_content (the document body) and metadata. Metadata is useful for later filtering and traceability.

```Python
from langchain_core.documents import Document

test_data = [
    {
        "content": "veDB for MySQL 是BytePlus提供的一种云原生、高性能的数据库服务。它为现代应用提供了自动扩缩容、高可用和卓越的性能。",
        "metadata": {"source": "product_docs", "category": "database", "version": "1.0"}
    },
    {
        "content": "LangChain 是一个用于构建大语言模型应用的框架。它提供了处理 LLM、向量存储、嵌入和构建复杂链的工具。",
        "metadata": {"source": "tech_blog", "category": "framework", "version": "0.1"}
    },
    {
        "content": "向量数据库能够为 AI 应用实现高效的相似性搜索。它们存储高维向量，并允许使用 HNSW 等算法快速检索相似向量。",
        "metadata": {"source": "research_paper", "category": "ai", "version": "2.0"}
    }
]

documents = [Document(page_content=doc["content"], metadata=doc["metadata"]) for doc in test_data]
```



2. #### Add to storage and verifying <span id="7FFKP6j9"></span>


Call the add_documents method to convert the document content into vectors and store them with the metadata in a MySQL table.

```Python
# Add the document to the vector store.
document_ids = vector_store.add_documents(documents)
print(f"成功添加 {len(document_ids)} 个文档。")

# Wait for a moment to ensure data writing is Completed.
import time
time.sleep(2)

# Perform a similarity Search to verify.
query = "什么是 veDB?"
results = vector_store.similarity_search(query, k=1)

print(f"\n对查询 '{query}' 的搜索结果:")
for doc in results:
    print(f"- 内容: {doc.page_content[:50]}...")
    print(f"  来源: {doc.metadata['source']}")
```



6. ### Build an RAG question\-answering chain <span id="LDVE6W7O"></span>


Now, we have a vector database filled with knowledge. The final step is to assemble the retriever, LLM, and a PromptTemplate into a complete RAG question\-answering chain.


1. #### Initialize the LLM <span id="0qHDi3K9"></span>


First, we need an LLM to generate the final answer. Here, we also wrap a simple VolcengineLLM class.

```Python
from langchain_core.runnables import Runnable
from typing import Optional, Any

class VolcengineLLM(Runnable):
    def __init__(self, client: Ark, model: str):
        self.client = client
        self.model = model

    def invoke(self, input: Any, config: Optional[dict] = None, **kwargs) -> str:
        prompt = str(input)
        try:
            completion = self.client.chat.completions.create(
                model=self.model,
                messages=[{"role": "user", "content": prompt}]
            )
            return completion.choices[0].message.content
        except Exception as e:
            print(f"调用 LLM 时出错: {e}")
            raise

llm = VolcengineLLM(client=ark_client, model=LLM_MODEL)
```



2. #### Create a prompt template <span id="PWzVyyu2"></span>


A good prompt template can guide the LLM on how to use the retrieved context to answer the problem.

```Python
from langchain_core.prompts import PromptTemplate

prompt_template = """你是一个乐于助人的人工智能助手。请根据以下上下文信息来回答问题。
如果根据上下文无法回答，就说你不知道，不要编造答案。

上下文:
{context}

问题: {question}

回答:"""

PROMPT = PromptTemplate(
    template=prompt_template, input_variables=["context", "question"]
)
```



3. #### Assemble and testing the QA chain <span id="GHl5kNRo"></span>


LangChain's RetrievalQA chain can easily integrate all components.

```Python
from langchain_classic.chains import RetrievalQA

qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff", # The "stuff" type inserts all retrieved document content into the Prompt.
    retriever=retriever,
    return_source_documents=True, # Returns the source document for traceability.
    chain_type_kwargs={"prompt": PROMPT}
)

# Test our RAG chain.
question = "veDB for MySQL 有哪些特点？"
result = qa_chain.invoke({"query": question})

print(f"问题: {question}")
print(f"\n答案: {result['result']}")
print("\n来源文档:")
for doc in result['source_documents']:
    print(f"- [{doc.metadata['source']}] {doc.page_content[:60]}...")
```



7. ### Cleanup and production considerations <span id="SQ93j95z"></span>


langchain\-volcengine\-mysql provides a method for data cleanup, but use it with caution in a production environment.


1. #### **Delete by ID** <span id="IRMb99Td"></span>


To delete specific documents, use the `delete` method and pass in a list of document IDs.

```Python
# Delete the previously added document
print(f"准备删除 {len(document_ids)} 个文档...")
vector_store.delete(ids=document_ids)
print("✓ 文档已删除。")
```



2. #### **Delete an entire table** <span id="DDwwjLMD"></span>


The `drop_table` method permanently deletes the entire table that stores vectors. **This is a dangerous operation. Use it only in test and development environments.** 

```Python
# Warning: This operation deletes the entire table!
print(f"准备删除表 '{vector_store.table_name}'...")
# vector_store.drop_table()
print("✓ 表已删除（操作已注释）。")
```


**Best practices for production environments**


* **Logical deletion**: In production environments, it is recommended to use logical deletion (adding an `is_deleted` field in the metadata) instead of physical deletion to facilitate data recovery and auditing.

* **Privilege control**: Minimize database user privileges. Grant only the SELECT, INSERT, UPDATE, and DELETE privileges required for RAG, and avoid granting high\-risk privileges such as DROP or CREATE.

* **Backups**: Back up your database regularly.


<span id="TOgOgdxE"></span>
## FAQs and troubleshooting


|Problem classification |Possible cause and solution |
|---|---|
|**Connection failed** |* **Check the network**: ensure your application server can access the RDS MySQL instance address and port.<br><br>* **Check the credentials**: ensure that the host, port, user, password, and database are correct.<br><br>* **Allowlists**: check if the application server's IP address has been added to the RDS MySQL IP allowlist. |
|**Privilege or table does not exist** |* **Insufficient permissions**: Confirm if the database user has SELECT, INSERT, UPDATE, and DELETE privileges on the target table, and the CREATE Privilege that might be required when creating the table for the first time.<br><br>* **Incorrect table name**: Check if table_name matches the actual table name in the database. |
|**Embedding dimension mismatch** |* **Error message**: You will typically see a database error like `Vector dimension mismatch`.<br><br>* **Solution**: Confirm that the `embedding_dim` parameter value in `mysql.configure` matches the output dimension of the Embedding model (EMBEDDING_MODEL). **This is one of the most common configuration errors.**  |
|**Model or API Key Error** |* **Invalid Endpoint ID**: Confirm that the values for EMBEDDING_MODEL and LLM_MODEL are correct model Endpoint IDs.<br><br>* **Invalid API Key**: Confirm that ARK_API_KEY is valid and has the Privilege to call your specified model. |
|**Dependency version conflict** |* **Checking the environment**: Use pip freeze to check if the library versions in the current environment are compatible with the requirements.<br><br>* **Creating a virtual environment**: As a best practice, create a separate Python virtual environment for each project to avoid dependency conflicts. |
