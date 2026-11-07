---
title: "Install the CLI"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/get-started-with-edge-function-cli-en"
---

This document describes how to install the Edge Functions CLI.

<span id="system-requirements"></span>
## System requirements

The device running the Edge Functions CLI must meet the following requirements:


* The operating system must be one of the following types:

   * ARM64 macOS

   * x86\-64 macOS

   * ARM64 Linux

   * x86\-64 Linux

* [Node.js](https://nodejs.org/) and [npm](https://www.npmjs.com/) must be installed. Version requirements are as follows:

   * Node.js: 8.17.0+

   * npm: 6.13.4+

* [wget](https://www.gnu.org/software/wget/) or [cURL](https://curl.se/) must be installed.


<span id="steps"></span>
## Steps

It is recommended to install the Edge Functions CLI as a [devDependency](https://docs.npmjs.com/cli/v11/configuring-npm/package-json#devdependencies) in your Node.js project, rather than installing it globally. This ensures that all collaborators in a function project use the same version of the Edge Functions CLI. If different collaborators in a function project use different versions of the Edge Functions CLI, collaboration conflicts may occur.


* If you don't have a Node.js project yet, you can use `npx @byteplus/nest init` to create a new function project, install the Edge Functions CLI in the function project, and create a local function.

* If you already have a Node.js project, you can install the Edge Functions CLI as a [devDependency](https://docs.npmjs.com/cli/v11/configuring-npm/package-json#devdependencies) in your function project.


<span id="npm"></span>
### npm

```shell
npm i --save-dev @byteplus/nest
```


<span id="yarn"></span>
### yarn

```shell
yarn add -D @byteplus/nest
```


<span id="view-the-installed-version-of-the-edge-functions-cli"></span>
## View the installed version of the Edge Functions CLI

After installation, you can run `npx nest --version` in the root directory of your function project to view the version of the Edge Functions CLI.

```shell
$ npx nest --version
  ______    _              ______                _   _
 |  ____|  | |            |  ____|              | | (_)
 | |__   __| | __ _  ___  | |__ _   _ _ __   ___| |_ _  ___  _ __
 |  __| / _` |/ _` |/ _ \ |  __| | | | '_ \ / __| __| |/ _ \| '_ \
 | |___| (_| | (_| |  __/ | |  | |_| | | | | (__| |_| | (_) | | | |
 |______\__,_|\__, |\___| |_|   \__,_|_| |_|\___|\__|_|\___/|_| |_|
               __/ |
              |___/

Version: 1.0.0
```
