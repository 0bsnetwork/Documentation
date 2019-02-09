# Installing Ubuntu Server

1. Once you booted from the USB drive you just made, let it load until you get to this screen,press ‘Enter’ select your language. I’m going with English here:  

![](../../.gitbook/assets/server-install-1.png)

![](blob:https://teams.microsoft.com/32f0158c-ff70-42ca-a601-545fa1ac2719)

2. Now you have to select your Keyboard Layout. I’m leaving this at default and proceeding further. \(These settings are up to you\)  

![](../../.gitbook/assets/server-install-2.png)

![](blob:https://teams.microsoft.com/e12ad1b9-b159-43eb-a8fd-aa43dbe1c985)

3. Press ‘Enter’ on ‘Install Ubuntu’ to proceed:  

![](../../.gitbook/assets/server-install-3.png)

![](blob:https://teams.microsoft.com/f8e50a0d-01a7-44ab-9414-01f29d6072e8)

4. This part is for setting Network options, I suggest you leave it on default:  

![](../../.gitbook/assets/server-install-4.png)

![](blob:https://teams.microsoft.com/1067b182-5be7-4ac0-8c9b-b8e2da2b551b)

5. Part where you can set Proxy settings, If you’re not using a Proxy to connect to the web, leave it on Default and proceed.  

![](../../.gitbook/assets/server-install-5.png)

![](blob:https://teams.microsoft.com/78da724e-fc48-4348-90c9-67272a065bd8)

6. On this screen, you choose from where your Ubuntu Server will download it’s packages. Leave it on default and proceed:  

![](../../.gitbook/assets/server-install-6.png)

![](blob:https://teams.microsoft.com/22937067-c5e7-4ca3-b893-6b52b77b6d7c)

7. Now, you can configure partitioning. If you’re using this machine solely for a node, then select ‘Use an Entire Disk’ and skip to step 12, if you’re installing it on a Virtual Machine, then follow next steps:  

![](../../.gitbook/assets/server-install-7.png)

![](blob:https://teams.microsoft.com/e4e53b27-f4d3-4850-b894-3325c330b49b)

8. Select your Virtual Disk, press ‘Enter’ and on the new window, select ‘Add Partition’ \(8.1\)  

![](../../.gitbook/assets/server-install-8.png)

![](blob:https://teams.microsoft.com/37e221ac-34ff-4c22-974f-576a682cbec5)

9. Now on this next window, you’re gonna create a ‘swap’ partition. On this Virtual Machine I used 2GB for RAM, so I’m creating the ‘swap’ partition to be 4GB \(Best swap partition size is RAM size + 2GB\), then change ‘Format’ to ‘swap’ as shown on step 9.1  

Once you’re done, select ‘Create’ to continue: 

![](../../.gitbook/assets/server-install-9.png)

10. Now, add another partition, leave the ‘Size’ field blank and make sure ‘Format’ is set to ‘ext4’ and mount is set to ‘/’, which is root partition. Press ‘Create’ to create root partition.  

![](../../.gitbook/assets/server-install-10.png)

![](blob:https://teams.microsoft.com/3d9a97b5-4cc2-4877-8afa-8b2b342fe593)

11. Now you have created a ‘swap’ and root ‘/’ partitions, select ‘Done’ to continue and again ‘Continue’ on the new window that pops out.  

![](../../.gitbook/assets/server-install-11.png)

![](blob:https://teams.microsoft.com/952de5b2-7f4e-4806-898d-990714f14b1f)

12. On this part, you’re gonna add your information like I’ve did in picture below. Remember your username and password because you will use those on your Ubuntu Server. Leave ‘Import SSH Identity’ at ‘No’ and proceed.  

![](../../.gitbook/assets/server-install-12.png)

![](blob:https://teams.microsoft.com/3195153e-5d8c-4796-aaa0-2468c3762484)

13. On the next screen, right before the actual installation process, it might ask you to choose from Ubuntu’s available Snaps. Don’t select any and proceed and let the installation finish. Once it’s finished, select ‘Reboot Now’ to reboot your machine.  

![](../../.gitbook/assets/server-install-13.png)

![](blob:https://teams.microsoft.com/9b847c7c-a8ca-4fb5-959a-55781ece0140)

14. When it asks you to remove the installation medium, unplug your bootable USB and press ‘Enter’ \(For VM installation, just press ‘Enter’\) and let it boot.  

![](../../.gitbook/assets/server-install-14.png)

![](blob:https://teams.microsoft.com/cd989db9-8014-4d3e-beb6-b676c45e3e5d)

15. If everything’s done properly, you’ll get prompted to login. Use your login credentials which you’ve entered on Step 12. After you’ve logged in, we can start the Node installation!  

![](../../.gitbook/assets/server-install-15.png)

![](blob:https://teams.microsoft.com/33f0c47b-ebf3-4b62-a4e7-da700e330f5a)

