---
title: "ListDatasetData - Get video data and details (Not recommended)"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/ListDatasetData"
---

&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Description</div>



* <div data-tips="true" data-tips-type="default">This is a V1 control plane API for retrieving video data. To get a list of data from a dataset and view the details of a single item, integrate the ListItems and GetItem APIs. For details, see <a href="https://www.volcengine.com/docs/85296/1783743">ListItems \- Get a list of data from a dataset</a> and <a href="https://www.volcengine.com/docs/85296/1783742">GetItem \- Query data details</a>.</div>



<span id="a83dd3a7"></span>
## Get a list of all data

Get all data in a specified dataset

<span id="5f92c1b4"></span>
### Request Description

API name: `ListDatasetDataAPI`

<span id="e06f935e"></span>
### Request Parameters

<span id="2320b9b4"></span>
#### Request


|**Parameter** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|DatasetID |String |Yes |"106260669" |Dataset ID |
|PageNumber |Int |No |1 |The page number of the search results.<br><br>The starting and default value is 1. A parameter error is reported if the value is less than 1.<br><br>Returns the default value if this parameter is not provided. |
|PageSize |Int |No |10 |The number of search results per page.<br><br>The default value is 10, and the maximum value is 100. A parameter error is returned if the value is less than or equal to 0 or greater than 100.<br><br>Returns the default value if omitted. |


<span id="f2e2234c"></span>
#### Request Example

```JSON
curl 'http://open.volcengineapi.com/?Action=ListDatasetDataAPI&Version=2025-03-01' \
--header 'Content-Type: application/json' \
--data '{
    "DatasetID": "106260669",
    "Page": 1,
    "PageSize": 10
}'
```


&nbsp;

<span id="9fb6703d"></span>
### Response Parameters

<span id="b895169b"></span>
#### Response


