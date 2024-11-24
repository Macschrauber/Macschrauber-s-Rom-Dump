## Summary

We discovered a serious bug: booting ***High Sierra*** without System Integrity Protection (csrutil disable) possibly corrupts another mounted (unsupported) APFS2* OS Preboot volume, even when on another drive.  
Consequently, the corrupted OS may appear as High Sierra and check for compatibility with Board IDs compatible with High Sierra, possibly prevents booting.  
I've created a tool to address this problem.

This is a follow-up by the writings a while ago in a Macrumors thread:  
https://forums.macrumors.com/threads/manually-configured-opencore-on-the-mac-pro.2207814/page-500?post=31995153#post-31995153

Screenshots of the issue:
![BootPicker](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/1%20ventura%20corrputed%20showing%20high%20sierra%20data.jpeg)
Ventura with High Sierra icon and data volume name  

![MP7,1BoardID](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/2%20Mac-27AD2F918AE68F61%20MP7,1%20cannot%20boot%20High%20Sierra.jpeg?raw=true)  

Try to boot the newer OS with ```High Sierra's PlatformSupport.plist``` got prevented because Board ID of Mac Pro7,1 is missing, if not on the spoofless approach.

<br>

## The problem:

Booting High Sierra (natively) and having APFS2 Volume(s) in the machine could possibly replace ```SystemVersion.plist``` and ```PlatformSupport.plist``` in the Proboot volume of another mounted APFS2 OS with its own outdated version.  

Also, the ```.contentDetails``` and ```.disk_label*``` files, which stores the name the BootPicker and OpenCore displays for the System name, could be renamed to the data volume name of the OS.  
If the Data Disk name for this system is 'Ventura - Data', High Sierra could have set the name for the System to 'Ventura - Data.'  

Where the latter is just cosmetic, the no more matching board ID in ```PlatformSupport.plist``` could make the system non-bootable.  

Also we found that it replaces 3 ```.im4``` files for Macs with T2 chip.  

<br>

## The effect:

The following example details is for a Mac Pro 5,1: A wrong ```PlatformSupport.plist``` file of High Sierra gives a **prohibited sign**, or in verbose mode, the message for an **unsupported board ID** of a Mac Pro 7,1 ```Mac-27AD2F918AE68F61``` if this machine is spoofed.  
And shuts down hard after 30 seconds.

If we set the boot-arg ```-no_compat_check``` in OpenCore's ```config.plist```, the OS ignores these issues and boots.  

A wrong ```SystemVersion.plist``` file of High Sierra gives a High Sierra icon in the OpenCore boot menu (which is just cosmetic) but could **prevent the OS from updating or installing** an OS reading the wrong High Sierra version 10.13.x.  

<br>

## The cure:

Replacing ```SystemVersion.plist```, ```PlatformSupport.plist``` and the ```.im4``` files with the proper versions.  
They are also stored in the CoreServices folder of the System volume and in the i386 folder of the Preboot volume.

So we replace the Preboot files with the proper files, and the situation is fixed. 
If the OS cannot boot anymore because of the missing Board ID (prohibition sign or Board ID message), we need to either boot another APFS2 capable OS, mount the System volume, and replace the files or add the boot-arg:  

```-no_compat_check``` to the OpenCore ```config.plist```.  

<br>

Screenshots of the cure  
___________________
1 Ventura SystemVersion_plist mismatch:<br>
![1](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/3%20Ventura%20SystemVersion_plist%20mismatch.png)
___________________
2 found High Sierra SystemVersion.plist in Ventura Preboot:<br>
![2](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/4%20show%20HS%20sys%20for%20Ventura.png)
___________________
3 fix SystemVersion.plist?:<br>
![3](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/5%20fix%20it%20sys.png)
___________________  
4 fixed SystemVersion.plist:<br>
![4](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/6%20fixed.png)
___________________  
5 Ventura PlatformSupport.plist mismatch:<br>
![5](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/7%20Ventura%20PlatformSupport_plist%20mismatch.png)
___________________  
6 the report when the tool is done:<br>
![6](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/8%20report%20after%20fix.png)
___________________  
7 .contentDetails fix:<br>
![7](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/9%20corrected%20contentDetails.png)  
___________________  
8 2nd readout, now ok:<br>
![8](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/A%20second%20test.png)
___________________  
![9](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/B%20ventura%20repaired.jpeg)
9 Ventura icon and System name are back<br>
___________________
![10](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/C%20Boot%20Picker%20with%20custom%20names.jpeg)
10 ESPs were renamed by the ```Label all bootloader ESPs```tool of the Dumper package, names are correct (or adjusted).<br>
___________________
![11](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/AA%20show%20preboot.png)
![12](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Rename_and_repair_preboot/AB%20rename%20preboot.png)  
Show and let rename the Preboot rendered name, as appears in the Apple Boot Picker or OpenCore boot menu.
___________________



<br>

## The tool:


```Preboot fixer and renamer``` checks all Preboot folders for matching SystemVersion / PlatformSupport plists and ```.im4``` files and asks for replacing them, if they don't match.  

If it is started on an APFS1 OS (late versions of Sierra, High Sierra, Mojave), it cannot mount the APFS2 System volume to read the original plists.  
However, it alarms, if it finds High Sierra ```SystemVersion.plist``` files in APFS2 Preboots.  

The wrong ```.contentDetails``` and the ```.disk_label*``` icon, drawn by the native Apple boot picker, can be rebuilt by the tool as well.  

You can edit the names and icons with the tool as well, even with multiple lines, by entering option-return for a new line.  
This is the button <proceed with label editor>. Thanks to @joevt for all the help and providing the bash functions for it.  

The names in the boot picker could be renamed by the preboot fixer and renamer tool.

The @joevt multiline names are ESPs, there is also a tool for renaming ESPs in the Dumper package

<br>

## Maybe a possible exorcism:

you can try to update the date of High Sierra's ```SystemVersion.plist```  
This needs more testing, but it seems it helps, preventing High Sierra from replacing files in newer System's Preboots.  
Boot High Sierra and do this in ```Terminal```  

```
sudo touch -t 203009110327 /System/Library/CoreServices/SystemVersion.plist
sudo touch -t 203009042358 /System/Library/CoreServices/PlatformSupport.plist
```
<br>

\*   
APFS1: APFS Systems with one volume  
APFS2: APFS Systems with a separated system and data volume  


<br>

I placed the tools in my firmware dumper package, to ease administration.
They can be found in the ```Readme & other tools``` folder.  
Using the Dumper, to check and backup the bootrom is a good practice for all Macs, but that's another topic ;-)  


<br>

link to the Macrumors Dumper post:  
https://forums.macrumors.com/threads/high-sierra-booting-possibly-corrupts-newer-systems-fix-description-and-a-boot-picker-renamer.2415320/
