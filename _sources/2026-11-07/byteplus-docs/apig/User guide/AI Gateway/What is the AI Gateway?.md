---
title: "What is the AI Gateway?"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/What_is_the_AI_Gateway"
---

The positioning of the OpenAI Development Mode and API Gateway products in large language model scenarios highly coincides. The API Gateway can serve as a crucial tool for large language model development, providing standardized entry, observability, and security authentication features. This article introduces API Gateway as an AI Gateway, discussing the main concepts, features, application scenarios, and advantages in large language model development.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>[Beta · Apply for Trial]</strong>: This feature is currently in beta stage, please contact your account manager if you wish to use it.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information 

Since the release of OpenAI, large language models have become important tools driving innovation in various fields, and the application scenarios for large language models are becoming increasingly broader. However, as the application of large language models deepens, challenges also emerge. Mainly includes:


* Generative AI poses new data security threats.

* Employees lack necessary AI development skills.

* AI development cannot integrate with the existing technology stack.

* Lack of a unified data policy. To address the above issues, there is an urgent need for a tool that can standardize development processes, control traffic, enhance Security, and provide observability capabilities for large models. This tool is: AI Gateway. The AI Gateway has capabilities very similar to those of the API gateways commonly seen in microservices development. However, the former is more integrated and optimized for large\-model scenarios, providing standardized call entrances for different models, aiming to enhance the usability and observability of model invocations.


<span id=".QUkg5bqU55So5p6E5bu655qE5oyR5oiY"></span>
## Challenges in Building AI Applications

<span id=".57y65LmP57uf5LiA6LCD55So5pa55byP"></span>
### Lack of a unified call method

With the rapid development and maturation of large model technology, large models are being widely applied across various industries, each with different structures and scales emerging incessantly. Since the performance of models varies across different scenarios, to achieve optimal business results, it often requires integrating multiple scenarios or different versions of models from the same vendor. This leads to increasingly fragmented model calls. Different business needs often require the integration of models from multiple vendors, causing integration and management costs to surge. This fragmentation presents significant challenges for businesses, including complex model call policies, adapting code to switch between different vendors, and stability and reliability issues during the integration process of multiple model service providers.

<span id=".5qih5Z6L5a6J5YWo566h5o6n5Zuw6Zq-"></span>
### Model security control difficulties

Whether the AI applications serve within a company or are aimed at internet users, the security control of model invocations must be considered. E.g.: In enterprises, it is necessary to authenticate and authorize users from different departments and conduct unified audits of model calls to ensure the security of model invocations. When serving internet users, it's also required to authenticate visitors and limit the number of times each individual accesses the model or the number of tokens to prevent malicious calls. This requires developers to add extra capabilities for authentication, authorization, traffic limiting, and degradation in the application, especially when adapting to multiple model service providers, it calls for additional adaptation efforts.

<span id=".5qih5Z6L5byA5Y-R6LCD6K-V5Zuw6Zq-"></span>
### Model development and debugging difficulties

As large models do not have fixed inputs and outputs like traditional applications, different prompt words can significantly impact the model's output, where inappropriate prompts can lead to meaningless or irrelevant outputs. Therefore, during the development and debugging of large model applications, it is necessary to more completely record the context of calls, including user inputs, prompt templates, model invocations, function calls, etc., and to rapidly retrieve call information based on user data. Furthermore, prompt words in large model application development need to be continuously optimized, requiring the ability to provide modifications to the prompt that are immediately effective and can be quickly verified in a canary environment. In the AI application development and construction process, especially when connecting to multiple different model providers, it can lead to fragmented model invocations, making security and observability capabilities more difficult to maintain, and also reducing the efficiency of the development process. As shown in the diagram below, developers need to connect to multiple model providers, implement logic for how traffic is allocated among different providers, obtain Monitoring data from each model provider, and also allocate a reasonable Quota to each model.

<span id=".QUkg572R5YWz55qE5YWz6ZSu6IO95Yqb"></span>
## Key capabilities of the AI gateway

<span id=".5aSa5qih5Z6L6K6_6Zeu5Luj55CG"></span>
### Multi\-model access proxy

As the number of large models continues to grow, and the invocation of models becomes increasingly fragmented, an AI gateway can provide a unified entry and a standardized API layer, enabling clients to access multiple model providers from the same client. Access can be made through a standardized model interface format regardless of the underlying model's supplier (e.g., OPEN AI's interface), shielding the differences between different model vendors' API call methods, and reducing adaptation cost. Also, depending on the traffic ratio of the scenarios, requests can be routed to different large models, helping users to migrate smoothly to new models (such as OpenAI, Doubao, etc.). The advantages of using a unified proxy are mainly reflected in the following aspects:


1. **Simplify integration**: Different model vendors may use their own unique API interfaces and call methods, which makes the integration process complex and time\-consuming. With the unified protocol of the AI gateway, developers do not need to adapt separately for each model vendor's API, just follow the unified interface specification for development, which greatly simplifies the difficulty and workload of integration.

2. **Improve development efficiency**: The unified protocol reduces the time cost for developers to switch and learn between different model APIs. They can focus more on business logic implementation without paying too much attention to the details of the underlying API, thus improving development efficiency.

3. **Reduce maintenance costs**: When the API of a model vendor changes, if there is no unified protocol, developers need to modify the adaptation code one by one. However, through the unified protocol of the AI gateway, developers only need to make changes once at the gateway to adapt to all models using that protocol, reducing maintenance costs.

