# Kandinsky 2.1 For Automatic1111 Extension
Adds a script that runs the Kandinsky 2.1 model.

## Disclaimer

ALPHA VERSION NOT PRODUCTION-READY

## Examples
The following are non cherry-picked examples, with various settings and resolutions.

<p align="center">
   <img src="https://github.com/MMqd/kandinsky-for-automatic1111/blob/main/images/sky,%20daylight,%20realistic,%20high%20quality,%20in%20focus,%2016k,%20HQ.jpg?raw=true" width="25%" alt="center image" />
</p>
<strong>Prompt: sky, daylight, realistic, high quality, in focus, 16k, HQ</strong><br>
Steps: 64<br>
Sampler: Default<br>
CFG scale: 7<br>
Seed: 3479955<br>
Size: 1024x1024<br>
Inference Steps: 128<br>
<br>

<p align="center">
   <img src="https://github.com/MMqd/kandinsky-for-automatic1111/blob/main/images/As%20the%20sun%20sets,%20les%20arbres%20whisper,%20mientras%20el%20río%20serpentea%20gracefully,%20отражая%20прекрасные%20colors,%20majestic%20mountains%20stand%20t.jpg?raw=true" width="25%" alt="center image" />
</p>
<strong>Prompt: As the sun sets, les arbres whisper, mientras el río serpentea gracefully, отражая прекрасные colors, majestic mountains stand tall, evoking tranquillité et harmonie, 空中舞动着美丽的蝴蝶, 空と地球の神秘なつながり, रंगबिरंगी वस्तुएं।</strong> (from chatgpt)<br>
In English: As the sun sets, the trees whisper, while the river gracefully meanders, reflecting beautiful colors, majestic mountains stand tall, evoking tranquility and harmony, butterflies dance in the air, the mysterious connection between sky and earth, colorful objects.<br>
Steps: 64<br>
Sampler: Default<br>
CFG scale: 7<br>
Seed: 3479955<br>
Size: 768x768<br>
Inference Steps: 128<br>
<br>

<p align="center">
   <img src="https://github.com/MMqd/kandinsky-for-automatic1111/blob/main/images/cat,%20realistic,%20high%20quality,%204k.jpg?raw=true" width="25%" alt="center image" />
</p>
<strong>Prompt: cat, realistic, high quality, 4k</strong><br>
Steps: 64<br>
Sampler: Default<br>
CFG scale: 7<br>
Seed: 3479955<br>
Size: 1024x1024<br>
Inference Steps: 128<br>


<p align="center">
   <img src="https://github.com/MMqd/kandinsky-for-automatic1111/blob/main/images/spaceship,%20retro,%20realistic,%20high%20quality,%204k.jpg?raw=true" width="25%" alt="center image" />
</p>
<strong>Prompt: spaceship, retro, realistic, high quality, 4k</strong><br>
Steps: 64<br>
Sampler: Default<br>
CFG scale: 7<br>
Seed: 3479955<br>
Size: 512x512<br>
Inference Steps: 128<br>
<br>

<p align="center">
   <img src="https://github.com/MMqd/kandinsky-for-automatic1111/blob/main/images/cyberpunk%20city,%20distopian,%20high%20quality,%204k.jpg?raw=true" width="25%" alt="center image" />
</p>
<strong>Prompt: cyberpunk city, distopian, high quality, 4k</strong><br>
Steps: 64<br>
Sampler: Default<br>
CFG scale: 3<br>
Seed: 3479955<br>
Size: 768x768<br>
Inference Steps: 128<br>

### Image Mixing
Combine images and/or prompts together. Can be used for style transfer, and combining a background with a subject.

<strong>Prompt: cat, high quality, 4k</strong><br>
Steps: 64<br>
Sampler: Default<br>
CFG scale: 7<br>
Seed: 3479955494<br>
Size: 1536x768<br>
Inference Steps: 128<br>

Mixed with:

<p align="center">
   <img src="https://github.com/MMqd/kandinsky-for-automatic1111/blob/main/images/sky,%20daylight,%20realistic,%20RAW%20photograph,%20high%20quality,%20in%20focus,%2016k,%20HQ.jpg?raw=true" width="25%" alt="center image" />
</p>

Result:
<p align="center">
   <img src="https://github.com/MMqd/kandinsky-for-automatic1111/blob/main/images/cat,%20high%20quality,%204k.jpg?raw=true" width="25%" alt="center image" />
</p>

## How To Use
1. Select "Kandinsky" in the scripts section
2. Set "Prior Inference Steps". Increasing the value improves the results, but it reaches a plateau at around 128. Beyond that, the image may change, but the quality remains consistent.

### Image Mixing
#### Prompt + Image
1. In text2img set the prompt
2. In the extra image field in the script section, set the image
3. Set the "Interpolate Image 1 Strength" to the desired amount of image generated by the prompt
4. Set the "Interpolate Image 2 Strength" to the desired amount of image in the script section

#### Image + Image
1. In img2img set an image
2. In the extra image field in the script section, set the image
3. Set the "Interpolate Image 1 Strength" to the desired amount of image generated by the prompt
4. Set the "Interpolate Image 2 Strength" to the desired amount of image in the script section

## Notes
* Prompt size is 512 tokens
* Seeds are somewhat consistent across different resolutions
* Changing sampling steps keeps the same image, while changing quality
* The seed is not as important as the prompt, the subjects/compositions across seeds are very similar
* It is very easy to "overcook" images with prompts, if this happens remove keywords or reduce CFG scale
    * Negative prompts aren't needed, so "low quality, bad quality..." can be ommited
    * Short positive prompts are good, too many keywords confuse the ai

## Features
* Text to image
* Batching
* Img2img
* Inpainting
* Image mixing
* vram optimizations (16 bit float and attention slicing)

## Supported Settings
* prompt
* negative prompt
* cfg scale
* seed
* width
* height
* sampling steps
* denoising strength
* batch count
* batch size (only first image's seed can be replicated)
* img2img image, and inpaint
* inpaint at full resolution (needs fixing)

Any other setting such as seed variations, will have no effect on generated images.

## Known Bugs
* Ram memory leak (still investigating)

## Limitations
* Uses the Hugging Face image generation pipeline to run Kandinsky (Only "kandinsky-community/kandinsky-2-1" is supported on Hugging Face, so no custom models)
* No controlnet
* No training
* No support for other extensions like ultimate-upscale, tiled diffusion, etc.
* No progress bar in GUI
* No choice for samplers
* Stable diffusion model and vae are not unloaded from ram, resulting in ~15gb ram usage
* Not possible to replicate seed in batches
* Strength of words in the prompt can't be set
* Other automatic1111 features such as seed variations, hires fix, tiling, etc. are not supported
* Can't be run with other automatic1111 scripts