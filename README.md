![rpidatv banner](/doc/img/spectreiq.jpg)
# rpidatv
**rpidatv** is a digital television transmitter for Raspberry Pi 3.  The core of the transmitter was written by Evariste Courjaud F5OEO and is maintained by him.  This version has been developed by a team of BATC members for use with an external synthesized oscillator and modulator/filter board to produce a signal suitable for driving a high power amateur television transmitter on the 146, 432 or 1296 MHz bands.  The idea is that the design should be reproducible by someone who has never used Linux before.  Detailed instructions on loading the software are listed below, and further details of the complete transmitter design and build are on the BATC Wiki at https://wiki.batc.org.uk/The_Portsdown_Transmitter.  There is a Forum for discussion of the project here: http://www.batc.org.uk/forum/viewforum.php?f=103

Our thanks to Evariste and all the other contributors to this community project.  All code within the project is GPL.

# Installation for BATC Portsdown Transmitter Version

The preferred installation method only needs a Windows PC connected to the same (internet-connected) network as your Raspberry Pi.  Do not connect a keyboard or HDMI display directly to your Raspberry Pi.

- First download the 25 November 2016 release of Raspbian Jessie Lite on to your Windows PC from here http://downloads.raspberrypi.org/raspbian_lite/images/raspbian_lite-2016-11-29/.  

- Unzip the image and then transfer it to a Micro-SD Card using Win32diskimager https://sourceforge.net/projects/win32diskimager/

- Before you remove the card from your Windows PC, look at the card with windows explorer; the volume should be labelled "boot".  Create a new empty file called ssh in the top-level (root) directory by right-clicking, selecting New, Text Document, and then change the name to ssh (not ssh.txt).  You should get a window warning about changing the filename extension.  Click OK.  If you do not get this warning, you have created a file called ssh.txt and you need to rename it ssh.  IMPORTANT NOTE: by default, Windows (all versions) hides the .txt extension on the ssh file.  To change this, in Windows Explorer, select File, Options, click the View tab, and then untick "Hide extensions for known file types". Then click OK.

- If you have a Pi Camera and/or touchscreen display, you can connect them now.  Power up the Pi with the new card inserted, and a network connection.  Do not connect a keyboard or HDMI display to the Raspberry Pi. 

- Find the IP address of your Raspberry Pi using an IP Scanner (such as Advanced IP Scanner http://filehippo.com/download_advanced_ip_scanner/ for Windows, or Fing on an iPhone) to get the Pi's IP address 

- From your windows PC use Putty (http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to log in to the IP address that you noted earlier.  You will get a Security warning the first time you try; this is normal.

- Log in (user: pi, password: raspberry) then cut and paste the following code in, one line at a time:

```sh
wget https://raw.githubusercontent.com/BritishAmateurTelevisionClub/rpidatv/master/install.sh
chmod +x install.sh
./install.sh
```
Note:  As of 21 February 2017, you will get the question :
#############################################################
WARNING: This update bumps to rpi-4.9.y linux tree
Be aware there could be compatibility issues with some drivers
Discussion here:
https://www.raspberrypi.org/forums/viewtopic.php?f=29&t=167934
##############################################################
Would you like to proceed? (y/N)

Answer: N

We are working on some compatibiity issues to allow the new linux tree to be used.

- If your ISP is Virgin Media and you receive an error after entering the wget line: 'GnuTLS: A TLS fatal alert has been received.', it may be that your ISP is blocking access to GitHub.  If (only if) you get this error with Virgin Media, paste the following command in, and press return.
```sh
sudo sed -i 's/^#name_servers.*/name_servers=8.8.8.8/' /etc/resolvconf.conf
```
Then reboot, and try again.  The comnmand asks your RPi to use Google's DNS, not your ISP's DNS.

- If your ISP is BT, you will need to make sure that "BT Web Protect" is disabled so that you are able to download the software.

- For French menus and keyboard, replace the last line above with 
```sh
./install.sh fr
```

- When it has finished, accept the reboot offered or type "sudo reboot now", log in again and the console menu should be displayed.  If not, you can start the software by typing:

```sh
/home/pi/rpidatv/scripts/menu.sh menu
```

When you reboot and log-in on the computer, the BATC logo should display on the Waveshare touchscreen and the Console Menu should be displayed on the computer.  You do not need to load any touchscreen drivers - if the touchscreen does not work try powering off and on again.  If your touchscreen appears as if the touch sense is 90 degrees out, try selecting the TonTec display in the Setup menu.

I succeeded in generating a direct RF output (from GPIO pin 32) on 437 MHz at 333KS using the on-board camera as the source; direct RF output does not work reliably at higher SRs.  

Advanced notes:  To load the development and staging versions, use the following lines:
```sh
wget https://raw.githubusercontent.com/davecrump/rpidatv/master/install.sh  #OR#
wget https://raw.githubusercontent.com/BritishAmateurTelevisionClub/rpidatv/batc_staging/install.sh
chmod +x install.sh
./install.sh -d    #OR#
./install.sh -s
```
