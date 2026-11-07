---
title: "Searchinfinity Search API Reference-Omnira"
product: "Searchinfinity"
product_code: "searchinfinity"
source: "https://docs.byteplus.com/en/docs/searchinfinity/Searchinfinity-Search-API-Reference-Omnira"
---

This document describes the input and output parameters of the Omnira Search API. Use this API to retrieve search results related to a query and integrate the returned data into your application.

&nbsp;

<span id=""></span>
# Authentication Method

Provides APIKey access method.


1. **Obtain an API Key**

* Log in to the console and navigate to **API Key**.

* Click **Create Key**.

* Enter an API Key name in the dialog box and click **Create Key**.


> Note: Keep your API Key secure. It is strongly recommended not to hardcode the key directly in your application code.



2. **Signature Construction**


The API Key authentication method requires adding Authorization header in the HTTP request as follows:

```Plain Text
Authorization: Bearer <API_KEY>
```


&nbsp;

<span id=""></span>
# Interface Details

<span id=""></span>
## URL


|**URL** |**https://torchlight.byteintlapi.com/search_api/omnira_search** |
|---|---|
|Method |POST |
|Content\-Type |application/json |


&nbsp;

<span id=""></span>
## Request 

<span id=""></span>
### web search

Returns matching web documents and, when available, images from those documents.


|**Field (Level 1)**  |**Field (Level 2)**  |**Type** |**Required** |**Default** |**Description** |
|---|---|---|---|---|---|
|Query<br><br> | &nbsp;<br><br> |String<br><br> |Yes |\- |Search query,cannot be empty. When SearchType=web, advanced query operators are supported:<br><br><br>* Site: Filters results by domain, e.g.  "Musk site:www.tesla.com"<br><br>* Recency: Filters results by publication time, 0 < recency <= 30. e.g."financial news recency:1"<br><br>* Multiple operators can be combined, e.g. "financial news site:www.cnfin.com recency:1" |
|SearchType |  |String |No |web |Search type. "web" for web search. Defaults to web when omitted. |
|DocCount |  |Number |No |10 |Number of documents to return. Values greater than 0 take effect. Max 20. |
|MaxSnippetLength |  |Number |No |300 |Applies only when SearchType=web. Maximum length of each snippet. Values greater than 0 take effect. Max 3000. |
|MaxImageCountPerDoc<br><br> |  |Number |No |1 |Applies only when SearchType=web. Maximum number of images returned per document. Values greater than 0 take effect. Max 10. |


<span id=""></span>
### Image search

Returns matching images with context from their source documents.


|**Field (Level 1)**  |**Field (Level 2)**  |**Type** |**Required** |**Default** |**Description** |
|---|---|---|---|---|---|
|Query |  |String |Yes |\- |Search query,cannot be empty. |
|SearchType |  |String |Yes |\- |Search type. "image" for image search.  |
|DocCount |  |Number |No |5 |Number of images to return. Values greater than 0 take effect. Max 20. |
|ImageFilter | |Object |No |\- |Applies only when SearchType=image. |
| |ShortEdgePixelMin |Number |No |\- |Minimum length of the image’s shorter edge, in pixels. The shorter edge is defined as min(width, height). A value of 0 or less is ignored. |
| |ShortEdgePixelMax |Number |No |\- |Maximum length of the image’s shorter edge, in pixels. A value of 0 or less is ignored. If ShortEdgePixelMin is greater than ShortEdgePixelMax, short\-edge filtering is not applied. |
| |AspectRatioMin |Number |No |\- |Minimum image aspect ratio, defined as height / width. A value of 0 or less is ignored. |
| |AspectRatioMax |Number |No |\- |Maximum image aspect ratio, defined as height / width. A value of 0 or less is ignored. If AspectRatioMin is greater than AspectRatioMax, aspect\-ratio filtering is not applied. |


&nbsp;

<span id=""></span>
## Response

<span id=""></span>
### Response


|**Field **  |**Type** |**Required** |**Description** |
|---|---|---|---|
|ResponseMetadata |Object |Yes |Standard response metadata. |
|Result |OmniraSearchResult |No |Search results. null if the request fails at the API layer. |


**ResponseMetadata**


