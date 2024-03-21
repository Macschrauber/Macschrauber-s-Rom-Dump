### What is EnableGop?

The basic idea is: if your GPU already works with OpenCore but not before it, then with this driver added to your Mac Pro firmware, your GPU should be able to work before OpenCore as well.  
This is essentially a firmware driver by Mike Beaton that injects code to provide a bootscreen for your GPU capable of Gop (Graphics Output Protocol), which is found in most unmodified GPUs made within the last 8 years.  

https://github.com/acidanthera/OpenCorePkg/tree/master/Staging/EnableGop  

The Dumper supports this firmware driver, reports its version, and also checks for some faults that may have occurred.
##
##

## EnableGop correctly inserted:
![EnableGop correctly injected](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_EnableGopSupport/EnableGop%20injected.png)
##
##
## EnableGop incorrectly insterted, multiple instances:
![multiple EnableGop](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_EnableGopSupport/multiple%20EnableGop%20analyse.png)
![multiple EnableGop dialog](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_EnableGopSupport/multiple%20EnableGop%20warning.png)
##
##
## EnableGop incorrectly inserted into old firmware:
![old firmware](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_EnableGopSupport/EnableGop%20old%20firmware.png)
##
##
## EnableGop 1.2 specific hint:
![EnableGop1.2](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_EnableGopSupport/versions%20warning.png)
