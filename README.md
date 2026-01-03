# Linux-CUDA-Lllama.cpp-guide
Step-by-step guide for installing dual-boot Linux Mint Cinnamon on an existing Windows PC, along with installing and configuring Lllama.CPP with CUDA

The following guide shows how to create a dual-boot Windows 10 or 11 and Linux Mint Cinnamon installation. In addition, a full guide to installing Nvidia and CUDA drivers is included. Finally, a complete guide to installing and configuring Lllama.cpp, along with suggested models and settings is provided.
The following equipment was used for this guide:
- Intel Core Ultra 7 265K CPU
- Gigabyte Aorus Elite WiFi 7 motherboard
- 96GB DDR5 6800 RAM
- Nvidia 3090 FE GPU
- Two M.2 NVMe SSD drives

To begin, make sure to back up all your important information, along with creating a Windows recovery drive:
[MS Recovery Drive Instructions] (https://support.microsoft.com/en-us/windows/recovery-drive-abb4691b-5324-6d4a-8766-73fab304c246)

Next, you will need to create a new partition on your existing boot drive. This is done by 'shrinking' the existing C: drive. 
A good size to start is 60-80GB for the Linux disk. However, if you plan to store LLM model files on the Linux partition, you should consider making it 250 - 500 GB if possible. 
This guide will also show how to access model files on other hard disks in the PC.

Running the Disk Management program (type diskmgmt into the Windows search box):

<img width="386" height="351" alt="1-diskmgmt" src="https://github.com/user-attachments/assets/e8afd4fc-5acc-40aa-bfb7-73e5ca0d501b" />

Next, choose your main boot drive, right click on it, then pick the Shrink Volume option:

<img width="425" height="326" alt="3-diskmgmt" src="https://github.com/user-attachments/assets/271c33eb-a289-405b-9500-4b691763b19e" />


