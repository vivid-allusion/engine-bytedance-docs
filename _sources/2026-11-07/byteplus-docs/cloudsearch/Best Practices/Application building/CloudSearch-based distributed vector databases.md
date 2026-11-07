---
title: "CloudSearch-based distributed vector databases"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/distributed-vector-databases"
---

Cloud Search supports serverless and containerized deployment and supports also k\-NN to offer vector search and vector storage capabilities. On the basis of Cloud Search clusters, k\-NN vector databases can offer large\-scale distributed capabilities, bringing users with vector search capabilities that can be scaled out by orders of magnitude.

This topic introduces the background and use scenarios of native vector search and databases in the Large Language Model (LLM) era.

<span id="19305be6"></span>
## Background information

With the development of emerging fields such as audio and video and recommendation, and the increasing demand for LLMs, multi\-modal search is introduced to satisfy more complex search requirements. Cloud Search **adds the vector search capability** on the basis of full\-text search to analyze and retrieve unstructured data.

In the context of vector search, a machine learning model is used to generate vectors to represent various types of data objects such as text, images, audio and video, and other data, and the distances between vectors represent the similarity between the objects themselves. The common vector libraries use ANN algorithms to search through a large set of vectors in a tiny fraction of the time.

k\-NN can be used as vector databases. They build vector indices by introducing advanced vector algorithm libraries and also persistently stores built vector indices to the disk. The indices are more stable. In conjunction with inverted indices of Cloud Search, vector search and full\-text search capabilities are combined to realize more powerful hybrid search capability.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6841989f484f48dc8b0841b50f54c496~tplv-goo7wpa0wc-image.image) </span>

<span id="ed794973"></span>
## Use scenarios

There are six categories of business scenarios based on k\-NN, which are currently applied in enterprise business scenarios:


* Multimodal search: such as image search, semantic search, and audio and video similarity search.

* AI\-powered content recommendation: such as video recommendation, advertising recommendation, relationship recommendation, and commodity recommendation.

* AI\-powered question answering: such as transformer\-based FAQs, LLM\-related FAQs, and generative QA with LangChain.

* Data deduplication: such as review and deduplication of videos, audios, and images, and detection of copyright of various types of materials.

* Security risk control: such as fraud detection, anti\-crime detection, risk assessment, and anomaly detection.

* Other applications: such as data mining, data analysis, search re\-ranking, and search by text.


The following implementation process takes the copywriting similarity recognition scheme as an example:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/466b2b1503ec4493ab7ccac1d5981c34~tplv-goo7wpa0wc-image.image) </span>

In the context of pushing copywriting to users, to improve user experience, ensure that no duplicate copywriting content is pushed to users and each push content will be subject to similarity recognition and deduplication.

Each copywriting generates embeddings through the BERT model and retrieval is run once in Cloud Search. If the similarity is lower than the threshold, the content is determined to be new and is written to k\-NN vector databases to gradually form a copywriting library. If the similarity is greater than the threshold, the content is determined to be duplicated and is pushed less frequently.
