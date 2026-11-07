---
title: "Set token and domain Global Variables"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Set_token_and_domain_Global_Variables"
---

Before calling OpenAPI, it is recommended to set `IDA_DOMAIN`and `JWT_TOKEN`environment variables in the end point. `IDA_DOMAIN`for unified management interface to access the domain name, `JWT_TOKEN`for unified management of authentication credentials. This avoids repeating domain names and tokens in each `curl`example, facilitates local debugging, and reduces the risk of token leakage and copy\-paste errors. Subsequent interface examples can refer to the corresponding configuration directly through `${IDA_DOMAIN}`and `${JWT_TOKEN}`.

Set global variables

```Plain
export IDA_DOMAIN='dataxxxx.xxxxxxxx.volces.com' # current privatization domain: actual deployment environment domain address
export JWT_TOKEN='eyxxxxxxxxxxxqs' # pass 
```


Verification was successful

```Plain
Verification
curl -X GET \
  "https://${IDA_DOMAIN}/aeolus/api/v3/open/misc/current_user" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H 'Content-Type: application/json' \
  --silent | jq # This is JSON, formatted and optional
```


Even if this is successful, if the end point is closed in the middle, you need to reset the global variable

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5bcbb7503cf4f628df01782038a421d~tplv-goo7wpa0wc-image.image) </span>
