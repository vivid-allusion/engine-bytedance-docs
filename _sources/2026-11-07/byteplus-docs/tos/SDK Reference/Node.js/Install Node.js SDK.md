---
title: "Install Node.js SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Install-the-node-js-sdk"
---

This document provides the download link and installation instructions for the TOS Node.js SDK.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before installing the SDK, you must first install Node.js version 10 or higher. You can visit the [NodeJS official website](https://nodejs.org/) to download the installation package. After installation is complete, you can use the `node -v` command to check the version information.

<span id=".c2RrLeS4i-i9veWcsOWdgA=="></span>
## SDK Download Link


* Latest source code address: [Source code address](https://github.com/volcengine/ve-tos-js-sdk)

* Version Revision Record: [Version Record](https://github.com/volcengine/ve-tos-js-sdk/blob/main/CHANGELOG.md)

* Historical Version URL: [Historical Version](https://github.com/volcengine/ve-tos-js-sdk/tags)


<span id=".5a6J6KOFLXNkaw=="></span>
## Install SDK

The TOS Node.js SDK is managed using NPM. If your local project has not yet initialized `package.json`, you can run the following command to initialize it.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The TOS Node.js SDK requires Node.js version 10 or higher.</div>


```javascript
npm init
```


After initializing `package.json` locally, run the following command to install the latest version of the SDK.

```javascript
// use npm
npm i @volcengine/tos-sdk

// use yarn
yarn add @volcengine/tos-sdk
```
