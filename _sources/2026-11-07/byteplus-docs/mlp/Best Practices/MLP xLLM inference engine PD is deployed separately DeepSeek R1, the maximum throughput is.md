---
title: "MLP xLLM inference engine PD is deployed separately DeepSeek R1, the maximum throughput is increased by 5 times"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/MLPxLLM"
---

This article will show you how to deploy DeepSeek R1 separately through the xLLM inference engine PD based on a minimum of 2 Hopper architecture servers to increase throughput by up to 5x.

<span id="55b356be"></span>
# brief introduction

xLLM is an efficient inference framework **fully self\-developed** by BytePlus ModelArk, which supports PD separation (Prefiling, Decoding), elastic scaling and other characteristics, and its performance is significantly ahead of the open source framework.

In the inference service of the BytePlus Machine Learning Platform (MLP), production support for PD split deployment using the xLLM inference engine has been implemented. Through this article, you can use the xLLM preset mirror to deploy the same DeepSeek\-R1 model inference service of ModelArk; at the same time, the performance data comparison of the xLLM mirror compared to the open\-source version of the SGLang community will be given here.

<span id="a711c6cc"></span>
# precondition

<span id="3c510737"></span>
## Download the model file to the local PFS

<span id="e304a311"></span>
### Preset model information

In order to make it easier to use DeepSeek models, we have prepared common models for you in advance in BytePlus's TOS. You can directly pull the model files into your own file system through the tosutil tool. The relevant preset model information includes:


|**Model Name** |**TOS path** |**model description** |
|---|---|---|
|DeepSeek\-R1 |tos://preset\-models\-ap\-southeast\-1/deepseek\-ai/DeepSeek\-R1/ |DeepSeek R1 model |
|DeepSeek\-V3 |tos://preset\-models\-ap\-southeast\-1/deepseek\-ai/DeepSeek\-V3/ |DeepSeek V3 model |
|DeepSeek\-R1 ModelArk version |tos://preset\-models\-ap\-southeast\-1/deepseek\-ai/vemlp\-deepseek\-r1\-enc/ |DeepSeek R1 model, the xLLM framework needs to be used in conjunction with this version |


> Tips：

> 1. At present, the PD separation deployment is in the preview state, and the function needs to be granted whitelist access list. You can contact BytePlus Machine Learning Platform product solutions or sales or after\-sales technical support students to communicate with grant whitelist access.

> 2. Please note that the mirror and model paths need to be adjusted appropriately according to the location of the region. For example, the DeepSeek\-R1 file is located in the ap\-southeast\-1 Region, and the TOS path is tos://preset\-models\-ap\-southeast\-1/deepseek\-ai/DeepSeek\-R1/.


<span id="98e9af1c"></span>
### Model download

Here is to download the DeepSeek model preset by BytePlus to the user's own PFS bucket as the basic model for subsequent model inference services. The specific operation steps are as follows:


* [Create Dev boxes Mount user vepfs directory](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/devinstance/create)


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a40404056374856a96e3a7ff7b6b3f6~tplv-goo7wpa0wc-image.image) </span>


* **Log in to the previous step Create Dev boxes under DeepSeek model weight file to vepfs directory:**  The entire download is expected to take **10** minutes


```Bash
export AK=xx
export SK=xx
export VEPFS_MODEL_PATH=/testphi3/models
cd $VEPFS_MODEL_PATHtosutil config -i $AK -k $SK  -e tos-ap-southeast-1.ivolces.com -re ap-southeast-1
tosutil cp tos://preset-models-ap-southeast-1/deepseek-ai/vemlp-deepseek-r1-enc/ . -r -u -j=32 -p=4 -nfj=16
```



* **Confirm model file exists:**  Model path: $VEPFS_MODEL_PATH/vemlp\-deepseek\-r1\-enc/vemlp\-deepseek\-r1\-enc/


```Bash
ls $VEPFS_MODEL_PATH/vemlp-deepseek-r1-enc/vemlp-deepseek-r1-enc/ | wc
#  19      19     508
```


<span id="8c4009bb"></span>
## Prepare GPU resources

You need to prepare at least two Hopper architecture machines, create resource queues, and create VPC, PFS, API gateway, VMP, TLS and other basic components in the global configuration module of the Machine Learning Platform (mlp) in advance, **and confirm SecurityGroup, ACL release the listening, calling, and indicator collection ports involved in subsequent inference services** .

<span id="d2b6771c"></span>
# Deploy inference services

<span id="30348af4"></span>
## 1. Creating services

