---
title: "Lightweight instances"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Lightweight_instances"
---

If you have extreme requirements for monitoring and do not want certain monitoring capabilities to be integrated by default and do not want the corresponding code to be loaded, you can create a lightweight instance. This instance does not include any monitoring feature; all feature plugins must be integrated as needed.

<span id=".5o6l5YWl56S65L6L"></span>
## Integration example

<span id="pageviewPlugin"></span>
### pageviewPlugin

**Version requirements**

apmplus/web \>= 1.7.0

**Feature description**

Monitor route changes to reconstruct the user's access path and track user visit counts.

**Application scenarios**

Available when initializing a lightweight instance with only the pageview monitoring capability integrated.

**Sample code**

```typescript
import { createMinimalBrowserClient } from '@apmplus/web/cn/minimal'
import { pageviewPlugin } from '@apmplus/integrations/pageview'

// Create a minimal instance
const client = createMinimalBrowserClient()

client('init',{
  ...
  // Import monitoring features that need to be collected as needed
  integrations: [pageviewPlugin()],
  ...
})
```


<span id="jsErrorPlugin"></span>
### jsErrorPlugin

**Version requirements**

apmplus/web \>= 1.7.0

**Feature description**

Listen for global JavaScript errors and report them.

**Application scenarios**

Initialize a lightweight instance and integrate only the JavaScript error monitoring capability.

**Sample code**

```typescript
import { createMinimalBrowserClient } from '@apmplus/web/cn/minimal'
import { jsErrorPlugin } from '@apmplus/integrations/jsError'

// Create a minimal instance
const client = createMinimalBrowserClient()
client('init',{
  ...
  // Import the monitoring features that need to be collected as needed
  integrations: [jsErrorPlugin()],
  ...
})
```


<span id="blankScreenPlugin"></span>
### blankScreenPlugin

**Version requirements**

apmplus/web \>= 1.7.0

**Feature description**

Detect blank screens and help associate exception information when a blank screen occurs.

**Application scenarios**

This is available only when a lightweight instance is initialized and only the blank screen monitoring capability is integrated.

**Sample code**

```typescript
import { createMinimalBrowserClient } from '@apmplus/web/cn/minimal'
import { blankScreenPlugin } from '@apmplus/integrations/blankScreen'

// Create a minimal instance
const client = createMinimalBrowserClient()
client('init',{
  ...
  // Import monitoring features for collection as needed
  integrations: [blankScreenPlugin()],
  ...
})
```


More open\-source monitoring capability plugins are available; refer to [On-demand integration plugins](https://docs.byteplus.com/en/docs/apmplus/Integrate_plugins_as_needed).
