## equipment:

2 sd cards, each one should be at least 8GB, but ideally one of those would be 64+ GB, sd card to usb adaptor.
![alt text](https://github.com/tomer-erez/install-linux-os-banana-pi-m4/blob/main/banana%20instructions/equipment.jpeg)
## softwares to download:

sdcard formatter: https://www.sdcard.org/downloads/formatter/sd-memory-card-formatter-for-windows-download/

win32diskmanager: https://sourceforge.net/projects/win32diskimager/

balenaetcher: https://www.balena.io/etcher/


# STEPS:

##  preaparing the sd card. 

insert one of the 2 sd cards to your computer(the smaller sd card)


open the sdcard formatter you downloaded, click on format. when the warning shows click yes.
![alt text](https://github.com/tomer-erez/install-linux-os-banana-pi-m4/blob/main/banana%20instructions/sdformatter-1.jpg)


download a linux image file. this image file is the operating system we wish to have on our banana pi.

i will be downloading ubuntu 18.04 (zip file) from the following link:
https://download.banana-pi.dev/d/ca025d76afd448aabc63/?p=%2FImages%2FBPI-M4%2Flinux&mode=list
extract the file into a folder on your computer.


open win32diskmanager.

click the blue folder icon and choose the image file you just downloaded from wherever you saved it.

click write and wait 5-15 minutes for it to finish.


open balenaetcher.
![alt text](https://github.com/tomer-erez/install-linux-os-banana-pi-m4/blob/main/banana%20instructions/balena1_page-0001.jpg)
click flash from file and choose the same image file again.
![alt text](https://github.com/tomer-erez/install-linux-os-banana-pi-m4/blob/main/banana%20instructions/balena2_page-0001.jpg)
click select target and choose the device to flash the image into, in this case the sd card.
![alt text](https://github.com/tomer-erez/install-linux-os-banana-pi-m4/blob/main/banana%20instructions/balena3_page-0001.jpg)
click flash and wait 5-15 minutes for it to finish. 

once the flashing is finished eject the sd card from your computer.


## booting the banana pi:

under your banana pi turn the bool sel switch to 0.

insert your sd card into the micro sd slot thats under the banana pi.
![alt text](https://github.com/tomer-erez/install-linux-os-banana-pi-m4/blob/main/banana%20instructions/sel%20switch-1.jpg)
plug-in the power supply for your banana pi.

connect an HDMI cable to a monitor and to the banana pi, connect a mouse and keyboard to the banana's USB slots.

turn the banana pi on.

you should see the default ubuntu desktop.
![alt text](https://github.com/tomer-erez/install-linux-os-banana-pi-m4/blob/main/banana%20instructions/desktop%20screen.jpg)
if you have gotten so far, every thing should work all right.

now you could start using the browser, development tools and all the applications
![alt text](https://github.com/tomer-erez/install-linux-os-banana-pi-m4/blob/main/banana%20instructions/pre%20burn%20desktop.png)
but we want to flash the image(operating system) on our EMMC,rather than using the sd card for the banana pi.

so our next step is to burn this operating system on our banana pi.


## the other sd card:

find the sd card that we have not used yet, connect to your computer.

format the sd card with sd card formatter.

open a folder in it called my_image or whatever name you want. 

put the image(the full .img file, not the .zip) file in the my_image. we dont flash the inmg file to it, just placing it there.

make sure the sd card has enough storage for the image file, weirdly enough mine demanded a 64GB card.

turn on the banana pi if it's not already on.

insert this sd card into a usb adaptor and connnect it to the banana pi.

if the bananapi does not recognize the card or gives you an "unable to mount" error,

type the following command in the MATE terminal(Applications->system tools->Mate terminal):
```
sudo apt install exfat-fuse exfat-utils
```
(with internet connection only).

disconnect the usb and connect it again, now the system should recognize it.



## burning the image on the EMMC.

open the ubuntu mate terminal.

if you can't see it on the top menu bar, look at the menu bar: Applications->system tools->Mate terminal.
![alt text](https://github.com/tomer-erez/install-linux-os-banana-pi-m4/blob/main/banana%20instructions/find%20terminal-1.jpg)

type the following command in the MATE terminal:
(that's a minus and then lower case L in the end)
```
sudo fdisk -l   
```
if the terminal asks for a password the default one should be: bananapi .

browse through the terminal output and you are supposed to see a file that weighs about 7 GB.

remember in which mmcblk did this 7GB file appear. should be in either mmcblk0 or mmcblk1.

navigate with terminal to where the image file is. (on our second sd card).

![alt text](https://github.com/tomer-erez/install-linux-os-banana-pi-m4/blob/main/banana%20instructions/cmd.png)

in my case here are the commands to navigate:
```
cd ..
```
```
cd ..
```
```
cd media 
```
```
cd pi
```
```
cd <sd card name, could be BPI-BOOT>
```
```
cd my_image
```
```
ls
```
you are supposed to see the image file name.

copy its whole name via CTRL+C.

type the following command :

(instead of your_image_file, paste the image file name you just copied)

(mmcblk0 or mmcblk1 according to where that 7 GB file is, should be 1)
```
sudo dd if=your_image_file of=/dev/mmcblk1 bs=10MB.
```
after 10-20 minutes the proccess should end.

turn off the banana pi and extract both sd cards: the one with the usb adaptor and the one in the sd card slot.

turn on the banana pi.

and you are done. you finished installing ubuntu mate on your banana pi.











