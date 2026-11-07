---
title: "Collab Search Agent API Reference"
product: "Byteplus AskEcho"
product_code: "askecho"
source: "https://docs.byteplus.com/en/docs/askecho/Collab_Search_Agent_API_Reference"
---

This document introduces the input and output parameters for the collab search agent API interface. By calling this interface, you can retrieve search results related to the search query. Building on this, it provides large model content summarization to obtain a refined and summarized single\-paragraph content, enhancing the efficiency of information acquisition. You can adapt these data for use in your project.

&nbsp;

<span id="46AZ9217"></span>
# Authentication Method

API Key access method is provided **only**.


1. **Obtain API Key**

   1. Open and log in to [Askecho-APIKey Management](https://console.byteplus.com/bp-ask-echo/api-key)。

   2. Click the [Create API Key] button to enter and create an API Key.

   3. Fill in the API Key Name in the pop\-up text box, and click Create.


> **Note**: Please keep your API Key safe. It is strongly recommended NOT to hardcode it directly into the code calling the model.



2. **Signature Construction**


The API Key signature authentication method requires adding Authorization in the HTTP request header as follows:

```Plain Text
Authorization: Bearer <API_KEY>
```


&nbsp;

<span id="dt5mreUC"></span>
# Interface Details

<span id="PnWvMhr3"></span>
### URL


|**URL** |https://torchlight.byteintlapi.com/agent_api/agent/collab |
|---|---|
|**Method** |POST |
|**Content\-Type** |application/json |


<span id="AgXFcq1e"></span>
## Request

<span id="i3wE0su4"></span>
### Request


|**Field Name (Level 1)**  |**Field Name (Level 2)**  |**Type** |**Required** |**Description** |
|---|---|---|---|---|
|Query | |String |Yes<br><br> |User search query, max 400 characters or 50 words, multi\-word search not supported. |
|Count | |Number |No |Number of returned items, max 20, default 10. |
|Filter | |Object |No |Filter conditions. |
| |Sites |String |No |Specify the Site scope for searching, multiple domains separated by '\|', max 5 supported.<br><br>Must input full domain, example: bytedance.com\|mp.qq.com |
| |BlockHosts |String |No |Specify blocked search Sites, multiple domains separated by '\|', max 5 supported.<br><br>Must input full domain, example: bytedance.com\|mp.qq.com |
| |Language |String |No |Specify language, BCP 47 format.<br><br><br>* EN: English (General, default)<br><br>* ZH\-HANS: Simplified Chinese<br><br>* ZH\-HANT: Traditional Chinese |
|TimeRange | |String |No |Specify the publication time for searching.<br><br>The following enumeration values; if empty, there is no restriction:<br><br><br>* OneDay: Within 1 day<br><br>* OneWeek: Within 1 week<br><br>* OneMonth: Within 1 month<br><br>* OneYear: Within 1 year<br><br>* YYYY\-MM\-DD..YYYY\-MM\-DD: Content published between Date A (inclusive) and Date B (inclusive), example "2024\-12\-30..2025\-12\-30" |


<span id="AOxxpsvy"></span>
## Response

<span id="GvhsUXjj"></span>
### Response


|**Field **  |**Type** |**Required** |**Description** |
|---|---|---|---|
|ResponseMetadata |Object |Yes |Standard response metadata. |
|Result |SearchResponse |No |Search results. null if the request fails at the API layer. |


**ResponseMetadata**


|**Field **  |**Type** |**Required** |**Description** |
|---|---|---|---|
|RequestId |String |Yes |Request ID. Matches the X\-Tt\-Logid response header. |
|Action |String |Yes |Always an empty string for this endpoint. |
|Version |String |Yes |Always an empty string for this endpoint. |
|Service |String |Yes |Always an empty string for this endpoint. |
|Region |String |Yes |Always an empty string for this endpoint. |
|Error |Object |No |API\-level error details, such as RPC, parameter, authentication, or service plan errors. |


**SearchResponse**


|**Field Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|ResultCount |Number |Yes |Number of results found. |
|WebResults |Array[WebItem] |No |List of search results. Each item follows the WebItem schema. |
|Choices |Array[Choice] |No |Streaming/non\-streaming response content. |
|Usage |Usage |No |Token and time consumption amount, output in the final frame. |
|SearchContext |SearchContext |Yes |Search context, including the original query, search type, and related metadata. |
|TimeCost |Number |Yes |Request latency in milliseconds. |
|LogId |String |Yes |Log ID. Matches the X\-Tt\-Logid response header. |


<span id="t60Zq8Nh"></span>
#### WebItem\-Search Result Item

> Web search result item



|**Field Name (Level 1)**  |**Field Name (Level 2)**  |**Type** |**Required** |**Description** |
|---|---|---|---|---|
|Id | |String |Yes |Result ID. |
|SortId | |Number |Yes |Sort ID. |
|Title | |String |Yes |Title. |
|SiteName | |String |No |Site name. |
|Url | |String |No |Landing page URL. |
|Snippet | |String |Yes |Relevant excerpt, approximately 100 characters. |
|Summary | |String |No |Model\-processed excerpt of the relevant content, approximately 300–500 characters. |
|PublishTime | |String |No |Publication time in ISO format. e.g. 2025\-05\-30T19:35:24+08:00 |
|LogoUrl | |String |No |Landing\-page favicon URL. |
|PublishTimeUnix | |Number |No |Publication time as a Unix timestamp in seconds. A value of 0 indicates that no valid publication time was returned. |


<span id="4myhnKa5"></span>
#### Choice\-Model Summary Result Item

> SearchType=web_summary，model summary result item.



|**Field Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Delta |Object |No |Used for streaming response. Contains incrementally updated content:<br><br><br>* role: Role identifier<br><br>* content: Text fragment |
|Message |Object |No |Used for non\-streaming response. Contains the complete reply message, same structure as Delta. |
|FinishReason |String |Yes |Reason for termination of generation, possible values:<br><br><br>* stop: API returned complete model output<br><br>* length: Reached max token limit<br><br>* content_filter: Content was filtered<br><br>* null: Generation not yet completed |
|Index |Number |Yes |Current selected index number. Usually 0 in a single response, may have multiple indices in multi\-choice configuration. |


<span id="reAJ2mw8"></span>
#### Usage\-Token and Time Usage Result


|**Field Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|PromptTokens |Number |Yes |Number of model input tokens in this request (including intent, rewriting, summarization, etc.). |
|CompletionTokens |Number |Yes |Number of model output tokens in this request (including intent, rewriting, summarization, etc.). |
|TotalTokens |Number |Yes |Total number of tokens consumed in this request (input + output). |
|SearchTimeCost |Number |Yes |Search time cost for this request. |
|FirstTokenTimeCost |Number |Yes |First frame time cost for this request. |
|TotalTimeCost |Number |Yes |Total time cost for this request. |


<span id="ZW4dRFOW"></span>
#### SearchContext\-Search Context Information


|**Field Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|SearchType |String |Yes |Search type enumeration value, default web. |
|OriginQuery |String |Yes |Original Query. |


<span id="Cjcd2N7f"></span>
## Request Example

```JSON
{
    "Query": "最新的北京游玩攻略",
    "Count": 5,
    "TimeRange":"OneYear"
}
```


<span id="VN6XFL5X"></span>
## Response Examples

<span id="vcTuvcBf"></span>
### Normal Request Examples


* First Frame (Search Results)


```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026091400000000000000000000000000",
        "Action": "",
        "Version": "",
        "Service": "",
        "Region": ""
    },
    "Result": {
        "ResultCount": 5,
        "WebResults": [
            {
                "Id": "7f22c69c3affd886584c30f4ddbb5ba5",
                "SortId": 1,
                "Title": "Beijing 2026 Travel Guide: Must-See Attractions & Tips - KKday",
                "SiteName": "",
                "Url": "https://www.kkday.com/en-us/destination/cn-beijing",
                "Snippet": "Plan your 2026 Beijing adventure with KKday! Discover essential travel tips, top attractions like th",
                "Summary": "Plan your 2026 Beijing adventure with KKday! Discover essential travel tips, top attractions like the Great Wall, and insider advice for an unforgettable trip.",
                "PublishTime": "2026-08-09T08:00:00+08:00",
                "LogoUrl": "https://p16-bpsearch-sign.ibyteimg.com/tos-mya-i-hgu9vfkfc6/239e01827d2445f89afe03f57c5a762d~tplv-hgu9vfkfc6-image.jpeg?rk3s=c7144bbe&x-expires=1789472620&x-signature=mkI5PVdNw3GZe0ESV4j2C3zvPMk%3D",
                "PublishTimeUnix": 1786233600
            },
            {
                "Id": "86bfd9ad66e686881199e1eee1f0bcd9",
                "SortId": 2,
                "Title": "THE 15 BEST Things to Do in Beijing (2026) - Must-See Attractions",
                "SiteName": "猫途鹰网",
                "Url": "https://www.tripadvisor.com/Attractions-g294212-Activities-Beijing.html",
                "Snippet": "Things to Do in Beijing, China: See Tripadvisor's 756,318 traveler reviews and photos of Beijing tou",
                "Summary": "Things to Do in Beijing, China: See Tripadvisor's 756,318 traveler reviews and photos of Beijing tourist attractions. Find what to do today, this weekend, or in September. We have reviews of the best places to see in Beijing. Visit top-rated & must-see attractions.",
                "PublishTime": "2026-08-04T22:32:40+08:00",
                "LogoUrl": "https://p16-bpsearch-sign.ibyteimg.com/tos-mya-i-hgu9vfkfc6/a254d7e9b09c4653854ddeb6054711c6~tplv-hgu9vfkfc6-image.jpeg?rk3s=c7144bbe&x-expires=1789472620&x-signature=Mf5iZ0IZWLeHt8utEeAoX27HXQQ%3D",
                "PublishTimeUnix": 1785853960
            },
            {
                "Id": "0c3ab874f0ff4f9c6558ef7d9d30ed70",
                "SortId": 3,
                "Title": "北京自由行完整攻略：2026年最新景點介紹、美食...",
                "SiteName": "中華遊 JetSo",
                "Url": "https://chinatraveljetso.com/%E5%8C%97%E4%BA%AC%E8%87%AA%E7%94%B1%E8%A1%8C/",
                "Snippet": "作為中國多個朝代的古都，北京擁有豐富的歷史文化底蘊，擁有豐富的世界遺產，近年前往北京體驗千年歷史文化成為港人旅行熱門選擇。 · 本篇北京自由行攻略將為您準備從故宮、長城的最佳遊覽路線詳細，介紹行前準備",
                "Summary": "作為中國多個朝代的古都，北京擁有豐富的歷史文化底蘊，擁有豐富的世界遺產，近年前往北京體驗千年歷史文化成為港人旅行熱門選擇。 · 本篇北京自由行攻略將為您準備從故宮、長城的最佳遊覽路線詳細，介紹行前準備、必去景點、美食推薦以及完整的五日行程規劃，讓您的北京之旅更加充實精彩。。ChinaTravelJetSo 編輯仲為你搜羅了最新的旅遊優惠碼，以及旅遊平台一些隱藏推廣頁面——最多減盡有200蚊，記住睇到最後啦！ · 行前準備：北京自由行出發前必知事項 ... 先分享最新獨家旅遊優惠給大家，睇到最後仲有一些旅遊平台一些隱藏推廣頁面！ · 從香港前往北京主要有飛機和高鐵兩種方式，兩者各有優劣，可根據您的預算、時間和旅伴需求來選擇。。飛機是往返兩地最快的方式，飛行時間僅需約3.5小時，適合追求效率、旅程時間較短的旅客。 · 主要航空公司：國泰航空 (Cathay Pacific)、中國國際航空 (Air China)、香港航空 (Hong Kong Airlines)。 · 價格參考：經濟艙來回機票約港幣$2,500 – $4,500。建議提前2-3個月預訂，並避開公眾假期旺季。 ... 從香港西九龍站乘搭高鐵直達北京西站，是個舒適且能沿途欣賞風景的選擇，特別適合家庭及長者同行。。使用一卡通乘搭巴士更可享半價優惠。（機場巴士除外）你可以在各地鐵站的客戶服務中心購買，需付¥20按金，離京前可辦理退卡取回按金，也可在手機上下載。 ... 打開北京地圖，以天安門為中心，往外擴散出二環、三環、四環、五環，北京知名景點及熱鬧老街幾乎都位於二環內，因此住在二環內是最方便的。",
                "PublishTime": "2026-02-09T17:32:15+08:00",
                "LogoUrl": "https://p16-bpsearch-sign.ibyteimg.com/tos-mya-i-hgu9vfkfc6/b021d1c648f24ee3ba2298d110123ef8~tplv-hgu9vfkfc6-image.jpeg?rk3s=c7144bbe&x-expires=1789472620&x-signature=WlkiT6awf35ef0yAvSZi%2BGbRC3I%3D",
                "PublishTimeUnix": 1770629535
            },
            {
                "Id": "03b17ca041f71a35b565fcff1fcded2f",
                "SortId": 4,
                "Title": "北京自由行旅游攻略2026:景点推荐",
                "SiteName": "",
                "Url": "https://www.klook.com/en-US/destination/c57-beijing/",
                "Snippet": "Find the top things to do in Beijing this 2026! Explore must-visit spots, top tours, and book your a",
                "Summary": "Find the top things to do in Beijing this 2026! Explore must-visit spots, top tours, and book your activities on Klook.",
                "PublishTime": "2026-06-29T04:42:21+08:00",
                "LogoUrl": "https://p16-bpsearch-sign.ibyteimg.com/tos-mya-i-hgu9vfkfc6/5d03aef65c0240d0b016fd5a6b3d5752~tplv-hgu9vfkfc6-image.jpeg?rk3s=c7144bbe&x-expires=1789472620&x-signature=kIlBeqiRiobSwyn3DmYd%2BOsk1d0%3D",
                "PublishTimeUnix": 1782679341
            },
            {
                "Id": "3d599365433c4023ecb482df32183e35",
                "SortId": 5,
                "Title": "【北京攻略】去北京必打卡的10大景点和好去处！ ...",
                "SiteName": "",
                "Url": "https://www.klook.com/zh-CN/blog/must-visit-attraction-beijing/",
                "Snippet": "以上就是边辑整理出的北京必访古迹！推荐给喜欢历史、文化、人文的旅客，亲眼见证这些历史总有另一番感受！有些园区如圆明园、颐和园十分广大，需要不少体力与时间，建议可以排上半天到一天，而后再接些放松行程啰！",
                "Summary": "以上就是边辑整理出的北京必访古迹！推荐给喜欢历史、文化、人文的旅客，亲眼见证这些历史总有另一番感受！有些园区如圆明园、颐和园十分广大，需要不少体力与时间，建议可以排上半天到一天，而后再接些放松行程啰！ ... 💡Klook 小贴士💡 立即下载Klook App以获取专为你提供的最佳旅行优惠和最新更新！可在 App Store 和 Play Store 下载。。上海 北京 成都 云南 张家界 重庆 广州 哈尔滨 深圳 苏州 & 杭州 西安 青岛 厦门 广东 南京 桂林 内蒙古 珠海 ... 奢华秀美的皇家园林、历经战争的断垣残壁、市井小民的传统街道，到北京总要体验一个『老』字，回味百年前的热闹盛世。 此篇「 北京必去景点 」特辑，要来介绍来北京不可错过的名胜古迹，各个拥有厚重的历史感，让旅程不虚此行！。「台湾故宫看宝物，北京故宫看建筑！」编辑曾经在北京听到这样一段有趣的话语，说的可真没错。 来故宫走一遭，会发现看的除了宝物之外，更多的是现场给的历史感。 皇帝登基于宝座、各地百官于殿内朝贺、抑或妃子休憩的房间，这些历史记载的曾经真实于此上演过。 故宫又名紫禁城，曾是二十四位皇帝的宫殿，有四座城门及城外护城河守护着，是北京必去的标志与象征。 回想明、清时期的热闹场景，百年后则成为中国各地观光客争相朝圣的必去景点！。由三座广大花园组成，座落于北京西郊的圆明园有着美称万园之园，是清朝皇帝创建的皇家宫苑之一。 园区内有湖泊、迷宫、洋楼、城堡、庭院等，也因为占地实在是太广大，一般观光客很难在一天走完。 编辑推荐里头必访景点大水法、迷宫万花阵。 其中大水法曾是中西设计的喷水池，由十二生肖的动物排列成，代表十二个时辰，每日固定向中央喷水报时，可想当时场景的气势。 虽然经历了英法、八国联军，许多古迹已残破不堪，但透过现场残迹及一旁说明图，能够想像当时壮观面貌。",
                "PublishTime": "2026-06-04T16:19:43+08:00",
                "LogoUrl": "https://p16-bpsearch-sign.ibyteimg.com/tos-mya-i-hgu9vfkfc6/5d03aef65c0240d0b016fd5a6b3d5752~tplv-hgu9vfkfc6-image.jpeg?rk3s=c7144bbe&x-expires=1789472620&x-signature=kIlBeqiRiobSwyn3DmYd%2BOsk1d0%3D",
                "PublishTimeUnix": 1780561183
            }
        ],
        "SearchContext": {
            "OriginQuery": "最新的北京游玩攻略",
            "SearchType": "agent_collab"
        },
        "TimeCost": 28,
        "LogId": "2026091400000000000000000000000000",
        "Choices": null,
        "Usage": null
    }
}
```



* Process Frame (Streaming Summary)


```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026091400000000000000000000000000",
        "Action": "",
        "Version": "",
        "Service": "",
        "Region": ""
    },
    "Result": {
        "ResultCount": 0,
        "WebResults": null,
        "SearchContext": {
            "OriginQuery": "最新的北京游玩攻略",
            "SearchType": "agent_collab"
        },
        "TimeCost": 0,
        "LogId": "2026091400000000000000000000000000",
        "Choices": [
            {
                "Delta": {
                    "Role": "assistant",
                    "Content": "###"
                },
                "Message": null,
                "FinishReason": "",
                "Index": 0
            }
        ],
        "Usage": null
    }
}
```



* Final Frame (Token Consumption)


```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026091400000000000000000000000000",
        "Action": "",
        "Version": "",
        "Service": "",
        "Region": ""
    },
    "Result": {
        "ResultCount": 0,
        "WebResults": null,
        "SearchContext": {
            "OriginQuery": "最新的北京游玩攻略",
            "SearchType": "agent_collab"
        },
        "TimeCost": 0,
        "LogId": "2026091400000000000000000000000000",
        "Choices": [
            {
                "Delta": {
                    "Role": "assistant",
                    "Content": ""
                },
                "Message": null,
                "FinishReason": "",
                "Index": 0
            }
        ],
        "Usage": {
            "PromptTokens": 3090,
            "CompletionTokens": 147,
            "TotalTokens": 3237,
            "SearchTimeCost": 28,
            "FirstTokenTimeCost": 905,
            "TotalTimeCost": 4707
        }
    }
}
```



* End Identifier


```JSON
[DONE]
```


<span id="4pvnMtoS"></span>
### Error Request Return Example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202505231206578F7BD0BCD73AF8703C1E",
        "Action": "WebSearch",
        "Version": "2025-01-01",
        "Service": "volc_torchlight_api",
        "Region": "cn-beijing",
        "Error": {
            "CodeN": 10400, // 该字段为错误码
            "Code": "10400",
            "Message": "query is empty"
        }
    },
    "Result": null
}
```


&nbsp;

<span id="KOcVE14Q"></span>
# Error Handling


|**Error Code** |**Description** |**Recommended Check/Handling Method** |
|---|---|---|
|10400 |General parameter error |Check the request body, especially the field types. |
|10403 |Permission error |Check whether the required service is enabled for the account. |
|10500 |Default internal error |This is a fallback server\-side error code. Retrying the request usually resolves the issue. |
|700901 |Invalid ApiKey |Check that the ApiKey is provided and passed correctly. See Authentication. |
|700429 |Request volume exceeded limit |Limit the number of concurrent search requests per second. |
