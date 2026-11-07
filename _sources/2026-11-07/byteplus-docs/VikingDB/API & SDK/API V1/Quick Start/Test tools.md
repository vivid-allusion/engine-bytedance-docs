---
title: "Test tools"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Test_tools"
---

<span id="test-tools"></span>
# Test tools

When you follow the core process and call the API operations to create a collection, write data to a collection, create an index, query index data, and search an index, errors may arise. In this case, you can use test tools for error detection.

The following example demonstrates how to call a VikingDB test tool in Python. **The domain name for the request is** [https://api-vikingdb.mlp.cn-hongkong.bytepluses.com](https://api-vikingdb.mlp.cn-hongkong.bytepluses.com) **for Hong Kong or** [https://api-vikingdb.mlp.ap-mya.byteplus.com ](https://api-vikingdb.mlp.ap-mya.byteplus.com)**for** **Johor.** 

<span id="81d49ce2"></span>
# Network latency detection

If an API request is slow, use the following code to check network latency. Replace the DOMAIN value with the public or private domain name for your request.

```Python
import time 
import requests 
DOMAIN = "api-vikingdb.mlp.ap-mya.byteplus.com" 

# Record the request sending and receiving times to calculate the overhead of the public network. 
def ping(): 
    time1  = time.time() 
    r = requests.request("GET", 
            url="https://{}{}".format(DOMAIN, "/api/viking_db/data/ping") 
        ) 
    time2 = int((time.time() - time1) * 1000) 
    print("receive msg {}, network cost {} ms".format(r.text, time2)) 

# Call the ping() function. 
ping()
```


If the returned latency is high, public network access may be abnormal. If the returned latency is low, the network is normal. In this case, check your code logic.
