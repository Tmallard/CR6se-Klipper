# Cr6se Klipper installation
This outline summarizes the guides and tools I used to sucessfully get Klipper running on my Creatlity CR6se. I am a Mechanical Engineer so some of the write ups
assume you are more well versed in the programing world. I will summarized the steps and commands as well as link the instruactions I used. If anything it will be 
a reminder for a future Klipper install. It was ot very hard once I had all the peices together.

Definitions
- [MainsailOS](https://docs.mainsail.xyz/) builds upon Raspberry Pi OS Lite by including Klipper,    Moonraker,and Mainsail into the disc image, making setup quick and Mainsail easier to use with    Klipper and Moonraker.

  - [Klipper](https://www.klipper3d.org/) is a 3d-Printer firmware. It combines the power of general purpose computer with one or more micro-controllers

  - [Moonraker](https://moonraker.readthedocs.io/en/latest/) is a Python 3 based web server that exposes APIs with which client applications may use to interact with the 3D printing firmware Klipper.

- [Raspberry Pi Imager](https://www.raspberrypi.com/software/) is the quick and easy way to install Raspberry Pi OS and other operating systems to a microSD card, ready to use with your Raspberry

- [Firmware.Bin](https://stackoverflow.com/questions/40853918/what-are-common-structures-for-firmware-files) The firmware file is the Executable and Linkable File, usually processed to a binary (. bin) or text represented binary (. hex). This binary file is the exact memory that is written to the embedded flash. 

- [Printer.cfg](https://www.klipper3d.org/Installation.html)Most Klipper settings are determined by a "printer configuration file" that will be stored on the Raspberry Pi. An appropriate configuration file can often be found by looking in the Klipper config directory for a file starting with a "printer-" prefix that corresponds to the target printer. The Klipper configuration file contains technical information about the printer that will be needed during the installation.

- [PuTTY](https://www.putty.org/) is an SSH and telnet client. This allows you to use the terminal of your Raspberry Pi from your PC. 

- [FileZilla](https://filezilla-project.org/) is a free, open source file transfer protocol (FTP) software tool that allows users to set up FTP servers or connect to other FTP servers in order to exchange files. FileZilla traditionally supported File Transfer Protocol over Transport Layer Security (FTPS).

The Main guide that outlines all these steps. This Document just outlines and highlight the process in my own non programer words. 
https://github.com/KoenVanduffel/CR-6_Klipper


# 1) Download Mainsial OS [offical instructions](https://docs.mainsail.xyz/setup/mainsailos/pi-imager)
  
- Download the latest [Raspberry Pi Imager](https://www.raspberrypi.com/software/)  

 - Select ```CHOOSE OS``` 
   - Scroll down to ```Other specific-purpose OS```
   - Select ```3D printing```
   - Choose ```Mainsail OS```
      - Choose Storage ```(Micro SD Card)```
      - Click the ```Settings gear```
          - ```Enable SSH !!!!!```
          - ```Add your Hostname```
          - ```Wi-Fi login```
          - ```Change your password```
          - ```Language etc```
      - Click ```Write```
      
 # 2) Expand Mainsail OS
   We are goign to expand the Mainsial OS and create a Firmware.bin file which will be 
   used to flash Klipper to your printers mainboard.
   
  - Insert the burned SD card from Step 1 in you Raspberry Pi and turn it on
  Type the commands Below
  
  ``` 
    cd klipper
    sudo service klipper stop
    make menuconfig 
  ```  
       
A GUI configuration will open up selcted the following (For 4.5.3 and 1.0.1.3 boards)    

 - select microcontroller - ```STM32```
 - processor model ```STM32F103```
 - Bootloader - ```28KiB```
 - Communication interface Serial ```USART1 PA10/PA9)```
 
 ```Enter "Q" to save and quit```
   
   Use the [make](https://forums.raspberrypi.com/viewtopic.php?t=75648) command to create the Klipper.Bin file which will be used to flash the printer main board. It will be placed in the pi directory /home/pi/klipper/out/
   ```
   make
   ```
  
# 3) FTP the Klipper.bin
Next use an FTP service to extract the Klipper.bin file from the Pi directory 
I used [FileZilla](https://filezilla-project.org/) with port 22 selected on the SSH connection.
  - Navigate to /home/pi/klipper/out/ and copy the Klipper.bin file to your PC

# 4) Format your SD Card 
```In order to flash the firmware to you main board you must formatt the SD card with the settings below. I used an 8 gig card with sucess```

#  The SDcard used to flash the motherboard MUST be formatted as FAT32 with 4096 bits sector size.

# 5) Load the Firmware onto the Printer
Next we are going to flash the firmware on the printers main board
  - Rename the Klipper.bin file to Firmware.bin
  - Drag onto your newly Formatted SD card from Step #4
  - Insert into the printer and boot several times
    - The touch screen should freeze if it continiues to boot it did not work. Try again with a         differnt card. An 8 gig card worked well for me. The printer is pickey with SD card too           big or small causes issues. 

# 6) Get the USB connection address
This step gets the proper USB connection address from the PI. This will be used in you Printer.cfg file (used in step 7) 

 - Connect to you Pi Via SSH using [Putty](https://putty.org/) with Port 22

   ```
   ls /dev/serial/by-id/*
   ```

The output should look like this (NOTE: the actual address will differ on yours):

   ```/dev/serial/by-id/usb-Klipper_stm32f103xe_36FFD8054255373740662057-if00```
   
- Replace the placeholder string in the [mcu] section of [Printer.cfg](https://www.klipper3d.org/Installation.html) with actual output string displayed in your terminal. Which we will get in the next step

# 7) Get the [Printer.cfg](https://www.klipper3d.org/Installation.html) file

The Klipper general repository for generic configurations is here https://github.com/Klipper3d/klipper/tree/master/config

Our Cr6se V 1.1.0.3 board is idencial in pin out to the 4.5.3 boards
https://github.com/Klipper3d/klipper/blob/master/config/printer-creality-cr6se-2021.cfg
  

# 8) Initial Startup Checks
https://docs.vorondesign.com/build/startup/

#9) Get Tuning
Vorons Anderw Ellis has put together an excellent tuing guide. It will walk you though the steps to gettign your snazzy new printer rockin!
https://ellis3dp.com/Print-Tuning-Guide/articles/index_tuning.html


   

     
 
  
