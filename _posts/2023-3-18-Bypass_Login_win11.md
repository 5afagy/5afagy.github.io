---
title: Exploit vulnerability to bypass login windows 11, 10 , 8.1 and 7
author: khafagy
date: 2023-3-28 19:32:00 -0500
categories: [Awareness]
tags: [vulnerability]

---
![image](https://raw.githubusercontent.com/5afagy/5afagy.github.io/main/assets/image/image29.png)

Forgot your Windows 11 password? Using your laptop some time ago and can’t remember the password now? If you have previously created a password reset disk, you can get in without much trouble. In this tutorial we’ll show you another method for resetting forgotten Windows 11 password – the Utilman.exe trick, without using any third-party software.

This way work also with windows 10 , 8.1 and 7.

**How to Reset Forgotten Windows 11 Password with Utilman.exe Trick**

Boot your locked PC from Windows 11 installation media (CD or USB). When you get to the initial setup screen, press the **SHIFT**+ **F10** keyboard shortcut to open Command Prompt.



![image](https://user-images.githubusercontent.com/115117722/228717606-0c52638c-5c44-4e95-b11a-32624ed22e77.png)


press the **SHIFT**+ **F10** keyboard shortcut to open Command Prompt.


![image](https://user-images.githubusercontent.com/115117722/228718592-9b691645-c236-4433-b1bb-e3f71beebb93.png)


Type the following command to move from the X:Sources folder to the root folder of your Windows 11 installation and press Enter:

`c:`


In the command, we use C: because it’s usually the drive letter to access the hard drive after booting the device with USB, but you may need to play around to find the correct drive letter. You can confirm the location using the dir command. If the result shows the “Programs Files” and “Windows” folders, you’re in the correct location.

Type the following command to navigate to the System32 folder and press Enter:

`cd windows\system32`

Type the following commands to replace the Utility Manager button with direct access to Command Prompt from the Sign-in screen and press Enter (on each line):

At this point, type the following commands to make backup of your existing Accessibility Manager tool (Utilman.exe), and replace Utilman.exe with cmd.exe.

`ren utilman.exe utilman_bak.exe`

`copy cmd.exe utilman.exe`

![image](https://user-images.githubusercontent.com/115117722/228718849-8c3daf2f-a8df-4571-bd73-00391f467f20.png)



Type the following command to restart the computer normally and press Enter:

`wpeutil reboot`

<br>


In the Sign-in screen, click the Accessibility button in the bottom-right corner to open Command Prompt. 

![image](https://user-images.githubusercontent.com/115117722/228717939-20956b6b-bb53-49bb-9750-25591eb54b75.png)


At this point reset the device and open windows and click the accessibility button.
and will open cmd and write this command 

`net user <your account> <new password>`

and login with new password 
      
  
Check my video on my linkedin more detiels from this post. 
[Check Post](https://www.linkedin.com/posts/khafagy_software-windows-bypass-activity-7047049591736668160-XlqK?utm_source=share&utm_medium=member_desktop) 

Finally, you can close the prompt command window, and with administrative permissions, you can log onto the system.

So, finally, you have reset the Windows 11 password with Utilman.exe. 
