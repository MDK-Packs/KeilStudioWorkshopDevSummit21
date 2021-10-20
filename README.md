# Arm DevSummit 2021: Introducing Keil Studio

Successful IoT implementations require collaboration and a robust ecosystem of support and tools. Keil Studio cloud embraces the Open-CMSIS-Pack initiative and provides a cloud-native platform with direct Git integration for collaboration of distributed teams, and modern CI workflows for rapid development.

This introductory workshop allows attendees to experience the workflow first-hand. They will prototype an IoT end node application, connect it to the cloud, and debug it via their browser.

## Required hardware

For the best workshop experience, you'll need the following:

- **NXP IMXRT1050-EVKB** (if you don’t have the hardware, you can still follow most of the workshop).
- Ethernet cable long enough to connect the board to your router.
- 5V USB power adapter with a Micro-USB cable to supply the dev board.
- We recommend a dual monitor setup, so that you can see the workshop and your Keil Studio workspace at the same time.

If you do not have access to the board, you can still follow much of the workshop. Debug will be demonstrated by the facilitators of the workshop.

### Basic hardware setup for the workshop

- Close **3-4** on jumper block **J1** (bottom left corner of the board).
- Attach the 5V USB power supply at **J9** (next to the Ethernet socket).
- Connect your computer to the development board at **J28** (top right corner of the board).

![Basic hardware setup](images/hw_setup.png)

## Pre-work

### Required software

