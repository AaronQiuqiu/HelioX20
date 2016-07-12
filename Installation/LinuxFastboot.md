##Linux Host

This section show how to install a new operating system to your Helio X20 using the fastboot method on a Linux host computer.

***

- **Step 1**: Make sure fastboot is set up on host computer
- **Step 2**: Connect host computer to Helio X20
- **Step 3**: Boot Helio X20 into fastboot mode
- **Step 4**: Flash Bootloader
- **Step 5**: Recall location of all downloaded files
- **Step 6**: Unzip all files
- **Step 7**: Flash all files to the Helio X20
- **Step 8**: Reboot Helio X20

***

#### **Step 1**: Make sure fastboot is set up on host computer. 

- Android SDK “Tools only” for Linux can be downloaded <a href="http://developer.android.com/sdk" target="_blank">here</a>
- The Linux “Tools Only” SDK download does not come with fastboot, you will need to use the Android SDK Manager to install platform-tools.
- To do this follow the “SDK Readme.txt” instructions included in your SDK “Tools Only” download.

If you are still having trouble setting up fastboot, <a href="https://youtu.be/W_zlydVBftA" target="_blank">click here</a> for a short tutorial video

#### **Step 2**: Connect host computer to Helio X20

- Helio X20 must be powered off (unplugged from power)
- Make sure microSD card slot on Helio X20 is empty
- S6 switch on Helio X20 must be set to ‘0-0-0-0’. All switches should be in “off” position
- Connect USB to microUSB cable from host computer to Helio X20

#### **Step 3**: Boot Helio X20 into fastboot mode

**Please read all bullet points before attempting**

- Press and hold the Vol (-) button on the Helio X20, this is the S4 button. Helio X20 should still NOT be powered on
- While holding the Vol (-) button, power on the Helio X20 by plugging it in
- Once Helio X20 is plugged into power, release your hold on the Vol (-) button.
- Wait for about 20 seconds.
- Board should boot into fastboot mode.

From the connected host machine terminal window, run the following commands:

```shell
# Check to make sure device is connected and in fastboot mode

$ fastboot devices
```

Typically it will show as below
```shell
de82318	fastboot
```

**At this point you should be connected to your Helio X20 with a USB to microUSB cable. Your Helio X20 should be booted into fastboot mode and ready to be flashed with the appropriate images.**

#### **Step 4**: Flash Bootloader

- Use host computer
- Open "Terminal" application
- Recall location of Bootloader download.
- The bootloader file should be named `heliox20_bootloader_emmc_Y-XX`
- Y represents Android or Linux
- XX represents the release number of the Bootloader
- `cd` to the directory with your unzipped **Bootloader Folder**

```shell
$ cd <extraction directory>

#Example: 
cd /Users/YourUserName/Downloads
#<extraction directory> = /Users/YourUserName/Downloads
#For this example we assume the "Bootloader" is in the Downloads folder.


$ cd <unzipped Bootloader folder>

#Example:
cd heliox20_bootloader_emmc_linux-40
#<unzipped Bootloader folder> = heliox20_bootloader_emmc_linux-40
#This example took place during release 40

# This command will execute the flashall script within the bootloader folder
$ ./flashall
```

Now that the bootloader is setup, we will flash all remaining parts of the operating system. In order to do this we will be using the fastboot commands that are now readily available to us in our Terminal command line.

#### **Step 5**: Recall location of all downloaded files

Recall location of all downloaded files from the downloads page, files will be different for Android and Linaro/Debian:

###### **Linaro/Debian**: Recall location of `boot` and `rootfs` downloaded from the downloads page
- You should have downloaded the `boot` file
- You should have downloaded ONE of rootfs` file (Either `Developer` or `Desktop - ALIP` version)

###### **Android**: Recall location of `boot.img.tar.xz`, `system.img.tar.xz`, `userdata.img.tar.xz`, `recovery.img.tar.xz`, `persist.img.tar.xz`, `cache.img.tar.xz`, downloaded from the downloads page
- All of these files should have been downloaded from the downloads page

#### **Step 6**: Unzip both all files

#### **Step 7**: Flash all images to the Helio X20

- Use host computer
- Use "Terminal" application
- Recall location of extracted(unzipped) files
- `cd` to the directory with your unzipped files
- From within extraction directory, execute the following commands:

###### **Linaro/Debian**:
```shell
# (Once again) Check to make sure fastboot device connected
$ sudo fastboot devices
# It will show similar to bellow if the device is connected successfully
de82318	fastboot

# cd to the directory the boot image and  were extracted
$ cd <extraction directory>

# Make sure you have properly unzipped the boot and rootfs downloads
$ sudo fastboot flash boot boot-linaro-jessie-qcom-snapdragon-arm64-**BUILD#**.img
$ sudo fastboot flash rootfs linaro-jessie-developer-qcom-snapdragon-arm64-**BUILD#**.img
```
**Note**: Replace **BUILD#** in the above commands with the file-specific date/build stamp.

###### **Android**:
```shell
# (Once again) Check to make sure fastboot device connected
$ sudo fastboot devices
# It will show similar to bellow if the device is connected successfully
de82318	fastboot

# cd to the directory with extracted images
$ cd <extraction directory>

# Make sure you have properly unzipped the downloads
$ sudo fastboot flash boot boot.img
$ sudo fastboot flash system system.img
$ sudo fastboot flash userdata userdata.img
$ sudo fastboot flash recovery recovery.img
$ sudo fastboot flash persist persist.img
$ sudo fastboot flash cache cache.img
```

#### **Step 8**: Reboot Helio X20

- Unplug power to Helio X20
- Unplug micro USB cable from Helio X20
- Ensure HDMI connection to monitor
- Ensure keyboard and/or mouse connection (Depending on your rootfs selection)
- Plug power back into Helio X20
- Wait for board to boot up
- Board will boot into either command line or desktop depending on rootfs

**Note:** For Linaro/Debian the **username** and **password** are both **“linaro”** when the login information is requested.

**Congratulations! You are now booting your newly installed OS directly
from eMMC on the Helio X20!**
