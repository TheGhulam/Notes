## Disable or Enable USB Ports/USB drive/Pen-Drive

1) Open regedit

2) Go to 
 >Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\USBSTOR

3) 
* To enable USB ports: change the value from 4 to 3.
* To disable USB ports: change the Value from 3 to 4 

## Modify hosts file to change DNS

1) Go To
>C:\Windows\System32\drivers\etc

2) Open hosts file
# Un-Formatted

### 1
How to Display Legal Notice on Start up of your Windows
If your PC has multiple users then you can display legal notice to every user before they login to your
PC. This legal notice will be displayed at every startup just before the Desktop is loaded. Using this
you can tell your friends about the do’s and don’ts in your computer when they login in your absence.
To do this:
1. Click on Start button and type regedit and press Enter
2. Navigate to the following key in the registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system
3. On the right side pane look for legalnoticecaption, double click on it and enter the desired
Legal Notice Caption.
4. Next below this look for legalnoticetext and enter the desired Legal Notice Text. The legal
notice text can be up to a page in its size so that it can include a set of do’s and don’ts for
your computer.
5. After you does this just restart your computer

### 1
Add Recycle Bin to My Computer in Windows 7
To add the Recycle Bin on My Computer, follow the steps:
1. Open up regedit.exe through the start menu search or run box
2. Go to:
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\3. Now right-click and create a New Key

### 1
Add Control Panel to My Computer in Windows 7
To add the Control Panel on My Computer, follow the steps:
1. Open up regedit.exe through the start menu search or run box
2. Go to:
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\3. Now right-click and create a New Key
4. Name the key with the following text as shown in the below figure
{26EE0668-A00A-44D7-9371-BEB064C98683}
Or
{21EC2020-3AEA-1069-A2DD-08002B30309D}
Tips:
Category View
{26EE0668-A00A-44D7-9371-BEB064C98683}
Icon View
{21EC2020-3AEA-1069-A2DD-08002B30309D}
4. Name the key with the following text as shown in the below figure:
{645FF040-5081-101B-9F08-00AA002F954E}
5. Close the Registry Editor and Open My Computer.

### 1
How to Disable Shutdown, Restart, Sleep and Hibernate
Someday, you might want to make a computer could not be turned off easily. For example because
you are running a program that needs a long time to wait (download a big file, rendering a video, etc.)
and you have to leave the room. To prevent anyone else to turn off the computer, then one way is to
disable the function of Shutdown, Restart, Sleep or Hibernate menu.
Follow these easy steps to disable Shutdown, Restart, Sleep and Hibernate:
1. Click Start button, type gpedit.msc in the Start menu’s search box and then press Enter.
Local Group Policy editor window will open.
2. Go to User Configuration > Administrative Templates > Start Menu And Taskbar
3. In the right pane, find the Remove and Prevent Access to the shutdown, Restart, Sleep,
and Hibernate. Then double click on it.
4. Select Enable, and then click OK.
Tips:
To make it back in to the normal function, just follow all the steps above, except for the last
one; you need to change back the option from Enable to Disable.
When being in a state of disable, in fact we can still shutdown the computer. The way is by
typing the below instructions in the search (Windows 7) and press Enter.
shutdown /s (for shutdown)
shutdown /r (to restart)
