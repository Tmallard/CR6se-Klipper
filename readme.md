# Cr6se Klipper installation
This outline summarizes the guides and tools I used to sucessfully get Klipper running on my Creatlity CR6se. I am a Mechanical Engineer so some of the write ups
assume you are more well versed in the programing world. I will summarized the steps and commands as well as link the instruactions I used. If anything it will be 
a reminder for a future Klipper install. It was ot very hard once I had all the peices together. 

# 1) Download Mainsial OS [offical instructions](https://docs.mainsail.xyz/setup/mainsailos/pi-imager)
  - MainsailOS builds upon Raspberry Pi OS Lite by including Klipper, Moonraker, 
     and Mainsail into the disc image, making setup quick and Mainsail easier to use with Klipper and Moonraker.
     - Download the latest Raspbery Pi Imager https://www.raspberrypi.com/software/
        The Pi imager allows you to burn pre made operating systems ready to expand on your Raspberry pi
        - Select “CHOOSE OS”, 
          - Scroll down to “Other specific-purpose OS”
            - Select “3D printing”
              - Choose Mainsail OS
                - Choose Storage (Micro SD Card)
          - Click the Settings gear
            - Enable SSH!!!!!
            - Add your Hostname
            - Wi-Fi login
            - Change your password
            - Language etc
          - Click Write
 # 2) Expand Mainsail OS
   We are goign to expand the Mainsial OS and create a Firmware.bin file which will be 
   used to flash Klipper to your printers mainboard
  - Insert the burned SD card from Step 1 in you Raspberry Pi and turn it on
  Type the commands Below
  
  ``` 
    cd klipper
    sudo service klipper stop
    make menuconfig 
  ```  
       
A GUI configuration will open up selcted the following (For 4.5.3 and 1.0.1.3 boards)    

    - select microcontroller - "STM32"
    - processor model "STM32F103" (is the default)
    - Bootloader - "28KiB"
    - Communication interface "Serial (on USART1 PA10/PA9)"
   Enter "Q" to save and quit
   Use the make commands to create the Klipper.Bin file which will be used to flash the printer main board. It will be place in the pi directory /home/pi/klipper/out/
  
# 3) FTP the Klipper.bin
Next use and FTP service to extract the Klipper.bin file from the Pi directory 
I used [FileZilla](https://filezilla-project.org/) with port 22 selected.
  - Navigate to /home/pi/klipper/out/ and copy the Klipper.bin file to your PC

# 4) Format your SD Card 
In order to flash the firmware to you main board you must formatt the SD card with the settings below. I used an 8 gig card with sucess

#  The SDcard used to flash the motherboard MUST be formatted as FAT32 with 4096 bits sector size.

# 5) Load the Firmware onto the Printer
Next we are going to flash the firmware on the printers main board
  - Rename the Klipper.bin file to Firmware.bin
  - Drag onto your newly Formatted SD card from Step #4
  - Insert into the printer and boot several times
    - The touch screen should freeze if it continiues to boot it did not work. Try again with a         differnt card. An 8 gig card worked well for me. The printer is pickey with SD card too           big or small causes issues. 

# 6) Get the USB connection address
This step gets the proper USB connection address from the PI. This will be used in you Print.cfg file (used in step 7) 

 - Connect to you Pi Via SSH using [Putty](https://putty.org/) with Port 22

   ```
   ls /dev/serial/by-id/*
   ```

The output should look like this (NOTE: the actual address will differ on yours):

   ```
   /dev/serial/by-id/usb-Klipper_stm32f103xe_36FFD8054255373740662057-if00
   ```
   
- Replace the placeholder string in the [mcu] section of print.cfg with actual output string displayed in your terminal. Which we will get in the next step

# 7) Get the Print.cfg file

https://www.klipper3d.org/Config_checks.html

   

     
 
  
