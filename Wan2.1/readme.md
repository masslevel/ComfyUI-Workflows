# Just another Wan 2.1 14B text-to-image post

---

**tl;dr: Got inspired by Wan 2.1 14B's understanding of materials and lighting for text-to-image. I mainly focused on high resolution and image fidelity (not style or prompt adherence) and here are my results including:
- [ComfyUI workflows](https://github.com/masslevel/ComfyUI-Workflows/tree/main/Wan2.1) on GitHub
- [Original high resolution gallery images](https://drive.google.com/drive/folders/1KgaA9XEnMWK7HzEVYjujJLVOMkGybJ8v?usp=sharing) with ComfyUI metadata on Google Drive
- The complete gallery on [imgur](https://imgur.com/a/ENoIXR0) in full resolution but compressed without metadata
- You can also get the original gallery PNG files on reddit using [this](https://ww.reddit.com/r/WidescreenWallpaper/comments/to3ld1/how_to_download_original_images_from_gallery_posts/) method

*If you get a chance, take a look at the images in full resolution on a computer screen.*
## Intro

*Greetings, everyone!*

Before I begin let me say that I may very well be late to the party with this post - I'm certain I am.

I'm not presenting anything new here but rather the results of my Wan 2.1 14B text-to-image (t2i) experiments based on developments and findings of the community. I found the results quite exciting. But of course I can't speak how others will perceive them and how or if any of this is applicable to other workflows and pipelines.

I apologize beforehand if this post contains way too many thoughts and spam - or this is old news and just my own excitement.

I tried to structure the post a bit and highlight the links and most important parts, so you're able to skip some of the rambling.

---
![intro image](https://i.imgur.com/QeLeYjJ.jpeg)

It's been some time since I created a post and really got inspired in the AI image space. I kept up to date on r/StableDiffusion, GitHub and by following along everyone of you exploring the latent space.

So a couple of days ago u/yanokusnir made this [post](https://www.reddit.com/r/StableDiffusion/comments/1lu7nxx/wan_21_txt2img_is_amazing/) about Wan 2.1 14B t2i creation and shared his awesome workflow. Also the research and findings by u/AI_Characters ([post](https://www.reddit.com/r/StableDiffusion/comments/1lx39dj/the_other_posters_were_right_wan21_text2img_is_no/)) have been very informative.

I usually try out all the models, including video for image creation, but haven't gotten around to test out Wan 2.1. After seeing the Wan 2.1 14B t2i examples posted in the community, I finally tried it out myself and I'm now pretty amazed by the visual fidelity of the model.

Because these workflows and experiments contain a lot of different settings, research insights and nuances, it's not always easy to decide how much information is sufficient and when a post is informative or not.

**So if you have any questions, please let me know anytime and I'll reply when I can!**

---
## "Dude, what do you want?"

In this post I want to showcase and share some of my Wan 2.1 14b t2i experiments from the last 2 weeks. I mainly explored image fidelity, not necessarily aesthetics, style or prompt following.

As many of you I've been experimenting with generative AI since the beginning and for me these are some of the highest fidelity images I've generated locally or have seen compared to closed source services.

**The main takeaway**: With the right balanced combination of prompts, settings and LoRAs, you can push Wan 2.1 images / still frames to higher resolutions with great coherence, high fidelity and details. A "lucky seed" still remains a factor of course.

---
## Workflow

Here I share my main [Wan 2.1 14B t2i workhorse workflow](https://github.com/masslevel/ComfyUI-Workflows/tree/main/Wan2.1) that also includes an extensive post-processing pipeline. It's definitely not made for everyone or is yet as complete or fine-tuned as many of the other well maintained community workflows.

![Workflow screenshot](https://i.imgur.com/yLia1jM.png)

The workflow is based on a component kind-of concept that I use for creating my ComfyUI workflows and may not be very beginner friendly. Although the idea behind it is to make things manageable and more clear how the signal flow works.

But in this experiment I focused on researching how far I can push image fidelity.

![simplified ComfyUI workflow screenshot](https://i.imgur.com/LJKkeRo.png)

I also created a [simplified workflow version](https://github.com/masslevel/ComfyUI-Workflows/tree/main/Wan2.1) using mostly ComfyUI native nodes and a minimal custom nodes setup that can create a basic image with some optimized settings without post-processing.

### masslevel Wan 2.1 14B t2i workflow downloads
[Download ComfyUI workflows here](https://github.com/masslevel/ComfyUI-Workflows/tree/main/Wan2.1) on GitHub

### Original full-size (4k) images with ComfyUI metadata
[Download here](https://drive.google.com/drive/folders/1KgaA9XEnMWK7HzEVYjujJLVOMkGybJ8v?usp=sharing) on Google Drive

**Note:** Please be aware that these images include different iterations of my ComfyUI workflows while I was experimenting. The latest released workflow version can be found on [GitHub](https://github.com/masslevel/ComfyUI-Workflows/tree/main/Wan2.1).

The Florence-2 group that is included in some workflows can be safely discarded / deleted. It's not necessary for this workflow. The Post-processing group contains a couple of custom node packages, but isn't mandatory for creating base images with this workflow.

### Workflow details and findings

**tl;dr: Creating high resolution and high fidelity images using Wan 2.1 14b + aggressive [NAG](https://chendaryen.github.io/NAG.github.io/) and sampler settings + LoRA combinations.**

I've been working on setting up and fine-tuning workflows for specific models, prompts and settings combinations for some time. This image creation process is very much a **balancing act** - like mixing colors or cooking a meal with several ingredients.

I try to reduce negative effects like artifacts and overcooked images using fine-tuned settings and post-processing, while pushing resolution and fidelity through image attention editing like NAG.

I'm not claiming that these images don't have issues - they have a lot. Some are on the brink of overcooking, would need better denoising or post-processing. These are just some results from trying out different setups based on my experiments using Wan 2.1 14b.

---

## Latent Space magic - or just me having no idea how any of this works.

![latent space intro image](https://i.imgur.com/DNealKy.jpeg)

I always try to push image fidelity and models above their recommended resolution specifications, **but without using tiled diffusion**, all models I tried before break down at some point or introduce artifacts and defects as you all know.

While FLUX.1 quickly introduces image artifacts when creating images outside of its specs, SDXL can do images above 2K resolution but the coherence makes almost all images unusable because the composition collapses.

But I always noticed the crisp, highly detailed textures and image fidelity potential that SDXL and fine-tunes of SDXL showed at 2K and higher resolutions. Especially when doing latent space upscaling.

Of course you can make high fidelity images with SDXL and FLUX.1 right now using a tiled upscaling workflow.

### But Wan 2.1 14B... (in my opinion)

- can be pushed to higher resolutions natively than other models for text-to-image (using specific settings), allows for greater image fidelity and better compositional coherence.
- definitely features very impressive world knowledge especially striking in reproduction of materials, textures, reflections, shadows and overall display of different lighting scenarios.

### Model biases and issues

The usual generative AI image model issues like wonky anatomy or object proportions, color banding, mushy textures and patterns etc. are still very much alive here - as well as the limitations of doing complex scenes.

Also text rendering is definitely not a strong point of Wan 2.1 14b - it's not great.

As with any generative image / video model - close-ups and portraits still look the best.

#### Wan 2.1 14b has biases like
- overly perfect teeth
- the left iris is enlarged in many images
- the right eye / eyelid protruded
- And there must be zippers on many types of clothing. Although they are the best and most detailed generated zippers I've ever seen.

These effects might get amplified by a combination of LoRAs. There are just a lot of parameters to play with.

This isn't stable nor works for every kind of scenario, but I haven't seen or generated images of this fidelity before.

**To be clear:** Nothing replaces a carefully crafted pipeline, manual retouching and in-painting no matter the model.

I'm just surprised by the details and resolution you can get in 1 pass out of Wan. Especially since it's a DiT model and FLUX.1 having different kind of image artifacts (the grid, compression artifacts).

Wan 2.1 14B images aren’t free of artifacts or noise, but I often find their fidelity and quality surprisingly strong.

---
## Some workflow notes

- Keep in mind that the images use a variety of different settings for resolution, sampling, LoRAs, NAG and more. Also as usual "seed luck" is still in play.
- All images have been created in 1 diffusion sampling pass using a high base resolution + post-processing pass.
- VRAM might be a limiting factor when trying to generate images in these high resolutions. I only worked on a 4090 with 24gb.
- **Current favorite sweet spot image resolutions for Wan 2.1 14B**
  - 2304x1296 (~16:9), ~60 sec per image using full pipeline (4090)
  - 2304x1536 (3:2), ~99 sec per image using full pipeline (4090)
  - Resolutions above these values produce a lot more content duplications
  - **Important note:** At least the LightX2V LoRA is needed to stabilize these resolutions. Also gen times vary depending on which LoRAs are being used.

---

- On some images I'm using high values with NAG (Normalized Attention Guidance) to increase coherence and details (like with PAG) and try to fix / recover some of the damaged "overcooked" images in the post-processing pass.
	- **Using KJNodes WanVideoNAG node**
		- default values
			- nag_scale: 11
			- nag_alpha: 0.25
			- nag_tau: 2.500
		- my optimized settings
			- nag_scale: 50
			- nag_alpha: 0.27
			- nag_tau: 3
		- my high settings
			- nag_scale: 80
			- nag_alpha: 0.3
			- nag_tau: 4

---

- **Sampler settings**
	- My buddy u/Clownshark_Batwing created the awesome [RES4LYF](https://github.com/ClownsharkBatwing/RES4LYF) custom node pack filled with high quality and advanced tools. The pack includes the infamous *ClownsharKSampler* and also adds advanced sampler and scheduler types to the native ComfyUI nodes. The following combination offers very high quality outputs on Wan 2.1 14b:
		- Sampler: res_2s
		- Scheduler: bong_tangent
		- Steps: 4 - 10 (depending on the setup)
	- I'm also getting good results with:
		- Sampler: euler
		- Scheduler: beta
		- steps: 8 - 20 (depending on the setup)

---

- Negative prompts can vary between images and have a strong effect depending on the NAG settings. Repetitive and excessive negative prompting and prompt weighting are on purpose and are still based on our findings using SD 1.5, SD 2.1 and SDXL.

### LoRAs
- The Wan 2.1 14B accelerator LoRA LightX2V helps to stabilize higher resolutions (above 2k), before coherence and image compositions break down / deteriorate.
- LoRAs strengths have to be fine-tuned to find a good balance between sampler, NAG settings and overall visual fidelity for quality outputs
- Minimal LoRA strength changes can enhance or reduce image details and sharpness
- Not all but some Wan 2.1 14B text-to-video LoRAs also work for text-to-image. For example you can use driftjohnson's [DJZ Tokyo Racing](https://civitai.com/models/1612738/djz-tokyo-racing-wan-14b?modelVersionId=1847195) LoRA to add a VHS and 1980s/1990s TV show look to your images. Very cool!
### Post-processing pipeline
The post-processing pipeline is used to push fidelity even further and trying to give images a more interesting "look" by applying upscaling, color correction, film grain etc.

Also part of this process is mitigating some of the image defects like overcooked images, burned highlights, crushed black levels etc.

The post-processing pipeline is configured differently for each prompt to work against image quality shortcomings or enhance the look to my personal tastes.
#### Example process
- Image generated in 2304x1296
- 2x upscale using a pixel upscale model to 4608x2592
- Image gets downsized to 3840x2160 (4K UHD)
- Post-processing FX like sharpening, lens effects, blur are applied
- Color correction and color grade including LUTs
- Finishing pass applying a vignette and film grain

**Note:** The post-processing pipeline uses a couple of custom nodes packages. You could also just bypass or completely delete the post-processing pipeline and still create great baseline images in my opinion. 

### The pipeline

#### ComfyUI and custom nodes
- Custom Nodes (mostly quality of life nodes)
	- Without the post-processing pipeline, the main workflow should work with these node packages:
	    - [Mikey Nodes](https://github.com/bash-j/mikey_nodes) expert and quality of life tools by my friend u/twistedgames
	    - [ComfyUI-GGUF](https://github.com/city96/ComfyUI-GGUF)
	    - [KJNodes](https://github.com/kijai/ComfyUI-KJNodes)
	    - [rgthree-comfy](https://github.com/rgthree/rgthree-comfy)
  - The simplified workflow only uses ComfyUI native nodes and the [ComfyUI-GGUF](https://github.com/city96/ComfyUI-GGUF) + [KJNodes](https://github.com/kijai/ComfyUI-KJNodes) nodes packages.

#### Models and other files

Of course you can use any Wan 2.1 (or variant like FusionX) and text encoder version that makes sense for your setup.

- Wan 2.1 using [wan2.1-t2v-14b-Q5_K_S.gguf or wan2.1-t2v-14b-Q8_0.gguf](https://huggingface.co/city96/Wan2.1-T2V-14B-gguf/tree/main) (city96)
- Text encoder [umt5-xxl-encoder-Q5_K_S.gguf or umt5-xxl-encoder-Q8_0.gguf](https://huggingface.co/city96/umt5-xxl-encoder-gguf/tree/main) (city96)
- Using WanVideoNAG like PAG (Perturbed Attention) to boost coherence and details. The node is part of the essential [KJNodes](https://github.com/kijai/ComfyUI-KJNodes) ComfyUI node package by Kijai
- Basic LoRAs
  - [LightX2V](https://huggingface.co/Kijai/WanVideo_comfy/resolve/main/Wan21_T2V_14B_lightx2v_cfg_step_distill_lora_rank32.safetensors) (Kijai)
  - [LightX2V v2 rank128](https://huggingface.co/Kijai/WanVideo_comfy/resolve/main/Lightx2v/lightx2v_T2V_14B_cfg_step_distill_v2_lora_rank128_bf16.safetensors?download=true) (Kijai)
  - [LightX2V v2 rank64](https://huggingface.co/Kijai/WanVideo_comfy/resolve/main/Lightx2v/lightx2v_T2V_14B_cfg_step_distill_v2_lora_rank64_bf16.safetensors?download=true) (Kijai)
  - [Phantom FusionX](https://huggingface.co/vrgamedevgirl84/Wan14BT2VFusioniX/resolve/main/FusionX_LoRa/Phantom_Wan_14B_FusionX_LoRA.safetensors?download=true) (vrgamedevgirl84)
  - [Wan FusionX Face Naturalizer](https://civitai.com/models/1755105/wanfusionxfacenaturalizer) (vrgamedevgirl84) - This LoRA enhances faces (and other details) when applying the Phantom FusionX LoRA.
- Pixel upscaling model: [SwinIR-M-x2 (classicalSR-DF2K-s64w8)](https://openmodeldb.info/models/2x-classicalSR-DF2K-s64w8-SwinIR-M) - My personal favorite because it doesn't introduce artifacts or over-sharpening in my opinion.

I also use other LoRAs in some of the images. For example:

- [Smartphone Snapshot PRS](https://civitai.com/models/1763826/wan21-smartphone-snapshot-photo-reality-style?modelVersionId=1996092) - a very cool LoRA by u/AI_Characters who created many more LoRAs for Wan 2.1 14B that work great for t2i.
- [vrgamedevgirl84 LoRAs](https://huggingface.co/vrgamedevgirl84/Wan14BT2VFusioniX/tree/main/OtherLoRa's)
- [DJZ Tokyo Racing](https://civitai.com/models/1612738/djz-tokyo-racing-wan-14b?modelVersionId=1847195) by riftjohnson
- There are also the [MoviiGen](https://huggingface.co/Kijai/WanVideo_comfy/resolve/main/Wan21_T2V_14B_MoviiGen_lora_rank32_fp16.safetensors) and [Wan 2.1 Fun-Reward LoRAs](https://huggingface.co/alibaba-pai/Wan2.1-Fun-Reward-LoRAs/tree/main) but I haven't experimented with those a lot yet. When used moderately they seem to improve coherence and details.
- I also use acceleration methods like Sage Attention / Triton but these aren't a requirement. They just speed up the workflow.

---
## Prompting

I'm still exploring the latent space of Wan 2.1 14B. I went through my huge library of over 4 years of creating AI images and tried out prompts that Wan 2.1 + LoRAs respond to and added some wildcards.

I also wrote prompts from scratch or used LLMs to create more complex versions of some ideas.

From my first experiments base Wan 2.1 14B definitely has the biggest focus on realism (naturally as a video model) but LoRAs can expand its style capabilities. You can however create interesting vibes and moods using more complex natural language descriptions.

But it's too early for me to say how flexible and versatile the model really is. A couple of times I thought I hit a wall but it keeps surprising me.

Next I want to do more prompt engineering and further learn how to better "communicate" with Wan 2.1 - or soon Wan 2.2.

---
## Outro

As said - please let me know if you have any questions.

It's a once in a lifetime ride and I really enjoy seeing everyone of you creating and sharing content, tools, posts, asking questions and pushing this thing further.

Thank you all so much, have fun and keep creating!

*End of Line*
