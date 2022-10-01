equipment: 2 sd cards, each one should be at least 8GB, but ideally one of those would be 64+ GB.

sd card to usb adaptor.

softwares to download:

sdcard formatter: https://www.sdcard.org/downloads/formatter/sd-memory-card-formatter-for-windows-download/

win32diskmanager: https://sourceforge.net/projects/win32diskimager/

balenaetcher: https://www.balena.io/etcher/


STEPS:

1. preaparing the sd card. 

1.2 insert one of the 2 sd cards to your computer(the smaller sd card). 

1.3 open the sdcard formatter you downloaded, click on format. when the warning shows click yes.

1.4 download a linux image file. this image file is the operating system we wish to have on our banana pi.

i will be downloading ubuntu 18.04 (zip file) from the following link:

https://download.banana-pi.dev/d/ca025d76afd448aabc63/?p=%2FImages%2FBPI-M4%2Flinux&mode=list

extract the file into a folder on your computer.


1.5 open win32diskmanager.

click the blue folder icon and choose the image file you just downloaded from wherever you saved it.

click write and wait a few minutes for it to finish.


1.6 open balenaetcher.

click flash from file and choose the same image file again.

click select target and choose the device to flash the image into, in this case the sd card.

click flash and wait 5-10 minutes for it to finish. 

once the flashing is finished eject the sd card from your computer.


2. booting the banana pi.

under your banana pi turn the bool sel switch to 0.

insert your sd card into the micro sd slot thats under the banana pi.

plug the power supply for your banana pi.

connect an HDMI cable to a monitor, connect a mouse and keyboard to the banana's USB slots.

turn the banana pi on.

you should see the default ubuntu desktop.

if you have gotten so far, every thing should work all right.

now you could start using the browser, development tools and all the applications you can play with

but we want to flash the image(operating system) on our EMMC,

rather than using the sd card for the banana pi.

so our next step is to burn this operating system on our banana pi.


3. the other sd card.

connect the other sd card to your computer.

open a folder in it called my_image or whatever name you want. 

put the image(the full .img file, not the .zip) file in the my_image.

make sure the sd card has enough storage for the image file, weirdly enough mine demanded a 64GB card.

turn on the banana pi if it's not already on.

insert this sd card into a usb adaptor and connnect it to the banana pi.


4. burning the image on the EMMC.

open the ubuntu mate terminal.

if you can't see it on the top menu bar, go to menu icon->system tools->Mate terminal.

type the following command sudo fdisk -l.   (that's a lower case l in the end :)

if the terminal asks for a password the default one should be: bananapi .

browse through the terminal output and you are supposed to see a file that weighs about 7 GB.

remember in which mmcblk did this 7GB file appeared. should be in either mmcblk0 or mmcblk1.

navigate with terminal to where the image file is. (on our second sd card).

in my case here are the commands to navigate:

cd ..

cd ..

cd ..

cd media !!!!!!!!!!!!!!!!!!!!!

cd my_image

ls

you are supposed to see the image file name.

copy its whole name via CTRL+C.

type the following command:

(instead of your_image_file, paste the image file name you just copied)

(mmcblk0 or mmcblk1 according to where that 7 GB file is)

sudo dd if=your_image_file of=/dev/mmcblk0 bs=10MB.

after 10 minutes or so the proccess should end.

turn off the banana pi and extract both sd cards: the one with the usb adaptor and the one in the sd card slot.

turn on the banana pi.

and you are done. you finished installing ubuntu mate on your banana pi.










