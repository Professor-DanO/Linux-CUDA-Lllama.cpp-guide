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

That is all you need for the Windows PC. From now on, the rest of the guide will focus on installing and configuring Mint Cinnamon Linux and Llama.cpp.

Next, download the Mint Cinammon Linux ISO install file:

[Linux Mint 22.2 "Zara" Cinnamon Edition](https://www.linuxmint.com/edition.php?id=322)

<img width="783" height="495" alt="7-mint" src="https://github.com/user-attachments/assets/113861cd-1fea-41fa-ab67-4399231c8e04" />

You will need to create a bootable USB flash drive (8GB or larger). I recommend using Rufus to create the bootable drive:

[Rufus Download](https://rufus.ie/en/#download)

Run Rufus, then select the Mint ISO file that you downloaded, then click Start:

<img width="347" height="437" alt="9-mint" src="https://github.com/user-attachments/assets/1e0229af-b875-4420-86db-01920b9ed804" />

Reboot your computer, then press the appropriate key to enter the boot device selection menu (typically F12), and choose the USB flash drive. Apologies for the potato quality phone photos.

<img width="450" height="200" alt="IMG_4427" src="https://github.com/user-attachments/assets/4bda77f4-a312-454c-91e7-e53cdfb5f983" />

Once Mint boots, choose the top selection:

<img width="400" height="170" alt="IMG_4428" src="https://github.com/user-attachments/assets/592e292a-16a7-417f-9da0-78091d96c9d5" />

Click on the Install Mint icon in the upper-left corner:

<img width="320" height="125" alt="IMG_4429" src="https://github.com/user-attachments/assets/c3c96a84-8df9-4b35-b3af-3451e86fe13d" />

Go through the standard OS installation routine and create a username and password along with choosing some settings:

<img width="354" height="214" alt="IMG_4430" src="https://github.com/user-attachments/assets/60a13cb8-569c-4cb2-aedf-7182929acba9" />

Here is the important bit- Mint will detect the partition you made on the C: drive and use it properly if you choose these options (your partition number may vary):

<img width="486" height="226" alt="IMG_4431" src="https://github.com/user-attachments/assets/cf0b6328-e923-4240-8693-8a0052c2d447" />

<img width="486" height="226" alt="IMG_4432" src="https://github.com/user-attachments/assets/7df982af-3724-432c-b272-8671324e80b8" />

Once the installation finished, remove the USB flash drive then press enter to reboot:

<img width="403" height="125" alt="IMG_4434" src="https://github.com/user-attachments/assets/60026171-3f9d-4073-8b33-ef0e2c57f6f0" />

Your computer will now reboot into the Grub boot loader, which provides options for booting into Mint or Windows:

<img width="425" height="95" alt="IMG_4435" src="https://github.com/user-attachments/assets/cf713164-9a0a-46ee-ab66-81414c858e43" />

Getting Mint Linux ready to go- Updating, software settings, and security

You will be greeted with the following screen when logging in for the first time, and there are some important steps to take within its menu system:

<img width="399" height="272" alt="21-mint" src="https://github.com/user-attachments/assets/3230f12d-ae87-4943-90eb-25c19eeb2955" />

First, let's start with some Nvidia driver updates- this guide uses the recommended Nvidia 580 open set of graphics drivers:

<img width="398" height="273" alt="22-Mint" src="https://github.com/user-attachments/assets/b88c6b52-64cc-4d1b-9a93-8fe92aa70799" />
<img width="395" height="273" alt="23-Mint" src="https://github.com/user-attachments/assets/9aceb116-236e-46eb-8fd7-941633d9fc03" />


Next, set up some Firewall Security by clicking the Status button so it is enabled:
<img width="492" height="275" alt="24-Mint" src="https://github.com/user-attachments/assets/e0e86605-3e5e-4381-8afd-44c2c6b5d682" />

Now get the system updated:

<img width="612" height="300" alt="25-Mint" src="https://github.com/user-attachments/assets/860584bb-66d5-427e-89cd-66acecadc162" />
<img width="774" height="300" alt="26-Mint" src="https://github.com/user-attachments/assets/c3fdceb3-9f80-4547-9809-0bb25b54a60c" />


Under Power Management, I chose the Performance setting:

<img width="716" height="327" alt="30-Mint" src="https://github.com/user-attachments/assets/f2b95107-4d88-4c8e-a8ed-a1cb6d27cc9e" />


I also enabled automatic backups with the snapshot settings:

<img width="614" height="332" alt="32-Mint" src="https://github.com/user-attachments/assets/ebdd940f-5648-459e-92f3-f5f33b7ebbe7" />

Installing CUDA

Several non-Nvidia guides and software suites are avaialable, but I found that Nvidia's CUDA 13.1 toolkit software and guide worked well after manually adding the paths in bash.rc. Start by downloading the correct package- Linux, x86_64, Ubuntu, 24.04. I used the deb (network) installer commands, but any of them work fine:

<img width="664" height="329" alt="33-CUDA" src="https://github.com/user-attachments/assets/cc01b949-f1ac-4b9c-9783-f14f28ad81b3" />

You will now see a set of commands to use in the terminal:

<img width="506" height="164" alt="34-CUDA" src="https://github.com/user-attachments/assets/d9e0bf6d-a4a6-4ae2-ae3c-1735423ffa61" />

Installation Instructions from the command line in a terminal window:

wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-keyring_1.1-1_all.deb

sudo dpkg -i cuda-keyring_1.1-1_all.deb

sudo apt-get update

sudo apt-get -y install cuda-toolkit-13-1


After the installation is complete, you will need to open bash.rc with a text editor and add the CUDA Toolkit path information. I used the Nano editor, and to save the file use CTRL-X, then Enter, then Enter.

nano ~/.bash.rc

<img width="359" height="125" alt="37-CUDA" src="https://github.com/user-attachments/assets/221b059a-9a5a-434e-9341-a384cd410a56" />

Close the terminal window, then open a new terminal window for the new path to take effect. You should be able to test the installation with nvcc --version as seen below:

<img width="217" height="67" alt="39-CUDA" src="https://github.com/user-attachments/assets/dbfd5631-a0f5-4c87-957f-dbd67bbb02ec" />















































