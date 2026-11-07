---
title: "Multimodal sample calls (prompts and files)"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Multimodal_sample_calls_prompts_and_files"
---

This topic describes the method for calling an agent in a multimodal manner. The method enables the direct input of multimodal files, such as images, videos, and PDF files, to the AgentKit model. The model can directly parse multimodal content without the need for analysis via external tools. For example, there is no need to embed a URL into a prompt or rely on file parsing tools for such analysis.

<span id="hZdCksTQ"></span>
## Prepare the environment


1. Initialize the Python environment.

   Use `uv` to build an independent Python virtual environment (Python 3.10+ is recommended).

   ```Bash
   # Initialize the uv configuration.
   uv init
   # Create a uv virtual environment.
   uv venv
   ```
   

2. Install dependencies.

   1. Install the latest version of VeADK.

      ```Bash
      uv pip install "git+https://github.com/volcengine/veadk-python.git"
      ```
      

   2. Install AgentKit SDK.

      ```Bash
      uv pip install agentkit-sdk-python
      ```
      

3. Enable the capability to upload multimodal files.

   Add `enable_responses=True` in the agent code. After you set the `enable_responses` parameter to true, the agent will support the Response API, thereby enabling the capability to upload images, videos, and PDF files.

   ```Bash
   agent = Agent(
       name=agent_name,
       description=description,
       instruction=system_prompt,
       tools=tools,
       enable_responses=True # Enable the capability to input multimodal files.
   )
   ```
   


<span id="tLSOORwz"></span>
## Modify the agent entry function

When AgentKit calls the `/invoke` interface, it triggers the agent entry function `@app.entrypoint`. Modify this function to read the `files` parameter (a list of multimodal file URLs) from `payload` and pass it to the VeADK model.


|Original code (text only) |Modified code (support for multimodal files) |
|---|---|
|```Python```<br>```@app.entrypoint```<br>```async def run(payload: dict, headers: dict):```<br>```    prompt = payload["prompt"]```<br>```    user_id = headers["user_id"]```<br>```    session_id = headers["session_id"]```<br>``````<br>```    logger.info(```<br>```        f"Running agent with prompt: {prompt}, user_id: {user_id}, session_id: {session_id}"```<br>```    )```<br>``````<br>```    session_service = runner.short_term_memory.session_service  # type: ignore```<br>``````<br>```    # Prevent duplicate session creation.```<br>```    session = await session_service.get_session(```<br>```        app_name=app_name, user_id=user_id, session_id=session_id```<br>```    )```<br>```    if not session:```<br>```        await session_service.create_session(```<br>```            app_name=app_name, user_id=user_id, session_id=session_id```<br>```        )```<br>``````<br>```    new_message = Content(role="user", parts=[Part(text=prompt)])```<br>```    try:```<br>```        async for event in runner.run_async(```<br>```            user_id=user_id,```<br>```            session_id=session_id,```<br>```            new_message=new_message,```<br>```            run_config=RunConfig(streaming_mode=StreamingMode.SSE),```<br>```        ):```<br>```            # Format SSE data.```<br>```            sse_event = event.model_dump_json(exclude_none=True, by_alias=True)```<br>```            logger.debug("Generated event in agent run streaming: %s", sse_event)```<br>```            yield sse_event```<br>```    except Exception as e:```<br>```        logger.exception("Error in event_generator: %s", e)```<br>```        # Return error information.```<br>```        error_data = json.dumps({"error": str(e)})```<br>```        yield error_data```<br><br><br> |```Python```<br>```@app.entrypoint```<br>```async def run(payload: dict, headers: dict):```<br>```    prompt = payload["prompt"]```<br>```    user_id = headers["user_id"]```<br>```    session_id = headers["session_id"]```<br>``````<br>```    logger.info(```<br>```        f"Running agent with prompt: {prompt}, user_id: {user_id}, session_id: {session_id}"```<br>```    )```<br>``````<br>```    session_service = runner.short_term_memory.session_service  # type: ignore```<br>``````<br>```    # Prevent duplicate session creation.```<br>```    session = await session_service.get_session(```<br>```        app_name=app_name, user_id=user_id, session_id=session_id```<br>```    )```<br>```    if not session:```<br>```        await session_service.create_session(```<br>```            app_name=app_name, user_id=user_id, session_id=session_id```<br>```        )```<br>``````<br>```    new_message = Content(role="user", parts=[Part(text=prompt)])```<br>```    # Read the list of files from payload, encapsulate each file URL as Part.from_uri, and add them to the message body.```<br>```    files = payload.get("files", [])```<br>```    for file_url in files:```<br>```        new_message.parts.append(Part.from_uri(file_uri=file_url))```<br>``````<br>```    try:```<br>```        async for event in runner.run_async(```<br>```                user_id=user_id,```<br>```                session_id=session_id,```<br>```                new_message=new_message,```<br>```                run_config=RunConfig(streaming_mode=StreamingMode.SSE),```<br>```        ):```<br>```            # Format SSE data.```<br>```            sse_event = event.model_dump_json(exclude_none=True, by_alias=True)```<br>```            logger.debug("Generated event in agent run streaming: %s", sse_event)```<br>```            yield sse_event```<br>```    except Exception as e:```<br>```        logger.exception("Error in event_generator: %s", e)```<br>```        # Return error information.```<br>```        error_data = json.dumps({"error": str(e)})```<br>```        yield error_data```<br><br><br> |