<span id="ab7fcecd"></span>
### Creating services


* Correctly fill in [service name], [private network], [API gateway], 8000 service inference port, 8080 monitoring indicator collection port and other **information.** 


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The current POC specifies 8000, 8080, <strong>please do not change the port</strong> , and <strong>check again whether SecurityGroup and ACL release all ports in advance.</strong></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b9f07a26a904734900763512001b355~tplv-goo7wpa0wc-image.image) </span>

<span id="8aff0b4d"></span>
### Create API gateway (when first Creating service)


* Fill in the **VPC** correctly and **turn on VMP**


<span id="a40b252f"></span>
## 2. Create Deployment

<span id="64bf5a5b"></span>
### new deployment


* On the Create service deployment tab above, click Add Deployment.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d5a7af67cf2458bac37b061aed5ac59~tplv-goo7wpa0wc-image.image) </span>


* **Correctly fill in the 8\-card Hopper architecture queue, high\-performance computing GPU type, etc.** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39deea2474aa4658a96179480d7e097c~tplv-goo7wpa0wc-image.image) </span>


* Prefill roles and Decode roles, **both need to correctly fill in the user model path**  **`$VEPFS_MODEL_PATH/vemlp-deepseek-r1-enc/vemlp-deepseek-r1-enc/`**  **.** 


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When setting <code>max tokens</code>, if the number of truncated tokens needs to include the output in <code>reason content</code>, set environment variables <code>XLLM_IGNORE_EOS = 1</code>. If you only need to limit the number of tokens output in <code>content</code>, set environment variables <code>XLLM_IGNORE_EOS = 0</code></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b3f29b8fe6147b8a716f2f38873779f~tplv-goo7wpa0wc-image.image) </span>


* Select [Subnet], [SecurityGroup], and click Create to wait for the instance to queue up and run.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/091ecb6ffecd4b92b27fb98732d6d7a4~tplv-goo7wpa0wc-image.image) </span>


* Observe the [decode] role instance log, report an error without model loading, and wait for the model to load and run [estimated 30 minutes].


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ee95acfef5543cda2779aeff5ae35fc~tplv-goo7wpa0wc-image.image) </span>


* From the call guide tab page of inference services, get the service call address. If you need to use token encryption, start token access on the current page.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>The current token has a valid period of 7 days by default and needs to be replaced when it expires.</strong> <strong>If you need a longer valid period token, please submit a</strong> <a href="https://console.byteplus.com/workorder/create">ticket </a><strong>request.</strong></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5d95b399fe1474c9bfcca8365f46929~tplv-goo7wpa0wc-image.image) </span>

<span id="5d8043aa"></span>
### monitoring page

Get the Grafana inference monitoring profile.

After importing, select the corresponding **datasources** and **services created on the Machine Learning Platform:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/111c8864e0ef4cdabfa0b5a83a341b6f~tplv-goo7wpa0wc-image.image) </span>

Monitoring is divided into two dimensions, the service dimension and the instance dimension. The service and instance metrics panels are:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1451dcddf0c4848a7306d884db10b74~tplv-goo7wpa0wc-image.image) </span>

Indicator definition:


|**Metric** |**explain** |
|---|---|
|QPS |Query Per Second Number of completed requests per second, reflecting processing power |
|Inflight Requests |Number of outstanding requests in the engine |
|wTPM |Tokens Per Min (10,000) The number of tokens processed per minute, reflecting the processing capacity |
|TPS \-\- Prompt Tokens/Sec |Average number of Prefill Tokens processed per second per card, reflecting processing capacity |
|TPS \-\- Generation Tokens/Sec |Average number of Decoded Tokens processed per second per card, reflecting processing power |
|TTFT |First Token Delay Reflects Quality of Service |
|TPOT |Token generation delay, reflecting quality of service |
|E2E |Request end\-to\-end completion delay, reflecting quality of service |
|Input Token Length |The average and statistical value of the input length of the request, reflecting the characteristics of the request |
|Output Token Length |The average and statistical value of the output length of the request, reflecting the characteristics of the request |
|KVCache Hit Rate |Prompt repetition rate between requests |
|request success rate |The percentage of requests successfully processed at the server level |


<span id="78feb049"></span>
# model call

<span id="965f5fa5"></span>
## Invoking models using OpenAI\-compatible methods

Creates a public service automatically after deployment, providing HTTP OpenAI API endpoints. It can be called according to the OpenAI compatible API method. For example:

