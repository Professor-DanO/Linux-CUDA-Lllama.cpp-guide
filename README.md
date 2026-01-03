# Linux-CUDA-Lllama.cpp-guide
Step-by-step guide for installing dual-boot Linux Mint Cinnamon on an existing Windows PC, along with installing and configuring Lllama.CPP with CUDA

The following guide shows how to create a dual-boot Windows 10 or 11 and Linux Mint Cinnamon installation. In addition, a full guide to installing Nvidia and CUDA drivers is included. Finally, a complete guide to installing and configuring Lllama.cpp, along with suggested models and settings is provided. These instructions also work well with other Nvidia GPUS and multiple Nvidia GPUs (tested with an RTX 3090 and 4070).

The following equipment was used for this guide:
- Intel Core Ultra 7 265K CPU
- Gigabyte Aorus Elite WiFi 7 motherboard
- 96GB DDR5 6800 RAM
- Nvidia 3090 FE GPU
- Two M.2 NVMe SSD drives

To begin, make sure to back up all your important information, along with creating a Windows recovery drive:

[MS Recovery Drive Instructions] (https://support.microsoft.com/en-us/windows/recovery-drive-abb4691b-5324-6d4a-8766-73fab304c246)

Next, you will need to create a new partition on your existing boot (C:) drive. This is done by 'shrinking' the existing C: drive. 
A good size to start is 60-80GB for the Linux disk. However, if you plan to store LLM model files on the Linux partition, you should consider making it 250 - 500 GB if possible. 
This guide will also show how to access model files on other hard disks in the PC.

Running the Disk Management program (type diskmgmt into the Windows search box):

<img width="386" height="351" alt="1-diskmgmt" src="https://github.com/user-attachments/assets/e8afd4fc-5acc-40aa-bfb7-73e5ca0d501b" />

Next, choose your main boot drive, right click on the C: volume, then pick the Shrink Volume option:

<img width="425" height="326" alt="3-diskmgmt" src="https://github.com/user-attachments/assets/271c33eb-a289-405b-9500-4b691763b19e" />

Next, choose how large a new partition should be created for the Linux install. In this case I picked 250,000 MB, which is 250 GB:

<img width="629" height="286" alt="4-diskmgmt" src="https://github.com/user-attachments/assets/6792282d-9ed4-4311-a4db-862ed1f934b4" />

Click on the Install Mint icon in the upper-left corner:

<img width="350" height="125" alt="IMG_4429" src="https://github.com/user-attachments/assets/c8fa4688-5fb7-42d4-a7bd-2df21afd58c4" />


That is all you need for the Windows PC. From now on, the rest of the guide will focus on installing and configuring Mint Cinnamon Linux and Llama.cpp.

Next, download the Mint Cinammon Linux ISO install file:

[Linux Mint 22.2 "Zara" Cinnamon Edition](https://www.linuxmint.com/edition.php?id=322)

<img width="783" height="495" alt="7-mint" src="https://github.com/user-attachments/assets/113861cd-1fea-41fa-ab67-4399231c8e04" />

You will need to create a bootable USB flash drive (8GB or larger). I recommend using Rufus to create the bootable drive:

[Rufus Download](https://rufus.ie/en/#download)

Run Rufus, then select the Mint ISO file that you downloaded, then click Start:

<img width="347" height="437" alt="9-mint" src="https://github.com/user-attachments/assets/1e0229af-b875-4420-86db-01920b9ed804" />

Reboot your computer, then press the appropriate key to enter the boot device selection menu (typically F12), and choose the USB flash drive:

<img width="450" height="200" alt="IMG_4427" src="https://github.com/user-attachments/assets/4bda77f4-a312-454c-91e7-e53cdfb5f983" />

Once Mint boots, choose the top selection:

<img width="400" height="170" alt="IMG_4428" src="https://github.com/user-attachments/assets/592e292a-16a7-417f-9da0-78091d96c9d5" />













