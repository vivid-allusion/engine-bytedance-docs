---
title: "How to resolve the issue where the step input parameter inputs.xxx does not exist"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/How_to_resolve_the_issue_where_the_step_input_parameter_inputs_does_not_exist"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue phenomenon

When executing a Custom steps task in a version 2 pipeline, the pipeline reports the error `input.xxx: not found`.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

The pipeline reports an error indicating that the inputs parameter cannot be found, which may be due to an issue with the script parameter configuration in the YAML file for Custom steps. When referencing an input parameter in a script, you must use the value of inputs.name. If entered incorrectly, this will result in such issues.

For example:

A YAML fragment for a custom step is shown below. To reference the key1 parameter in the script, you can use `export a=$(inputs.key1)`. If you mistakenly write `export a=$(inputs.key01)`, the pipeline will report the error `input.key01: not found`.

```yaml

step: v2-custom-step

...

script: |
  export a=$(inputs.key1)
  echo "a：$a"
  export b=$(inputs.key2)
  echo "b：$b"
inputs:
    
  - name: key1
  
...

  - name: key2
  
...
```


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

Check your Custom steps YAML file and ensure that the names of the step input parameters referenced in the script are consistent with the corresponding inputs.name values.
