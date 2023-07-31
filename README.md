# prompt-generator-comfyui
Custom prompt generator node for ComfyUI

# Table Of Contents
- [Setup](#setup)
- [Features](#features)
- [Example Workflow](#example-workflow)
- [Variables](#variables)
  - [How Recursive Works?](#how-recursive-works)
  - [How Preprocess Mode Works?](#how-preprocess-mode-works)
- [Example Outputs](#example-outputs)

# Setup
- Clone the repository with ```https://github.com/alpertunga-bile/prompt-generator-comfyui.git``` command under ```custom_nodes``` folder.
- Put your generator under ```prompt_generators``` folder. You can create your prompt generator with [this repository](https://github.com/alpertunga-bile/prompt-markdown-parser). You have to put generator as folder. Do not just put ```pytorch_model.bin``` file for example.
- Run the ComfyUI
- Open the ```hires.fixWithPromptGenerator.json``` workflow

# Features
- Print generated text to terminal and log the node's state under  ```generated_prompts``` folder with date as filename.

# Example Workflow
![example_workflow](https://github.com/alpertunga-bile/prompt-generator-comfyui/assets/76731692/f50652a9-8751-41f3-81cf-d4cb61dd8a34)
- **Prompt Generator Node** may look different with final version but workflow is not going to change

# Variables
- For ```model_type``` variable copy and paste the model's name from [this site](https://huggingface.co/models?pipeline_tag=text-generation) like this ```tiiuae/falcon-40b```
- You can get information about variables from [this](https://happytransformer.com/text-generation/settings/) link

## How Recursive Works?
- Let's say we give ```a, ``` as seed and recursive level is 1. I am going to use the same outputs for this example to understand the functionality more accurately.
- With self recursive, let's say generator's output is ```b```. So next seed is going to be ```b``` and generator's output is ```c```. Final output is ```a, c```. It can be used for generating random outputs.
- Without self recursive, let's say generator's output is ```b```. So next seed is going to be ```a, b``` and generator's output is ```c```. Final output is ```a, b, c```. It can be used for more accurate prompts.

## How Preprocess Mode Works?
- **exact_keyword** => ```(masterpiece), ((masterpiece))``` is not allowed. Checking the pure keyword without parantheses and weights. Adding prompts from the beginning of the generated text so add important prompts to seed.
- **exact_prompt** => ```(masterpiece), ((masterpiece))``` is allowed but ```(masterpiece), (masterpiece)``` is not. Checking the exact match of the prompt.
- **none** => Everything is allowed even the repeated prompts.

# Example Outputs
![ComfyUI_00062_](https://github.com/alpertunga-bile/prompt-generator-comfyui/assets/76731692/82522192-b486-4703-86e2-18aff79fe29b)
![ComfyUI_00054_](https://github.com/alpertunga-bile/prompt-generator-comfyui/assets/76731692/906c9c1d-d8b5-4aa7-89cc-6a1918eac454)
![ComfyUI_00048_](https://github.com/alpertunga-bile/prompt-generator-comfyui/assets/76731692/e559c843-8e4c-4f45-9a39-c7f457218467)