- Keil Studio Cloud runs in a browser. You need a **Chromium** based browser (Chrome/Edge - no matter if you run Windows, Mac, or Linux).
- Create a user account at [studio.keil.arm.com](https://studio.keil.arm.com) and ensure you can login. If you have an Arm or Mbed account, you can use these to access the site.

### CMSIS-DAP Firmware

For jumpers, switches, and cable connections refer to the image above!

Make sure that you have updated your CMSIS-DAP firmware to the latest version. This makes the board compatible with [Keil Studio Cloud](https://keil.arm.com) that enables browser-based project creation and debugging. The following instructions apply if your board is equipped with a Kinetis K20DX device (marked as M20AGV) at **U23**.

#### Using HyperFlash

If your board is configured for HyperFlash (**SW7** is set to **OFF/ON/ON/OFF**), use the following CMSIS-DAP firmware: [DAPLink 0254](./DAPLink/0254_k20dx_mimxrt1050_evk_hyper_0x8000.bin)

#### Using QSPI Flash

If your board is configured for QSPI Flash (**SW7** is *not set* to **OFF/ON/ON/OFF**), use the following CMSIS-DAP firmware: [DAPLink 0254](./DAPLink/0254_k20dx_mimxrt1050_evk_qspi_0x8000.bin)

#### Jumper settings

Close **1-2** on jumper block **J27** (top right corner of the board). 

#### Flashing instructions for Windows users

1. While holding down the **SW4** button, connect the board's USB debug port (**J28**) to the computer. It should enumerate and mount as **MAINTENANCE**.
1. Drag-and-drop the firmware file onto the mounted drive.
1. Wait for the file copy operation to complete.
1. Power cycle the board. It will now enumerate and mount as **RT1050-EVK**.
2. In Windows Explorer, open **RT1050-EVK** and double-click on **DETAILS.TXT** to check the firmware version (**Interface Version** being the important number):
   ```
   # DAPLink Firmware - see https://mbed.com/daplink 
   Unique ID: 02270b0347784e4500169003d917004ce561000097969900
   HIC ID: 97969900
   Auto Reset: 0
   Automation allowed: 0
   Overflow detection: 0
   Daplink Mode: Interface
   Interface Version: 0254
   Bootloader Version: 0244
   Git SHA: f499eb6ec4a847a2b78831fe1acc856fd8eb2f28
   Local Mods: 0
   USB Interfaces: MSD, CDC, HID, WebUSB
   Bootloader CRC: 0xfdb85682
   Interface CRC: 0xa5cd1195
   Remount count: 0
   URL: http://www.nxp.com/imxrt1050evk
   ```

#### Flashing instructions for MAC users

1. While holding down the **SW4** button, connect the board's USB debug port (**J28**) to the computer. It should enumerate as **MAINTENANCE**.
1. In a terminal execute  
   `sudo mount -u -w -o sync /Volumes/MAINTENANCE ; cp -X <path_to_firmware_file> /Volumes/MAINTENANCE/`  
   *Note*: If your drive does not mount as MAINTENANCE make sure to change this to match the name of the mounted disk attached to your system.
1. Wait for the file copy operation to complete.
1. Power cycle the board. It will now enumerate and mount as **RT1050-EVK**.
2. You can check the firmware version of the board by running:  
   `cat /Volumes/RT1050-EVK/DETAILS.TXT`  
   Refer to the output above.

#### Flashing instructions for Linux users

1. While holding down the **SW4** button, connect the board's USB debug port (**J28**) to the computer. It should enumerate as **MAINTENANCE**.
1. In a terminal execute  
   `$ cp <path_to_firmware_file> /media/<USERNAME>/MAINTENANCE && sync`  
   *Note*: make sure to change MAINTENANCE to the name of the mount point of the drive on your system.
1. Power cycle the board. It will now enumerate and mount as **RT1050-EVK**.
2. You can check the firmware version of the board by runnung:  
   `cat /media/<USERNAME>/RT1050-EVK/DETAILS.TXT`  
   Refer to the output above.

#### Accessing the board under Linux

1. On Linux, permission to access USB devices from user space must be explicitly granted via udev rules. This repo contains [daplink.rules](./DAPLink/daplink.rules) that you can copy to make this work.
1. To install, copy the [daplink.rules](./DAPLink/daplink.rules) to `/etc/udev/rules.d/` on Ubuntu:  
   `$ sudo cp daplink.rules /etc/udev/rules.d`
1. To see your changes without a reboot, you can force the udev system to reload:  
   ```
   $ sudo udevadm control --reload  
   $ sudo udevadm trigger
   ```
1. Once connected, run `dmesg` to check the USB connection:
   ```
   [1705027.680326] usb 1-4: USB disconnect, device number 5 
   [1705043.749234] usb 1-4: new full-speed USB device number 6 using xhci_hcd
   [1705043.907107] usb 1-4: New USB device found, idVendor=0d28, idProduct=0204, bcdDevice=10.00
   [1705043.907112] usb 1-4: New USB device strings: Mfr=1, Product=2, SerialNumber=3
   [1705043.907115] usb 1-4: Product: DAPLink CMSIS-DAP
   [1705043.907117] usb 1-4: Manufacturer: ARM
   [1705043.907119] usb 1-4: SerialNumber: 02270b0347784e4500169003d917004ce561000097969900
   [1705043.914218] usb-storage 1-4:1.0: USB Mass Storage device detected
   [1705043.914748] scsi host1: usb-storage 1-4:1.0
   [1705043.915433] cdc_acm 1-4:1.1: ttyACM0: USB ACM device
   [1705043.917585] hid-generic 0003:0D28:0204.005B: hiddev1,hidraw2: USB HID v1.00 Device [ARM DAPLink CMSIS-DAP] on usb-0000:00:14.0-4/input3
   ```   

## Optional pre-work

Two of the projects shown in the workshop require additional accounts being set up:

- Set up a [GitHub](https://www.github.com) account for forking one of the example projects.
- Set up an AWS account if you want to follow the last step in the tutorial:
  - Create an account at [aws.amazon.com](https://aws.amazon.com).
  - For the workshop, you need to configure a Thing in the AWS IoT console. You also need to have copies of your client certificate and private key available. For creation, follow [these instructions](https://github.com/MDK-Packs/Documentation/tree/master/AWS_Thing).

## Slides

The [slide deck](./documents/Keil_Studio_DevSummit_2021.pdf) contains screenshots of the workshop. Use it to recreate the workshop in your own pace.

## Learn more

#### At DevSummit

- A session explaining the background of the workshop: [CI/CD and MLOps workflow for IoT endpoint development](https://devsummit.arm.com/en/sessions/145) (on demand)
- A workshop about [IoT DevOps made simple and scalable in the cloud](https://devsummit.arm.com/en/sessions/539?utm_source=armdevsummit&utm_medium=social&utm_campaign=2021_armdevsummit_mk17_arm_na_na_conv&utm_content=spo) (21 Oct, 9.15 PST): Get started with the recently announced, Arm Virtual Hardware during this pop-up workshop. Arm Virtual Hardware is an evolution of Arm's modelling technology delivering functionally accurate models of Arm-based SoCs for application developers to build and test software before and after silicon and hardware availability. This workshop will show you how to simplify and implement IoT DevOps at scale in the cloud with Arm Virtual Hardware.

#### Blogs

- [Cloud-based embedded development to supercharge IoT](https://www.arm.com/blogs/blueprint/cloud-based-embedded-development)
- [Cloud infrastructure for continuous integration tests](https://community.arm.com/developer/tools-software/tools/b/tools-software-ides-blog/posts/infrastructure-for-continuous-integration-tests)

## Feedback

If you want to get in touch, please raise an issue or send in a PR.