```Bash
# Streaming mode
curl -X POST https://scur1lll****.apigateway-ap-southeast-1.volceapi.com/mlp/s-20250220014946-lmddr/v1/chat/completions \
 -H "Content-Type: application/json" -d '{
    "model": "vemlp-deepseek-r1-enc",
    "messages": [
        {"role": "user", "content": "Help me design a three-day tour itinerary in Beijing"}
    ],
    "max_tokens": 20,
    "stream": true
}'

# Non-streaming mode
curl -X POST https://scur1****.apigateway-ap-southeast-1.volceapi.com/mlp/s-20250220014946-lmddr/v1/chat/completions \
 -H "Content-Type: application/json" -d '{
    "model": "vemlp-deepseek-r1-enc",
    "messages": [
        {"role": "user", "content": "Help me design a three-day tour itinerary in Beijing"}
    ],
    "max_tokens": 800
}'
```


<span id="e09ff4ea"></span>
## Streaming output sample

```JSON
{"id": "chatcmpl-17399634109****", "choices": [{"index": 0, "delta": {"role": "assistant", "content": "", "reasoning_content": "Okay", "tool_calls": []}, "finish_reason": ""}], "created": 1739963410, "model": "vemlp-deepseek-r1-enc", "system_fingerprint": "fp", "object": "chat.completion.chunk", "usage": {"prompt_tokens": 9, "completion_tokens": 1, "total_tokens": 10, "completion_tokens_details": {"reasoning_tokens": 1}}}
{"id": "chatcmpl-17399634109****", "choices": [{"index": 0, "delta": {"role": "assistant", "content": "", "reasoning_content": ",", "tool_calls": []}, "finish_reason": ""}], "created": 1739963410, "model": "vemlp-deepseek-r1-enc", "system_fingerprint": "fp", "object": "chat.completion.chunk", "usage": {"prompt_tokens": 9, "completion_tokens": 2, "total_tokens": 11, "completion_tokens_details": {"reasoning_tokens": 2}}}...
```


<span id="15e95f7a"></span>
## Sample non\-streaming output

