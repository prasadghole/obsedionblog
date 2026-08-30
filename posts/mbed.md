---
title: "Mbed on NRF52-DK board"
date: 2022-11-05
tags: []
publish: false
---

# mbed Ecosystem
ARM mbed provide cloud and desktop platform for developing firmware using multiple toolchain.
It compiles application and mbed OS code into single binary file to be loaded or debugged.i

It uses *arm rtx * RTOS as base OS along with other components.

# Online Keil compliler support
My board NRF52-DK is not supported. Hence only option limited is mbed IDE.


# My hands on experience
## Build
Connected board nRF52DK with BLE support. I was able to build the project but not able
to download or debug. I think debug server connection is not established.

## Debug
Trying to download example code from[NRF site](https://os.mbed.com/platforms/Nordic-nRF52-DK/) 

I was able successfully compile the code but when debug started observed message "timeout on debug
server "

### Debug with Segger Ozone
On mbed site debugging with Segger connected information is not available (for me yet).

I tried to use Segger Ozone and was successfully. For NRF52-DK board using SWD connection I was able 
to debug the .elf file generated.
![[attachments/mbed-Ozone_NRF52DK_Debug.png]]


## Deploy
### Manually copy

## mbed-cli
Downloaded installer.exe but when installed it still installed source code. Hence we need to build 
the tool using 
``python setup.py install``
It need python 27. After installing also I faced some dependency issues. I installed the 
mbed-cli by using virtual environment requirement.txt file from mbed-os folder from 
example folder.

With below commands I was able to build and deploy the program on board.
```
mbed-cli target GCC_ARM
mbed-cli compile -f 
```

## Speed
mbed IDE being jaz=vascript electron node platform is very resource consuming. During clean build
    it almost take 900 MB of RAM .
