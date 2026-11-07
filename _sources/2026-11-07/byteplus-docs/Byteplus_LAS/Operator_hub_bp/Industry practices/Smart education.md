---
title: "Smart education"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Smart-education"
---

The core competitiveness of teaching content production lies in accurately expressing knowledge structures, rapidly generating teaching content, and flexibly adapting to various teaching scenarios. However, traditional teaching content production relies on manual recording, data collation, typesetting and transcription, and repeated revisions, resulting in high costs, long cycles, and difficulty in reuse. LAS multimodal operators focus on two sub\-scenarios: teaching video generation and teaching material digitalization, helping schools, online education platforms, and training institutions provide high\-quality, large\-scale teaching content at lower costs.

<span id="4915dd05"></span>
# Application scenarios

<span id="fa69793f"></span>
## Teaching video generation

Automatically generate explanation videos, teaching videos featuring digital humans, courseware dubbing, and short knowledge videos for scenarios such as course recording, knowledge explanation, exercise explanations, and enrollment promotion. This caters to sectors including K12, vocational education, language training, and internal corporate training, enhancing the efficiency of course content production and supporting the supply of video content across multiple subjects, versions, and batches.

<span id="894a2f05"></span>
## Digitization of teaching materials

For the digitization of content such as textbooks, handouts, test papers, lesson plans, and experimental materials, convert paper\-based or unstructured materials into editable, searchable, and reusable digital content. This enables the accumulation of teaching materials, construction of question banks, organization of courseware, and management of teaching and research assets, thereby improving content management efficiency and subsequent processing capabilities.

<span id="3c68119b"></span>
# Related operators

For the two sub\-scenarios of smart education, LAS provides corresponding multimodal operators:


* Video Script Planner: Handles the planning of scripts from the inspiration and conception of teaching videos to video generation.

* Image generation: Handles the task of generating input image materials for teaching video generation.

* Audio generation: Handles the task of generating audio materials for teaching video generation. You can contact technical support to obtain support for targeted audio generation operator capabilities.

* [Enhanced/basic video generation](https://docs.byteplus.com/docs/Byteplus_LAS/video_gen_enhanced): Handles highly controllable video production for teaching video generation. You can also contact technical support to obtain support for targeted video generation operator capabilities.

* Audio and Video Merge: Handles tasks such as dubbing synthesis for the final video.

* [PDF Document Parsing (Doubao)](https://docs.byteplus.com/docs/Byteplus_LAS/86966): Handles high\-fidelity structured parsing for teaching material digitalization.


<span id="18c5d876"></span>
## Video generation operators (teaching video generation)

LAS provides a general video generation operator based on Seedance 2.x capabilities, and also supports video generation operators targeted for educational scenarios (contact technical support to apply for use). Focusing on highly controllable video generation scenarios, it can organize screen structure, text layout, visual elements, and animation logic into a manageable generation workflow, making video content better suited for high\-demand production scenarios in terms of stability, controllability, brand consistency, and accuracy of information expression.

<span id="09a2bc61"></span>
### Application process flow

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1d6903de5654b11a9b8c293f71ef432~tplv-goo7wpa0wc-image.image) </span>


* **Inspiration and script preparation:**  Organize the teaching script (poetry, key points, and courseware outline) and visual reference images, and clarify the target art style, duration, and narration style.

* **Storyboard and illustration asset generation:**  Use Seedream / Seedance to generate cover images, character reference images, and storyboard clips, providing stable visual assets for the teaching video.

* **Narration audio generation:**  Synthesize clear and gentle standard Mandarin narration audio according to the script, generating both the full narration and segmented explanations by sentence for easy alignment with visuals.

* **Read\-along page generation:**  Generate horizontal teaching courseware pages with a rice paper texture based on prompts, supporting a unified layout for title, author, poem lines, phonetic annotation, explanation, and illustrations, with sentence\-by\-sentence highlighting and smooth transitions.

* **Output a controllable video:**  Render a 1280×720 teaching video with one click, ensuring stable animation rhythm and consistent brand style, with issues traceable and layout reproducible.


<span id="d7070fa6"></span>
## PDF Document Parsing (Doubao) (Digitization of teaching materials)

PDF Document Parsing (Doubao) is a multimodal data processing operator provided by the AI Data Lake Service (LAS), offering visual\-level structured parsing of PDF, image, PPT, and other files, high\-fidelity Markdown output, image recognition, and flexible output modes. It can be widely used for accurately converting PDFs to structured Markdown, restoring image\-text formulas, batch processing, and building knowledge bases.

<span id="6ffbc51f"></span>
### Application workflow


* **Select the operator:**  Go to the "Operator Plaza" in the LAS product console, select "PDF Document Parsing (Doubao)", and click "Online Experience".

* **Upload documents:**  Close the sample document, click "Upload File", select teaching materials, handouts, exam papers, lesson plans, or other PDF or image files, and complete the upload.

* **Configure parsing parameters:**  Select the parsing mode (normal / detail) and configure the page range according to the teaching scenario, then click "Confirm" to submit the task.

* **Return results:**  After parsing is complete, the operator returns structured Markdown or plain text content. Click "Download" to obtain the results, which can then be integrated into question banks, courseware, and knowledge base workflows.


<span id="ed0dd8d0"></span>
# Examples

The following examples are all drawn from real\-world smart education scenarios, demonstrating the use of two types of operators in typical teaching tasks.

<span id="006d94e0"></span>
## Example 1 · Teaching video generation

Based on the script of Li Bai's "Viewing the Waterfall at Mount Lu," a targeted video generation operator is used to produce a 1280×720 landscape poetry companion video for children's poetry enlightenment and classroom teaching scenarios.


* **Input:**  A complete multimodal generation script, including a cover image, a reference image for the Li Bai character, 12 opening storyboard segments, illustrations for each line, full and line\-by\-line reading audio, as well as companion page structure and visual requirements.

* **Processing:**  Seedream generates the cover image and character reference image → Seedance generates 12 opening storyboards based on the character reference image → generates full and line\-by\-line reading audio → the targeted video generation operator renders poetry companion pages with rice paper texture according to the prompts.

* **Output:**  A 16:9 traditional ink\-style teaching video, where the title, verses, phonetic annotations, explanations, illustrations, and reading audio are presented synchronously. The animation rhythm is stable, the brand tone is consistent, and the video can be used directly for classroom instruction or at\-home poetry reading.


<span id="857cd14b"></span>
## Example 2 · Teaching material digitization (PDF Document Parsing)

For blurry pages and complex layouts in PDFs containing multiple columns, images, and summary blocks, PDF Document Parsing quickly converts them into editable and searchable structured teaching materials.


* **Blurry page parsing:**  The normal mode extracts table of contents numbers and titles; the detail mode restores them as standard Markdown level\-one headings plus ordered lists, with clear retention of page references and numbering hierarchy.

* **Complex layout parsing:**  The normal mode restores the main text; the detail mode automatically reorganizes multi\-column content into multi\-level headings and paragraphs, preserving column structures such as "Guangzhou Seven Days" and the hierarchy of subheadings.

* **Output:**  Structured Markdown or text files that can be directly integrated into downstream processes such as question bank development, courseware organization, teaching research asset management, and knowledge base entry.
