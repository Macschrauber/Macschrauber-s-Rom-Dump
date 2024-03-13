## Summary

We discovered a serious bug: booting High Sierra without System Integrity Protection (csrutil disable) possibly corrupts another mounted (unsupported) APFS2* OS Preboot volume, even when on another drive.  
Consequently, the corrupted OS may appear as High Sierra and check for compatibility with Board IDs compatible with High Sierra, possibly prevents booting.  
I've created a tool to address this problem.

This is a follow-up by the writings a while ago in another thread:  
[URL]https://forums.macrumors.com/threads/manually-configured-opencore-on-the-mac-pro.2207814/page-500?post=31995153#post-31995153[/URL]

[SPOILER="Screenshots of the issue"]
[ATTACH type="full" alt="1 ventura corrputed showing high sierra data.jpeg"]2332224[/ATTACH]
Ventura with High Sierra icon and data volume name
[ATTACH type="full" alt="5 Mac-27AD2F918AE68F61 MP7,1 cannot boot High Sierra.jpeg"]2332225[/ATTACH]
Try to boot the newer OS with [ICODE]High Sierra's PlatformSupport.plist[/ICODE] got prevented because Board ID of Mac Pro7,1 is missing
[/SPOILER]

## The problem:

Booting High Sierra (natively) and having APFS2 Volume(s) in the machine could possibly replace [ICODE]SystemVersion.plist[/ICODE] and [ICODE]PlatformSupport.plist[/ICODE] in the Proboot volume of another mounted APFS2 OS with its own outdated version.  

Also, the [ICODE].contentDetails[/ICODE] and [ICODE].disk_label*[/ICODE] files, which stores the name the BootPicker and OpenCore displays for the System name, could be renamed to the data volume name of the OS.  
If the Data Disk name for this system is 'Ventura - Data', High Sierra could have set the name for the System to 'Ventura - Data.'  

Where the latter is just cosmetic, the no more matching board ID in [ICODE]PlatformSupport.plist[/ICODE] could make the system non-bootable.  

Also we found that it replaces 3 [ICODE].im4[/ICODE] files for Macs with T2 chip.  


## The effect:

The following example details is for a Mac Pro 5,1: A wrong [ICODE]PlatformSupport.plist[/ICODE] file of High Sierra gives a [B]prohibited sign[/B], or in verbose mode, the message for an [B]unsupported board ID[/B] of a Mac Pro 7,1 [ICODE]Mac-27AD2F918AE68F61[/ICODE] if this machine is spoofed.  
And shuts down hard after 30 seconds.

If we set the boot-arg [ICODE]-no_compat_check[/ICODE] in OpenCore's [ICODE]config.plist[/ICODE], the OS ignores these issues and boots.  

A wrong [ICODE]SystemVersion.plist[/ICODE] file of High Sierra gives a High Sierra icon in the OpenCore boot menu (which is just cosmetic) but could [B]prevent the OS from updating or installing[/B] an OS reading the wrong High Sierra version 10.13.x.  


## The cure:

[I]Replacing [ICODE]SystemVersion.plist[/ICODE], [ICODE]PlatformSupport.plist[/ICODE] and the [ICODE].im4[/ICODE] files with the proper versions[/I].  
They are also stored in the CoreServices folder of the System volume and in the i386 folder of the Preboot volume.

So we replace the Preboot files with the proper files, and the situation is fixed. 
If the OS cannot boot anymore because of the missing Board ID (prohibition sign or Board ID message), we need to either boot another APFS2 capable OS, mount the System volume, and replace the files or add the boot-arg:  

[ICODE]-no_compat_check[/ICODE] to the OpenCore [ICODE]config.plist[/ICODE].

[SPOILER="Screenshots of the cure"]
[ATTACH type="full" alt="1 Ventura SystemVersion_plist mismatch.png"]2332226[/ATTACH]
1 Ventura SystemVersion_plist mismatch
[ATTACH type="full" alt="2 show HS sys for Ventura.png"]2332227[/ATTACH]
2 found High Sierra SystemVersion.plist in Ventura Preboot
[ATTACH type="full" alt="3 fix it sys.png"]2332228[/ATTACH]
3 fix SystemVersion.plist ?
[ATTACH type="full" alt="4 fixed.png"]2332229[/ATTACH]
4 fixed SystemVersion.plist
[ATTACH type="full" alt="5 Ventura PlatformSupport_plist mismatch.png"]2332230[/ATTACH]
... same for PlatformSupport.plist ...
[ATTACH type="full" alt="9 report after fix.png"]2332231[/ATTACH]
5 the report when the tool is done
[ATTACH type="full" alt="10 wrong contentDetails.png"]2332232[/ATTACH]
6 .contentDetails fix
[ATTACH type="full" alt="11 corrected contentDetails.png"]2332233[/ATTACH]
7 .contentDetails fixed
[ATTACH type="full" alt="12 second test.png"]2332234[/ATTACH]
8 a second run of Preboot fixer

[ATTACH type="full" alt="2 ventura repaired.jpeg"]2332242[/ATTACH]
9 Ventura icon and System name are back

[/SPOILER]

## The tool:


[ICODE]Preboot fixer and renamer[/ICODE] checks all Preboot folders for matching SystemVersion / PlatformSupport plists and [ICODE].im4[/ICODE] files and asks for replacing them if they don't match.  

If it is started on an APFS1 OS (late versions of Sierra, High Sierra, Mojave), it cannot mount the APFS2 System volume to read the original plists.  
However, it alarms if it finds High Sierra [ICODE]SystemVersion.plist[/ICODE] files in APFS2 Preboots.  

The wrong [ICODE].contentDetails[/ICODE] and the [ICODE].disk_label*[/ICODE] icon drawn by the native Apple boot picker can be rebuilt by the tool as well.  

You can edit the names and icons with the tool as well, even with multiple lines by entering option-return for a new line.  
This is the button <proceed with label editor>. Thanks to [USER=710085]@joevt[/USER] for all the help and providing the bash functions for it.  

[ATTACH type="full" alt="IMG_6279.jpeg"]2339442[/ATTACH]
[CENTER]the names in the boot picker could be renamed by the preboot fixer and renamer tool
The [USER=710085]@joevt[/USER] multiline names are ESPs, there is also a tool for renaming ESPs in the Dumper package[/CENTER]



## Maybe a possible exorcism:

you can try to update the date of High Sierra's  [ICODE]SystemVersion.plist[/ICODE]  
This needs more testing but it seems it helps, preventing High Sierra from replacing files in newer System's Preboots.  
Boot High Sierra and do this in [ICODE]Terminal[/ICODE]  

```sudo touch -t 203009110327 /System/Library/CoreServices/SystemVersion.plist
sudo touch -t 203009042358 /System/Library/CoreServices/PlatformSupport.plist```




*
[INDENT]APFS1: APFS Systems with one volume[/INDENT]
[INDENT]APFS2: APFS Systems with a separated system and data volume[/INDENT]



I placed the tools in my firmware dumper package to ease administration.
They can be found in the [ICODE]Readme & other tools[/ICODE] folder.  
Using the Dumper to check and backup the bootrom is a good practice for all Macs, but that's another topic ;-)  




link to the Dumper post:
[URL unfurl="true"]https://forums.macrumors.com/threads/healthy-nvram-normal-behaviour-on-4-1-5-1-machines.2333460/page-4?post=32055801#post-32055801[/URL]
