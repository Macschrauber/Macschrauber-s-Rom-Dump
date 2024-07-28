### What is it?

A tool for dumping (reading) and flashing (writing) the firmware of a Mac Pro 4,1 / 5,1 combined with an analyser of the NVRAM content and the firmware validity.
<br>
Also it can dump and analyse firmwares from the most Macs from around 2006 to 2017.
<br>

![1](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Dumper/main%20dialog.png?raw)  

It reads and writes to a ch341a USB programmer as well to work with desoldered flash chips. It detects a connected programmer and installs the libs to communicate with it. 
  
I added some tools around the Mac administration that I wrote and find useful. Check out the other .md files for them.  

<br>

### example output of the Dumper (main GUI tool) with some problems
![1](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Dumper/5a.%20analyses%20scrollable.png)  

<br>

### example flashing dialog of the Dumper  
![2](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_Dumper/8%20readout%20of%20the%20flashed%20firmware%20to%20verify.png)  

<br>

### example output of a rom dump by the cli tool, version 10-3-2024
```
$test_nvram 1.bin  
===================================================  
test_nvram_shell_script 21-Mar-2024 by Macschrauber  
scanning: 1.bin  
  
nvram.vol position: 0x120000, size: 0x30000, header size: 0x48  
vss1_position: 00120048: 2456 5353       $VSS  
vss2_position: 00130048: 2456 5353       $VSS  
fsys_position: 00148000: 4673 7973       Fsys  
gaid_position: 00148800: 4761 6964       Gaid  
0x120048 first stream start position ok, stored in /tmp/VSS_Store1.bin, length: 0x0000ffb8  
0x130048 second stream start position ok, stored in /tmp/VSS_Store2.bin, length: 0x0000ffb8  
0x148000 Fsys start position ok, header: 080000 000008  
0x148800 Gaid start position ok, header: 080000 000018  
Firmware 144.0.0.0.0 (latest) built on Fri Apr 12 12:43:00 2019  
Bios Version: MP51.88Z.F000.B00.1904121248  
MP41, Serial from firmware: 3Txxxxxxxxxxx  
Macserial reported the serial number seems to be possibly valid  
MP41 backplane made in 2009  
LBSN: J59xxxxxx1LTC   BD: xx04xxxx04xx   LBSN sector of MP51  
hwc: 9MD   son: 625-9217  
CRC32 checksums: ok  
Bootblock version: AAPLEFI1.88Z.0005.I00.1904121247  
Bootblock of 144.0.0.0.0 (rebuilt firmware)  
Base_18 hardware descriptor  
Fsys | Gaid headers: 080000 000008 | 080000 000018  
Fsys: 0 override-version, 1 overrides, 2 ssn, 3 hwc, 4 son, 5 EOF (ok)  
fmm-computer-name: xxx Mac Pro  
BootOrder: 1:Boot0080  
Boot0080: Mac OS X PciRoot(0x0)/Pci(0x3,0x0)/Pci(0x0,0x0)/SasEx(0x01000000,0x00253856,0xDF5F,0xB181,0,0,0)/HD(2,GPT,066DD320-xxxx-449D-88CB-48B603A295E1,0x64028,0x1D161920)/VenMedia(BE74FCF7-xxxx-49F3-9147-01F4042E6842,25188281F5051E4F83CD2563D5B62E7C)/\41651A92-xxxx-4950-A503-8C39B4859C2F\System\Library\CoreServices\boot.efi  
BootFFFF: PciRoot(0x0)/Pci(0x1F,0x2)/Sata(0x4,0x0,0x0)/HD(2,GPT,FFE4FF73-xxxx-4969-B1F5-1ACC09BEF3D5,0x64028,0x746A2D60)/VenMedia(BE74FCF7-xxxx-49F3-9147-01F4042E6842,5C66853E1A247A4DA378F5D95F5F72CA)/\809DFFD4-xxxx-4ED6-AD2D-7F3D999488F1\System\Library\CoreServices\boot.efi  
3 boots since last garbage collection, MTC counter: 1 - 3  
1  (2 deleted) Memory Configs g (ok)  
1  (0 deleted) Memory Configs h (ok)  
1  (0 deleted) Memory Configs i (ok)  
1  (0 deleted) Memory Configs j (ok)  
0  Microsoft certificates (ok)  
1  (0 deleted) BluetoothActiveControllerInfos (ok)  
1  (0 deleted) BluetoothInternalControllerInfos (ok)  
0  (2 deleted) Boot PathProperties0000 (ok)  
1  (0 deleted) NVRAM PathProperties0000 (ok)  
VSS2 is empty (ok after recent full nvram reset or after flashing a rebuilt firmware)  
41827 bytes free space of 65464  
VSS1 (Formatted) (Healthy), found 45 variables (29 valid, 16 deleted)  
VSS2 (Formatted) (Healthy)  
```
<br><br>
### ==> I needed to encrypt the disk image as Gatekeeper flaggs it for containing Flashrom. <==  
### *The password is **rom**.*
<br><br>

