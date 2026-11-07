---
title: "Environment Variables"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-environment-variables"
---

This document describes how to add environment variables to a function and reference them in your code.

Environment variables are key\-value pairs. By using environment variables, you can adjust the behavior of functions in different environments without updating the code.

<span id="steps"></span>
## Steps

<span id="add-environment-variables-to-a-function"></span>
### Add environment variables to a function

Follow these steps to add environment variables to a function.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. Find the function to which you want to add environment variables, and click on the function name.

3. Select the **Settings** tab, then select **Environment variables**.

4. Click **Add variable**. In the **Add variable** dialog box, enter the **Variable name** and **Value** for each variable. You can add one or multiple environment variables. The rules for variable names are as follows:

   * Must start with an English letter or underscore (_).

   * Can only contain English letters, numbers, and underscores (_).

   * Variable names must be unique within the same function.

5. Click **OK**. The environment variables you added will appear in the environment variable list.


<span id="reference-environment-variables-in-function-code"></span>
### Reference environment variables in function code

You can access the value of an environment variable with the key `key` in your code using `env.key`. For example, the following code retrieves the value of the environment variable with the key `test`.

```JavaScript
const value = env.test;
```


If you need to modify the value of an environment variable, you must republish the function after making the changes. The changes will only take effect in the function after the function is published.