```Bash
{"id":"chatcmpl-1739963676****","object":"chat.completion","created":1739963676,"model":"vemlp-deepseek-r1-enc","system_fingerprint":"fp","choices":[{"index":0,"message":{"role":"assistant","content":"\n\nHere is a three-day classic itinerary in Beijing designed for you, covering historical sites, royal gardens, modern landmarks and local cultural experiences. The itinerary is compact but combines work and rest:\n\n🌟 **Day 1: Classic Tour of the Central Axis**\n","reasoning_content":"Well, the user asked me to help design a three-day tour itinerary in Beijing. First, I need to consider the user's possible background and needs. As the capital of China, Beijing has many classic attractions, such as the Forbidden City, Tiananmen Square, the Great Wall and so on. The user may be visiting Beijing for the first time and want to see these must-see places. However, it is also possible that they have already visited some attractions and want to experience them more deeply. However, it is usually safer to focus on classic attractions for the first design. \n\nNext, I have to make sure whether the three-day itinerary is reasonable. Beijing is very large, and the travel time between attractions may need to be considered. For example, the Great Wall is in the suburbs and needs to be arranged separately for one day. The first day may be in the city center, arranging more concentrated places such as Tiananmen Square, the Forbidden City, and Jingshan. On the second day, you can consider the Summer Palace and Yuanmingyuan. Both are in Haidian District, a little far from the city center, but can be put on the same day. On the third day, you can arrange some cultural experiences, such as Hutong, Nanluoguxiang, 798 Art District, etc. \n\nAlso pay attention to whether the time allocation is reasonable. For example, the Forbidden City takes half a day, and if Tiananmen Square and Chairman Mao Memorial Hall are included, it may take a whole morning. Go to Jingshan Park in the afternoon, and then go to Wangfujing in the evening. Is this arrangement too rushed? It may need to be adjusted. In addition, the user's physical strength should be considered, especially the Great Wall may require more walking in one day, so it may be more appropriate to arrange the Summer Palace and Yuanmingyuan on the second day, and relatively relaxing cultural attractions on the third day. \n\nIn terms of food, users may want to experience Beijing's specialties, such as roast duck, fried noodles with soybean paste, shabu-shabu mutton, etc. Therefore, it is necessary to recommend nearby restaurants or snack streets in the daily itinerary. For example, it may not be convenient to have lunch near the Forbidden City on the first day, but you can recommend Wangfujing's snack street or nearby restaurants. If you have dinner in Wangfujing, Quanjude is a classic choice, but you may need to book in advance. \n\nIn terms of transportation, the Beijing subway is more convenient, but some attractions may require taxis or buses. For example, the Great Wall usually requires taking a bus or a special tourist line, or joining a one-day tour group. Users should be reminded to pay attention to the time and method of transportation to avoid delaying the trip. \n\nIn addition, seasonal factors should also be considered. If it is summer, pay attention to sun protection and hydration; if it is winter, keep warm. But the user did not mention the specific time, so a general reminder may be needed. \n\nAlso pay attention to the opening hours and closing days of the attractions. For example, the Forbidden City is closed on Mondays, so the itinerary should avoid Mondays. If the user does not know this, it may be a wasted trip. So a reminder is needed in the precautions. \n\nPerhaps the user also wants to experience Beijing's culture, such as hutongs and courtyards, so the third day is arranged to visit Nanluoguxiang and Houhai, as well as 798 Art District, so that there is both traditional culture and modern art, which is more comprehensive. \n\nFinally, check whether the itinerary covers the main attractions in Beijing and whether three days are enough. Day 1: Tiananmen Square, Forbidden City, Jingshan, Wangfujing. Day 2: The Great Wall, Bird's Nest and Water Cube. Day 3: Summer Palace, Old Summer Palace, Nanluoguxiang, Houhai. Or maybe you need to adjust it. For example, if you go to the Great Wall on the second day, you may be tired in the afternoon, so you can arrange the night view of the Bird's Nest and the Water Cube in the evening. The Summer Palace and the Old Summer Palace may be compact on the third day, but you can arrange to visit them in the morning and afternoon respectively. Or should you put the Summer Palace and the Old Summer Palace on the second day, and the Great Wall on a separate day? You need to consider whether the route is reasonable. \n\nYou may go to the Great Wall on the second day, and then go to the Bird's Nest and the Water Cube after returning to the city. This is more convenient because the Great Wall is in the northern suburbs and the Bird's Nest is also in the north, which may be more suitable. The Summer Palace and the Old Summer Palace are in the western suburbs, so you can arrange them there on the third day, and then go to Nanluoguxiang and Houhai in the afternoon. Or vice versa? You need to check the map to confirm the geographical location. \n\nIn addition, the user may be interested in watching the flag-raising ceremony, so you can suggest getting up early on the first morning to watch the flag-raising ceremony, but you need to check the time in advance, and you may need to get up very early. For example, the flag-raising ceremony is very early in summer. Are users willing? \n\nIn short, it is necessary to comprehensively consider the distribution of scenic spots, time arrangements, transportation, diet and the user's physical strength to ensure that the itinerary is reasonable and feasible, not too rushed, and can cover the main attractions.\n","tool_calls":[]},"finish_reason":"length"}],"usage":{"completion_len":799,"prompt_len":12,"total_len":811,"completion_tokens_details":{"reasoning_tokens":758}}}
```


<span id="1c78ce39"></span>
# performance testing

<span id="101060d3"></span>
## performance comparison

Take 3500:1500 as an example:


* BytePlus xLLM version DeepSeek inference performance is about the same as the SGLang version (without MTP) limit throughput, about 1800 tokens/s

* At the same throughput level (approximately 900 tokens/s), the BytePlus xLLM version AVG TPOT is 26 ms 78% lower than the SGLang (MPT) version and the TTFT is 42% lower at 1073 ms

* Under SLO with limited TTFT < 600 ms and TPOT < 30 ms, BytePlus xLLM version has 100% higher throughput than SGLang.


Take 2500:1500 as an example:


* BytePlus xLLM version DeepSeek inference performance is 60% higher than SGLang version limit throughput at 1612 tokens/s

* At the same throughput level (approximately 500 tokens/s), the BytePlus xLLM version AVG TPOT is 21% lower than the SGLang version and the TTFT is 50% lower at 573 ms.

* Under SLO with limited TTFT < 600 ms and TPOT < 30 ms, the throughput of BytePlus xLLM version is 500% higher than that of SGLang.


<span id="077b787e"></span>
## Input and output 3500:1500

<span id="21fd2063"></span>
### xLLM