|**Field Name** |**Type** |**Description** |
|---|---|---|
|TotalCount |Int |Total number of query results |
|Items |Array<[ListDatasetDataAPIRespItem](https://bytedance.larkoffice.com/docx/RqtRd9HtHoSwi4xxUuKc29CJnAf#share-NjkPdU0Jqonpztxh3weclmiMnhh)\> |Search results |


<span id="3c17cd22"></span>
#### ListDatasetDataAPIRespItem


|**Field name** |**Type** |**Description** |
|---|---|---|
|ContentID |String |A unique identifier for media content within the same dataset. |
|ContentType |String |Content type. The supported enumerated values are:<br><br><br>* "**collection**": A media collection, such as the metadata for a TV series.<br><br>* "**video**": Video content, such as the video and metadata for a single TV series episode or a movie. |
|ParentContentID |String |Unique identifier for the parent content. |
|SequenceIndex |Int64 |The sequence information of sub\-content within parent content (e.g., episode numbers in a TV series), used to link video content for cross\-video understanding within the same media series. |
|Status |String |Status: Completed (0), Processing (1), Data error (2) |
|ErrorCode |String |Error message for the returned data. |
|Timestamp |Int64 |Update timestamp: Unix representation in seconds |


<span id="23c93ea7"></span>
#### Processing status

**Error codes for data access and quality issues:** 

10001: InvalidJsonLineError \- Invalid JSON line

10002: DataPrimaryKeyNotFoundError \- Data primary key not found

10003: DataContentTypeNotFoundError \- Data content type not found

10004: UnsupportedContentTypeError \- Unsupported content type

10005: DuplicateMediaSequenceIndexError \- Duplicate media sequence index

10006: MediaCannotBeSetAsParentError \- Videos cannot be set as parent content

10007: ParentContentMustBeCollectionError \- Parent content must be a Collection

10008: ParentContentNotUploadedError \- Parent content not uploaded

10009: InvalidVideoUrlError \- Invalid video URL

10010: InvalidImageUrlError \- Invalid image URL

10011: VideoUrlNotUploadedError \- Video URL not uploaded

10012: InvalidMediaSequenceIndexError \- Invalid media sequence index (is negative)

**Video processing error codes and their meanings:** 

20000: VideoProcessError \- Video processing error

20001: VideoDurationExceedsLimitError \- Video duration exceeds the limit

20002: VideoSizeExceedsLimitError \- Video size exceeds the limit

22001: VideoUnderstandingClipsCommonException \- An exception occurred during the video understanding process.

22002: VideoUnderstandingClipsNoCallbackError \- No callback for video understanding.

22003: VideoUnderstandingClipsResultFailed \- Failed to get the video understanding result.

<span id="c1d0d48b"></span>
#### Response Example

```JSON
"Result": {
        "Items": [{
                "ContentID": "test_0522_collection_01",
                "ContentType": "collection",
                "ParentContentID": "",
                "SequenceIndex": 0,
                "Timestamp": 1748953903,
                "Status": 0,
                "ErrorCode": "0"
        },
        {
                "ContentID": "test_0522_series_01",
                "ContentType": "video",
                "ParentContentID": "test_0522_collection_01",
                "SequenceIndex": 1,
                "Timestamp": 1748953166,
                "Status": 0,
                "ErrorCode": "0"
        },
        {
                "ContentID": "test_0522_single_01",
                "ContentType": "video",
                "ParentContentID": "",
                "SequenceIndex": 0,
                "Timestamp": 1748511326,
                "Status": 0,
                "ErrorCode": "0"
        },
        "ContentID": "test_0522_series_02", "ContentType": "video", "ParentContentID": "test_0522_collection_01", "SequenceIndex": 2, "Timestamp": 1748503206, "Status": 0, "ErrorCode": "0"
},
{
        "ContentID": "test_0522_series_03",
        "ContentType": "video",
        "ParentContentID": "test_0522_collection_01",
        "SequenceIndex": 3,
        "Timestamp": 1748413589,
        "Status": -1,
        "ErrorCode": "unknown"
}]
}
```


&nbsp;

<span id="18e69314"></span>
## Get Data Details

API Name: `GetDatasetDataAPI`

Get details of video data by specifying the dataset ID and data ID.

<span id="e3545394"></span>
### Request Parameters

<span id="6419fa68"></span>
#### Request


|**Parameter** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|DatasetID |String |Yes |"106260669" |Dataset ID |
|ContentID |String |Yes |"106260669_5770528247083860262" |Unique data identifier |


<span id="fa25fa45"></span>
#### Request Example

```Plain Text
curl  'http://open.volcengineapi.com/?Action=GetDatasetDataAPI&Version=2025-03-01' \
--header 'Content-Type: application/json' \
--data '{
    "DatasetID": "106260669",
    "ContentID": "test_0522_collection_01"
}'
```


&nbsp;

<span id="00877836"></span>
### Response parameters

<span id="04990d3d"></span>
#### Response


|**Field name** |**Type** |**Description** |
|---|---|---|
|Content |String |Raw data field |
|VideoContent |GetDatasetDataAPIRespVideoContent |Returns the content generated from video understanding when Type is 'video'. |
|CollectionContent |GetDatasetDataAPIRespCollectionContent |Returns a summary of content generated from all videos in the collection when Type is 'collection'. |


<span id="17f49bfb"></span>
#### GetDatasetDataAPIRespVideoContent


|**Field name** |**Type** |**Description** |
|---|---|---|
|Title |String |Generated video title |
|Summary |String |Generated video summary |
|[Insight](https://docs.byteplus.com/docs/viking-aisearch/ListDatasetData#a626c8c2) |String |Returns all content from the video storyline analysis as a string in JSON format.<br><br>See Insight |


<span id="af6fe918"></span>
#### GetDatasetDataAPIRespCollectionContent


|**Field name** |**Type** |**Description** |
|---|---|---|
|Summary |String |Generated series summary |


<span id="a626c8c2"></span>
#### Insight


|**Field name** |**Type** |**Description** |
|---|---|---|
|Summaries |Array<String\> |Summary |
|Titles |Array<String\> |Title |
|Clips |Array<[Clips](https://bytedance.larkoffice.com/docx/Hi9sdPw7ooS5jKxmffQczY05nvf#share-YSYCd8Cq2oBSvfxyx0FcltI3ngd)\> |Analysis of video segments |


**Clips**


|**Field Name** |**Type** |**Description** |
|---|---|---|
|Title |String |Title |
|Summary |String |Summary |
|Score |Float |Highlight score. The higher the score, the stronger the highlight.<br><br>Value range: 1\-5 |
|Dialogue |String |Video dialogue |
|Start |Float |Start time |
|End |Float |End time |


<span id="6d8264f5"></span>
##### Insight field details

```JSON
{
  "Summaries": [
    "Jack, a free-spirited artist, and Rose, a young socialite trapped in an oppressive engagement, find a soul-stirring connection aboard the ill-fated RMS Titanic. Their whirlwind romance is tragically interrupted when the 'unsinkable' ship strikes an iceberg in the North Atlantic. As the vessel begins its slow, terrifying descent into the freezing depths, the couple must navigate flooded corridors and the chaos of a collapsing social order to stay together. Ultimately, the story explores the sacrifice of true love against the backdrop of one of history’s greatest maritime disasters, revealing the endurance of the human spirit."
  ],
  "Titles": [
    "Unsinkable Dreams: Love and Tragedy on the High Seas"
  ],
  "Clips": [
    {
      "Title": "The Last Promise in the Freezing Sea",
      "Summary": "In the aftermath of the sinking, Jack and Rose cling to a wooden door frame floating in the sub-zero waters of the Atlantic. Jack, shivering uncontrollably, urges Rose to promise that she will survive, no matter what happens or how hopeless it seems. The scene captures the haunting silence of the ocean at night, punctuated only by the distant cries of survivors. Jack’s self-sacrifice becomes evident as he remains in the water to ensure Rose stays afloat, a moment of profound emotional weight and heartbreaking devotion.",
      "Score": 4.5,
      "Dialogue": "Winning that ticket, Rose, was the best thing that ever happened to me... You must promise me that you'll survive.",
      "Start": 7414.5,
      "End": 7460.0
    },
    {
      "Title": "The Heart of the Ocean and Eternal Memory",
      "Summary": "The elderly Rose stands at the stern of the research vessel, privately revealing that she has kept the 'Heart of the Ocean' diamond all these years. She drops the priceless jewel into the sea, finally letting go of the physical token of her past. As she drifts into sleep, the screen transitions to a dreamlike vision of the Titanic restored to its former glory, with Jack waiting for her by the Grand Staircase. The film concludes with a sweeping shot of the couple reuniting amidst the applause of those lost at sea, followed by the final credits.",
      "Score": 3.5,
      "Dialogue": null,
      "Start": 7460.0,
      "End": 8142.5
    }
  ]
}
```


<span id="3557bf4f"></span>
#### Response example

```JSON
{
  "ResponseMetadata": {
    "RequestId": "",
    "Service": "",
    "Action": "",
    "Region": "",
    "Version": ""
  },
  "Result": {
    "Content": "{\"description\":\"In 1983, a young boy vanishes into thin air in a small Indiana town. As friends, family, and local police search for answers, they are drawn into an extraordinary mystery involving top-secret government experiments, terrifying supernatural forces, and one very strange little girl.\",\"genre\":\"Drama / Sci-Fi / Horror\",\"parent_content_id\":\"\",\"sequence_index\":0,\"title\":\"Stranger Things Episode 3\",\"translated_name\":\"Stranger Things\",\"writers\":[\"The Duffer Brothers\",\"Justin Doble\"],\"country\":\"USA\",\"year\":\"2016\",\"language\":\"English\",\"content_id\":\"test_0522_collection_01\",\"content_type\":\"collection\",\"runtime\":\"48 min\",\"cast\":[\"Winona Ryder\",\"David Harbour\",\"Finn Wolfhard\",\"Millie Bobby Brown\",\"Gaten Matarazzo\",\"Caleb McLaughlin\",\"Natalia Dyer\",\"Charlie Heaton\",\"Cara Buono\",\"Matthew Modine\",\"Joe Keery\",\"Rob Morgan\",\"John Reynolds\",\"Joe Chrest\",\"Noah Schnapp\"],\"douban_rating\":\"8.9\",\"release_date\":\"2016-07-15 (USA)\",\"director\":\"Shawn Levy\"}",
    "VideoContent": null,
    "CollectionContent": {
      "Summary": "Directory: Video 1 - The Vanishing of Will Byers..."
    }
  }
}
```


&nbsp;

```JSON
{
  "ResponseMetadata": {
    "RequestId": "",
    "Service": "",
    "Action": "",
    "Region": "",
    "Version": ""
  },
  "Result": {
    "Content": "{\"country\":\"USA\",\"language\":\"English\",\"sequence_index\":2,\"video_url\":[\"http://ai-search-rec-video.byte-test.com/d1d5d4c432cb4cebae6f5728902504fd/main.m3u8\"],\"writers\":[\"The Duffer Brothers\"],\"translated_name\":\"Stranger Things\",\"content_type\":\"video\",\"director\":\"The Duffer Brothers\",\"genre\":\"Drama / Sci-Fi / Horror\",\"runtime\":\"55 min\",\"title\":\"Stranger Things Episode 2: The Weirdo on Maple Street\",\"cast\":[\"Winona Ryder\",\"David Harbour\",\"Finn Wolfhard\",\"Millie Bobby Brown\",\"Gaten Matarazzo\",\"Caleb McLaughlin\",\"Natalia Dyer\",\"Charlie Heaton\",\"Matthew Modine\",\"Joe Keery\"],\"content_id\":\"test_0522_series_02\",\"description\":\"In 1983, following the mysterious disappearance of Will Byers, a small Indiana town is plunged into a web of conspiracy and supernatural events. A mysterious young girl with telekinetic powers, known only as 'Eleven,' is found in the woods by Will's friends. As Joyce Byers receives impossible phone calls from her missing son, local police chief Jim Hopper begins to uncover a cover-up involving the Hawkins National Laboratory. The boys hide Eleven in Mike's basement, realizing she may be the key to finding Will. Meanwhile, a dark entity from an alternate dimension begins to manifest, threatening the safety of everyone in Hawkins.\",\"douban_rating\":\"8.9\",\"parent_content_id\":\"test_0522_collection_01\",\"release_date\":\"2016-07-15 (USA)\",\"year\":\"2016\"}",
    "VideoContent": {
      "Title": "Psychic Resonance and the Shadows of Hawkins Lab",
      "Summary": "The mystery deepens as Eleven demonstrates her telekinetic abilities, using a Dungeons & Dragons board to explain Will's location in the 'Upside Down.' Joyce becomes increasingly convinced Will is communicating through lights and electricity, leading to a breakdown in conventional logic. Government agents monitor the town's communications, using the 'Hawkins Lab' as a front for extra-dimensional experiments. As the boys bond with Eleven, they face a crisis of belief: trusting their eyes or the supernatural evidence before them, all while a predatory shadow lurks at the edges of reality.",
      "Insight": "{\"Summaries\":[\"The mystery deepens as Eleven demonstrates her telekinetic abilities, using a Dungeons & Dragons board to explain Will's location in the 'Upside Down.' Joyce becomes increasingly convinced Will is communicating through lights and electricity, leading to a breakdown in conventional logic. Government agents monitor the town's communications, using the 'Hawkins Lab' as a front for extra-dimensional experiments. As the boys bond with Eleven, they face a crisis of belief: trusting their eyes or the supernatural evidence before them, all while a predatory shadow lurks at the edges of reality.\"],\"Titles\":[\"Psychic Resonance and the Shadows of Hawkins Lab\"],\"Clips\":[{\"Title\":\"The Mystery of the Missing Boy\",\"Summary\":\"The episode opens with a tense atmosphere at the police station, followed by shots of the dark woods where Will's bike was found...\",\"Score\":3.5,\"Dialogue\":\"Hawkins Police Department. Hopper speaking.\",\"Start\":0.0,\"End\":83.0},{\"Title\":\"Stranger Things Main Title\",\"Summary\":\"The iconic red neon text 'STRANGER THINGS' fades in against a backdrop of floating dust motes, accompanied by a pulsing synthesizer score, establishing the 80s sci-fi aesthetic.\",\"Score\":1.0,\"Dialogue\":\"A Netflix Original Series.\",\"Start\":2588.5,\"End\":2594.5}]}"
    },
    "CollectionContent": null
  }
}
```


<span id="254cec1d"></span>
#### Parse

Example of making a request and parsing the response with Python

```Python
import hashlib
import hmac
import json
from datetime import datetime
from urllib.parse import parse_qsl, urlencode, urlparse

import pytz
import requests
from requests import PreparedRequest
from requests.auth import AuthBase

class OpenApiAuth(AuthBase):
    """default method"""

    def __init__(
        self,
        access_key: str,
        secret_key: str,
        region: str,
        host: str,
        service_name: str,
    ) -> None:
        self.access_key = access_key
        self.secret_key = secret_key
        self.region = region
        self.host = host
        self.service_name = service_name

    def __call__(self, r: PreparedRequest):
        def sha256str(content: str | bytes) -> str:
            if content is None:
                content = ""
            if isinstance(content, str):
                content = content.encode("utf-8")
            return hashlib.sha256(content).hexdigest()

        def hmac_sha256(key: bytes, content: str) -> bytes:
            return hmac.new(key, content.encode("utf-8"), hashlib.sha256).digest()

        # Format timestamp
        now = datetime.now(tz=pytz.timezone("UTC"))
        timestr = now.strftime("%Y%m%dT%H%M%SZ")
        datestr = now.strftime("%Y%m%d")

        # headers
        # Remove unused headers for cleaner logs
        del r.headers["User-Agent"]
        del r.headers["Accept-Encoding"]
        del r.headers["Accept"]
        del r.headers["Connection"]
        del r.headers["Content-Length"]
        r.headers.update(
            {
                "X-Date": timestr,
                "Host": self.host,
            }
        )

        # Select headers to be included in the signature
        signed_headers = dict(
            filter(
                lambda x: x[0] in ["content-type", "content-md5", "host"]
                or x[0].startswith("x-"),
                r.headers.lower_items(),  # Convert keys to lowercase
            )
        )

        # Exclude port from the Host header for port 80 or 443
        if "host" in signed_headers:
            parse_result = urlparse("//" + signed_headers["host"])
            host = parse_result.hostname
            port = parse_result.port
            if port in ["80", "443"]:
                signed_headers["host"] = host

        # Package/Assemble all header information
        signed_str = "".join([f"{k}:{v}\n" for k, v in sorted(signed_headers.items())])

        SignedHeaders = ";".join(sorted(signed_headers.keys()))

        scheme, netloc, path, params, query, fragment = urlparse(r.url)

        # Standard practice: Sort query parameters in ascending order
        query = parse_qsl(query)
        query.sort()
        query = urlencode(query)

        # 1. Create a canonical request
        canoncial_request = "\n".join(
            [r.method, path, query, signed_str, SignedHeaders, sha256str(r.body)]
        )

        # 2.Create signing string
        credential_scope = "/".join(
            [datestr, self.region, self.service_name, "request"]
        )
        signing_str = "\n".join(
            ["HMAC-SHA256", timestr, credential_scope, sha256str(canoncial_request)]
        )

        # 3. Calculate signing key
        kdate = hmac_sha256(self.secret_key.encode("utf-8"), datestr)
        kregion = hmac_sha256(kdate, self.region)
        kservice = hmac_sha256(kregion, self.service_name)
        signing_key = hmac_sha256(kservice, "request")
        
        # 4. Calculate signature
        Signature = hmac_sha256(signing_key, signing_str).hex()

        r.headers["Authorization"] = (
            f"HMAC-SHA256 Credential={self.access_key}/{credential_scope}, SignedHeaders={SignedHeaders}, Signature={Signature}"
        )
        return r
    
auth = OpenApiAuth(
    access_key="",  # use your own access_key
    secret_key="",  # use your own secret_key
    region="cn-beijing",
    host="open.volcengineapi.com",
    service_name="aisearch",
)

def GetDatasetDataAPI(dataset_id, content_id):
    payload = {"DatasetID": dataset_id, "ContentID": content_id}
    action = "GetDatasetDataAPI"
    resp = requests.post(
        f"http://open.volcengineapi.com/?Action={action}&Version=2025-03-01",
        json = payload,
        auth = auth,
    )

    text = resp.text
    text = json.loads(text)
    data = text["Result"]

    if isinstance(data, dict) and "Content" in data and isinstance(data["Content"], str):
        try:
            data["Content"] = json.loads(data["Content"])
            data["VideoContent"]["Insight"] = json.loads(
                data["VideoContent"]["Insight"]
            )
        except json.JSONDecodeError:
            print("The Content field is not a valid JSON string")

    # save data as json file
    with open("data.json", "w", encoding="utf-8") as f:
        json.dump(data, f, ensure_ascii=False, indent=2)

if __name__ == "__main__":
    # view content_id details
    GetDatasetDataAPI("106266573", "10009_2")
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To experience more of Viking AI's search capabilities, visit: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search Engine, an all\-in\-one intelligent engine for enterprise search, recommendations, and Q&A</a></div>
