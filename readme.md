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
            - Enable SSH
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
       
A GUI configuration will open up selcted the following     

    - select microcontroller - "STM32"
    - processor model "STM32F103" (is the default)
    - Bootloader - "28KiB"
    - Communication interface "Serial (on USART1 PA10/PA9)"
   Enter "Q" to save and quit
   

     
 
  