<span id="kbbjQQWW"></span>
## Multimodal file call test

After the modification is complete, you can execute the `curl` command to call the `/invoke` interface, passing in the prompt (text instruction) and files (a list of multimodal file URLs). The following are sample calls for different file types:

<span id="ebaUktNp"></span>
### Image file call

```Bash
curl --location 'http://127.0.0.1:8000/invoke' \
--header 'Content-Type: application/json' \
--header 'user_id: 123' \
--header 'session_id: 1234243' \
--data '{
    "prompt": "describe this image , without using any tool",
    "files": ["your image url"]
}'
```


**Sample response**

```Plain Text
Start with the chicken feet: they have a bright, glossy golden-yellow color from the marinade, with the characteristic textured, wrinkled skin of cooked chicken feet, showing the raised scales/ridges clearly. The marinade is a thin, slightly reddish-orange oily sauce coating every surface, with small bits of chopped red chili peppers scattered amongst them, adding pops of bright red color. They are stacked in a heaping pile, some overlapping each other, looking plump and tender.
The plate is a simple rectangular white porcelain dish with rounded corners, sitting on a warm brown wooden surface that has visible wood grain. In the background, there's a blurred dark woven rattan or wicker texture, giving a rustic, homey food photography setting. A tiny hint of a whole red chili is visible on the far left edge of the frame. The lighting is warm and bright, highlighting the glossy sheen of the sauce on the chicken feet, making them look appetizing and savory, likely a spicy or marinated snack (like salted lemon chicken feet or spicy pickled chicken feet). 
```


<span id="n6B6aog8"></span>
### Video call

```Bash
curl --location 'http://127.0.0.1:8000/invoke' \
--header 'Authorization: Bearer U2asJlgLEaUtTMwVmp2iOhKDe_mkhfJu****' \
--header 'Content-Type: application/json' \
--header 'user_id: 123' \
--header 'session_id: 122442' \
--data '{
    "prompt": "describe this video, without using any tool",
    "files": [" your video url"]
}'
```


**Sample response**

```Plain Text
Opening (0-2s): A slow-motion close-up of glossy golden marinated chicken feet, with thick amber marinade dripping slowly off the ridged skin onto the white plate below, warm backlighting making the sauce glisten brightly.
3-4s: Cut to a hand slicing a plump bright red chili pepper on a wooden cutting board, releasing its juice and seeds onto the board, highlighting the spicy ingredient in the dish.
5-6s: A chef in a white coat places marinated chicken feet from a ladle onto the heaping plate, pouring the remaining thick yellow marinade over the pile, coating every piece.
7-8s: A close-up shot of the finished piled chicken feet, showing the wrinkled skin coated in sauce with red chili pieces scattered throughout.
9-11s: A person takes a bite of one of the chicken feet, looking satisfied as they chew the tender snack.
12-13s: The plate of chicken feet is shown paired with a frosty glass of beer and a small dish of dried red chilies, framing it as a perfect drinking appetizer.
14-15s: The plate is shown next to a takeout paper bag with a Chinese "tea" character logo, positioning it as a takeaway snack that pairs well with tea.
16-17s: Final close-up with text overlay (with minor typos) describing the snack as crunchy, spicy, and irresistible, with a 2-second countdown graphic.
```


<span id="iSUb2R4b"></span>
### PDF file

```Bash
curl --location 'http://127.0.0.1:8000/invoke' \
--header 'Authorization: Bearer U2asJlgLEaUtTMwVmp2iOhKDe_mkhfJu****' \
--header 'Content-Type: application/json' \
--header 'user_id: 123' \
--header 'session_id: 122442' \
--data '{
    "prompt": "describe this PDF main idea, without using any tool",
    "files": ["Your PDF FILE URL"]
}'
```


**Sample response**

```Plain Text
This PDF is a full overview of Creative Agent, an AI-powered end-to-end platform for creating professional quality videos from a single initial concept:
Core Value: It bridges the gap between a creative idea and a finished polished video, offering two workflows: a hands-on storyboard canvas for full manual control (for bespoke campaigns) and an automated UGC one-click workflow for fast, scalable content production.
Step-by-Step Workflow:
Start with a creative brief (prompt, duration, industry templates, reference images) to generate a structured storyboard.
Use an infinite node-based storyline canvas to refine shots: adjust the timeline, work with script nodes, source images, and use a context-aware AI chat panel to refine visuals conversationally, creating variation nodes to iterate on initial drafts.
Convert static image nodes into animated video clips by defining camera motion/effects, then assemble the final cut on the timeline, adjusting pacing and shot order before exporting the finished video.
Underlying AI Framework: The platform uses a proprietary context engineering system that expands simple user prompts into detailed, production-ready video instructions, following a three-stage pipeline:
Structure: Define the narrative blueprint
Dynamics: Add motion and environmental effects
Validation: Harmonize style and finalize optimized prompts
It uses two specialized pipelines to build the story blueprint and engineer cinematic motion, with quality checks at each stage.
Technical Architecture: Built on a modern enterprise stack: Next.js 13 frontend with React/Tailwind, Prisma + MySQL backend, cloud-native containerized deployment, integrating with best-in-class AI services (BytePlus for image/video generation, OpenAI for LLM orchestration, HiAgent for workflow tasks) using an adapter architecture for flexibility.
Final Pitch: Creative Agent acts as an intelligent co-pilot, combining user control with AI consistency to turn creative concepts into finished videos, framing it as augmented creativity rather than just automation.
```
