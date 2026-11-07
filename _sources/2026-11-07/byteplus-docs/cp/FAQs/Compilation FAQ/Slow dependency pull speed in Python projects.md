---
title: "Slow dependency pull speed in Python projects"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Slow_dependency_pull_speed_in_Python_projects"
---

It is recommended to add the `-i` parameter to the `pip install` command.

```Shell
# When the pipeline uses a public resource pool as a private resource pool, please visit the following URL.
pip install -i https://mirrors.ivolces.com/pypi/simple/ -r requirements.txt

# When the pipeline uses a third-party cluster as a private resource pool, please visit the following URL.
pip install -i https://mirrors.volces.com/pypi/simple/ -r requirements.txt
```
