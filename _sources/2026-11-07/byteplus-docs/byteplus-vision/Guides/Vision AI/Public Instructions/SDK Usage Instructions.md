---
title: "SDK Usage Instructions"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/SDK-Usage-instructions"
---

<span id="03sJJR0L"></span>
# Preparatory Instructions (Mandatory Reading)

> **Note: ** Interface types fall into three categories: synchronous interfaces, asynchronous interfaces, and synchronous\-to\-asynchronous interfaces.


To integrate with the BytePlus Visual Service, you can use the code examples provided in this guide. It offers ready\-to\-use snippets for both Python and Golang, demonstrating how to call synchronous, asynchronous, and synchronous\-to\-asynchronous interfaces. These examples help you quickly understand the SDK workflow and accelerate your development process. The following are general instructions for using the SDK, using [Video Generation](https://docs.byteplus.com/en/docs/byteplus-vision/omnihuman-video_generation) as an example:

**Step1:**  Check the `Action` and corresponding `Version` in the `Query Parameters - Parameter` section of the interface documentation. Based on the Action, search the SDK globally to find the corresponding example or refer to the examples in this document.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d4822576201dc5f40c270d826d4aab69.png) </span>

**Step2:**  Check the `Request example` of the interface documentation, and copy the content of `Request example` to the `#Request Body` section of the invocation example.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_11eeb4cf8238e3cf8ad3ab22bb44e44f.png) </span>

**Step3:**  Update other key information, such as AK/SK, then run the program for debugging.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77225aa9da5b464a8bcd79dc942cf1a6~tplv-goo7wpa0wc-image.image) </span>

**Step4:**  Once the SDK example has been successfully tested and verified, you may then formally integrate it into the project.

<span id="1Lfz59J4"></span>
# Python

