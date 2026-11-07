---
title: "Use Pages Templates"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/use-pages-templates_en"
---

This document describes how to create a Pages project from a template, and explains common template types and model integration.

<span id="create-a-project-from-a-template"></span>
## Create a Project from a Template

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260521082254-1629399706752.png) </span>

After you select **Template**, complete the following steps:


1. Choose a template from the template list, such as `Vuejs`, `Nextjs`, `HTML2Markdown`, `OpenClaw`, or `VibeCoding`.

2. In the **Select Git Provider Account** section, choose the GitHub account that will be used to create the template project.

3. In the **Configure Project** section, enter or select the following information:

   * **Project Page Name**

   * **Repository Name**

   * **Acceleration Zone**

   * **Repository Visibility** (**Private** or **Public**)

4. Configure related parameters in the **Environment Variables** section as required by the selected template.

5. If the selected template requires model capabilities, add the related model configuration in the **Model Settings** section.

6. If needed, configure a custom domain in **Acceleration Settings** and choose whether to auto\-generate a free certificate.

7. Click **Create**.


After the template project is created, Pages performs the following actions:


* Creates a new repository automatically under the selected GitHub account.

* Automatically triggers the first deployment by using the generated repository.

* Generates an accessible preview link after deployment succeeds.


<span id="common-templates"></span>
## Common Templates

The main configuration areas are mostly the same across templates. The main differences are usually reflected in the template positioning, preset capabilities, environment variable requirements, and model configuration requirements. The common templates in the current console can be understood as follows:


* `Vuejs` and `Nextjs` are general framework templates. They mainly provide starter projects based on the corresponding technology stack and are suitable for building custom sites or applications from a base project.

* `HTML2Markdown` is a scenario\-oriented utility template. It provides preset tool capabilities and related configuration items and is suitable for quickly creating a utility project with a clearly defined purpose.

* `VibeCoding` and `OpenClaw` are scenario\-oriented AI application templates. `VibeCoding` is used to create a sample project that generates applications with model capabilities. `OpenClaw` is an OpenClaw application template built on Next.js. Neither of them is just a frontend framework option. Instead, both are template projects with preset business capabilities.


<span id="model-integration"></span>
## Model Integration

In the current console, the **Model Settings** section supports adding model configuration for some templates.

Both `OpenClaw` and `VibeCoding` support model integration through Volcengine Ark. In addition, `VibeCoding` also supports third\-party model integration.

<span id="notes"></span>
## Notes


* For projects created from a template, Pages first creates the corresponding repository and automatically runs the first deployment.

* After a template project is created, subsequent updates still require a new deployment based on repository changes.