If you encounter an error regarding an unknown developer when attempting to open the Dumper, macOS displays a message stating:  
```macOS cannot verify the developer of``` 
  
To allow the system to open the Dumper, perform a Ctrl-click on it and select open. 

<br>

### If you receive a message indicating that either the apps or the disk image (.dmg) is damaged:

These issues arise from the presence of Flashrom in the package, which is flagged as potentially harmful by Mac Os' Gatekeeper and some malware scanners.  

  
If this dialog persists, you can resolve it using Terminal with the following command:  
```
xattr -cr "/path/to/RomDump Macschrauber.app"
xattr -cr "/path/to/appname.app"
```


<br>

Alternatively, you can:

Execute the scripts in the folder "is damaged fix"
They also can be flagged, if, do ```xattr -cr "/path/to/the.app"```

<br>

Use my Github Downloader to obtain a copy with no quarantine flag set:
<br>
[https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/releases/download/Release/Download.the.Dumper.from.github.zip](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/releases/download/Release/Download.the.Dumper.from.github.zip)
<br>
You may need to right-click on the App and select open.
<br><br>
Or, if you want to use an older version, use the downloader button `I have the .DMG file`. This unflags the .DMG by copying it to the user's Download folder and let the downloader remove the quarantine flags.


<br><br>
———————————————————————————————————————————————


### Yes, you can indeed disable parts of SIP while leaving others enabled.

If you run csrutil status, even while booted normally, you will see the component parts of it. Each of these can be selectively disabled by running one of the following commands while booted into Recovery mode:

+	csrutil enable --no-internal
+	csrutil enable --without kext 
+	csrutil enable --without fs
+	csrutil enable --without debug
+	csrutil enable --without dtrace
+	csrutil enable --without nvram

You can disable two or more components by structuring the command as follows:
csrutil enable --without kext  --without nvram


for running RomDump Macschrauber csrutil enable --without kext is enough
<br><br>
———————————————————————————————————————————————
### Special thanks to:

+ flashrom.org for the cli tool communicating with the Mac firmware chip.
+ tsialex @ Macrumors for investigating the Mac bootrom and sharing the information.  
+ Syncretic @ Macrumors for scanvss.  
+ LongSoft for UEFIExtract.  
+ joevt for rebuilding DirectHW.kext for all Mac OS versions.  
+ startergo for help with compiling issues.  
+ Takaaki Naganoya @ Piyomaru Software for the scrollable dialog "displaytextview"  
  
———————————————————————————————————————————————

### I have a youtube channel: https://www.youtube.com/channel/UCx5HT0rwmVaKNraMHW-Z3bQ

<br><br>
  
### If you require assistance with a damaged boot rom, feel free to contact me in English or German at ```macschrauber@gmx.de```
### Also I can upgrade Mac Pro 4,1 (2009) firmwares properly to Mac Pro 5,1 (2010-2012).
(The Netkas tool or the underlying processes don't work anymore.)
<br><br>

If you want to communicate at Github the preferred language is English.