|**Field **  |**Type** |**Required** |**Description** |
|---|---|---|---|
|RequestId |String |Yes |Request ID. Matches the X\-Tt\-Logid response header. |
|Action |String |Yes |Always an empty string for this endpoint. |
|Version |String |Yes |Always an empty string for this endpoint. |
|Service |String |Yes |Always an empty string for this endpoint. |
|Region |String |Yes |Always an empty string for this endpoint. |
|Error |Object |No |API\-level error details, such as RPC, parameter, authentication, or service plan errors. |


**Result**


|**Field **  |**Type** |**Required** |**Description** |
|---|---|---|---|
|TotalDocCount |Number |Yes |Total number of matching documents. May differ from the number returned in Documents |
|Documents |Array[OmniraSearchDocument] |No |Documents returned for this request, limited by DocCount. |
|ErrorCode |Number |Yes |Internal service error code. |
|ErrorMsg |String |Yes |Internal service error message. |
|TimeCost |Number |Yes |Request latency in milliseconds. |


**OmniraSearchDocument**


|**Field **  |**Type** |**Required** |**Description** |
|---|---|---|---|
|Rank |Number |Yes |Position of the result in the ranked list. |
|Url |String |No |Document URL. |
|Title |String |No |Document title. |
|Snippet |Array[OmniraSearchSnippet] |No |* When SearchType=web<br><br><br>Content snippets, with images from the document when available. Limits are controlled by MaxSnippetLength and MaxImageCountPerDoc.<br><br><br>* When SearchType=image<br><br><br>Images and context from their source documents. |
|DocumentInfo |OmniraSearchDocumentInfo |No |Document metadata. For image searches, only Filetype is populated. |
|HostInfo |OmniraSearchHostInfo |No |Site information. Returned only when SearchType=web |


**OmniraSearchSnippet**


|**Field **  |**Type** |**Required** |**Description** |
|---|---|---|---|
|Type |String |No |Snippet type.  |
|Text |String |No |Text snippet.<br><br><br>* When SearchType=web, query\-relevant snippet from the source document.<br><br>* When SearchType=image, context from the image’s source document. |
|Image |OmniraSearchSnippetImage |No |Image snippet. |


**OmniraSearchSnippetImage**


|**Field **  |**Type** |**Required** |**Description** |
|---|---|---|---|
|Width |Number |No |Image width in pixels. |
|Height |Number |No |Image height in pixels. |
|ImageUrl |String |No |Image URL.<br><br><br>* When SearchType=web, image from the source document.<br><br>* When SearchType=image, image relevant to the query. |
|Alt |String |No |Image alternative text.  |
|ThumbnailUrl |OmniraSearchThumbnailUrl |No |Thumbnail image Url. |


**ThumbnailUrl\-Thumbnail Image Snippet**


|**Field **  |**Type** |**Required** |**Description** |
|---|---|---|---|
|Tiny<br><br> |String |No |URL of the extra\-small thumbnail. The longest edge is 112 pixels. |
|Small |String |No |URL of the small thumbnail. The longest edge is 224 pixels. |
|Medium |String |No |URL of the medium thumbnail. The longest edge is 448 pixels. |
|Large |String |No |URL of the large thumbnail. The longest edge is 896 pixels. |


**OmniraSearchDocumentInfo**


|**Field **  |**Type** |**Required** |**Description** |
|---|---|---|---|
|Filetype |String |No |Document type. |
|ContentLength |Number |No |Content length in tokens. Available only when SearchType=web. |
|PublishTime |String |No |Publication time in the format. Available only when SearchType=web. |


**OmniraSearchHostInfo**

Available only when SearchType=web. This field is not returned when SearchType=image.


|**Field **  |**Type** |**Required** |**Description** |
|---|---|---|---|
|Hostname |String |No |Site hostname. |
|IconUrl |String |No |Site favicon URL. |


&nbsp;

<span id=""></span>
## Sample request

<span id=""></span>
### web search request

```JSON
{
  "Query": "latest AI technology",
  "SearchType": "web",
  "DocCount": 5,
  "MaxSnippetLength": 300,
  "MaxImageCountPerDoc": 1
}
```


<span id=""></span>
### image search request

```JSON
{
  "Query": "Beijing‘s Autumn",
  "SearchType": "image",
  "DocCount": 5,
  "ImageFilter": {
    "ShortEdgePixelMin": 300,
    "ShortEdgePixelMax": 2000,
    "AspectRatioMin": 0.5,
    "AspectRatioMax": 2.0
  }
}
```


&nbsp;

<span id=""></span>
## Sample response

<span id=""></span>
### Successful Request Example

