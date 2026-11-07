---
title: "Practice of learning to rank based on Cloud Search"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/learning-to-rank"
---

This topic uses BytePlus Cloud Search and the open\-source Metarank ranking tool to implement learning to rank in three stages: recall, ranking, and reranking. When users enter queries, personalized search and recommendation results are returned.

<span id="d2a98f7f"></span>
## Application scenarios

Learning to Rank (LTR) is a machine learning technique with broad application scenarios.


* In the **e\-commerce recommendation** field, it helps platforms analyze and model users’ purchase history, search records, browsing behavior, and other data.

* In the **advertising delivery** field, it helps search engines analyze and model users’ search keywords and provides the most precise and effective advertising solutions.

* In the **financial risk control** field, it helps institutions analyze customer credit ratings and fraud risks, improving risk control capabilities and operational efficiency.


<span id="9d53dc25"></span>
## Background introduction

The search process of BytePlus Cloud Search generally includes two stages: **recall + ranking**. Use the user\-entered text as keywords, apply the BM25 scoring algorithm, traverse the database to select the highest\-scoring documents, sort them, and then return the query results. Since the BM25 algorithm mainly considers factors such as term frequency and inverse document frequency, the search result ranking depends solely on the relevance to the retrieved text.

In most cases, using **recall + ranking** meets the requirements, but some scenarios require users to achieve personalization recommendations. To achieve personalization recommendations, introduce a **reranking** stage based on the existing recall and ranking. Compared to the first two stages, the reranking stage focuses more on user behavior. It uses feedback features such as clicks, favorites, and purchases, applies machine learning algorithms, automatically learns and adjusts parameters based on features and feedback, estimates user preferences for returned results, and ultimately achieves an effect combining personalization with search and recommendations. This ranking training process is also known as Learning to Rank (LTR).

In Volcengine Cloud Search Service ES, the reranking stage currently supports two methods: built\-in plugins and open\-source tools.


* **Use built\-in plugins**: Install the reranking stage as a plugin into the ES instance, such as the [elasticsearch-learning-to-rank](https://elasticsearch-learning-to-rank.readthedocs.io/en/latest/index.html) plugin.

   The user submits a query and receives search and recommendation results. The entire process remains transparent to the business; the business only needs to interact with the search service.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12b50777d92b4d8085d338ca4696ac66~tplv-goo7wpa0wc-image.image) </span>

* **Use open source tools**: the **recall + ranking** phase normally uses the ES instance, while the **reranking** phase uses open source tools, such as the [metarank](https://docs.metarank.ai/introduction/intro) tool.

   User inputs a query, obtains intermediate results through the ES instance's **recall + ranking** phase; then inputs the intermediate results to interact with the LTR model tool, finally returning the search recommendation results. The entire process requires the business side to handle intermediate results independently, completing interactions with the search engine service and the LTR model tool, offering greater flexibility.

   This article mainly introduces the process of implementing learning\-to\-rank using open source tools.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/750e746b8f114fc995cdec24b1d8f339~tplv-goo7wpa0wc-image.image) </span>


<span id="30576d1c"></span>
## Step one: prepare the environment


