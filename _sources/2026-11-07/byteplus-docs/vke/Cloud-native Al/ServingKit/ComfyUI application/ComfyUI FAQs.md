---
title: "ComfyUI FAQs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ComfyUI_FAQs"
---

This topic provides answers to frequently asked questions related to ComfyUI applications.


<span id="rj2U7Ryc"></span>
### How can I modify my ComfyUI workflow to use acceleration nodes of ServingKit?

To do so, you can configure the modules in the workflow by following the instructions below.


|Module name |Workflow without acceleration node |Workflow using acceleration node |Description |
|---|---|---|---|
|Resource Pool |No |Exclusive module |Add a Resource Pool node to your workflow and configure single\-GPU inference. |
|Load Models Here |Universal UNET loader |OpenVefuser DiT Loader |Replace the UNET loader with the OpenVefuser plugin developed by BytePlus for inference. |
|OpenVefuser Apply FBCache |No |Exclusive module |Add an FBcache node to your workflow to enable cache reuse. |
|Sampler |KSampler |OpenVefuser KSampler |Replace the KSampler with the OpenVefuser plugin developed by BytePlus for inference. |






<span id="hLdYGZEL"></span>
### How do I resolve the "model missing" message when I open a ComfyUI workflow?

It depends on whether you have local model files:


<span id="12AUk0jH"></span>
#### Local model files present