|**Request Rate (reqs/s)**  |**max\-concurrency** |**input_len** |**output_len** |**mean E2E Latency(ms)**  |**Request throughput (req/s)**  |**throughput(output tokens/s)**  |**Total token throughput (tok/s)**  |**Total token throughput (tok/s/single card)**  |**Mean TTFT(ms)**  |**P99 TTFT(ms)**  |**Mean TPOT(ms)**  |**P99 TPOT(ms)**  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1 |1 |3,500 |1500 |23953.39 |0.04 |62.62 |208.72 |13.04 |528.13 |719.97 |15.63 |16.37 |
|4 |4 |3,500 |1500 |32044.15 |0.12 |181.05 |603.48 |37.72 |773.37 |1377.75 |20.86 |23.22 |
|8 |8 |3,500 |1500 |40851.36 |0.19 |284.93 |949.76 |59.36 |1073.12 |3524.93 |26.54 |29.25 |
|16 |16 |3,500 |1500 |42173.29 |0.37 |548.62 |1828.72 |114.3 |1790.02 |7123.8 |26.94 |29.94 |


<span id="25543cb7"></span>
### SGLang v0.4.3 MTP


|**Request Rate (reqs/s)**  |**max\-concurrency** |**input_len** |**output_len** |**mean E2E Latency(ms)**  |**Request throughput (req/s)**  |**throughput(output tokens/s)**  |**Total token throughput (tok/s)**  |**Total token throughput (tok/s/single card)**  |**Mean TTFT(ms)**  |**P99 TTFT(ms)**  |**Mean TPOT(ms)**  |**P99 TPOT(ms)**  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1 |1 |3,500 |1500 |52746.71 |0.02 |28.44 |94.79 |5.92 |580.44 |596.18 |34.8 |44.51 |
|4 |4 |3,500 |1500 |59667.4 |0.07 |98.41 |328.03 |20.5 |790.48 |1729.88 |39.28 |47.38 |
|8 |8 |3,500 |1500 |77055.98 |0.1 |148.82 |496.06 |31 |1141.76 |4027.89 |50.64 |61.7 |
|16 |16 |3,500 |1500 |113699.01 |0.14 |203.33 |677.78 |42.36 |1818.16 |8657.87 |74.64 |87.47 |
|32 |32 |3,500 |1500 |176652.66 |0.18 |262.6 |875.34 |54.71 |3105.7 |17596.39 |115.78 |145.02 |


<span id="35ca38b8"></span>
### SGLang v0.4.2 BytePlus Optimized Edition


|**Request Rate (reqs/s)**  |**max\-concurrency** |**input_len** |**output_len** |**mean E2E Latency(ms)**  |**Request throughput (req/s)**  |**throughput(output tokens/s)**  |**Total token throughput (tok/s)**  |**Total token throughput (tok/s/single card)**  |**Mean TTFT(ms)**  |**P99 TTFT(ms)**  |**Mean TPOT(ms)**  |**P99 TPOT(ms)**  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1 |1 |3,500 |1500 |73067.18 |0.01 |20.53 |68.43 |4.28 |756.43 |817.75 |48.24 |48.37 |
|4 |4 |3,500 |1500 |78122 |0.05 |76.73 |255.78 |15.99 |2467.48 |3789.51 |50.47 |52.33 |
|8 |8 |3,500 |1500 |86411.57 |0.09 |138.78 |462.6 |28.91 |4583.25 |5601.21 |54.59 |57.64 |
|16 |16 |3,500 |1500 |112645.2 |0.14 |212.94 |709.8 |44.36 |7668.19 |11117 |70.03 |74.73 |
|32 |32 |3,500 |1500 |152704.8 |0.21 |314.15 |1047.16 |65.45 |13326.75 |22025.72 |92.98 |101.45 |
|48 |48 |3,500 |1500 |191965.54 |0.25 |374.85 |1249.51 |78.09 |18942.63 |33179.09 |115.43 |127.43 |
|64 |64 |3,500 |1500 |220016.54 |0.29 |436.09 |1453.65 |90.85 |24463.15 |44384.46 |130.46 |145.56 |
|80 |80 |3,500 |1500 |246107.09 |0.32 |487.34 |1624.45 |101.53 |29875.5 |55652.09 |144.25 |162.76 |
|128 |128 |3,500 |1500 |338296.45 |0.35 |529.77 |1765.92 |110.37 |70625.67 |357620.25 |178.57 |246.56 |


<span id="348e17f6"></span>
## Input and output 2500:1500

<span id="582c681b"></span>
### xLLM


