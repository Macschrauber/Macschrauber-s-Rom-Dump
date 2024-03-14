# ESP Tools

What ESP is blessed one can see when dumping the firmware with the Dumper.



To mount ESP Partitions one can use my ESP tools:

what's in?


**the copy ESP tool:**
- select source ESP from a list with bootloader flavor, drive's made, type, interface, physical position
![1](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/1%20select%20source%20ESP.png)
- select destination ESP from same list
![2](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/2%20select%20destination%20ESP.png)
- it copies the ESP from source to destination, asks for confirmation if destination ESP has a bootloader
![3](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/3%20confirm%20to%20delete%20destination%20ESP.png)
- also can copy to a folder for archiving. Folder name contains bootloader flavor and a time stamp
- copies archived bootloaders back

<br>

**the tools for mounting the ESPs:**
- mount all ESPs: just dumb mount all ESPs found on all volumes
- mount ESP from list: shows a list with drive's made, type, interface, physical position
- mount ESP from list & show bootloader: same as mount ESP from list plus list the bootloader flavor
![1](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/Mount%20ESP%20from%20list%20(Readme%20&%20other%20tools%20-%20ESP%20tools).png)
- Automount ESP with bootloader: Mounts the ESP with the blessed bootloader. Works or not, it depends...

- unmount all ESPs: just unmount all mounted ESPs

- open all ESPs: it does just what the name says

<br>

**for don't just show "EFI Boot" in the bootpicker:**
- Label all bootloader ESPs: reads all ESPs, prompts you to rename to whatever you want, default is the ESP flavor
![1](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/ask%20to%20change%20rp.png)
![2](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/changed%20rp.png)
![3](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_ESP_tools/labels%20in%20bootpicker.jpg)
<br>

- Label mounted bootloader ESP: Same as Label all bootloader ESPs, but just for the single mounted one

hint: if the rendered name is white on white / black on black then you may set automatic light / dark mode and a system setting is not written. If you once change to dark mode and back to automatic mode this setting is corrected.  
I just added a button to overwrite that since version 20-2-2024.)


<br>

**for identifying the mounted ESPs:**
- Tag all ESPs: Places a null bytes file in the root of the ESP with drive's made, type, interface, physical position
- Check ESPs for MS certificates: It checks the ESPs for a bootloader containing Microsoft Uefi Windows certificates

<br>

**Blessing:**
- Bless OpenCore ESP: Bless (set the bootvar to it) the selected ESP
 
<br>

**Preboot fixer and renamer:**
- Not exactly a ESP tool, this let you rename the Boot Picker entry for the OS. If your entries suddenly change to xyz - data you suffered from High Sierra overwriting Preboot volumes of newer OS.
In OpenCore you will see a mismatched High Sierra *icon. This is due overwritten SystemVersion.plist. Also invalid board ID / the forbidden sign can happen.
*This tool also repairs these issues.

   (hint: if the rendered name is white on white / black on black then you may set automatic light / dark mode and a system setting is not written. If you once change to dark mode and back to automatic mode this setting is corrected.*
I just added a button to overwrite that, this will be in the next release after 17-2-2024.)

<br>


The ESP Tools are part of the Dumper. To ease administration I decided to link the whole Dumper.
One can find it in /Readme & other tools/ESP Tools/