4. **Enhance portability**: The unified protocol makes the system more scalable and easier to integrate new models. When migrating to new models is needed, you only need to configure it on the AI gateway and add a new model service provider, avoiding large\-scale modifications to the existing system, thus enhancing the system's flexibility and scalability.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For a detailed introduction and usage method of the AI multi\-model access proxy, please refer to <a href="https://docs.byteplus.com/en/docs/apig/AI_Multi-Model_Proxy">AI multi\-model proxy</a>.</div>


<span id=".56iz5a6a5oCn5rK755CG"></span>
### Stability governance

As large models are increasingly integrated into critical business chains, the stability of model invocation becomes crucial. The AI gateway enhances calling stability through various mechanisms.


* **Support canary testing for different models**. e.g., when introducing a bean\-paste model, you can switch a percentage of the traffic to bean\-paste to verify and compare the effects between different models or different versions of models.

* **Implement token\-based rate limiting**. Limiting token usage can effectively manage the use of model resources. Besides limiting overall model invocation tokens, you can also impose limits on different users or channels, e.g., allocate different gateway identities (known as "consumers" in the gateway) to different internal teams and set respective token usage quotas for different teams, ensuring fair distribution of resources among users or teams while avoiding unnecessary waste.

* **Provide timeout handling and failover features between different models**. Based on the Priority of models, if a model fails to respond or encounters an error, the gateway will automatically switch to the next model, effectively ensuring the stability and reliability of the application. In the growing trend of multimodal applications, the role of the AI gateway has become increasingly prominent. The average failure rate of visual models (5%) is higher than that of chat models (2%), and the processing latency is significantly longer, making the capabilities of timeout handling and failover particularly critical. The AI gateway effectively addresses high failure risks and long latencies through stability governance mechanisms, ensuring consistency in user experience and reliability of the service.


<span id=".5qih5Z6L6LCD55So5Y-v6KeC5rWL"></span>
### Model invocation observability

Model invocation observability is similar to traditional Web applications, focusing mainly on three metrics: latency, QPS, and TPS. In large model scenarios, latency can be further broken down into Time to First Token (TTFT) and Time Per Output Token (TPOT), and these latency metrics serve different roles in assessing model performance.


* **TTFT**: The time it takes for the model to generate the first output after the user enters a query. In real\-time interactions, low latency in obtaining responses is very important, but it is less critical in offline workloads. This metric is driven by the time needed to process the prompt information and generate the first output token.

* **TPOT**: The time required to generate an output token for each user of the query system. This metric is related to each user's perception of the "speed" of the model. For example, a TPOT of 100 milliseconds/token means each user can process 10 tokens per second, or about 450 words per minute, which is much faster than an average person's reading speed.

* **Latency**: The total time it takes for the model to generate a complete response for the user. The overall response latency can be calculated using the first two metrics: Latency = (TTFT) + (TPOT) \* (number of tokens to be generated). Through the AI gateway, the observable add\-on enhances model inference metrics. Once the add\-on is loaded, the corresponding metrics can be obtained, helping users effectively track and understand how the model is used, e.g., identifying which projects consume the most tokens to optimize resource allocation; clarifying which models perform best on specific tasks to guide project selection of suitable models; and managing cost distribution among different teams or applications for cost control. The AI gateway can also consolidate and record the call information of multiple models, recording each call's input and output, and can add debug information such as userId and call channel to the logs as per user requirement.


<span id=".5a6J5YWo6K6k6K-B"></span>
### Security certification

The cost of calling large model inferences is significant, to prevent malicious users from accessing the inference services. It is necessary to authenticate the user's identity, only valid users are allowed to access, e.g., a company develops internal tools for different departments, allowing the HR department's resume filtering tools to access certain models, while customer service chatbots can access a different set of models. The gateway handles the authentication from the client to the gateway and from the gateway to each major model vendor, freeing large model applications from complex authentication functions. The AI gateway offers the following two methods of authentication:


* API\-Key authentication: Suitable for issuing long\-term credentials to users for model access.

* JWT authentication: Suitable for issuing temporary access credentials, JWT tokens will automatically expire after seven days. In addition, the AI gateway can also implement the following features:

* **Quota management**: Quotas can be specified for different departments within a company or for different external users for different access models, e.g., allocating a department or an application within a company with a daily access to ten million DouBao PRO 128K models and fifty million DouBao Lite 128K models.

* **Key management**: Storing and rotating API keys for different major model vendors.

* **Logs and auditing**: Retain detailed logs recording who accessed what, when, and why, which is especially useful for compliance in regulated industries.


<span id=".566A5YyWIFByb21wdCDlvIDlj5HosIPor5U="></span>
### Simplifying Prompt development and debugging

A Prompt is a typical way of optimizing large model outputs, by carefully designing and selecting Prompts, the generation process of the large model can be guided to better meet user needs. During the development of Prompts, it is necessary to continuously design and optimize prompts, explore the impact of different Prompts on model outputs, and enable the model to better understand the user's intentions and requirements. The AI gateway can optimize the daily Prompt update process during Prompt development, enable dynamic updates of Prompts, prevent Prompt coupling in the engineering code, and also provide canary release capabilities for Prompts.


* **Prompt Template dynamic updates**: Developers often use Prompt Templates to interact with large models, and during actual development and testing, they continuously adjust the templates to test interactions with the large models. Therefore, the gateway needs to be able to dynamically load Prompts, for example by reading from a Nacos configuration center or dynamically from other users' Prompt management platforms, instead of requiring users to modify add\-ons at the gateway every time.

* **Prompt canary release**: usually, Prompt does not have a canary release mechanism, and once released, all users will use the latest version of Prompt, unable to conduct small\-scale canary testing for new features. For production applications, this release method carries too much risk. The routing capability through the AI gateway can route specified user IDs or a specified proportion of traffic to the new version of Prompt.