|**Request Rate (reqs/s)**  |**max\-concurrency** |**input_len** |**output_len** |**mean E2E Latency(ms)**  |**Request throughput (req/s)**  |**throughput(output tokens/s)**  |**Total token throughput (tok/s)**  |**Total token throughput (tok/s/single card)**  |**Mean TTFT(ms)**  |**P99 TTFT(ms)**  |**Mean TPOT(ms)**  |**P99 TPOT(ms)**  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1 |1 |2500 |1500 |24852.24 |0.04 |60.35 |160.94 |10.06 |394.39 |530.74 |16.32 |17.05 |
|4 |4 |2500 |1500 |32088.48 |0.12 |178.37 |475.64 |29.73 |573.84 |935.18 |21.02 |25.28 |
|8 |8 |2500 |1500 |39355.71 |0.2 |294.19 |784.52 |49.03 |766.48 |2456.25 |25.74 |28.45 |
|16 |16 |2500 |1500 |40876.41 |0.38 |563.23 |1501.94 |93.87 |1227.04 |5024.98 |26.45 |30.07 |
|18 |18 |2500 |1500 |43335.67 |0.4 |604.77 |1612.71 |100.79 |1303.45 |5798.67 |28.04 |31.91 |


<span id="b533226c"></span>
### SGLang v0.4.3 MTP


|**Request Rate (reqs/s)**  |**max\-concurrency** |**input_len** |**output_len** |**mean E2E Latency(ms)**  |**Request throughput (req/s)**  |**throughput(output tokens/s)**  |**Total token throughput (tok/s)**  |**Total token throughput (tok/s/single card)**  |**Mean TTFT(ms)**  |**P99 TTFT(ms)**  |**Mean TPOT(ms)**  |**P99 TPOT(ms)**  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1 |1 |2500 |1500 |45172.48 |0.02 |33.21 |88.55 |5.53 |344.03 |353.08 |29.91 |33.69 |
|4 |4 |2500 |1500 |55608.83 |0.07 |103.99 |277.31 |17.33 |472.99 |848.48 |36.78 |42.67 |
|8 |8 |2500 |1500 |61904.59 |0.13 |187.5 |500.01 |31.25 |725.7 |2253.81 |40.81 |45.19 |
|16 |16 |2500 |1500 |89486.59 |0.17 |255.01 |680.02 |42.5 |1216.71 |4552.25 |58.89 |69.56 |
|32 |32 |2500 |1500 |132389.41 |0.23 |348.11 |928.31 |58.02 |2412.81 |10893.85 |86.71 |107.96 |
|48 |48 |2500 |1500 |198236 |0.23 |346.82 |924.85 |57.8 |3353.08 |19873.77 |130.01 |162.63 |
|64 |64 |2500 |1500 |241460.59 |0.25 |382.03 |1018.75 |63.67 |4231.3 |26655.71 |158.26 |195.83 |
|80 |80 |2500 |1500 |310641.77 |0.15 |217.99 |581.32 |36.33 |9358.43 |33755.17 |200.99 |240.58 |


<span id="16c0795e"></span>
## accuracy test

