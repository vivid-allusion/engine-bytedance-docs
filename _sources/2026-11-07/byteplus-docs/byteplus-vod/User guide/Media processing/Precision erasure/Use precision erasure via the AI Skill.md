---
title: "Use precision erasure via the AI Skill"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/precision-erasure-skill"
---

The [byted-byteplus-vod-precision-erasure](https://clawhub.ai/volcengine-skills/byted-byteplus-vod-precision-erasure) skill is an official BytePlus VOD skill that enables you to remove hardcoded subtitles and on\-screen text from videos through simple natural language commands within your AI assistant — no API integration required. Powered by automated OCR detection and AIGC\-based inpainting, it delivers seamless background restoration and outputs a clean, subtitle\-free video.

Typical use cases include content localization, cross\-language dubbing and translation, and video secondary creation.

<span id="21b19580"></span>
## Prerequisites

Before installation, ensure you have the following information ready:


1. **ArkClaw environment**: An environment capable of running official skills (such as Trae, OpenClaw, or ArkClaw).

2. **Access Key (AK/SK)** : Create and obtain your `Access Key ID` and `Secret Access Key` from the [BytePlus IAM console](https://console.byteplus.com/auth/login?redirectURI=%2Fiam%2Fkeymanage%2F).

3. **VOD space name**: Create a space in the [BytePlus VOD console](https://console.byteplus.com/auth/login?redirectURI=%2Fvod%2Foverview%2F) and record its name.


<span id="2595c388"></span>
## Quick start

<span id="1b24e560"></span>
### Step 1: Install the skill

In your AI assistant's chat window, send the following command to install the skill:

```Plain
Install this skill from ClawHub: https://clawhub.ai/volcengine-skills/byted-byteplus-vod-precision-erasure
```


<span id="dc632698"></span>
### Step 2: Configure environment variables

Set up your credentials and workspace by sending the following command (replace the placeholders with your actual information):

```Plain
Configure environment variables for byted-byteplus-vod-precision-erasure:
VOD_ACCESS_KEY = "Your_Access_Key_ID"
VOD_SECRET_KEY = "Your_Secret_Access_Key"
VOD_SPACE_NAME = "Your_VOD_Space_Name"
VOD_REGION = "ap-southeast-1"
```


<span id="64e8a10e"></span>
## Skill in action

Once configured, you can describe your requirements directly in the chat window using natural language.

<span id="b6e1e430"></span>
### **Scenario 1: Automatic subtitle erasure**


* **User prompt:**   *"Remove all subtitles from this video."* 

* **Skill action:**  Runs OCR detection to locate subtitle regions across the entire video and applies AIGC inpainting to restore the background seamlessly.


<span id="4b0f0b73"></span>
### **Scenario 2: Remove all on\-screen text**


* **User prompt:**   *"Erase all text from this video, including subtitles, scene labels, and character introductions."* 

* **Skill action:**  Switches to full text erasure mode, detecting and removing all on\-screen text overlays across the video.


<span id="440d856f"></span>
### **Scenario 3: Erase subtitles in specific segments**


* **User prompt:**   *"Remove subtitles only between 10s and 60s."* 

* **Skill action:**  Applies `Selected` mode, restricting erasure to the specified time range while leaving the rest of the video unchanged.


<span id="ddf1e03f"></span>
### **Scenario 4: Erase subtitles while preserving specific segments**


* **User prompt:**   *"Remove all subtitles except the opening credits in the first 15 seconds."* 

* **Skill action:**  Applies `Skip` mode, erasing subtitles across the entire video while preserving the defined segment.
