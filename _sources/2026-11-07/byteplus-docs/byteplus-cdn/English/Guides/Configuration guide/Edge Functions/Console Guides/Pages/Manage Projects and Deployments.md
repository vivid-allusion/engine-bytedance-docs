---
title: "Manage Projects and Deployments"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/manage-projects-and-deployments_en"
---

This document describes how to view project details, modify project settings, and manage deployment history in Pages.

<span id="view-project-details"></span>
## View Project Details

After you enter a Pages project, the current project details page includes the following tabs:


* **Overview**

* **Deployments**


<span id="manage-settings-on-the-overview-page"></span>
## Manage Settings on the Overview Page

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260521082757-186519274222.png) </span>

The **Overview** page currently includes the following management areas:


* **General Settings**: View or edit the Pages project name, project description, project, and acceleration region.

* **Domain Management**: View the currently bound domains and add new custom domains.

* **Git Management**: View the current repository and switch the production branch.

* **Build and Output Settings**: Modify the root directory, build output directory, build command, and install command.

* **Environment Variables**: Add or update environment variables.

* **Preview**: View the preview thumbnail and preview URL for the current deployment.


<span id="git-management"></span>
## Git Management

For projects created from Git, you can do the following in **Overview \> Git Management**:


* View the current repository.

* View the current production branch.

* Switch the production branch.


After you switch the production branch, subsequent deployments that you trigger are based on the selected production branch.

<span id="build-and-output-settings"></span>
## Build and Output Settings

In **Overview \> Build and Output Settings**, you can modify the following settings:


* **Root Directory**

* **Build Output Directory**

* **Build Command**

* **Install Command**


These settings determine how Pages installs dependencies, runs the build, and publishes static assets from the specified directory.

<span id="environment-variables"></span>
## Environment Variables

In **Overview \> Environment Variables**, you can add or modify environment variables.

The current environment variable configuration has the following characteristics:


* Uses the **Key / Value** structure.

* `Value` is masked by default.

* You can reveal the plaintext value through the icon on the right.

* Copying `Value` is supported.


<span id="view-deployment-history"></span>
## View Deployment History

On the project details page, click the **Deployments** tab to view deployment history.

The current deployment list displays the following information:


* **Deployment ID**

* **Status**

* **Created At**

* **Completed At**

* **Actions**


From the deployment list, you can perform the following operations:


* **New Deployment**: Trigger a new deployment.

* **Download**: Download the output artifacts of the selected deployment.

* **Rollback**: Roll back the online version to a historical successful deployment.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <strong>Rollback</strong> action is available only when there is at least one historical successful deployment that can be rolled back to.</div>


<span id="view-deployment-details"></span>
## View Deployment Details

On the **Deployments** tab, click a **Deployment ID** to enter the **Deployment Details** page.

<span id="general"></span>
### General

The **General** section displays the basic information of the deployment, including:


* Project name

* Environment, such as `Production`

* Branch

* Duration

* Date

* Commit information


<span id="build-logs"></span>
### Build Logs

On the **Build Logs** tab, you can view complete build logs for troubleshooting issues during dependency installation, build, and publishing.

<span id="build-summary"></span>
### Build Summary

On the **Build Summary** tab, you can view the list of build artifacts for the current deployment, including file paths and file sizes.

<span id="functions"></span>
### Functions

If the current deployment contains a `/functions` directory, the corresponding function routes are also displayed on the **Functions** tab. For details, see [Use Pages Functions](https://docs.byteplus.com/docs/byteplus-cdn/use-pages-functions_en).

<span id="notes"></span>
## Notes


* For projects created from Git, changes in the code repository do not take effect until you trigger a new deployment.

* For projects created by uploading a ZIP file, you can later upload a new ZIP package through **Deployments \> New Deployment** to update the project.
