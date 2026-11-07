---
title: "Create a Pages Project"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/create-pages-project_en"
---

This document describes how to create a Pages project in the console.

<span id="before-you-begin"></span>
## Before You Begin


1. Sign in to the [Pages console](https://console.byteplus.com/cdn/cdn-bp/synthopages/list).

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260520084548-190124740695.png) </span>

2. Click **Create Project**.

3. In the **Creation Method** section, choose one of the following options:

   * **Upload File**: Upload a local ZIP package.

   * **Git**: Import code from a Git repository and build it.

   * **Template**: Generate a project from a preset template and deploy it automatically. For details, see [Use Pages Templates](https://docs.byteplus.com/docs/byteplus-cdn/use-pages-templates_en).


<span id="create-a-project-by-uploading-a-zip-file"></span>
## Create a Project by Uploading a ZIP File

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260520084824-68660348179.png) </span>

After you select **Upload File**, upload the file, configure the following parameters, and then click **Create**:


|Category |Parameter |Description |
|---|---|---|
|**Basic Settings** |**Upload File** |Upload a ZIP package. The ZIP package must contain the `index.html` entry file. |
|**General Settings** |**Project** |Enter the project name. |
||**Description** (Optional) |Enter the project description. |
||**Project** |Select the associated BytePlus project. |
||**Acceleration Region** |Select an available acceleration region in the console. |
|**Acceleration Settings** |**Domain** (Optional) |Configure a custom domain. If you leave it blank, the project can still be accessed through the platform preview address after creation. |
||**Auto\-Generate Free Certificate** |Automatically apply for a free certificate for the custom domain. |


After the project is created, Pages automatically triggers the first deployment.

<span id="import-a-project-from-git"></span>
## Import a Project from Git

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260521081553-1071987012961.png) </span>

After you select **Git**, complete the following steps:


1. In the **Import Git Repository** section, first add a GitHub account.

2. On the GitHub authorization page, choose whether to allow Pages to access:

   * All repositories, or

   * Selected repositories.

3. After authorization is complete, return to the Pages console. The console displays the list of repositories that Pages is authorized to access under the current account.

4. Click **Import** next to the target repository.

5. After the repository is imported, configure the following settings:

   
   |Category |Parameter |Description |
   |---|---|---|
   |**Import Git Repository** |**GitHub Account / Repository** |Displays information about the imported repository. |
   ||**Production Branch** |The default branch is used for the initial build. After the project is created, you can change the production branch on the project details page. |
   |**Build and Output Settings** |**Root Directory** |Specifies the directory that contains the project source code. |
   ||**Build Output Directory** |Specifies the build output directory, for example, `dist`. |
   ||**Build Command** |Specifies the build command, for example, `npm run build`. |
   ||**Install Command** |Specifies the dependency installation command, for example, `npm install` or `npm ci`. |
   |**Environment Variables** |**Key / Value** |Optional. Sets environment variables for the build or runtime. |
   |**General Settings** |**Pages Project Name** |Enter the project name. |
   ||**Project Description** (Optional) |Enter the project description. |
   ||**Project** |Select the associated BytePlus project. |
   ||**Acceleration Region** |Select an available acceleration region in the console. |
   |**Acceleration Settings** |**Domain** (Optional) |Configure a custom domain. If you leave it blank, the project can still be accessed through the platform preview address after creation. |
   ||**Auto\-Generate Free Certificate** |Automatically apply for a free certificate for the custom domain. |
   

6. Click **Create**.


After the project is created, Pages automatically pulls the repository code and triggers the first deployment. After deployment succeeds, you can access the deployed result from the **Preview** entry in the project list or from the **Preview** section on the project details page.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Environment variable names must use valid characters. Do not enter email addresses or other values that contain <code>@</code> directly in the <strong>Key</strong> field.</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260521081802-1076860719883.png) </span>

<span id="notes"></span>
## Notes


* For projects created from Git, code changes in the repository do not take effect until you trigger a new deployment.

* For projects created by uploading a ZIP file, you can later upload a new ZIP package through **Deployments \> New Deployment** to update the project.
