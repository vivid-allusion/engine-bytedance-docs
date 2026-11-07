---
title: "Create a Function Using Function Templates"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli_use_function_template_en"
---

This document describes how to create functions using function templates in Edge Functions CLI.

For Edge Functions CLI, the function templates available to you depend on whether you have set up your Access Key ID and Secret Access Key:


* If you haven't set up your Access Key ID and Secret Access Key, you can only use the built\-in template.

* If you have set up your Access Key ID and Secret Access Key, you can use all templates supported by Edge Functions.


<span id="prerequisites"></span>
## Prerequisites


* You have installed Edge Functions CLI. See [Install CLI](https://docs.byteplus.com/en/docs/byteplus-cdn/get-started-with-edge-function-cli-en).

* You have set up your Access Key ID and Secret Access Key in the global project configuration file. See [Set up your Access Key ID and Secret Access Key](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-cli-login-en).


<span id="steps"></span>
## Steps


1. Run the following command on your device. This command will install Edge Functions CLI, create a function project, and create a local function within the project. See [nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-en).


```shell
$ npx @byteplus/nest@latest init
```



2. Follow the command line prompts to set the function name and select a function template. Then press Enter to confirm.


```shell
$ npx @byted/nest@latest init
Need to install the following packages:
@byteplus/nest@1.0.0
Ok to proceed? (y) y

✓ Name: test
? Select a template you want to start with:
▸ URL Rewriting
  Rewrite URL links in webpages using HTML Rewriter.                                                
  Aggregate Requests
  HTTP to HTTPS Upgrade
  JSON Processing
  Modify Origin Server Error Response Pages
  CORS (Cross-Origin Resource Sharing) Handling
```



3. According to your needs, follow the command line prompts to set other parameters and press Enter to confirm.


```shell
$ npx @byteplus/nest@latest init
Need to install the following packages:
@byteplus/nest@1.0.0
Ok to proceed? (y) y

✓ Name: test
✓ Select a template you want to start with: URL Rewriting
✓ Put code file in src/ directory?: Yes
✓ Entry File in src/ (optional, default is index.js): index.js
✓ Project Name (optional, default is "default"): 
✓ Description: 
==> 🛠️  Creating a BytePlus Function `test` in directory /Users/MyFolder/test ...
==> [info]: 📦  Generating package.json...
==> [info]: 🧾  Generating nest.json for project...
==> [info]: 🖨️  Generating code files from template...✓
==> [info]: 📥  Installing dependencies...✓
==> [info]: 👏  Done!, New function created at ./test

==> Continue Developing
==> [info]: Change directory: cd ./test
==> [info]: Start dev server: npm run start

==> Publish Function
==> [info]: Setting access_key: npm run nest config -g set cloud.access_key <your_access_key>
==> [info]: Setting secret_key: npm run nest config -g set cloud.secret_key <your_secret_key>
==> [info]: Deploy function: npm run deploy
```


After the command completes, your current directory structure will be as follows:

```markdown
└── 📁MyFolder
    └── 📁test
        └── nest.json
        └── package-lock.json
        └── package.json
        └── 📁src
            └── index.js
    └── package.json
```


Here, the `test` directory is your created function project, and `test/src/index.js` is the entry file for your local function. The content of index.js is the function template you selected.

You can view the code file generated from the function template using the following command in the `MyFolder` directory:

```shell
$ cat test/src/index.js
addEventListener('fetch', event => {
  event.respondWith(onFetch(event));
})

const OLD_URL = "s.taobao.com";
const NEW_URL = "s.mynewdomain.com";

async function onFetch(event) {
  const path = event.request.path;
  const response = await fetch(`https://www.taobao.com${path}`);

  const rewrite = function(element, tag) {
    if (element.hasAttribute(tag)) {
      const href = element.getAttribute(tag);
      const new_href = href.replace(OLD_URL, NEW_URL);
      console.log(`replace(${tag}) ${href} => ${new_href}`);
      element.setAttribute(tag, new_href);
    }
  }
  const rewriteBody = createHtmlStream(
    response.body,
    undefined,
     [
        [
          'a',  // CSS selector, 'a' stands for selecting all the 'a' tags in the webpage
          {
            // This onElement callback will be triggered after 'a' tags in the webpage are parsed
            onElement(element) {
              rewrite(element, "href")
            }
          }
        ],
        [
          'img',
          {
            // This onElement callback will be triggered after 'img' tags in the webpage are parsed
            onElement(element) {
              rewrite(element, "src")
            }
          }
        ]
      ]
  );

  return new Response(
    rewriteBody,
    {
      status: response.status,
      headers: response.headers
    }
  )
```
