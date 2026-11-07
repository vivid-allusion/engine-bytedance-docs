---
title: "Multi-instance scenarios"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Multi-instance_scenarios"
---

This article describes how to create multiple instances in WebPro Monitoring.

<span id=".U2NyaXB05pa55byP"></span>
## Script method

Because the SDK is mounted on a custom global name, the script inherently supports multiple instances.

```javascript
// You can view detailed installation methods in [SDK integration](./104857)
installFunction(window, document, '{{SDK URL}}', '{{aid}}', '{{Global variable name}}')

// Configuration. Detailed configuration can be viewed in [SDK Integration].
window.{{client Global variable name}}('init', {
  aid: '{{your aid}}',
  token:  '{{your token}}'
})
window.{{client Global variable name}}('start')
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to upload two copies of multi\-instance data to two different projects, please create two instances and enter a different aid in each instance.</div>


<span id=".TlBN5pa55byP"></span>
## NPM method

Create an instance using createBrowserClient.

```javascript
import { createBrowserClient } from '@apmplus/web'// client a
const a = createBrowserClient()

a('init', {
    aid: 'aid a'，
    token: 'token'，
    pid: 'Initial page PID',
    userId: 'User identifier',
    release: 'Application release version',
    env: 'Application deployment environment',
})
a('start')

// client b
const b = createBrowserClient()

b('init', {
    aid: 'aid b'，
    token: 'token'，
    pid: 'Initial page PID',
    userId: 'User identifier',
    release: 'Application release version',
    env: 'Application deployment environment',
})
b('start')
```
