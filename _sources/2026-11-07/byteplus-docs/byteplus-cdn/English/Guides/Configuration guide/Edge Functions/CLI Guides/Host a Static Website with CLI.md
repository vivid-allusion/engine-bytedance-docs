---
title: "Host a Static Website with CLI"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/pages_host_webpage_en"
---

This document explains how to host static pages using Edge Functions Pages.

<span id="what-is-edge-functions-pages"></span>
## What is Edge Functions Pages

Edge Functions Pages is a static page hosting service provided by BytePlus Edge Functions. It helps developers quickly and efficiently deploy static sites to the global edge network. With Edge Functions Pages, you can easily host various types of static content, including but not limited to:


* Static websites (HTML/CSS/JavaScript)

* Single\-page applications (SPA)

* Documentation sites

* Blogs

* Static asset libraries


Edge Functions Pages leverages BytePlus edge nodes distributed worldwide to cache your static assets close to users, delivering low latency and high availability.

<span id="basic-concepts"></span>
## Basic concepts

<span id="pages-instance"></span>
### Pages instance

A Pages instance is the basic unit used to host and manage static pages in Edge Functions. Each Pages instance has a unique ID. A Pages instance can contain multiple assets; each asset corresponds to a static site version and has its own unique ID.

With a Pages instance, you can centrally manage the lifecycle of static pages, including:


* Create, configure, and delete the instance

* Upload, deploy, and manage asset versions


<span id="assets"></span>
### Assets

An asset is a stored static site version within a Pages instance. Each asset contains the complete static site files, and a unique asset ID is generated after upload.

<span id="usage-limits"></span>
## Usage limits

The usage limits of Edge Functions Pages are as follows.


* Up to 10 Pages instances per BytePlus account

* Up to 100 historical assets per instance; excess assets are cleaned automatically

* Up to 100 deployments per instance per month

* Each asset’s gzipped tarball must be ≤ 50 MB

* Up to 500 files per asset

* Up to 25 MB per file within an asset


<span id="example-scenario"></span>
## Example scenario

You have a static website project containing .html, .css, and .js files, and you want to quickly host and publish it via Edge Functions Pages.

<span id="runtime-requirements"></span>
## Runtime requirements

The device running the Edge Functions CLI must meet the following requirements:


* Operating systems:

   * ARM64 macOS

   * x86\-64 macOS

   * ARM64 Linux

   * x86\-64 Linux

* [Node.js](https://nodejs.org/) and [npm](https://www.npmjs.com/) installed. Version requirements:

   * Node.js: 8.17.0+

   * npm: 6.13.4+

* [wget](https://www.gnu.org/software/wget/) or [cURL](https://curl.se/) installed.


<span id="steps"></span>
## Steps

<span id="step-1-install-the-edge-functions-cli"></span>
### Step 1: Install the Edge Functions CLI

Edge Functions Pages does not require a local function project, so you can install the CLI globally:

```shell
npm install -g @byteplus/nest
```


<span id="step-2-set-your-access-key-id-and-secret-access-key"></span>
### Step 2: Set your Access Key ID and Secret Access Key

Run the following commands in any directory to set your BytePlus account’s Access Key ID and Secret Access Key in the Edge Functions CLI. You can obtain the Access Key ID and Secret Access Key from the [BytePlus Console](https://console.byteplus.com/iam/keymanage):

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


<span id="step-3-create-and-publish-a-pages-instance"></span>
### Step 3: Create and publish a Pages instance


1. Create a static asset directory and put your site files into it:

   ```shell
   mkdir -p site
   # Put your static files (e.g., .html, .css, .js) into the site directory
   ```
   

2. Create and immediately publish a Pages instance by running:

   ```shell
   npx nest pages create --name demo-site --assets ./site --deploy
   ```
   

   #### Parameter descriptions    <span id="parameter-descriptions"></span>

   
   |Parameter |Type |Required |Description |
   |---|---|---|---|
   |\-\-name |string |Yes |Name of the new Pages instance |
   |\-\-assets |string |Yes |Local static asset directory path (must include index.html) |
   |\-\-deploy |flag |No |Deploy the Pages instance immediately after creation |
   

   On success, you will see output similar to:

   ```shell
   ==> New Pages demo-site created!
   ==> [info]: Compressing given assets directory ./site...✓
   ==> [info]: Uploading assets...✓
   ==> [info]: Deploying pages...✓
   ==> Pages demo-site is publishing, you can visit it by open http://pywahntknjrhcufp.synthopages.bytepluses.com in browser a few minutes later
   ```
   

   The publish operation typically takes 1–5 minutes to take effect. After that, you can access your static site via the domain provided in the command output.

   If your Pages instance has not yet associated a custom domain, the system automatically assigns a temporary public domain for preview. The domain suffix is synthopages.bytepluses.com. Note that this domain is for preview purposes only. You can open this domain in a browser to preview your static site.


<span id="step-4-bind-a-custom-domain-to-the-static-site"></span>
### Step 4: Bind a custom domain to the static site

To access your static site via a custom domain, add the domain to your Pages instance:

```shell
nest pages domain add -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


On success, you will see output similar to:

```Plain Text
==> [info]: Adding domain "wow.test.example.com" to pages p-2e9hpae39m2sqksy...✓
==> Domain wow.test.example.com was added successfully.
```


The newly added domain needs to be verified before it can be officially used. You need to add a CNAME record for the domain, and then run the following command to verify it:

```shell
nest pages domain verify -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


If you want the domain to support HTTPS, upload the corresponding SSL/TLS certificate:

```shell
# Set the SSL/TLS certificate for the specified domain of the Pages instance
nest pages domain update \
  -p p-2e9hpae39m2sqksy \
  --domain wow.test.example.com \
  --certificate ~/path/test.example.com.crt \
  --private-key ~/path/test.example.com.key
```
