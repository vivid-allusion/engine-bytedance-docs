---
title: "Multi-instance scenarios"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Multi-instance_scenarios_minipro"
---

In a multi\-instance setup, the listener initialized by the first instance is reused, so when initializing additional instances, they can directly enter subscription status, resulting in significantly higher performance compared to initializing the first instance.

<span id=".Q0pTIOaWueW8jw=="></span>
## CJS method

The following `apmplus-mini.js` can be obtained in [integrating SDK-CJS](https://docs.byteplus.com/en/docs/apmplus/Integrate_Mini_Program_Pro_SDK). The code to create multiple instances is as follows:

```typescript
//apmplus-mini.js
const client = require('./apmplus-mini.js');
const client2 = client.createClient()
const client3 = client.createClient()
```


<span id=".TlBNIOaWueW8jw=="></span>
## NPM method

Suppose multiple instances are created on the WeChat Mini Program platform; the code is as follows:

```typescript
import { createMiniProgramClient, WxAdapter } from '@apmplus/mini-program'
const client = createMiniProgramClient([WxAdapter])
const client3 = createMiniProgramClient([WxAdapter]) 
const client3 = createMiniProgramClient([WxAdapter])
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Because the listener initialized by the first instance is reused starting from the second instance, a listener will only be destroyed after all of its subscriptions have been destroyed.</div>
