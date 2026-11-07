---
title: "Usage instructions"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/hue_Usage_instructions"
---

<span id="概述"></span>
## Overview

Hue is a browser\-based graphical user interface that enables rapid development and debugging of various applications in the Hadoop ecosystem.

<span id="hue-功能"></span>
## Hue features

The unified Hue interface allows you to perform the following operations on components:


1. HDFS: view, create, manage, rename, move, delete files or directories, upload and download files, and more

2. Hive: edit and execute HQL, save SQL templates, copy templates, edit templates, and more

3. Spark: edit and execute SparkSQL, and more

4. YARN: view and filter user jobs, and more


<span id="hue使用"></span>
## Using Hue

Accessing the Hue UI

Hue uses LDAP authentication by default. You can check the LDAP slapd.conf configuration to obtain login usernames and passwords. It is recommended to log in with the hive account. To allow other accounts to use Hue in the future, add the corresponding accounts in LDAP in advance.

<span id="hue-ui-使用"></span>
### Using the Hue UI

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/1fd2c0b957c547c594684497a9bc7311) </span>

After entering the Hue UI, you can select the desired function from the left tab. For example, in Editor, you can choose the corresponding execution engine, and then execute SQL statements for that engine in the Notebook on the right.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/fe79c435f2234460a528b827688671d1) </span>

Switch to the File Browser page to browse and manage files on HDFS.

Switch to the Jobs page to query and manage jobs.