> SDK path：[https://github.com/byteplus-sdk/byteplus-sdk-python](https://github.com/byteplus-sdk/byteplus-sdk-python)


<span id="1e57ZP8H"></span>
## Synchronous interface (returns the result directly), Action=CVProcess

<span id="ynKHPKRn"></span>
### Example

> Path of the example in the SDK: [https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/visual/cv_process.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/visual/cv_process.py)


```Python
# coding:utf-8
from __future__ import print_function

from byteplus_sdk import visual
from byteplus_sdk.visual.VisualService import VisualService

if __name__ == '__main__':
    visual_service = VisualService()

    # call the method below if you don't set ak and sk in $HOME/.volc/config
    visual_service.set_ak('AK')
    visual_service.set_sk('SK')

    # Request Body (Check interface documentation and copy the required parameters)
    form = {
        "req_key": "xxx",
        # ...
    }

    resp = visual_service.cv_process(form)
    print(resp)
```


<span id="SwiE1Ouq"></span>
## Asynchronous interface: Submit Task (returns taskId), Action=CVSubmitTask

<span id="Ds4LZpZK"></span>
### Example

> Path of the example in the SDK: [https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/visual/cv_submit_task.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/visual/cv_submit_task.py)


```Python
# coding:utf-8
from __future__ import print_function

from byteplus_sdk import visual
from byteplus_sdk.visual.VisualService import VisualService

if __name__ == '__main__':
    visual_service = VisualService()

    # call below method if you don't set ak and sk in $HOME/.volc/config
    visual_service.set_ak('AK')
    visual_service.set_sk('SK')
    
    # Request Body (Check interface documentation and copy the required parameters) 
    form = {
        "req_key": "xxx",
                # ....
    }
    resp = visual_service.cv_submit_task( form)
    print(resp)
```


<span id="5lOTxtaQ"></span>
## Asynchronous interface: Get Result (returns result), Action=CVGetResult

<span id="I8uu7HKX"></span>
### Example

> Path of the example in the SDK: [https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/visual/cv_get_result.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/visual/cv_get_result.py)


```Python
# coding:utf-8
from __future__ import print_function

from byteplus_sdk import visual
from byteplus_sdk.visual.VisualService import VisualService

if __name__ == '__main__':
    visual_service = VisualService()

    # call below method if you don't set ak and sk in $HOME/.volc/config
    visual_service.set_ak('AK')
    visual_service.set_sk('Sk')
    
    # Request Body (Check interface documentation and copy the required parameters)
    form = {
        "req_key": "xxx",
        "task_id": "xxx"
    }
    resp = visual_service.cv_get_result(form)
    print(resp)
```


<span id="gJdvLOGf"></span>
## Asynchronous interface: Cancel Task, Action=CVCancelTask

<span id="eN6lWgKX"></span>
### Example

> Path of the example in the SDK: [https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/visual/cv_cancel_task.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/visual/cv_cancel_task.py)


```Python
# coding:utf-8
from __future__ import print_function

from byteplus_sdk import visual
from byteplus_sdk.visual.VisualService import VisualService

if __name__ == '__main__':
    visual_service = VisualService()

    # call below method if you don't set ak and sk in $HOME/.volc/config
    visual_service.set_ak('AK')
    visual_service.set_sk('Sk')

    form = {
        "req_key": "xxx",
        "task_id": "xxx"
    }
    resp = visual_service.cv_cancel_task(form)
    print(resp)
```


<span id="uc4aCU6y"></span>
## Synchronous\-to\-asynchronous interface: Submit Task (returns taskId), Action=CVSync2AsyncSubmitTask

<span id="qfyskNG5"></span>
### Example

> Path of the example in the SDK: [https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/visual/cv_sync2async_submit_task.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/visual/cv_sync2async_submit_task.py)


```Python
# coding:utf-8
from __future__ import print_function

from byteplus_sdk import visual
from byteplus_sdk.visual.VisualService import VisualService

if __name__ == '__main__':
    visual_service = VisualService()

    # call below method if you don't set ak and sk in $HOME/.volc/config
    visual_service.set_ak('AK')
    visual_service.set_sk('SK')
    
    # Request Body (Check interface documentation and copy the required parameters) 
    form = {
        "req_key": "xxx",
        # ...

    }
    resp = visual_service.cv_sync2async_submit_task(form)
    print(resp)
```


<span id="QYVVQ7cV"></span>
## Synchronous\-to\-asynchronous interface: Get Result (returns result), Action=CVSync2AsyncGetResult

<span id="Hk8fa3pk"></span>
### Example

> Path of the example in the SDK: [https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/visual/cv_sync2async_get_result.py](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/visual/cv_sync2async_get_result.py)


```Python
# coding:utf-8
from __future__ import print_function

from byteplus_sdk import visual
from byteplus_sdk.visual.VisualService import VisualService

if __name__ == '__main__':
    visual_service = VisualService()

    # call below method if you don't set ak and sk in $HOME/.volc/config
    visual_service.set_ak('AK')
    visual_service.set_sk('SK')
    
    # Request Body (Check interface documentation and copy the required parameters)
    form = {
        "req_key": "xxx",
        "task_id": "xxx",
        "req_json": "{\"logo_info\":{\"add_logo\":true,\"position\":1, \"language\":1,\"opacity\":0.5}}"
    }
    resp = visual_service.cv_sync2async_get_result(form)
    print(resp)
```


<span id="jaMBRdP5"></span>
# Golang

> SDK path：[https://github.com/byteplus-sdk/byteplus-sdk-golang](https://github.com/byteplus-sdk/byteplus-sdk-golang)


<span id="oCRuHlVh"></span>
## Synchronous interface (returns the result directly), Action=CVProcess

<span id="t4gx0y54"></span>
### Example

> Path of the example in the SDK: [https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/visual/CVProcess.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/visual/CVProcess.go)


```Go
package main

import (
        "encoding/json"
        "fmt"
        
        "github.com/byteplus-sdk/byteplus-sdk-golang/service/visual"
)

func main() {
        testAk := ""
        testSk := ""

        visual.DefaultInstance.Client.SetAccessKey(testAk)
        visual.DefaultInstance.Client.SetSecretKey(testSk)
        //visual.DefaultInstance.SetRegion("region")
        //visual.DefaultInstance.SetHost("host")

        //Request Body (Check interface documentation and copy the required parameters)
        reqBody := map[string]interface{}{
                "req_key": "",
                //"binary_data_base64": []string{""},
                "image_url": "",
        }

        resp, status, err := visual.DefaultInstance.CVProcess(reqBody)
        fmt.Println(status, err)
        b, _ := json.Marshal(resp)
        fmt.Println(string(b))
}
```


<span id="Amcrmp3o"></span>
## Asynchronous interface: Submit Task (returns taskId), Action=CVSubmitTask

<span id="4thpbnSx"></span>
### Example

> Path of the example in the SDK: [https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/visual/CVSubmitTask.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/visual/CVSubmitTask.go)


```Go
package main

import (
    "encoding/json"
    "fmt"
    
    "github.com/byteplus-sdk/byteplus-sdk-golang/service/visual"
)

func main() {
    testAk := ""
    testSk := ""

    visual.DefaultInstance.Client.SetAccessKey(testAk)
    visual.DefaultInstance.Client.SetSecretKey(testSk)
    //visual.DefaultInstance.SetRegion("region")
    //visual.DefaultInstance.SetHost("host")

    // Request body. Please refer to the request body in interface documentation
    reqBody := map[string]interface{}{
        "req_key": "realman_avatar_picture_omni15_cv",
        "image_url": "",
        "audio_url": "",
    }

    resp, status, err := visual.DefaultInstance.CVSubmitTask(reqBody)
    fmt.Println(status, err)
    b, _ := json.Marshal(resp)
    fmt.Println(string(b))
}
```


<span id="uCMv1hpN"></span>
## Asynchronous interface: Get Result (returns result), Action=CVGetResult

<span id="5jJ0UX46"></span>
### Example

> Path of the example in the SDK: [https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/visual/CVGetResult.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/visual/CVGetResult.go)


```Go
package main

import (
        "encoding/json"
        "fmt"

        "github.com/byteplus-sdk/byteplus-sdk-golang/service/visual"
)

func main() {
        testAk := ""
        testSk := ""

        visual.DefaultInstance.Client.SetAccessKey(testAk)
        visual.DefaultInstance.Client.SetSecretKey(testSk)
        //visual.DefaultInstance.SetRegion("region")
        //visual.DefaultInstance.SetHost("host")

        // Request body. Please refer to the request body in interface documentation
        reqBody := map[string]interface{}{
                "req_key": "realman_avatar_picture_omni15_cv",
                "task_id": "",
        }

        resp, status, err := visual.DefaultInstance.CVGetResult(reqBody)
        fmt.Println(status, err)
        b, _ := json.Marshal(resp)
        fmt.Println(string(b))
}
```


<span id="3xXL8HN5"></span>
## Asynchronous interface: Cancel Task, Action=CVCancelTask

<span id="olOK0kH1"></span>
### Example

> Path of the example in the SDK: [https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/visual/CVCancelTask.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/visual/CVCancelTask.go)


```Go
package main

import (
        "encoding/json"
        "fmt"

        "github.com/byteplus-sdk/byteplus-sdk-golang/service/visual"
)

func main() {
        testAk := ""
        testSk := ""

        visual.DefaultInstance.Client.SetAccessKey(testAk)
        visual.DefaultInstance.Client.SetSecretKey(testSk)
        //visual.DefaultInstance.SetRegion("region")
        //visual.DefaultInstance.SetHost("host")

        // Request body. Please refer to the request body in interface documentation
        reqBody := map[string]interface{}{
                "req_key": "realman_avatar_picture_omni15_cv",
                "task_id": "",
        }

        resp, status, err := visual.DefaultInstance.CVCancelTask(reqBody)
        fmt.Println(status, err)
        b, _ := json.Marshal(resp)
        fmt.Println(string(b))
}
```


<span id="OAurtwyk"></span>
## Synchronous\-to\-asynchronous interface: Submit Task (returns taskId), Action=CVSync2AsyncSubmitTask

<span id="NxCoW4XO"></span>
### Example

> Path of the example in the SDK: [https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/visual/CVSync2AsyncSubmitTask.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/visual/CVSync2AsyncSubmitTask.go)


```Go
package main

import (
        "encoding/json"
        "fmt"

        "github.com/byteplus-sdk/byteplus-sdk-golang/service/visual"
)

func main() {
        testAk := ""
        testSk := ""

        visual.DefaultInstance.Client.SetAccessKey(testAk)
        visual.DefaultInstance.Client.SetSecretKey(testSk)
        //visual.DefaultInstance.SetRegion("region")
        //visual.DefaultInstance.SetHost("host")

        // Request body. Please refer to the request body in interface documentation
        reqBody := map[string]interface{}{
                "req_key": "",
                "image_urls":      []string{""},
                "positive_prompt": "beautiful",
        }

        resp, status, err := visual.DefaultInstance.CVSync2AsyncSubmitTask(reqBody)
        fmt.Println(status, err)
        b, _ := json.Marshal(resp)
        fmt.Println(string(b))

        // example: transfer resp to response structure
        // if status != 200 {
        //         fmt.Println("request err, response is:", string(b))
        //         return
        // }
        // respData := new(model.ResponseStructxxx)
        // if err = json.Unmarshal(b, respData); err != nil {
        //         fmt.Println("unmarshal err:", err)
        //         return
        // }
        // fmt.Println(respData.Data.Status)
}
```


<span id="LYWqAQcg"></span>
## Synchronous\-to\-asynchronous interface: Get Result (returns result), Action=CVSync2AsyncGetResult

<span id="Ql3NZZML"></span>
### Example

> Path of the example in the SDK: [https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/visual/CVSync2AsyncGetResult.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/visual/CVSync2AsyncGetResult.go)


```Go
package main

import (
        "encoding/json"
        "fmt"

        "github.com/byteplus-sdk/byteplus-sdk-golang/service/visual"
        // "github.com/volcengine/volc-sdk-golang/service/visual/model"
)

func main() {
        testAk := ""
        testSk := ""

        visual.DefaultInstance.Client.SetAccessKey(testAk)
        visual.DefaultInstance.Client.SetSecretKey(testSk)
        //visual.DefaultInstance.SetRegion("region")
        //visual.DefaultInstance.SetHost("host")

        // Request body. Please refer to the request body in interface documentation
        reqBody := map[string]interface{}{
                "req_key": "",
                "task_id": "",
        }

        resp, status, err := visual.DefaultInstance.CVSync2AsyncGetResult(reqBody)
        fmt.Println(status, err)
        b, _ := json.Marshal(resp)
        fmt.Println(string(b))

        // example: transfer resp to response structure
        // if status != 200 {
        //         fmt.Println("request err, response is:", string(b))
        //         return
        // }
        // respData := new(model.ResponseStructxxx)
        // if err = json.Unmarshal(b, respData); err != nil {
        //         fmt.Println("unmarshal err:", err)
        //         return
        // }
        // fmt.Println(respData.Data.Status)
}
```
