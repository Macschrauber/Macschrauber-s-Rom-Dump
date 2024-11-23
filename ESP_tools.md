# ESP Tools

What ESP is blessed, one can see when dumping the firmware with the Dumper.  
The ESP Tools that show a list of ESPs mark them with a `*` as first character of the line.



To mount ESP partitions, one can use my ESP Tools:
  
what's in?


**`Copy ESP`:**
- select the source ESP from a list that includes bootloader flavor, drive make, type, interface, and physical position
![1](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/1%20select%20source%20ESP.png)
- select the destination ESP from same list
![2](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/2%20select%20destination%20ESP.png)
- it copies the ESP from source to destination, asks for confirmation, when destination ESP has a bootloader
![3](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/3%20confirm%20to%20delete%20destination%20ESP.png)
- also it can copy to a folder for archiving. Folder name contains bootloader flavor and a time stamp
- copies archived bootloaders back

<br>

**the tools for mounting the ESPs:**
- ```Mount all ESPs```: just dumb mount all ESPs found on all volumes
- ```Mount ESP from List```: shows a list with drive's made, type, interface, physical position
- ```Mount ESP from List & show Bootloader```: same as mount ESP from list plus list the bootloader flavor
![1](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/Mount%20ESP%20from%20list%20(Readme%20&%20other%20tools%20-%20ESP%20tools).png)  

This tool also can deselect the Uefi Windows bootloader, preventing direct booting without OpenCore protection. Important for
classic Mac Pro units with one active NVRAM stream.  

![1](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/ask%20for%20deactivate%20Windows%20ESP.png)
<br>

- ```Automount ESP with bootloader```: Mounts the ESP with the blessed bootloader. Works or not, it depends...

- ```Unmount all ESPs```: just unmount all mounted ESPs

- ```Open all ESPs```: it does just what the name says

<br>

**for don't just show "EFI Boot" in the bootpicker:**
- ```Label all bootloader ESPs```: reads all ESPs, prompts you to rename to whatever you want, default is the ESP flavor
![1](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/ask%20to%20change%20rp.png)
![2](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/changed%20rp.png)
![3](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/labels%20in%20bootpicker.jpg)
<br>

- ```Label mounted bootloader ESP```: Same as Label all bootloader ESPs, but just for the single mounted one


<br>

**for identifying the mounted ESPs:**
- ```Tag all ESPs```: Places a null bytes file in the root of the ESP with drive's made, type, interface, physical position
- ```Check ESPs for MS certificates```: It checks the ESPs for a bootloader containing Microsoft UEFI Windows certificates.  
  Giving also the option to deselect Uefi Windows bootloader to prevent unprotected boot for machines what need that.  
  It got an option for setup to live in the `login items`, to deactivate Windows ESPs for being unable to start without `OpenCore` or `Refind Plus` protection.
  Also it scans the NVRAM streams for `Windows certificates` if csr values are set as needed.


![1](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/Check%20ESPs%20for%20MS%20certificates/3%20added.png)
![2](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/Check%20ESPs%20for%20MS%20certificates/setup.png)
![3](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/Check%20ESPs%20for%20MS%20certificates/deactivate%20Windows%20ESP%20dialog.png)


**Blessing:**
- ```Bless OpenCore ESP```: Bless (set the bootvar to it) the selected ESP
 
<br>

**```Preboot fixer and renamer```:**
- not exactly an ESP tool, this let you rename the Boot Picker entry for the OS. If your entries suddenly change to xyz - data you suffered from High Sierra overwriting Preboot volumes of newer OS.
In OpenCore you will see a mismatched High Sierra *icon. This is due overwritten SystemVersion.plist. Also invalid board ID / the forbidden sign can happen.

This tool also repairs these issues.<br>
Detailed information in:<br>
https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/Rename_and_repair_preboot.md

<br>


To ease administration, the ESP Tools are part of the Dumper.
One can find it in ```/Readme & other tools/ESP Tools/```
