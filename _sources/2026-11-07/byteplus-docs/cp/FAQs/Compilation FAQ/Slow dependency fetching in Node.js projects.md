---
title: "Slow dependency fetching in Node.js projects"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Slow_dependency_fetching_in_Nodejs_projects"
---

It is recommended to add the `--registry` and `--disturl` parameters to the `npm install` command.

```Plain Text
npm i --registry=https://registry.npmmirror.com --disturl=https://npmmirror.com/dist
```
