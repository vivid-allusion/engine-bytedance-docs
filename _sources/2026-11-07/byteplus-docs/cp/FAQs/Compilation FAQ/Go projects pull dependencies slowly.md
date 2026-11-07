---
title: "Go projects pull dependencies slowly"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Go_projects_pull_dependencies_slowly"
---

It is recommended to add the following command at the beginning to use GOPROXY.

```Plain Text
export GOPROXY=https://goproxy.cn,direct

# If pulling from a private repository is required, setting GOPRIVATE is optional.
# export GOPRIVATE=git.mycompany.com,github.com/my/private
```