The SGLang\-based [MMLU accuracy test tool ](https://github.com/sgl-project/sglang/blob/main/benchmark/mmlu/bench_other.py)evaluates xLLM DeepSeek's accuracy to **89.5%**  :

```JSON
Average accuracy 0.920, latency 228.48, #q: 100 - abstract_algebra
Average accuracy 0.867, latency 169.80, #q: 135 - anatomy
Average accuracy 0.947, latency 196.47, #q: 152 - astronomy
Average accuracy 0.870, latency 77.30, #q: 100 - business_ethics
Average accuracy 0.928, latency 203.03, #q: 265 - clinical_knowledge
Average accuracy 0.979, latency 141.33, #q: 144 - college_biology
Average accuracy 0.730, latency 317.51, #q: 100 - college_chemistry
Average accuracy 0.890, latency 355.62, #q: 100 - college_computer_science
Average accuracy 0.890, latency 304.65, #q: 100 - college_mathematics
Average accuracy 0.908, latency 290.19, #q: 173 - college_medicine
Average accuracy 0.961, latency 174.44, #q: 102 - college_physics
Average accuracy 0.880, latency 105.63, #q: 100 - computer_security
Average accuracy 0.970, latency 157.97, #q: 235 - conceptual_physics
Average accuracy 0.842, latency 201.92, #q: 114 - econometrics
Average accuracy 0.876, latency 170.10, #q: 145 - electrical_engineering
Average accuracy 0.944, latency 228.55, #q: 378 - elementary_mathematics
Average accuracy 0.952, latency 243.86, #q: 126 - formal_logic
Average accuracy 0.660, latency 134.53, #q: 100 - global_facts
Average accuracy 0.948, latency 232.80, #q: 310 - high_school_biology
Average accuracy 0.897, latency 292.87, #q: 203 - high_school_chemistry
Average accuracy 0.960, latency 97.97, #q: 100 - high_school_computer_science
Average accuracy 0.885, latency 141.75, #q: 165 - high_school_european_history
Average accuracy 0.944, latency 97.97, #q: 198 - high_school_geography
Average accuracy 0.969, latency 115.37, #q: 193 - high_school_government_and_politics
Average accuracy 0.951, latency 319.19, #q: 390 - high_school_macroeconomics
Average accuracy 0.959, latency 469.05, #q: 270 - high_school_mathematics
Average accuracy 0.979, latency 171.25, #q: 238 - high_school_microeconomics
Average accuracy 0.887, latency 249.44, #q: 151 - high_school_physics
Average accuracy 0.967, latency 282.98, #q: 545 - high_school_psychology
Average accuracy 0.931, latency 240.87, #q: 216 - high_school_statistics
Average accuracy 0.951, latency 161.86, #q: 204 - high_school_us_history
Average accuracy 0.954, latency 217.05, #q: 237 - high_school_world_history
Average accuracy 0.839, latency 152.26, #q: 223 - human_aging
Average accuracy 0.947, latency 89.46, #q: 131 - human_sexuality
Average accuracy 0.917, latency 95.95, #q: 121 - international_law
Average accuracy 0.917, latency 81.23, #q: 108 - jurisprudence
Average accuracy 0.896, latency 139.88, #q: 163 - logical_fallacies
Average accuracy 0.812, latency 168.86, #q: 112 - machine_learning
Average accuracy 0.942, latency 75.59, #q: 103 - management
Average accuracy 0.949, latency 101.60, #q: 234 - marketing
Average accuracy 0.990, latency 104.15, #q: 100 - medical_genetics
Average accuracy 0.954, latency 356.24, #q: 783 - miscellaneous
Average accuracy 0.873, latency 240.59, #q: 346 - moral_disputes
Average accuracy 0.806, latency 999.57, #q: 895 - moral_scenarios
Average accuracy 0.935, latency 274.42, #q: 306 - nutrition
Average accuracy 0.897, latency 179.42, #q: 311 - philosophy
Average accuracy 0.926, latency 218.93, #q: 324 - prehistory
Average accuracy 0.826, latency 511.05, #q: 282 - professional_accounting
Average accuracy 0.760, latency 2197.88, #q: 1534 - professional_law
Average accuracy 0.963, latency 229.55, #q: 272 - professional_medicine
Average accuracy 0.928, latency 412.38, #q: 612 - professional_psychology
Average accuracy 0.800, latency 74.08, #q: 110 - public_relations
Average accuracy 0.861, latency 244.45, #q: 245 - security_studies
Average accuracy 0.965, latency 142.07, #q: 201 - sociology
Average accuracy 0.960, latency 74.24, #q: 100 - us_foreign_policy
Average accuracy 0.578, latency 170.61, #q: 166 - virology
Average accuracy 0.918, latency 90.26, #q: 171 - world_religions
{"task": "mmlu", "backend": "xllm", "num_gpus": 1, "latency": 20960.509, "accuracy": 0.895, "num_requests": 14042, "other": {"nsub": 57, "parallel": 16}}
```


<span id="883659d8"></span>
# Appendix

<span id="b1d76a2c"></span>
## stress testing

<span id="0b29943d"></span>
### SGLang's test method

<span id="58ee80cc"></span>
#### **Torture testing method** We use the industry\-wide approach torture testing xLLM and SGlang backend. The following script is derived from vllm:

https://github.com/vllm\-project/vllm/blob/main/benchmarks/benchmark_serving.py

There are usually two evaluation modes for using this script:


* Method 1: Yes Set \*\* `--request-rate`\*\*


The client side uses a Poisson process to simulate the arrival time of the request. The request\-rate is the number of requests sent per second. For example, setting it to 10 means sending 10 requests per second. It is also commonly referred to as RPS (Request Per Sec), which **represents the number of requests accepted per second by the service** . Use the request\-rate method to test, gradually increase the request rate from low to high, the client side sends requests continuously, and observe the system's output requests per second, TTFT, TPOT. If the request rate and the finished request per sec are approximately the same, it means that the RPS is within the system bearer limit at this time. Then observe whether the TTFT and TPOT satisfy the SLA, and find the critical point that does not satisfy the SLO. This is the upper limit of the system's carrying capacity.


* Method 2: Yes Set \*\* `--max-concurrency`\*\*


It is used to control the maximum number of concurrent requests and set the \-\-request\-rate inf. Indicates that the client side only allows the system to process max\-concurrency requests simultaneously. \*\* Indicates the number of users simultaneously waiting for the request to complete. For example, if max\-concurrency is 10, then the client side first sends 10 requests to keep the service busy. As soon as one request is completed, a new one will be sent immediately to ensure that the server level is busy processing 10 requests at the same time. There is no essential difference between controlling the request rate and controlling max\-concurrency. The request rate is still within the bearer range of the system, and increasing RPS means increasing max\-concurrency.

In papers evaluating "small" models such as Qwen and Llama, the request rate approach is usually used. Because the max concurrency the request can withstand is very high. For example, if the request rate is 4, the system concurrency can reach 40; if the request rate is 10, the system concurrency can reach 80. For example, in 4, 6, 8, 12,... mode sampling request rate, you can touch the upper limit.

In evaluating the "big" model of DeepSeek R1, it is **recommended to use the method of controlling max\-concurrency** . Because the max concurrency that a request can withstand is relatively low, it is more accurate to control the granularity of max\-concurrency than to control the request rate. For example, when the request rate = 2, the concurrency of the system may have reached the upper limit. Request rate may need to be sampled at 0.1 granularity, but sampling max concurreny in 4, 6, 8, 12,... can more accurately control the load.

<span id="b9fc023b"></span>
#### SGLang environment configuration


* Mirror: You can select \*\* "Preset mirror" \- "SGLang" \*\* in the console, or you can directly enter the following address


```Python
vemlp-ap-southeast-1.cr.volces.com/preset-images/sglang-edge:0.4.2.post4
```



* Number of instances: Set to 2

* Example Specifications: Select "ml.hpcpni3l.48xlarge"

* Entry command:


```Python
MODEL_PATH=/amltest-stg/gw_test/DeepSeek-R1     # Needs to be updated to the actual storage path of the model

IP_PORT=$MLP_ROLE_HEAD_IP:20000

NCCL_SOCKET_IFNAME=eth1 GLOO_SOCKET_IFNAME=eth1 python3 -m sglang.launch_server \
  --model-path $MODEL_PATH \
  --tp 16 \
  --dist-init-addr $IP_PORT \
  --nnodes 2 \
  --node-rank $MLP_ROLE_INDEX \
  --trust-remote-code \
  --host 0.0.0.0 \
  --port 8080 \
  --enable-metrics

# You need to modify `--port` to a port opened for HTTP protocol,
# and also ensure the corresponding port is allowed in the SecurityGroup settings
```


<span id="94ddb956"></span>
#### SGLang test script

```Python
#!/bin/bash

# Define input and output lengths
INPUT_LEN=3500
OUTPUT_LEN=1500

# Create logs directory (if it does not exist)
mkdir -p logs

# Define request rates and max concurrency
declare -a request_rates=(1 4 8 16 32 48 64 80 128 160)
declare -a max_concurrency=(1 4 8 16 32 48 64 80 128 160)
declare -a num_prompts=(4 16 32 64 128 192 256 320 512 640)

# Run benchmark tests
for i in "${!request_rates[@]}"; do
    RATE=${request_rates[$i]}
    CONCURRENCY=${max_concurrency[$i]}
    PROMPTS=${num_prompts[$i]}
    
    echo "Running benchmark with request rate $RATE, concurrency $CONCURRENCY, prompts $PROMPTS"
    
    python3 -m sglang.bench_serving --backend sglang \
        --dataset-name random \
        --dataset-path ./ShareGPT_V3_unfiltered_cleaned_split.json \
        --random-input-len $INPUT_LEN \
        --random-output-len $OUTPUT_LEN \
        --random-range-ratio 1 \
        --request-rate $RATE \
        --max-concurrency $CONCURRENCY \
        --num-prompts $PROMPTS \
        --host 0.0.0.0 --port 40000 \
        > logs/${CONCURRENCY}_fp8_r1_${INPUT_LEN}_${OUTPUT_LEN}.txt 2>&1
    
    wait
done
```


<span id="7ffeedf7"></span>
### Test Methods for xLLM

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0161a9b1f1f044ceac038779337f7e3b~tplv-goo7wpa0wc-image.image" name="sglang-testing.zip">sglang-testing.zip</Attachment>


```Bash
# Modify --base-url to the model inference service endpoint
bash sglang-testing/bench.sh
```