1. Log on to the [Cloud Search console](https://console.byteplus.com/es), then create an ES instance with version 7.10.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c900769741e42dba3d6ba7d604e7637~tplv-goo7wpa0wc-image.image) </span>

2. Install the Python Client dependencies.

   ```Python
   pip install -U elasticsearch7==7.10.1 # ES数据库相关
   pip install -U pandas #分析splash的csv
   ```
   


<span id="a228f775"></span>
## Step two: prepare the dataset

This article chooses the RankLens dataset recommended in the open source Metarank sorting tool documentation. You can download the original dataset [dataset/metadata.jsonl.gz](https://github.com/metarank/ranklens/blob/master/dataset/metadata.jsonl.gz).

After decompression, about 2,500 articles are obtained, each containing information such as movie posters, actors, and ratings. Example information is as follows:

```JSON
{
    ...
    "description": "When a rare phenomenon gives police officer John Sullivan the chance to speak to his father, 30 years in the past, he takes the opportunity to prevent his dad's tragic death.  After his actions inadvertently give rise to a series of brutal murders he and his father must find a way to fix the consequences of altering time.",
    "director": {
        "gender": 2,
        "id": 17812,
        "name": "Gregory Hoblit",
        "popularity": 1.62
    },
    "id": 3510,
    "overview": "When a rare phenomenon gives police officer John Sullivan the chance to speak to his father, 30 years in the past, he takes the opportunity to prevent his dad's tragic death.  After his actions inadvertently give rise to a series of brutal murders he and his father must find a way to fix the consequences of altering time.",
    "poster": "https://image.tmdb.org/t/p/original/eu3Hrjj271dnBdNAF0HqfmwWASt.jpg",
    "releaseDate": "2000-04-28",
    "tags": [
        "time travel",
        "father-son relationship",
        "alternate reality",
        "father son relationship",
        "supernatural"
    ],
    "title": "Frequency",
    "tmdbId": 10559,
    "tmdbPopularity": 10.95,
    "tmdbVoteAverage": 7.2,
    "tmdbVoteCount": 1254,
    "topActors": [
        {
            "gender": 1,
            "id": 31167,
            "name": "Elizabeth Mitchell",
            "popularity": 8.646
        },
        ...
    ]
}
```


<span id="f8de330d"></span>
## Step three: connect to ES instance


1. Obtain the instance access address on the ES instance details page.

2. Connect to the instance.

   ```Python
   # 连接 ES 实例。如果遗忘实例访问用户（admin）的密码，可以选择重置密码。
   cloudSearch = CloudSearch("https://{user}:{password}@{ES_URL}", 
                       verify_certs=False, 
                       ssl_show_warn=False)
   ```
   


<span id="149d6f71"></span>
## Step four: connect to Metarank service

Start the Metarank service locally.


* The dataset parameter ( **\-\-data**) specifies the transformed dataset, including metadata and user click\-through information.

* The configuration file parameter ( **\-\-config**) specifies the model configuration.


For parameter configuration and file download, refer to [Metarank Quickstart](https://docs.metarank.ai/introduction/quickstart).

```Bash
java -jar metarank-0.7.1.jar standalone --data events.jsonl.gz  --config events-config.yml
```


<span id="707cbd6d"></span>
## Step five: write the dataset

Write the RankLens dataset to the ES instance.

```Python
import json

path = '${下载的数据集所在路径}'
with open(path, 'r') as f:
  bulk_docs = []
  n = 0
  for line in f.readlines():
    doc = json.loads(line.rstrip())
    if 'title' in doc:
        n += 1
        bulk_docs.append({"index": {"_id": doc['id']}})
        bulk_docs.append(doc)
        
        ## 每次批量写入50条数据
        if n % 50 == 0:        
          resp = cloudSearch.bulk(bulk_docs, index='events2')
          bulk_docs = []  
```


<span id="ad657c44"></span>
## Verify results


1. Text query and Metarank reranking.

   ```Python
   @app.route('/search', methods=['GET'])
   def search():
       return innerSearch()
   
   def innerSearch():
       # 获取参数
       query = request.args.get('query')
       method = request.args.get('retrieval')
       n = int(request.args.get('size'))
       rank = request.args.get('rank')
       start = time.time()
       
       # 文本查询
       docs = retrieve(method, query, n) 
       done1 = time.time()
       if len(docs['hits']['hits']) == 0:
           return render_template('search.html', help=False, query=query, method=method, rank=rank, size=n, took={"search": 1000*(done1-start), "rank": 0, "total": 1000*(done1-start)})
   
       # Metarank重排
       sorted = rerank(rank, query, docs['hits']['hits'])
       done2 = time.time()
       return render_template('search.html', help=False, query=query, docs=sorted, method=method, rank=rank, size=n, took={"search": 1000*(done1-start), "rank": 1000*(done2-done1), "total": 1000*(done2-start)})
   ```
   

2. User click feedback. Write user preference feedback to Metarank.

   ```Python
   @app.route('/feedback', methods=['GET'])
   def feedback():
       item = request.args.get('item')
       
       # 点击反馈
       interaction = metarank.feedbackInteraction(item)
   
       return innerSearch()
   ```
   


<span id="1d753d8f"></span>
## Video demonstration

<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/960d64557bac41d9809afa192d5a1c18~tplv-goo7wpa0wc-image.image" controls></video>