1. Download the TOS tool [tosutil](https://docs.byteplus.com/en/docs/tos/Download-and-install) or [TOSBrowser](https://docs.byteplus.com/en/docs/tos/Install-tos-browser), which you will use to manage ComfyUI nodes or download content. For details, see [Commonly used TOS tools](https://docs.byteplus.com/en/docs/tos/TOS_common_tools_overview).

2. Get an API access key that has at least read and write access to TOS. For details, see [Getting access keys](https://docs.byteplus.com/en/docs/IAM/about-access-keys).

3. Log in to the [tosutil](https://docs.byteplus.com/en/docs/tos/Download-and-install) or [TOSBrowser](https://docs.byteplus.com/en/docs/tos/Install-tos-browser) tool and upload model files. This example shows how to upload model files from a macOS machine over the Internet by using tosutil.

   1. Open the local terminal and execute the following command to register configuration information.

      ```Bash
      ./tosutil config -i $your_ak -k $your_sk -e $your_tos_endpoint -re $your_region
      ## Example
      ## ./tosutil config -i AK****** -k sk****** -e tos-cn-beijing.volces.com -re cn-beijing
      ```
      

   2. Execute the following command to upload the local model files to the `models` directory of ComfyUI in the TOS bucket.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The <code>models</code> directory of ComfyUI in TOS contains multiple subdirectories for different scenarios. You need to upload the model files to the corresponding subdirectory. For example, when uploading files related to the LoRA model, use the <code>models/loras</code> directory. For information about the ComfyUI <code>models</code> directory, see the <a href="https://docs.comfy.org/development/core-concepts/models">official ComfyUI documentation</a>.      </div>
      

      ```Bash
      ./tosutil cp $your_local_model_file_path  $your_tos_comfyui_models_path  -r
      ## Example
      ## ./tosutil cp /Users/Downloads/qwen-image-edit-2509.safetensors  tos://comfyui/models/diffusion_models/  -r
      ```
      





<span id="hq23FeiN"></span>
#### No local model files present


1. Download the required model files from public model library services such as Hugging Face and ModelScope, then upload them to your TOS bucket.

2. Download models using the oniond tool.

   1. On the **Application details** page of ComfyUI, go to the **Service specifications** section on the **Service overview** tab and click the instance name corresponding to the application.

   2. On the instance (pod) details page, click **Console** in the upper\-right corner to log in to the pod.

   3. Execute the following command in the pod to download the models.

      ```Bash
      http_proxy="" https_proxy="" oniond download model WanVideo_comfy --include InfiniteTalk/Wan2_1-InfiniTetalk-Single_fp16.safetensors --dir /app/ComfyUI/models/vae/
      ## http_proxy="" https_proxy="" : HTTP and HTTPS configuration. If your ComfyUI application has the http_proxy environment variable, you must specify the variable value here.
      ## oniond download model WanVideo_comfy --include InfiniteTalk/Wan2_1-InfiniTetalk-Single_fp16.safetensors : Download the required model.
      ## --dir /app/ComfyUI/models/vae/ : Download the model to the specified directory.
      ```
      

3. Restart the ComfyUI application.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6f580e79aa142c7066fe91a0ef4984b7.png) </span>




<span id="AKWl7Yrp"></span>
### How do I call workflow JSON using the native ComfyUI API?


1. On the ComfyUI application page, click the dropdown symbol in the upper\-left corner, select **Settings** and enable **Dev Mode**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_43ebabe74c6ab87801a506d5c6fcf75c.png) </span>

2. On the ComfyUI application page, click the drop\-down symbol in the upper\-left corner, select **Settings \> Export (API)**  to export the workflow JSON file to be executed.

3. Create a script in your Python environment and call it using the native ComfyUI API:

   * **Execute the model**: Create a Python script named `prompt.py` and run the `python3 prompt.py` command to execute the model to generate an image.

      The following `prompt.py` file provides an example. Adjust parameter values in this sample code as needed.

      ```Python
      import requests
      import json
      import os
      import random
      INPUT_IMAGE_NODE_1 = "17"
      INPUT_IMAGE_NODE_2 = "25"
      POSITIVE_PROMPT_NODE = "28"
      NEGATIVE_PROMPT_NODE = "14"
      SEED_NODE = "37"
      WORKFLOW_FILE_PATH = "data/qwenimageedit2509.json" # Replace the value with the relative address of your own workflow JSON file.
      APIGATEWAY_HOST = "sd4034************.apigateway-cn-beijing.volceapi.com" # Replace the value with your own ComfyUI domain name.
      
      headers = {}
      
      def generate_image(image_file_name_1, image_file_name_2, prompt, negative_prompt=""):
          # ComfyUI access address.
          server_url = f"http://{APIGATEWAY_HOST}"
          
          # Load the workflow template.
          script_dir = os.path.dirname(os.path.abspath(__file__))
          workflow_file_path = os.path.join(script_dir, WORKFLOW_FILE_PATH)
          with open(workflow_file_path, 'r', encoding="utf-8") as f:
              workflow = json.load(f)
          
          # Modify prompts based on your workflow node ID.
          workflow[POSITIVE_PROMPT_NODE]["inputs"]["prompt"] = prompt          # Positive prompt node.
          workflow[NEGATIVE_PROMPT_NODE]["inputs"]["prompt"] = negative_prompt # Negative prompt node.
          workflow[SEED_NODE]["inputs"]["seed"] = random.randint(0, 999999999999999) # Random seed.
          workflow[INPUT_IMAGE_NODE_1]["inputs"]["image"] = image_file_name_1
          workflow[INPUT_IMAGE_NODE_2]["inputs"]["image"] = image_file_name_2
          # Submit prompts.
          submit_url = f"{server_url}/prompt"
          response = requests.post(submit_url, json={"prompt": workflow}, headers=headers)
          
          if response.status_code == 200:
              print(f"Response Headers: {response.headers}")
              prompt_id = response.json()["prompt_id"]
              print(f"Task submitted! Prompt ID: {prompt_id}")
              return prompt_id
          else:
              print("Submission failed:", response.text)
              return None
      
      # Usage example.
      if __name__ == "__main__":
          prompt_id = generate_image(
              image_file_name_1="*******.jpg",  # An image file. Ensure the file has been uploaded.
              image_file_name_2="*******.png",  # An image file. Ensure the file has been uploaded.
              prompt="Apply the light beige ribbed texture and the U-neck short-sleeve slim fit design; retain the model's light denim frayed mini skirt, waist belt, white handbag, red plaid silk scarf and white sneakers, as well as the light gray background and lighting, to make the top fit the model's figure naturally and create a cohesive style",  # Positive prompts. Replace them as needed.
              negative_prompt="Vibrant gaudy tones, overexposed, static, unclear details, stylized distortion, artwork-like unnatural effect, overall grayish tone, worst quality, low quality, JPEG compression artifacts, ugly, incomplete, extra fingers, poorly drawn hands, poorly drawn face, deformed, mutilated, malformed limbs, fused fingers, cluttered background, three legs"  # Negative promptst. Replace them as needed.
          )
          print(prompt_id)
      ```
      

   * **Query history**: Create a Python script named `history.py` and run the `python3 history.py` command to query the history.

      The following `history.py` file provides an example. Adjust parameter values in this sample code as needed.

      ```Python
      import requests
      import json
      import os
      from datetime import datetime
      from PIL import Image
      import io
      import matplotlib.pyplot as plt
      
      # Obtain the directory where the current script is located.
      script_dir = os.path.dirname(os.path.abspath(__file__))
      # Create a directory for saving images in the directory where the model script is located.
      images_dir = os.path.join(script_dir, "comfyui_history_images")
      os.makedirs(images_dir, exist_ok=True)
      
      # headers = {'x-upstream-session-id': 'MTkyLjE2OC4zMi4y******'}
      headers = {}
      
      def get_comfyui_history(server_url="http://127.0.0.1:7860", max_entries=None):
          """
          Get all history records of ComfyUI
          
          Parameters:
          server_url: ComfyUI server address (default: http://127.0.0.1:7860)
          max_entries: Maximum number of records to return (default: return all)
          
          Returns:
          Dictionary containing history records, sorted in reverse chronological order
          """
          history_url = f"{server_url}/history"
          
          try:
              response = requests.get(history_url, headers=headers)
              print(f"----Response Headers----: {response.headers}")
              response.raise_for_status()  # Check HTTP errors.
              history_data = response.json()
              
              # If there is no history, display the following content.
              if not history_data:
                  print("No history records found")
                  return {}
              
              # Limit the maximum number of returned entries. If max_entries is provided, limit the number of returned entries.
              if max_entries and max_entries > 0:
                  # Convert the dictionary to a list, then slice the list, and convert it back to a dictionary.
                  # Note that dictionaries are unordered. Slicing here is based on the insertion order of dictionary items in Python 3.7+.
                  # To follow a specific order, sort before slicing.
                  items = list(history_data.items())
                  sorted_history = dict(items[:max_entries])
              else:
                  sorted_history = history_data
              
              return sorted_history
          
          except requests.exceptions.RequestException as e:
              print(f"Failed to get history records: {e}")
              return {}
          except json.JSONDecodeError:
              print("Failed to parse JSON response")
              return {}
      
      def download_image(image_url, save_path=None):
          """Download and display the image"""
          try:
              response = requests.get(image_url, headers=headers)
              response.raise_for_status()
              print(f"----Response Headers----: {response.headers}")
              
              # Create an image from byte data.
              img = Image.open(io.BytesIO(response.content))
              
              # (Optional) Save the image (if needed).
              if save_path:
                  img.save(save_path)
                  print(f"Image saved to: {save_path}")
              
              # Display the image.
              plt.figure(figsize=(8, 8))
              plt.imshow(img)
              plt.axis('off')
              plt.title("Generated Image")
              plt.show()
              
              return True
          except Exception as e:
              print(f"Failed to download/display image: {e}")
              return False
      
      def print_history_summary(history, server_url="http://127.0.0.1:8188", show_images=True):
          """
          Print history record summary and display images
          
          Parameters:
          history: Dictionary of history records
          server_url: ComfyUI server address
          show_images: Whether to display images
          """
          if not history:
              print("No available history records")
              return
          
          print(f"\n{'='*50}")
          print(f"{len(history)} history record(s) found")
          print(f"{'='*50}")
          
          for i, (prompt_id, task) in enumerate(history.items()):
              # History extraction status.
              status = "Completed" if task['status']['completed'] else "Incomplete"
              
              # Collect image information.
              image_urls = []
              if 'outputs' in task:
                  for node_id, node_output in task['outputs'].items():
                      if 'images' in node_output:
                          for image in node_output['images']:
                              # Construct a URL to access the image.
                              image_url = f"{server_url}/view?filename={image['filename']}&type=output"
                              image_urls.append(image_url)
              
              print(f"\nRecord #{i+1}:")
              print(f"├─ Prompt ID: {prompt_id}")
              print(f"├─ Status: {status}")
              print(f"├─ Generated images: {len(image_urls)}")
              
              # Display the image.
              if show_images and image_urls:
                  print("├─ Displaying image...")
                  # Display only the first image (to avoid showing too many).
                  image_url = image_urls[0]
                  save_path = os.path.join(images_dir, f"{prompt_id}.png")
                  
                  # Download and display the image.
                  if download_image(image_url, save_path):
                      print(f"├─ Display completed: {image_url}")
                  else:
                      print("├─ Image display failed")
                  
                  # If there are more images, display only the URLs.
                  if len(image_urls) > 1:
                      print(f"├─ Other image URLs ({len(image_urls)-1}):")
                      for j, url in enumerate(image_urls[1:3]):  # Display up to 2 additional URLs.
                          print(f"│  ├─ Image {j+2}: {url}")
                      if len(image_urls) > 3:
                          print(f"│  └─ ...and {len(image_urls)-3} more images")
              elif image_urls:
                  # If the image is not displayed, display only the URL.
                  print("├─ Image URLs:")
                  for j, url in enumerate(image_urls[:3]):  # Display URLs for up to 3 images.
                      print(f"│  ├─ Image {j+1}: {url}")
                  if len(image_urls) > 3:
                      print(f"│  └─ ...and {len(image_urls)-3} more images")
              else:
                  print("├─ Images: None")
      
      # Usage example.
      if __name__ == "__main__":
          server_address = "http://sdxxxxxxxxxxpjg.apigateway-cn-beijing.volceapi.com"  # Replace the value with your own ComfyUI application access address.
          
          # Obtain all historical records.
          history = get_comfyui_history(server_url=server_address, max_entries=1)
          
          # Print summary and display the image.
          print_history_summary(history, server_url=server_address, show_images=True)
          
          # (Optional) Save the complete history to a file.
          comfyui_history = os.path.join(script_dir, "comfyui_history.json")
          with open(comfyui_history, 'w') as f:
              json.dump(history, f, indent=2)
          print("\nComplete history records saved to comfyui_history.json")
      ```
      






<span id="k0tl2Lfh"></span>
### What should I do if the ComfyUI application page cannot display logs?

ComfyUI application logs are associated with the Upstream Ingress of the API Gateway instance linked to the application. The Method settings in the routing matching rule bound to the Upstream Ingress must include the Patch method.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d92ebc308f20a0ce49e6c3dea4e41f31.png) </span>

If your existing Upstream Ingress does not meet this requirement, you can create a new Upstream Ingress or submit an [API Gateway ticket](https://console.byteplus.com/workorder/create?step=1) to contact technical support for updating it.
