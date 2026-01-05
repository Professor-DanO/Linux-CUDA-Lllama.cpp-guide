# Linux-CUDA-Lllama.cpp-guide
Welcome to this step-by-step primer for installing dual-boot Linux on an existing Windows PC, along with installing and configuring Lllama.CPP with CUDA!

This guide shows how to create a dual-boot Windows 10 or 11 and Linux Mint Cinnamon system, along with installing Nvidia and CUDA drivers. Complete instructions for installing and configuring Lllama.cpp, along with suggested models and settings, is provided. A comprehensive set of benchmark results using several different models is also included. This manual was also tested and works well with a standalone Mint Linux install, along with other Nvidia GPUS and multiple Nvidia GPUs (e.g., RTX 3090 and 4070 in the same PC).

The following equipment was used:
- Intel Core Ultra 7 265K CPU
- Gigabyte Aorus Elite WiFi 7 motherboard (Intel 200S overclocking and XMP memory profile enabled)
- 96GB DDR5 6800 RAM
- Nvidia 3090 FE GPU
- Two M.2 NVMe SSD drives

# Preparations
To begin, make sure to back up all your important information, along with creating a Windows recovery drive if needed:

[MS Recovery Drive Instructions](https://support.microsoft.com/en-us/windows/recovery-drive-abb4691b-5324-6d4a-8766-73fab304c246)

It is also helpful to have a Windows 10 or 11 bootable installation USB Flash Drive, especially if you want to remove the Linux system and boot loader later on:

[Create installation media for Windows](https://support.microsoft.com/en-us/windows/create-installation-media-for-windows-99a58364-8c02-206f-aa6f-40c3b507420d)

# Creating the new disk partition for Linux

Create a new partition on your existing boot (C:) drive. This is done by 'shrinking' the existing C: drive. 

A good size to start is 60-80GB for the Linux disk. However, if you plan to store LLM model files on the Linux partition, you should consider making it 250 - 500 GB if possible. 
This guide will also show how to access model files on other hard disks in the PC.

### Running the Disk Management program (type diskmgmt into the Windows search box):

<img width="386" height="351" alt="1-diskmgmt" src="https://github.com/user-attachments/assets/e8afd4fc-5acc-40aa-bfb7-73e5ca0d501b" />


Next, choose your main boot drive, right click on the C: volume, then pick the Shrink Volume option:

<img width="425" height="326" alt="3-diskmgmt" src="https://github.com/user-attachments/assets/271c33eb-a289-405b-9500-4b691763b19e" />


Now, choose how large a new partition should be created for the Linux install. In this case I picked 250,000 MB, which is 250 GB:

<img width="629" height="286" alt="4-diskmgmt" src="https://github.com/user-attachments/assets/6792282d-9ed4-4311-a4db-862ed1f934b4" />


That is all you need for the Windows PC. From now on, the rest of the guide will focus on installing and configuring Mint Cinnamon Linux and Llama.cpp!

# Downloading and installing Linux Mint

### Download the Mint Cinammon Linux ISO install file:

[Linux Mint 22.2 "Zara" Cinnamon Edition](https://www.linuxmint.com/edition.php?id=322)

<img width="783" height="495" alt="7-mint" src="https://github.com/user-attachments/assets/113861cd-1fea-41fa-ab67-4399231c8e04" />

### Create a bootable USB flash drive (8GB or larger). I recommend using Rufus to create the bootable drive:

[Rufus Download](https://rufus.ie/en/#download)

### Run Rufus, then select the Mint ISO file that you downloaded, then click Start:

<img width="347" height="437" alt="9-mint" src="https://github.com/user-attachments/assets/1e0229af-b875-4420-86db-01920b9ed804" />

### Reboot your computer, then press the appropriate key to enter the boot device selection menu (typically F12), and choose the USB flash drive.
Apologies for the potato quality phone photos in this section.

<img width="450" height="200" alt="IMG_4427" src="https://github.com/user-attachments/assets/4bda77f4-a312-454c-91e7-e53cdfb5f983" />

Once Mint boots, choose the top selection:

<img width="400" height="170" alt="IMG_4428" src="https://github.com/user-attachments/assets/592e292a-16a7-417f-9da0-78091d96c9d5" />

### Click on the Install Mint icon in the upper-left corner:

<img width="320" height="125" alt="IMG_4429" src="https://github.com/user-attachments/assets/c3c96a84-8df9-4b35-b3af-3451e86fe13d" />

Go through the standard OS installation routine and create a username and password along with choosing some settings:

<img width="354" height="214" alt="IMG_4430" src="https://github.com/user-attachments/assets/60a13cb8-569c-4cb2-aedf-7182929acba9" />

Here is the important bit- Mint will detect the partition you made on the C: drive and use it properly if you choose these options (your partition number may vary):

<img width="486" height="226" alt="IMG_4431" src="https://github.com/user-attachments/assets/cf0b6328-e923-4240-8693-8a0052c2d447" />

<img width="486" height="226" alt="IMG_4432" src="https://github.com/user-attachments/assets/7df982af-3724-432c-b272-8671324e80b8" />

### Once the installation finished, remove the USB flash drive then press enter to reboot:

<img width="403" height="125" alt="IMG_4434" src="https://github.com/user-attachments/assets/60026171-3f9d-4073-8b33-ef0e2c57f6f0" />

Your computer will now reboot into the Grub boot loader, which provides options for booting into Mint or Windows:

<img width="425" height="95" alt="IMG_4435" src="https://github.com/user-attachments/assets/cf713164-9a0a-46ee-ab66-81414c858e43" />

# Getting Mint Linux ready to go- Updating, software settings, and security

You will be greeted with the following screen when logging in for the first time, and there are some important steps to take within its menu system:

<img width="399" height="272" alt="21-mint" src="https://github.com/user-attachments/assets/3230f12d-ae87-4943-90eb-25c19eeb2955" />

### Start with some Nvidia driver updates- this guide uses the recommended Nvidia 580 open set of graphics drivers:

<img width="398" height="273" alt="22-Mint" src="https://github.com/user-attachments/assets/b88c6b52-64cc-4d1b-9a93-8fe92aa70799" />
<img width="395" height="273" alt="23-Mint" src="https://github.com/user-attachments/assets/9aceb116-236e-46eb-8fd7-941633d9fc03" />


### Set up Firewall Security by clicking the Status button so it is enabled:
<img width="492" height="275" alt="24-Mint" src="https://github.com/user-attachments/assets/e0e86605-3e5e-4381-8afd-44c2c6b5d682" />

### Update the system files and apps:

<img width="612" height="300" alt="25-Mint" src="https://github.com/user-attachments/assets/860584bb-66d5-427e-89cd-66acecadc162" />
<img width="774" height="300" alt="26-Mint" src="https://github.com/user-attachments/assets/c3fdceb3-9f80-4547-9809-0bb25b54a60c" />


Under Power Management, I chose the Performance setting:

<img width="716" height="327" alt="30-Mint" src="https://github.com/user-attachments/assets/f2b95107-4d88-4c8e-a8ed-a1cb6d27cc9e" />


I also enabled automatic backups with the snapshot settings:

<img width="614" height="332" alt="32-Mint" src="https://github.com/user-attachments/assets/ebdd940f-5648-459e-92f3-f5f33b7ebbe7" />


# Downloading and Installing CUDA

While several guides and software suites are available, I found that Nvidia's CUDA 13.1 toolkit software and guide instructions worked well (after manually adding the paths in bash.rc.) Start by choosing the correct package- Linux, x86_64, Ubuntu, 24.04. I used the deb (network) installer commands, but any of them work fine:

(https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=24.04)

<img width="664" height="329" alt="33-CUDA" src="https://github.com/user-attachments/assets/cc01b949-f1ac-4b9c-9783-f14f28ad81b3" />

You will now see a set of commands to use in the terminal:

<img width="506" height="164" alt="34-CUDA" src="https://github.com/user-attachments/assets/d9e0bf6d-a4a6-4ae2-ae3c-1735423ffa61" />

### Installation Instructions from the command line in a terminal window:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-keyring_1.1-1_all.deb

sudo dpkg -i cuda-keyring_1.1-1_all.deb

sudo apt-get update

sudo apt-get -y install cuda-toolkit-13-1
```

After the installation is complete, you will need to open bash.rc with a text editor and add the CUDA Toolkit path information. I used the Nano editor, and to save the file use CTRL-X, then Enter, then Enter.

### nano ~/.bash.rc

```
export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}

export LD_LIBRARY_PATH=/usr/local/cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
<img width="359" height="125" alt="37-CUDA" src="https://github.com/user-attachments/assets/221b059a-9a5a-434e-9341-a384cd410a56" />

Close the terminal window, then open a new terminal window for the new path to take effect. You should be able to test the installation with nvcc --version as seen below:

<img width="217" height="67" alt="39-CUDA" src="https://github.com/user-attachments/assets/dbfd5631-a0f5-4c87-957f-dbd67bbb02ec" />


# Installing and configuring Llama.cpp

The following guide is mostly taken from the ggml-org Github repository, along with some additional information to get it all working properly with CUDA. Make sure you are in your working home directory (pwd).
[Llama.cpp repository page for reference](https://github.com/ggml-org/llama.cpp)

### Install Git:
```
sudo apt install git
```
### Clone the repo:
```
git clone https://github.com/ggml-org/llama.cpp
```
Change the directory
```
cd llama.cpp
```
### Install cmake:
```
sudo apt install cmake
```
### Install the necessary development libraries (to prevent the CURL not found error later):
```
sudo apt install libcurl4-openssl-dev libssl-dev
```
### Build llama.cpp part 1:
```
cmake -B build -DGGML_CUDA=ON -DBUILD_SHARED_LIBS=OFF -DLLAMA_CURL=ON -DGGML_CUDA_FA_ALL_QUANTS=ON
```
### Build llama.cpp part 2 (takes a while):
```
cmake --build build --config Release -j --clean-first
```
<img width="508" height="320" alt="41-llamacpp" src="https://github.com/user-attachments/assets/f3574667-73ac-4888-8a41-dfb2fbe1c7ec" />


### Edit the bash.rc file again to add the llama.cpp path. Add the following two lines and a commented description if you like:
```
export LLAMACPP=/home/dano/llama.cpp

export PATH=$LLAMACPP/build/bin:$PATH
```
Exit the current terminal window and start a new terminal window for the path settings to take effect.

You are all done with the installations and configurations- congratulations! It is now time to start working with model inference.

# Choosing and Downloading Model Files

I recommend that you download a small model to begin. A great place to get started is the unsloth repository collection on HuggingFace:

[Unsloth Qwen3-4B-Instruct-2507](https://huggingface.co/unsloth/Qwen3-4B-Instruct-2507-GGUF)

### Here is the direct link to the Q6 model download:

(https://huggingface.co/unsloth/Qwen3-4B-Instruct-2507-GGUF/blob/main/Qwen3-4B-Instruct-2507-UD-Q6_K_XL.gguf)

You should also check out the Best Practices page for the model, which will give you important information about proper settings:

(https://unsloth.ai/docs/models/qwen3-how-to-run-and-fine-tune/qwen3-2507)

For this model, the following are recommended, and we'll see how to set up llama.cpp with this shortly:

### Instruct Model Settings:

Temperature = 0.7

Min_P = 0.00 (llama.cpp's default is 0.1)

Top_P = 0.80

TopK = 20

Once you've downloaded the model, it should be in the following directory (YMMV):

/home/dano/Downloads/Qwen3-4B-Instruct-2507-UD-Q6_K_XL.gguf

# Starting up Llama-server and running your first inference

Use the command line interface to start the llama-server program. There are many settings that can be adjusted, and most of them will be covered here.

### Start a terminal window, then (assuming your model file is in the Downloads folder), enter the following:
```
llama-server --model Downloads/Qwen3-4B-Instruct-2507-UD-Q6_K_XL.gguf --port 8080 -fit on --jinja --temp 0.7 --top-p 0.8 --top-k 20 --min-p 0.0 --threads -1 --no-mmap --flash-attn 1 --ctx-size 32768
```
If everything works correctly, you should see a link to http://127.0.0.1:8080 on the screen. Start your Firefox web browser, enter that addresses, and you should see the Chat Window open!

<img width="634" height="527" alt="48-llamacpp" src="https://github.com/user-attachments/assets/f39cf97a-a4d1-4b55-9418-1db457f6cf5e" />

### Quantize the KV cache to 8bits to use less RAM and hopefully speed things up:
```
llama-server --model Downloads/Qwen3-4B-Instruct-2507-UD-Q6_K_XL.gguf --port 8080 -fit on --jinja --temp 0.7 --top-p 0.8 --top-k 20 --min-p 0.0 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 32768
```
# Benchmark results with RTX 3090 FE and 96GB of DDR5 6800 RAM:
Each test was run three times, with the average of the three token generation times provided for each model. Unless otherwise specified, the context size was 8192 and kv caches were q8_0. The prompt was:

Write a Flappy Bird game program in Java.


| Model  | Performance |
| ------------- | ------------- |
| Qwen3-4B-Instruct-2507-UD-Q6_K_XL L  | 125.5 t/s  |
| Qwen3-Next-80B-A3B-Instruct-UD-Q4_K_XL  | 44.6 t/s  |
| Qwen3-Next-80B-A3B-Instruct-UD-Q6_K_XL  | 33.7 t/s |
| GPT-OSS-120b-UD-Q4_K_XL  | 34.5 t/s   |
| GPT-OSS-20b-MXFP4  | 170 t/s  |
| MiniMax-M2.1-UD-Q3_K_XL  | 20 t/s  |
| GLM-4.5-Air-UD-Q4_K_XL  | 20.2 t/s  |
| Qwen3-VL-32B-Instruct-UD-Q4_K_XL  | 35.5 t/s  |
| Devstral-Small-2-24B-Instruct-2512-UD-Q6_K_XL  | 38.4 t/s  |



### Qwen3-Next-80B-A3B-Instruct-UD-Q4_K_XL- 44.6 t/s
```
llama-server --model Qwen3-Next-80B-A3B-Instruct-UD-Q4_K_XL.gguf --port 8080 -fit on --jinja --temp 0.7 --top-p 0.8 --top-k 20 --min-p 0.0 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 8192
```

### Larger quant version of Qwen3-Next-80B-A3B-Instruct-UD-Q6_K_XL - 33.7 t/s

Note the new settings for different hard drive location (/media/dano/models/LLM-Models/QWEN3-MOE/..) and split, two-part model files (..00001-of-00002.gguf): 
```
llama-server --model /media/dano/models/LLM-Models/QWEN3-MOE/Qwen3-Next-80B-A3B-Instruct-UD-Q6_K_XL-GGUF/Qwen3-Next-80B-A3B-Instruct-UD-Q6_K_XL-00001-of-00002.gguf --port 8080 -fit on --jinja --temp 0.7 --top-p 0.8 --top-k 20 --min-p 0.0 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 4096
```

### GPT-OSS-120b-UD-Q4_K_XL - 34.5 t/s 
```
llama-server --model gpt-oss-120b-UD-Q4_K_XL-00001-of-00002.gguf --port 8080 -fit on --jinja --temp 1.0 --top-p 1.0 --top-k 0.0 --min-p 0.0 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 8192
```

### GPT-OSS-20b MXFP4- 170 t/s
```
llama-server --model /media/dano/models/LLM-Models/GPT-OSS/gpt-oss-20b-GGUF/gpt-oss-20b-MXFP4.gguf --port 8080 -fit on --jinja --temp 1.0 --top-p 1.0 --top-k 0.0 --min-p 0.0 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 8192
```

### Long context- 60K text prompt, 66K context- Qwen3-Next-80B-A3B-Instruct-UD-Q4_K_XL- prompt processing 675 t/s, token generation 38 t/s
```
llama-server --model Qwen3-Next-80B-A3B-Instruct-UD-Q4_K_XL.gguf --port 8080 -fit on --jinja --temp 0.7 --top-p 0.8 --top-k 20 --min-p 0.0 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 66000
```

### Very long context- 205K text prompt, 260K context- Qwen3-Next-80B-A3B-Instruct-UD-Q4_K_XL- prompt processing 585 t/s, token generation 26 t/s
```
llama-server --model Qwen3-Next-80B-A3B-Instruct-UD-Q4_K_XL.gguf --port 8080 -fit on --jinja --temp 0.7 --top-p 0.8 --top-k 20 --min-p 0.0 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 66000
```

### Large Model test - MiniMax-M2.1- (about the largest I could fit with room for some decent context and kv cache ~ 102GB) - 20 t/s
```
llama-server --model /media/dano/models/LLM-Models/MiniMax-M2.1/MiniMax-M2.1-UD-Q3_K_XL-00001-of-00003.gguf --port 8080 -fit on --jinja --temp 1.0 --top-p 0.95 --top-k 40 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 8192
```
System prompt: You are a helpful assistant. Your name is MiniMax-M2.1 and is built by MiniMax.

### Another large model - GLM-4.5-Air-UD-Q4_K_XL (~64GB)- 20.2 t/s
```
llama-server --model /media/dano/models/llamacpp-models/GLM-4.5-Air-UD-Q4_K_XL-00001-of-00002.gguf --port 8080  -fit on --jinja --temp 0.8 --top-p 0.6 --top-k 2 --repeat-penalty 1.1 --min-p 0.0 --seed 3407 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 8192
```

### Dense model testing:
Qwen3-VL-32B-Instruct-UD-Q4_K_XL.gguf - 35.5 t/s
```
llama-server --model Qwen3-VL-32B-Instruct-UD-Q4_K_XL.gguf --port 8080 -fit on --jinja --temp 0.7 --top-p 0.8 --top-k 20 --min-p 0.0 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q4_0 --cache-type-v q4_0 --ctx-size 8192
```
Devstral-Small-2-24B-Instruct-2512-UD-Q6_K_XL.gguf (note the use of a second hard drive- simply copy and paste the name of the file using the Linux file system GUI) - 38.4 t/s
```
llama-server --model /media/dano/models/LLM-Models/Mistral/Devstral-Small-2-24B-Instruct-2512-UD-Q6_K_XL-GGUF/Devstral-Small-2-24B-Instruct-2512-UD-Q6_K_XL.gguf --port 8080 -fit on --jinja --temp 0.15 --min-p 0.01 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 8192
```

### Testing performace of the new '-fit on' flag in llama.cpp versus other methods:

-fit on - 44.6 t/s
```
llama-server --model Qwen3-Next-80B-A3B-Instruct-UD-Q4_K_XL.gguf --port 8080 -fit on --jinja --temp 0.7 --top-p 0.8 --top-k 20 --min-p 0.0 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 8192
```
-ot ".ffn_.*_exps.=CPU" - 34 t/s
```
llama-server --model Qwen3-Next-80B-A3B-Instruct-UD-Q4_K_XL.gguf --port 8080 -ot ".ffn_.*_exps.=CPU" --jinja --temp 0.7 --top-p 0.8 --top-k 20 --min-p 0.0 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 8192
```
-ot ".ffn_(up|down)_exps.=CPU" - 40.25 t/s
```
llama-server --model Qwen3-Next-80B-A3B-Instruct-UD-Q4_K_XL.gguf --port 8080 -ot ".ffn_(up|down)_exps.=CPU" --jinja --temp 0.7 --top-p 0.8 --top-k 20 --min-p 0.0 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 8192
```
Manual setting- --n-cpu-moe 24 -ngl 99 - 44.6 t/s
```
llama-server --model Qwen3-Next-80B-A3B-Instruct-UD-Q4_K_XL.gguf --port 8080 --n-cpu-moe 24 -ngl 99 --jinja --temp 0.7 --top-p 0.8 --top-k 20 --min-p 0.0 --threads -1 --no-mmap --flash-attn 1 --cache-type-k q8_0 --cache-type-v q8_0 --ctx-size 8192
```












































