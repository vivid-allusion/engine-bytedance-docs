---
title: "Building long-conversation-supported Chatbot based on LLM"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/build_long_session_chatbot_with_llm"
---

This topic introduces a solution for long\-conversation\-supported Chatbot built on Valkey\-Search and LLM.

<span id="XtomkPkp"></span>
## Objective

As large language models (LLMs) become more widely used in natural language processing, intelligent conversational systems based on LLMs have become a crucial part of human\-computer interaction. However, current mainstream LLMs are limited by the number of tokens that can be processed in a single request (typically a few thousand). When handling long\-range and multi\-turn conversations, they often exceed the model's token capacity limit due to the accumulation of historical records, resulting in the loss of key contextual information and affecting the coherence and accuracy of the conversation.

To address this challenge, Cache for Redis offers a vectorized conversational memory management solution based on the Valkey\-Search module. This solution leverages Valkey\-Search's efficient vector storage and retrieval capabilities to convert historical conversation content into vector form and store it persistently in a Redis instance, thereby building a Chatbot system with "long\-term memory". Each time a user provides input, Redis can dynamically retrieve the most relevant historical fragments through vector similarity calculation and integrate them into the model's input as context. This solution not only breaks through the limit on the number of tokens for a single request but also improves the accuracy of information association and the quality of system responses in long conversations, providing reliable technical support for achieving sustainable and highly consistent multi\-turn conversational interactions.

<span id="2ZLBNcDg"></span>
## Architecture

In the current solution architecture, users' historical conversation records are uniformly stored in sessions with state\-keeping capabilities. In addition to storing conversation text content, each session also supports dynamic expiration mechanisms such as configuring Time to Live (TTL). This not only ensures the timeliness of data but also enables the reasonable allocation of storage resources. The TTL mechanism allows the system to automatically clear long\-inactive session data, effectively controlling system load and enhancing user privacy protection.

Before sending a request to the large language model, the system first performs a semantic similarity search on the current user's conversation history using the vector search capability provided by Valkey\-Search. The process is as follows: Each historical conversation is converted into a high\-dimensional vector using an embedding model and then persisted in a Redis database. When user provides new input, the system vectorizes it in real time and uses it as a query to retrieve the historical conversation snippets with the highest semantic relevance from Redis.

The retrieved context is then filtered and sorted before being passed to the prompt optimization module. This module logically combines the retrieved results with the current user input, structuring them to build a complete prompt that meets the large language model's input specifications and has a natural contextual flow. This optimization mechanism improves the prompt's semantic clarity and logical consistency, helping the model to more accurately grasp the conversational context and user intent to generate more relevant responses.

Finally, the context\-enhanced prompt is submitted to the large language model for inference and content generation. This architecture enables context awareness in long conversations, allowing the Chatbot to bypass the token limit for a single request. It maintains conversational coherence and personalization across multiple interactions, improving the user experience and interaction quality.

The system architecture design of Chatbot that supports long sessions, built based on Valkey\-Search and LLM, is shown in the following figure.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a22b153ce22c361c8617f6f17c55cc73.png) </span>

<span id="UjynvFhR"></span>
## Implementation

<span id="pdwySZ2u"></span>
### Preparation

Prepare the following resources and complete the necessary configurations.


|Resource category |Required configuration |
|---|---|
|Redis |This solution requires the following Cache for Redis resources:<br><br><br>* Create Redis 7.0 instance. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance).<br><br>* The Valkey\-Search module has been enabled for the Redis instance. For specific procedures, refer to [Enabling extension module](https://docs.byteplus.com/en/docs/redis/enable_extended_module).<br><br>* Configure an access allowlist for the Redis instance. For specific procedures, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist). |
|ECS<br><br> |This solution requires the following ECS\-related resources:<br><br><br>* Create ECS instance. For specific procedures, refer to [Purchasing and using ECS instance](https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances).<br><br>* Install the Redis Python client and other AI\-related Python dependency libraries, such as transformers, gradio, torch, and mdtex2html, on the [ECS](https://console.byteplus.com/ecs/instance) server.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Ensure you are using Python 3.10. You can run the <code>python --version</code> command to check the current Python version.   </div><br>   <br><br>* The port used for Web interface of ChatBot in this solution is `7860`. Therefore, you must add port `7860` to the security group rules for your ECS instance, ensuring that both outbound and inbound rules allow access to port `7860`. To configure security group rules, refer to [Adding security group](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules). |


<span id="YetT9eZt"></span>
### Procedure


1. Log on to ECS instance where the required environment is installed. For specific procedures on logging on ECS instance, refer to [Logging on to instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-an-instance).

2. In the command\-line window or terminal of ECS instance, execute following command to clone code.

   ```Bash
   git clone https://github.com/byteplus-sdk-samples/cache_for_redis_examples/tree/main/chatbot
   ```
   

3. Go to the Chatbot project directory, find the section that creates the Redis client in the `chatbot.py` file, and modify the corresponding configuration based on your Redis instance's actual situation and the large language model you are using.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The following code only shows the configuration for Cache for Redis and the large language model in the Chatbot project.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can view the connection address and port number of the instance on Redis console. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/redis/view-address">Viewing connection address</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you forget the password for the default account of your Redis instance, you can reset the password on the console. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/redis/reset-password">Resetting password</a>.   </div>
   

   ```Python
   class RedisClient:
       def __init__(self, host='<Connection address of Redis instance>', port=<Port of Redis connection address, default port 6379>, password='<Password for default account in Redis instance>', db=< Redis database name>):
           self.client = redis.Redis(host=host, port=port, db=db)
           self.text2vec_tokenizer = AutoTokenizer.from_pretrained("<Large language model used>")
           self.text2vec_model = AutoModel.from_pretrained("<Large language model used>").cpu()
   ```
   

   The code example is as follows.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The large language model used in this example is <code>GanymedeNil/text2vec-large-chinese</code>. You can also replace it with your own model. When using open\-source models, comply with relevant agreements, laws, and regulations.   </div>
   

   ```Python
   class RedisClient:
       def __init__(self, host='redis-cnlfwm1ecuiqv****.redis.ibytepluses.com', port=6379, password='PwdTest@123', db=0):
           self.client = redis.Redis(host=host, port=port, db=db)
           self.text2vec_tokenizer = AutoTokenizer.from_pretrained("GanymedeNil/text2vec-large-chinese")
           self.text2vec_model = AutoModel.from_pretrained("GanymedeNil/text2vec-large-chinese").cpu()
   ```
   

4. Go to the root directory of the Chatbot project and execute following command to install.

   ```Bash
   python3 -m pip install -r requirements.txt
   ```
   

5. In the root directory of the Chatbot project, execute following command to start the service.

   ```Bash
   python3 chatbot.py
   ```
   

6. Open a browser and enter `<ECS public IP>:7860` in the URL to open the Chatbot web interface.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can view the public IP address of specified ECS instance on the list page of the <a href="https://console.byteplus.com/ecs/instance">ECS console</a>. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Instance-overview-1">Viewing instance information</a>.   </div>
   

   The code example is as follows.

   ```Plain Text
   180.184.***.***:7860
   ```
   


<span id="EJ9CGnSC"></span>
## Result

Combined with the vector storage and retrieval capabilities provided by the Valkey\-Search module of Cache for Redis, Chatbot can effectively capture and utilize the semantic information of historical conversations, thereby achieving accurate understanding of users' long\-term conversation intentions and coherent responses, significantly improving the accuracy of question answering and the consistency of the conversation experience.