<span id=""></span>
#### web search response

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
        "TotalDocCount": 20,
        "Documents": [
            {
                "Rank": 0,
                "Url": "https://deepmind.google/",
                "Title": "Google DeepMind",
                "Snippet": [
                    {
                        "Type": "text",
                        "Text": "Latest news\nIntroducing Gemini 3.8 Flash and 3.8 Flash Cyber\nSeptember 2026\nModelsAlphaGenome Atlas: A predictive map of every possible DNA letter change in the human genome\nSeptember 2026\nScienceIntroducing WeatherNext 3, our most advanced and accurate global weather AI model\nSeptember 2026\nScienceProactive cyber defense for governments and enterprises\nSeptember 2026\nModelsIntroducing agentic video understanding with Gemini\nSeptember 2026\nModelsGemini Omni 1.1 Flash lets you build with more control\nAugust 2026\nModelsPiloting the world's first double-blind AI evaluations\nAugust 2026\nResponsibility & SafetyIntelligent transcription with Gemini 3.5 Transcribe\nAugust 2026From Atari to EVE Online: Building on 15 Years of AI Research in Games\nAugust 2026\nResearchModels\nBuild with our next generation AI systems\nNew\nGemini\nFrontier intelligence with action\nGemini app\nGoogle AI Studio\nGoogle Antigravity\nGemini Enterprise Agent Platform\nNew\nGemini Audio\nAdvanced real-time audio models, built on Gemini\nGoogle AI Studio\nGemini API\nGemini Live API\nGemini Omni\nCreate anything from anything, starting with video\nGemini app\nGoogle Flow\nNano Banana ...\n"
                    }
                ],
                "DocumentInfo": {
                    "Filetype": "webpage",
                    "ContentLength": 3850
                },
                "HostInfo": {
                    "Hostname": "Google DeepMind",
                    "IconUrl": "https://p19-volcsearch-d-sign-sg.ibyteimg.com/tos-alisg-i-h9hire4aei-sg/img/b8235b2a70b77a5603b0d1ed7e701f0f~tplv-h9hire4aei-224.jpeg?rk3s=feb11e32&x-expires=1794561372&x-signature=Jr%2FpFXO%2BX%2FvszoCTXObaHBd7msM%3D"
                }
            },
            {
                "Rank": 1,
                "Url": "https://blog.csdn.net/liuzixu34/article/details/158687733",
                "Title": "2026年AI圈最前沿全景报告:从对话工具到自主智能，技术与产业的全面跃迁_人工智能前沿最新进展-CSDN博客",
                "Snippet": [
                    {
                        "Type": "text",
                        "Text": "最新推荐文章于 2026-08-22 21:57:54 发布\n原创 于 2026-03-16 16:06:55 发布 · 2.3w 阅读\n2026年AI圈最前沿全景报告：从对话工具到自主智能，技术与产业的全面跃迁\n2026年，人工智能行业彻底告别“大模型军备竞赛”的野蛮生长阶段，迈入“技术深耕、价值落地、生态完善、治理规范”的高质量发展新时期。这一年，AI的核心突破不再局限于参数规模的堆砌，而是聚焦“认知升级、物理交互、效率提升、安全可控”四大核心目标，实现了从“虚拟对话”到“现实行动”、从“单点赋能”到“全链重构”、从“技术突破”到“产业普惠”的三重跨越。\n本文将从技术范式重构、核心技术突破、细分领域前沿、产业深度落地、生态与治理、挑战与展望六大维度，结合2026年最新技术成果、标杆案例、行业数据，全面梳理AI圈最前沿动态，拆解技术迭代逻辑与产业应用路径，为从业者、研究者提供一份全面、详实的前沿参考。\n世界模型是2026年AI圈的核心技术热点，其核心逻辑是让AI摆脱“...\n"
                    }
                ],
                "DocumentInfo": {
                    "Filetype": "webpage",
                    "ContentLength": 16950,
                    "PublishTime": "2026-08-22T13:57:54Z"
                },
                "HostInfo": {
                    "Hostname": "CSDN博客",
                    "IconUrl": "https://p19-volcsearch-d-sign-sg.ibyteimg.com/tos-alisg-i-h9hire4aei-sg/img/a1684c00ee5f4a62c7c1047d6d51b665~tplv-h9hire4aei-224.jpeg?rk3s=feb11e32&x-expires=1794561372&x-signature=VX7Je%2BrjJARwojt7UY3ofar5FYY%3D"
                }
            },
            {
                "Rank": 2,
                "Url": "https://www.synapnews.com/articles/openais-gpt-6-astra-features-and-gpt-56-sol-autonomous-ai-arrives-in-2026",
                "Title": "OpenAI’s GPT-6 Astra Features & GPT-5.6 Sol: Autonomous AI Arrives in 2026",
                "Snippet": [
                    {
                        "Type": "text",
                        "Text": "technology news visual for openai ’s gpt - 6 astra features & gpt - 5 . 6 sol : autonomous ai arrives in 2026 photo by conny schneider on unsplash . jump to section the evolution of autonomy ..."
                    }
                ],
                "DocumentInfo": {
                    "Filetype": "webpage",
                    "PublishTime": "2026-09-09T22:22:53+08:00"
                },
                "HostInfo": {
                    "Hostname": "SynapNews"
                }
            },
            {
                "Rank": 3,
                "Url": "https://openai.com/zh-Hans-CN/research/",
                "Title": "研究 | OpenAI",
                "Snippet": [
                    {
                        "Type": "text",
                        "Text": "GPT\nOpenAI 的 GPT 系列模型是快速、多用途、高性价比人工智能系统，旨在理解背景信息、生成内容，并对文本、图片等进行推理。\n目前针对专业化工作负载能力最强、效率最高的前沿模型\n发布\n2026年9月3日\nMore intelligence from every token for your hardest work\nRelease\n2026年7月9日\n领先的前沿模型，为专业工作和持久运行的智能体而打造\n视觉\nOur research on visual and multimodal AI has led to advances in image generation, vision-language understanding, and models that can reason across images and text.\nSharper details, faster generation, and more precise editing\nChatGPT Images 2.5\n2026年9月8日\nA state-of-the-art model that makes precise, immediately usable visuals\nChatGPT Images 2.0\n2026年4月21日\n原生多模态模型，可生成精确、逼真且高度写实的输出内容\n2025年...\n音频\nOur research on applying AI to audio processing and audio generation has led to advances in speech recognition, real-time speech generation, and models that can listen and respond simultaneously.\nNatural, real-time conversations with AI\nGPT-Live\n2026年7月8日\n应对合成语音的挑战与机遇\n英文语音识别的稳健性和准确性正在接近人类水平\n"
                    }
                ],
                "DocumentInfo": {
                    "Filetype": "webpage",
                    "ContentLength": 1379,
                    "PublishTime": "2026-09-02T16:00:00Z"
                },
                "HostInfo": {
                    "Hostname": "OpenAI",
                    "IconUrl": "https://p19-volcsearch-d-sign-sg.ibyteimg.com/tos-alisg-i-h9hire4aei-sg/img/dfb3ee5d713404378b85dab44c8be041~tplv-h9hire4aei-224.jpeg?rk3s=feb11e32&x-expires=1794561372&x-signature=mAOp1TkuWKqtMhfIkJgkp5n2KoM%3D"
                }
            },
            {
                "Rank": 4,
                "Url": "https://www.independent.co.uk/tech/chatgpt-astra-agi-nvidia-huang-ai-b3046386.html",
                "Title": "New ChatGPT is world’s first human-level AI, says Nvidia boss",
                "Snippet": [
                    {
                        "Type": "text",
                        "Text": "nvidia ceo jensen huang has claimed that the latest version of chatgpt marks the first instance of artificial general intelligence ( agi ) , or human - level ai . openai ’s gpt - 6 model , known as ..."
                    }
                ],
                "DocumentInfo": {
                    "Filetype": "webpage",
                    "PublishTime": "2026-09-08T04:49:00+08:00"
                },
                "HostInfo": {
                    "Hostname": "The Independent",
                    "IconUrl": "https://p19-volcsearch-d-sign-sg.ibyteimg.com/tos-alisg-i-h9hire4aei-sg/img/5fb84fd42a4d58bb9f843aab5fa5a22b~tplv-h9hire4aei-224.jpeg?rk3s=feb11e32&x-expires=1794561372&x-signature=yHznTPQw9lLq9qAOEK1VD%2B9mW%2Bs%3D"
                }
            }
        ],
        "ErrorCode": 0,
        "ErrorMsg": "",
        "TimeCost": 369
    }
}
```


<span id=""></span>
#### Image search response

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
        "TotalDocCount": 20,
        "Documents": [
            {
                "Rank": 0,
                "Url": "https://www.trip.com/moments/poi-beijing-fall-leaves-viewing-148849016/",
                "Title": "[2025 Beijing ] Travel Guide for Fall Foliage Sightseeing in Beijing (Updated Nov)",
                "Snippet": [
                    {
                        "Type": "text",
                        "Text": "Asia|China|Beijing|Fall Foliage Sightseeing in Beijing|[2025 Beijing ] Travel Guide for Fall Foliage Sightseeing in Beijing (Updated Nov)|"
                    },
                    {
                        "Type": "image",
                        "Image": {
                            "Width": 640,
                            "Height": 853,
                            "ImageUrl": "https://p16-volcsearch-d-sign-sg.ibyteimg.com/tos-alisg-i-h9hire4aei-sg/image/df3c6e86fd9c0ba0bed9a7e9a114f735~tplv-h9hire4aei-448.jpeg?rk3s=feb11e32&x-expires=1794561326&x-signature=hLbxH%2BKIFCVm0%2BCZnL6v8kfCqAk%3D",
                            "Alt": "Explore Shijingshan’s Ancient Ginkgo Viewing Spots for 300 RMB! The Ultimate Autumn Day Trip in Beijing"
                        }
                    },
                    {
                        "Type": "text",
                        "Text": "Explore Shijingshan’s Ancient Ginkgo Viewing Spots for 300 RMB! The Ultimate Autumn Day Trip in Beijing|When the autumn breeze sweeps across the Western Hills, Beijing’s autumn hides in a tree of golden ginkgo in Shijingshan. Want to see the millenni"
                    }
                ],
                "DocumentInfo": {
                    "Filetype": "image"
                }
            },
            {
                "Rank": 1,
                "Url": "https://au.trip.com/moments/detail/beijing-1-152036753/",
                "Title": "2-Day Beijing Autumn Trip: A No-Hassle Guide to Ginkgo and Red Leaves",
                "Snippet": [
                    {
                        "Type": "image",
                        "Image": {
                            "Width": 640,
                            "Height": 853,
                            "ImageUrl": "https://p16-volcsearch-d-sign-sg.ibyteimg.com/tos-alisg-i-h9hire4aei-sg/image/a8680015fe2ab0e55950aaac6e9c6295~tplv-h9hire4aei-448.jpeg?rk3s=feb11e32&x-expires=1794561326&x-signature=h%2Fx7abjGXp6Z10P9pqTtLEtxEyE%3D",
                            "Alt": "北京秋日2天不绕路|银杏红叶这样走"
                        }
                    }
                ],
                "DocumentInfo": {
                    "Filetype": "image"
                }
            },
            {
                "Rank": 2,
                "Url": "https://www.sotwe.com/HorizonsEastern?lang=en",
                "Title": "Eastern Horizon with Malik Ayub Sumbal",
                "Snippet": [
                    {
                        "Type": "text",
                        "Text": " days ago\nBeijing Late Autumn Ginkgo Magic –A Golden Symphony of Leaves, Eastern Horizon @HorizonsEastern with Malik Ayub Sumbal. https://t.co/hIcj546KyL #Beijing #Winter\nEastern Horizon with Malik Ayub Sumbal @HorizonsEastern\n12 days ago\nBeijing’s late-autumn magic is in full swing! From mid-October to early November, the city turns into its golden hour: Ginkgo trees lining every boulevard, park, and temple courtyard burst into butter-yellow and liquid gold. #Beijing #Ginkgo"
                    },
                    {
                        "Type": "image",
                        "Image": {
                            "Width": 1200,
                            "Height": 676,
                            "ImageUrl": "https://p16-volcsearch-d-sign-sg.ibyteimg.com/tos-alisg-i-h9hire4aei-sg/image/8be3b0516eb6abbc58a7aa7201b16aa6~tplv-h9hire4aei-448.jpeg?rk3s=feb11e32&x-expires=1794561326&x-signature=11wPF7sAxTKwpVMYT7XY0iuoHiU%3D",
                            "Alt": "HorizonsEastern's tweet photo. Beijing’s late-autumn magic is in full swing!\n\nFrom mid-October to early November, the city turns into its golden hour: Ginkgo trees lining every boulevard, park, and temple courtyard burst into butter-yellow and liquid gold. \n\n#Beijing #Ginkgo https://t.co/w0dt2a6l2G"
                        }
                    },
                    {
                        "Type": "text",
                        "Text": "Eastern Horizon with Malik Ayub Sumbal @HorizonsEastern\n12 days ago\nBeijing Late Autumn Ginkgo Magic –A Golden Symphony of Leaves, Eastern Horizon @HorizonsEastern with Malik Ayub Sumbal. https://t.co/hIcj546KyL #Beijing #Winter\nEastern Horizon with Malik Ayub Sumbal @HorizonsEastern\n12 days ago\nBeijing’s late-autumn..."
                    }
                ],
                "DocumentInfo": {
                    "Filetype": "image"
                }
            },
            {
                "Rank": 3,
                "Url": "https://www.hellotickets.com/china/beijing/beijing-in-september/sc-143-4453",
                "Title": "10 Things to Do in Beijing in September",
                "Snippet": [
                    {
                        "Type": "text",
                        "Text": " vibrant.\nFrom coffee festivals and a tennis open, to events with the latest technology, there are many things Beijing has for you in September. In addition, you can enjoy its main attractions such as the Forbidden City, the Temple of Heaven, or the Ancient Shops Quarter, accompanied by perfect weather. So without further ado, I invite you to read on to discover all that Beijing has to offer in the ninth month of the year.\n1. Experience the Mid-Autumn Festival"
                    },
                    {
                        "Type": "image",
                        "Image": {
                            "Width": 768,
                            "Height": 576,
                            "ImageUrl": "https://p16-volcsearch-d-sign-sg.ibyteimg.com/tos-alisg-i-h9hire4aei-sg/image/fb4868615094ec16569a7b845e61de4c~tplv-h9hire4aei-448.jpeg?rk3s=feb11e32&x-expires=1794561326&x-signature=hP%2FSYHgdhDJA%2B2LBs4kRYpC5AFA%3D",
                            "Alt": "Autumn in Beijing| ©Caitriana Nicholson"
                        }
                    },
                    {
                        "Type": "text",
                        "Text": "Autumn in Beijing| ©Caitriana Nicholson\nIf you are lucky enough to be in Beijing for the month of September, you should definitely experience the Mid-Autumn Festival, one of the most important and traditional festivities in China.\nThis celebration takes place on the 15th day of the eighth Chinese lunar month, which usually"
                    }
                ],
                "DocumentInfo": {
                    "Filetype": "image"
                }
            },
            {
                "Rank": 4,
                "Url": "https://au.trip.com/moments/detail/china-110000-136085224/",
                "Title": "Autumn in Beijing – A Word That Becomes a Feeling",
                "Snippet": [
                    {
                        "Type": "image",
                        "Image": {
                            "Width": 640,
                            "Height": 853,
                            "ImageUrl": "https://p16-volcsearch-d-sign-sg.ibyteimg.com/tos-alisg-i-h9hire4aei-sg/image/335bafb71bd5c6a9a074e35b468a36f9~tplv-h9hire4aei-448.jpeg?rk3s=feb11e32&x-expires=1794561326&x-signature=%2BFp0Eai%2FTNAz3vbnIRhAglQgIXY%3D",
                            "Alt": "Autumn in Beijing – A Word That Becomes a Feeling"
                        }
                    },
                    {
                        "Type": "text",
                        "Text": "Autumn in Beijing – A Word That Becomes a Feeling\nAutumn in Beijing – A Word That Becomes a Feeling If someone asked me how beautiful autumn is, I would smile and say: come to Beijing, find a centuries-old ginkgo tree, and sit with a warm cup of tea. Amid the"
                    }
                ],
                "DocumentInfo": {
                    "Filetype": "image"
                }
            }
        ],
        "ErrorCode": 0,
        "ErrorMsg": "",
        "TimeCost": 317
    }
}
```


<span id=""></span>
### Error Response Example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026091400000000000000000000000002",
        "Action": "",
        "Version": "",
        "Service": "",
        "Region": "",
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

<span id=""></span>
# Error Handling


|**Error Code** |**Description** |**Recommended Check or Action** |
|---|---|---|
|10400 |General parameter error |Check the request body, especially the field types. |
|10403 |Permission error |Check whether the required service is enabled for the account. |
|10403 |Free quota exhausted |Check whether paid API access is enabled in console. |
|10500 |Default internal error |This is a fallback server\-side error code. Retrying the request usually resolves the issue. |
|700901 |Invalid APIKey |Check that the ApiKey is provided and passed correctly. See Authentication. |
|700429 |Request rate limit exceeded |Limit the number of concurrent search requests per second. |
