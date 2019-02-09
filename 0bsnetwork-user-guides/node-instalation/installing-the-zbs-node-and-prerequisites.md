# Installing the ZBS Node and prerequisites

1. Before everything, we need to install Java 8. \(For now, only Java 8 is supported\). Enter this into your command line: **sudo add-apt-repository -y ppa:webupd8team/java** 

2. After that is done, enter this: **sudo apt-get update** 

3. Next is this line: **sudo apt-get -y install oracle-java8-installer** \(It will prompt you for Terms of Use, accept them\) 

4. Now, check if it’s the correct Java version with: **java -version** \(You should get text like this\) ![](blob:https://teams.microsoft.com/2cfd2a24-222e-4ec8-b88e-dccf30aeb345)   


![](../../.gitbook/assets/java-version.png)

5. Go to this 0bsnetwork Github to download latest .deb file for our Node: [Link](https://github.com/0bsnetwork/Zbs/releases) 

Right-Click on the latest .deb file and click on ‘Copy Link Address’  

![](../../.gitbook/assets/node-install-1.png)

 ![](blob:https://teams.microsoft.com/a2325651-2f2b-4eff-bbc3-90d9f053c4c6)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​  


6. Enter this command with the link you’ve just copied to your command line: **wget link**  

![](../../.gitbook/assets/wget.png)

  
![](blob:https://teams.microsoft.com/b23c518b-3cc6-457c-b157-9b5cda19f733)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​  


7. Once that’s downloaded, we’re gonna install it using depackage \(dpkg\):  

![](../../.gitbook/assets/dpkg.png)

  
![](blob:https://teams.microsoft.com/18fa0062-f9b9-49f5-b19b-e9941764e9dd)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​  


8. Now we’re gonna navigate where the node package is installed using: **cd /etc/zbs** 

9. Let’s edit the node config file now: **sudo nano zbs.conf** 

10. You will get this config file opened, change ‘node-name’ with your desired name and change the ‘password’ to your desired one:  

![](../../.gitbook/assets/node-install-2.png)

 ![](blob:https://teams.microsoft.com/61788ad0-2e3f-4080-b2a7-2a003c6aebce)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​  


11. Enable node’s REST API by editing the line ‘enable = yes’  

![](../../.gitbook/assets/node-install-3.png)

 ![](blob:https://teams.microsoft.com/98a98da8-b4c3-4485-a1c4-4684fb770c31)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​  


12. Once you’re done, press Ctrl + X to exit and save the config file. 

13. Start your 0bs node service with this line: **sudo systemctl start zbs.service** 

14. Now to check out how’s our node running, type this into the command line:  

**journalctl -u zbs.service -f** 

You should get something like this:  

![](../../.gitbook/assets/node-install-4.png)

 ![](blob:https://teams.microsoft.com/783538af-646b-43fc-9147-5a8bdaee8559)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​  


If it looks like this, it means your node is up, running and downloading latest blocks! Now there are few more steps before we end the setup. 

15. Open up your browser and type this into your search bar: **localhost:7431**  

![](../../.gitbook/assets/swagger-1.png)

 ![](blob:https://teams.microsoft.com/dc1184fa-f5bf-48af-a361-4d0b890c83e4)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​  


16. Now click on ‘utils’, then on ‘/utils/hash/secure’ 

In the white box, type NewApiKey and press ‘Try it out’ on the bottom to get your secure API hash.  

![](../../.gitbook/assets/swagger-2.png)

 ![](blob:https://teams.microsoft.com/293265c3-1435-4aa7-86d6-d2ddf1ba84ea)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​  


17. Copy your API Hash and let’s get back to your terminal.  

![](../../.gitbook/assets/swagger-3.png)

 ![](blob:https://teams.microsoft.com/b81372ee-2239-47f6-86b3-32ba3822c804)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)​  


18. Open up the Node config file again with: **sudo nano zbs.conf** and edit ‘api-key-hash’ with the hash you just copied. Save and close the config file and restart your node service with:  

**sudo systemctl restart zbs.service**  

![](../../.gitbook/assets/node-install-5.png)

Congratulations, you now have your 0bs Node up and running!  

