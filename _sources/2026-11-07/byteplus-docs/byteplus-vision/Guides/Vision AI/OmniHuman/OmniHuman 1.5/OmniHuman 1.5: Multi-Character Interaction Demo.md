---
title: "OmniHuman 1.5: Multi-Character Interaction Demo"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/OmniHuman1-5-Multi-Character-Interaction-Demo"
---

# Preparatory Instructions (Mandatory Reading)

To animate multiple characters from a single image, this guide provides the complete workflow using OmniHuman 1.5. You will learn how to perform subject detection to isolate each character, generate individual speaking videos using their unique masks, and stitch the clips together to create a multi\-character interaction.

>  **⚠️**  Note: OmniHuman 1.5 does not support using a single audio clip to drive a conversation between different characters. In a multi\-character scenario, one audio clip can only be used to drive one character to speak or multiple characters to speak simultaneously. If you need to enable a conversation between different characters, please call the interface multiple times to generate videos and then stitch the videos together.

## **Step 1: Subject Recognition (Optional)**

This step is used to identify whether an image contains human, human\-like, anthropomorphic, or similar subjects. **This step can be skipped** if you've already confirmed the image contains human, human\-like, anthropomorphic, or similar subjects.

## **Step 2: Subject Detection**

This step detects subjects in images and supports returning mask images corresponding to the subjects. **This step is required** when specifying which subject will speak during video generation.

Retrieve the mask URL from the response and use the corresponding one to drive the character. The mask URLs in the list are sorted in descending order of their corresponding subject's mask area ** ** (from largest to smallest). If you need to preview the mask images, you can download them via the URLs, manually change the file name extension to .png, and save them as .png files before viewing.

## **Step 3: Video Generation**

Initiate video generation using the selected mask URL. OmniHuman 1.5 generates video effects matching the input image based on a single image, text prompt, and audio file uploaded by the user.

## Step 4: Stitch the videos  **(Optional)**

If you need to enable a conversation between different characters, please call the interface multiple times to generate videos and then stitch the videos together.

# Sample code

Note: The sample code is for testing and debugging. It may be integrated into the project as needed. (Directly copying the code as\-is is not recommended; instead, it is advisable to adapt it independently or update the relevant package.)

## Python

1. Perform Subject Detection, then initiate Video Generation using the selected mask URL.

```Python
# coding:utf-8
from __future__ import print_function
import json

from byteplus_sdk import visual
from byteplus_sdk.visual.VisualService import VisualService

if __name__ == '__main__':
    visual_service = VisualService()

    # call below method if you don't set ak and sk in $HOME/.volc/config | Replace the AK/SK retrieved from the BytePlus Console.
    visual_service.set_ak('AK*****')
    visual_service.set_sk('*****==')

    # Step 2. Subject Detection request body. Complete subject detection and get mask urls.
    form = {
        "req_key": "realman_avatar_object_detection_cv",
        "image_url": "https://xxxxx"
    }

    resp = visual_service.cv_process(form)
    #print(resp)

    #Handle Subject Detection response and get mask URL
    if "data" not in resp:
        raise KeyError("missing data")
    resp_data_str = resp["data"].get("resp_data")
    if not resp_data_str:
        raise KeyError("missing resp_data")
    inner_data = json.loads(resp_data_str)
    
    object_detection = inner_data.get("object_detection_result")
    if not object_detection:
        raise KeyError("missing object_detection_result")
    mask = object_detection.get("mask")
    if not mask:
        raise KeyError("missing mask")
    mask_urls = mask.get("url", [])

    #get first mask URL. You can modify the mask url to select different character. #for example, using mask_urls[1]
    if mask_urls:
        first_mask_url = mask_urls[0]
        #print("first mask URL:", first_mask_url)
        
        #Step 3. Video Generation Request body. Initiate video generation using the selected mask URL
        asyncform = {
            "req_key": "realman_avatar_picture_omni15_cv",
            "image_url": "https://xxxxx",
            "mask_url" : first_mask_url,  
            "audio_url" : "https://xxxxx"
        }
        asyncResp = visual_service.cv_submit_task(asyncform)
        print(asyncResp) #You can get the task_id from the response.

    else:
        print("mask URL not found")
```

2. Retrieve the video URL from the response using the task_id.

```Python
# coding:utf-8
from __future__ import print_function

from byteplus_sdk import visual
from byteplus_sdk.visual.VisualService import VisualService

if __name__ == '__main__':
    visual_service = VisualService()

    #call below method if you don't set ak and sk in $HOME/.volc/config | Replace the AK/SK retrieved from the BytePlus Console.
    visual_service.set_ak('AK*****')
    visual_service.set_sk('*****==')
    
    # Video Generation Request Body
    form = {
        "req_key": "realman_avatar_picture_omni15_cv",
        "task_id": "xxxxx"
    }
    resp = visual_service.cv_get_result(form)
    print(resp)
```

3. Please repeat steps 1 and 2 to initiate video generation using different mask URLs, then stitch the videos as needed for business requirements.

## Integration Instructions

### SDK Usage Instructions

Please refer to [SDK Usage Instructions](https://docs.byteplus.com/en/docs/byteplus-vision/SDK-Usage-instructions)

### HTTP Access Instructions

Please refer to [HTTP Request Sample](https://docs.byteplus.com/en/docs/byteplus-vision/http_request_sample)

### API Key Usage Instructions

Please refer to [API Key Usage Instructions](https://docs.byteplus.com/en/docs/byteplus-vision/api-key-usage-instructions)
