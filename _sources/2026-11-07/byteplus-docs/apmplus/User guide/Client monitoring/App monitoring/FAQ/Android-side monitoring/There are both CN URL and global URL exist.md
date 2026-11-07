---
title: "There are both CN URL and global URL exist."
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/There_are_both_CN_URL_and_global_URL_exist"
---

**Problem description**

```Plain Text
*** Terminating app due to uncaught exception 'APMInsightURLError', reason: 'There are both CN URL and global URL exist. Please remove one of the subspecs in the CN for Chinese App and the Global for global App.' 
```


**The cause of the problem**

Subspecs have not been explicitly declared.

**Solutions**

Setting specific subspecs in the Podfile, for example by using pod 'RangersAPM', '3.0.3' in this way, will result in this issue.

```Plain Text
pod 'RangersAPM', '3.0.3', :subspecs => [
'Crash',
'WatchDog',
xxxx
'CN' # Must be imported.
]
```
