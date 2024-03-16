### Shell Script / CLI tool examples

commands
```
$test_nvram -help
test_nvram_shell_script 8-Mar-2024
takes *.bin, *.rom, *.vol, *.fd and one or more of these arguments:
-help               this text
-force              don't check filesize and type
-freshdump          treat the file like it was just dumped on this machine
-shortserial        truncate the serial number
-nointro            do not show version and filename
-condense_gfxutil   do not show the full path for Bootvars
-DontCheckVolumes   do not mount or check volumes for bootvar decoding
-showvars           show all NVRAM VSS variable names
-vars               show all variables in all NVRAM volume stores as hexdump and text
-varstextonly       show all variables in all NVRAM volume stores as text
-mtccounts1         show deleted MTC counts
-mtccounts2         show MTC count of VSS2
-mtccounts12        show all MTC counts
-showall            show MTC (VSS1 deleted, VSS2) and all NVRAM variables
-showlbsn           show LBSN, hwc, son
-showbathealth      show battery-health variables condensed
-showfullbathealth  show battery-health variables (gives a hughe report)
-hexdump            show a hexdump of the variables and certificates that have been read
-gathernvram.vol    collect the extracted nvram volumes in /Users/svenradke/All_Nvrams
-rename             ask to rename the given file by machine, serial, firmware, additions
-forcerename        same as -rename but don't ask
-simulaterename     same as -forcerename but just write out the new filename
_________________________________________________________________________________________________
 without giving a file:
-dump               dump the firmware with flashrom or eficheck to a file
-SST25VF032B        use this flash chip (MacPro 4,1 2009)
-MX25L3205D         use this flash chip (MacPro 5,1 2010-2011)
-MX25L3206E         use this flash chip (MacPro 5,1 2012)
-chip='yourflash'   use this flash chip, quotate it
-chip=auto          let flashrom detect the chip, if possible
-chip=eficheck      use eficheck if machine is capable

-scanvss            run Syncretic's scanvss to analyse the NVRAM streams, ~2006 to ~2012 Macs only
  for arguments quote like:
   '-scanvss -v'       ...show variable values
   '-scanvss -g'       ...show hex GUIDs
   '-scanvss -D'       ...hide deleted variables
   '-scanvss -d'       ...show header details
   '-scanvss -V1'      ...show only VSS1
   '-scanvss -V2'      ...show only VSS2
   '-scanvss -a'       ...show everything, same as -v -g -d
-freespace          read this machine's NVRAM with scanvss and just print free space of VSS1

```

<br>

just freespace in VSS1
```
user$ test_nvram -freespace
Apparent free space in VSS1: 27668 bytes
```

<br>

dumping with Flashrom on a Mac Pro 5,1
```
user$ test_nvram -dump
no spi-flash type given, but found MP51. Assuming MX25L3205D from experience
...Requesting load of /users/user/Library/Application Support/Macschrauber/DirectHW.kext.
/users/user/Library/Application Support/Macschrauber/DirectHW.kext loaded successfully (or already loaded).

doing flashrom097r1711 -p internal:laptop=this_is_not_a_laptop -c MX25L3205D/MX25L3208D -r /users/user/Downloads/18.09.2023_21-33-13_MX25L3205D_dump.bin -o /users/user/Downloads/18.09.2023_21-33-13_MX25L3205D_dump.log
...reading /users/user/Downloads/18.09.2023_21-33-13_MX25L3205D_dump.bin with Flashrom
...Flashrom was executed and gave no error

...com.coresystems.DirectHW unloaded and personalities removed.
.../users/user/Downloads/18.09.2023_21-33-13_MX25L3205D_dump.bin was created
.../users/user/Downloads/18.09.2023_21-33-13_MX25L3205D_dump.log was created
===================================================
test_nvram_shell_script 17-Sep-2023 by Macschrauber
scanning: /users/user/Downloads/18.09.2023_21-33-13_MX25L3205D_dump.bin

Firmware 144.0.0.0.0 (latest) built on Fri Apr 12 12:43:00 2019
Bios Version: MP51.88Z.F000.B00.1904121248
(U)efi version: 1.10
MP51, Serial from firmware: CKxxxxxxxxEUG
LBSN: J50xxxxxxxxBH9A   BD: 10xxxx10xxxx
hwc: EUG   son: 000xxxxxxxxx96
EnableGop 1.3 EFI module identified
CRC32 checksums: ok
Bootblock of 144.0.0.0.0 (rebuilt firmware)
Base_21 hardware descriptor
Boot000x is EFI\OC\OpenCore.efi (LauncherOption: Full)
OCLP: 0.6.9 | -allow_fv | MacPro5,1
fmm-computer-name: MacPro51 (2)
boot-args: keepsyms=1 debug=0x100 -lilubetaall -btlfxallowanyaddr ipc_control_port_options=0 -nokcmismatchpanic -disable_sidecar_mac -lilubetaall
BootOrder: 1:Boot0080
Boot0001: OpenCore |EFI|disk1s1 (SATA DVD Bay B (Lower):SAMSUNG 470 Series SSD)|EFI|PciRoot(0x0)/Pci(0x1F,0x2)/Sata(0x1,0x0,0x0)/HD(1,GPT,53A70A2A-B1A7-4368-A858-870B8D9807CC,0x28,0x64000)/EFI\OC\OpenCore.efi
Boot0080: |Apple_APFS|disk0s2 (PCI-Express Internal:Samsung SSD 970 EVO Plus 500GB)|PciRoot(0x0)/Pci(0x7,0x0)/Pci(0x0,0x0)/Msg(34,010000000025385291504418)/HD(2,GPT,7D2C57B3-FF74-4E5A-83B9-CA26ED30F50F,0x64028,0x3A321FE0)/VenMedia(BE74FCF7-0B7C-49F3-9147-01F4042E6842,A4AEE393BBBE594BB7CF61C455EDEE09)/\31F61C0A-1EAA-4D9B-BDD4-9786D5D5A009\System\Library\CoreServices\boot.efi
Boot0080 is MacOs 10.14.6, label: Mojave
BootFFFF: |Apple_APFS|disk0s2 (PCI-Express Internal:Samsung SSD 970 EVO Plus 500GB)|PciRoot(0x0)/Pci(0x7,0x0)/Pci(0x0,0x0)/Msg(34,010000000025385291504418)/HD(2,GPT,7D2C57B3-FF74-4E5A-83B9-CA26ED30F50F,0x64028,0x3A321FE0)/VenMedia(BE74FCF7-0B7C-49F3-9147-01F4042E6842,A4AEE393BBBE594BB7CF61C455EDEE09)/\31F61C0A-1EAA-4D9B-BDD4-9786D5D5A009\System\Library\CoreServices\boot.efi
BootFFFF is MacOs 10.14.6, label: Mojave
6 boots since last garbage collection, MTC counter: 12 - 18
VSS1                   VSS2
7 (1 active)           1 Memory Configs g (ok)
7 (1 active)           0 Memory Configs h (ok)
1 (1 active)           0 Memory Configs i (ok)
1 (1 active)           0 Memory Configs j (ok)
0                      0 Microsoft certificates (ok)
1 (1 active)           1 BluetoothActiveControllerInfos (ok)
1 (1 active)           1 BluetoothInternalControllerInfos (ok)
1 (1 active)           1 current-network (ok)
1 (1 active)           1 NVRAM PathProperties0000 (ok)
27668 bytes free space of 65464
VSS1 (Formatted) (Healthy), found 67 variables (42 valid, 25 deleted)
VSS2 (Formatted) (Healthy), found 40 variables (40 valid)
...renamed: 18.09.2023_21-33-13_MX25L3205D_dump.bin to MP51_144.0.0.0.0_CKxxxxxxxxEUG_EnableGop_1.3_18.09.2023_21-33-13.bin
...renamed: /users/user/Downloads/18.09.2023_21-33-13_MX25L3205D_dump.log to /users/user/Downloads/MP51_144.0.0.0.0_CKxxxxxxxxEUG_EnableGop_1.3_18.09.2023_21-33-13.log
```

<br>

dumping with eficheck on a MacBook Air 6,2
```
~ % test_nvram -dump -chip:eficheck
...reading /users/user/Downloads/23.07.2023_18-22-32_eficheck_dump.bin
Password:
.../users/user/Downloads/23.07.2023_18-22-32_eficheck_dump.bin was created

===================================================
test_nvram_shell_script 23-Jul-2023 by Macschrauber
scanning: /users/user/Downloads/23.07.2023_18-22-32_eficheck_dump.bin

8MB file detected, analysing in progress
Firmware 478.0.0.0.0 built on Fri Jan 13 17:47:58 PST 2023
Bios Version: MBA61.88Z.F000.B00.2301131747
MBA62, Serial from firmware: C17xxxxxxxxxx
hwc: G085   son: MD760D/
CRC32 checksums: ok
Base_18 hardware descriptor
fmm-computer-name: MacBook Air from user
BootOrder: 1:Boot0080
Boot0080: \7AFD3F6D-2719-4CA3-B821-FA9B4D74770B\System\Library\CoreServices\boot.efi
Boot0082: \7AFD3F6D-2719-4CA3-B821-FA9B4D74770B\System\Library\CoreServices\boot.efi
BootFFFF: \pDZ\A20E739E-78F6-3924-A686-272E77E54C35\System\Library\CoreServices\boot.efi
15 boots since last garbage collection, MTC counter: 86 - 101
VSS1                   VSS2
1 (1 active)           1 (1 active) Memory Configs g
1 (1 active)           1 (1 active) Memory Configs h
1 (1 active)           1 (1 active) Kernel Panic dumps type A: Pointer type (ok)
0                      0 Microsoft certificates (ok)
26 (1 active)          42 (1 active) Boot PathProperties0000 (ok)
11 (1 active)          12 (1 active) NVRAM PathProperties0000 (ok)
VSS1: found 177 variables (47 valid, 130 deleted)
VSS2: found 264 variables (50 valid, 214 deleted)
17785 bytes free space of 65456 in VSS1
416 bytes free space of 65456 in VSS2
...renamed: 23.07.2023_18-22-32_eficheck_dump.bin to MBA62_478.0.0.0.0_C17xxxxxxxx_23.07.2023_18-22-32.bin
```

<br>

full check with the cli tool:
```
Last login: Sun Jul 23 23:29:33 on ttys000
MacPro51:~ user$ test_nvram /Users/user/Downloads/CKxxxxxCEUG_144.0.0.0.0_gop_1.3_MX25L3205D_23.07.2023_23-34-10.bin -showall
===================================================
test_nvram_shell_script 23-Jul-2023 by Macschrauber
scanning: /Users/user/Downloads/CKxxxxxCEUG_144.0.0.0.0_gop_1.3_MX25L3205D_23.07.2023_23-34-10.bin
Firmware 144.0.0.0.0 (latest) built on Fri Apr 12 12:43:00 2019
Bios Version: MP51.88Z.F000.B00.1904121248
MP51, Serial from firmware: CKxxxxxCEUG
LBSN: J5xxxxxBH9A   BD: 10xxxx10xxxx
hwc: EUG   son: 00031xxxxxxxx
EnableGop 1.3 EFI module identified
CRC32 checksums: ok
Bootblock of 144.0.0.0.0 (rebuilt firmware)
Base_21 hardware descriptor
Boot000x is EFI\OC\OpenCore.efi (LauncherOption: Full)
OCLP: 0.6.8 | -allow_fv -allow_amfi | MacPro5,1
fmm-computer-name: MacPro51 (2)
MTC count (VSS1, Normal): 111
MTC count (VSS2, Normal): 106
MTC counts VSS1 (DELETED) (1): 106
MTC counts VSS1 (DELETED) (2): 107
MTC counts VSS1 (DELETED) (3): 108
MTC counts VSS1 (DELETED) (4): 109
MTC counts VSS1 (DELETED) (5): 110
boot-args: -no_compat_check keepsyms=1 debug=0x100 -lilubetaall -btlfxallowanyaddr ipc_control_port_options=0 -nokcmismatchpanic -disable_sidecar_mac
BootOrder: 1:Boot0080
Boot0080: \31F61C0A-1EAA-4D9B-BDD4-9786D5D5A009\System\Library\CoreServices\boot.efi
BootFFFF: \31F61C0A-1EAA-4D9B-BDD4-9786D5D5A009\System\Library\CoreServices\boot.efi
OCBtOrder: 1:OCBt0080
OCBt0080: \31F61C0A-1EAA-4D9B-BDD4-9786D5D5A009\System\Library\CoreServices\boot.efi
OCBt0081: Mac OS X \31F61C0A-1EAA-4D9B-BDD4-9786D5D5A009\System\Library\CoreServices\boot.efi
OCBtFFFF: \31F61C0A-1EAA-4D9B-BDD4-9786D5D5A009\System\Library\CoreServices\boot.efi
5 boots since last garbage collection, MTC counter: 106 - 111
VSS1                   VSS2
6 (1 active)           1 Memory Configs g (ok)
6 (1 active)           1 Memory Configs h (ok)
1 (1 active)           1 Memory Configs i (ok)
1 (1 active)           1 Memory Configs j (ok)
6 (1 active)           1 Kernel Panic dumps type A: Pointer type
11 (11 active)         11 Kernel Panic dumps type B: Compressed (caution)
0                      0 Microsoft certificates (ok)
1 (1 active)           1 BluetoothActiveControllerInfos (ok)
6 (1 active)           1 Boot PathProperties0000 (ok)
1 (1 active)           1 NVRAM PathProperties0000 (ok)
2 (2 active)           2 Boot00xx variables
2 (2 active)           2 OCbt00xx variables
16854 bytes free space of 65464
VSS1 (Formatted) (Healthy), found 96 variables (58 valid, 38 deleted)
VSS2 (Formatted) (Healthy), found 58 variables (58 valid)
---------------------
all variables in VSS1:
1 (ACPI Variable):AcpiGlobalVariable (Normal)
1 (Apple Backup Boot Variable):Boot0080 (Normal)
1 (Apple Backup Boot Variable):BootOrder (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0000 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0001 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0002 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0003 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0004 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0005 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0006 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0007 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0008 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0009 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo000K (Normal)
1 (Apple Boot Variable):AAPL,PanicInfoLog (Normal)
1 (Apple Boot Variable):AAPL,PathProperties0000 (Normal)
1 (Apple Boot Variable):EFIBluetoothDelay (Normal)
1 (Apple Boot Variable):IDInstallerDataV2 (Normal)
1 (Apple Boot Variable):LocationServicesEnabled (Normal)
1 (Apple Boot Variable):SystemAudioVolume (Normal)
1 (Apple Boot Variable):SystemAudioVolumeDB (Normal)
1 (Apple Boot Variable):_kdp_ipstr (Normal)
1 (Apple Boot Variable):bluetoothActiveControllerInfo (Normal)
1 (Apple Boot Variable):boot-args (Normal)
1 (Apple Boot Variable):csr-active-config (Normal)
1 (Apple Boot Variable):fmm-computer-name (Normal)
1 (Apple Boot Variable):ignition-failure-boot (Normal)
1 (Apple Boot Variable):ignition-failure-reason (Normal)
1 (Apple Boot Variable):prev-lang-diags:kbd (Normal)
1 (Apple Boot Variable):run-efi-updater (Normal)
1 (Apple NVRAM Variable):AAPL,PathProperties0000 (Normal)
1 (Apple NVRAM Variable):security-key (Normal)
1 (Apple Wireless Network Variable):preferred-count (Normal)
1 (Apple Wireless Network Variable):preferred-networks (Normal)
1 (EFI Global):Boot0001 (Normal)
1 (EFI Global):Boot0080 (Normal)
1 (EFI Global):BootFFFF (Normal)
1 (EFI Global):BootOrder (Normal)
1 (EFI Global):ConOutDev (Normal)
1 (EFI Global):Lang (Normal)
1 (EFI Global):MemoryConfig (Normal)
1 (EFI Global):MemoryConfih (Normal)
1 (EFI Global):MemoryConfii (Normal)
1 (EFI Global):MemoryConfij (Normal)
1 (EFI Global):PlatformLang (Normal)
1 (MTC variable):MTC (Normal)
1 (OpenCore Variable):OCBt0080 (Normal)
1 (OpenCore Variable):OCBt0081 (Normal)
1 (OpenCore Variable):OCBtFFFF (Normal)
1 (OpenCore Variable):OCBtOrder (Normal)
1 (OpenCore Variable):OCLP-Model (Normal)
1 (OpenCore Variable):OCLP-Settings (Normal)
1 (OpenCore Variable):OCLP-Version (Normal)
1 (OpenCore Variable):revblock (Normal)
1 (OpenCore Variable):revpatch (Normal)
1 (Setup Variable):Setup (Normal)
1 4c024000-2802-4a2a-8880-4a4088108c00:@@AB%` (Normal)
1 62bf9b1c-8568-48ee-85dc-dd3057660863:boot-feature-usage (Normal)
---------------------
4 (Apple Boot Variable):SystemAudioVolume (DELETED)
4 (Apple Boot Variable):SystemAudioVolumeDB (DELETED)
5 (Apple Boot Variable):AAPL,PanicInfoLog (DELETED)
5 (Apple Boot Variable):AAPL,PathProperties0000 (DELETED)
5 (EFI Global):MemoryConfig (DELETED)
5 (EFI Global):MemoryConfih (DELETED)
5 (EFI Global):_AGP_DISABLED (DELETED)
5 (MTC variable):MTC (DELETED)
---------------------
all variables in VSS2:
1 (ACPI Variable):AcpiGlobalVariable (Normal)
1 (Apple Backup Boot Variable):Boot0080 (Normal)
1 (Apple Backup Boot Variable):BootOrder (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0000 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0001 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0002 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0003 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0004 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0005 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0006 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0007 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0008 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo0009 (Normal)
1 (Apple Boot Variable):AAPL,PanicInfo000K (Normal)
1 (Apple Boot Variable):AAPL,PanicInfoLog (Normal)
1 (Apple Boot Variable):AAPL,PathProperties0000 (Normal)
1 (Apple Boot Variable):EFIBluetoothDelay (Normal)
1 (Apple Boot Variable):IDInstallerDataV2 (Normal)
1 (Apple Boot Variable):LocationServicesEnabled (Normal)
1 (Apple Boot Variable):SystemAudioVolume (Normal)
1 (Apple Boot Variable):SystemAudioVolumeDB (Normal)
1 (Apple Boot Variable):_kdp_ipstr (Normal)
1 (Apple Boot Variable):bluetoothActiveControllerInfo (Normal)
1 (Apple Boot Variable):boot-args (Normal)
1 (Apple Boot Variable):csr-active-config (Normal)
1 (Apple Boot Variable):fmm-computer-name (Normal)
1 (Apple Boot Variable):ignition-failure-boot (Normal)
1 (Apple Boot Variable):ignition-failure-reason (Normal)
1 (Apple Boot Variable):prev-lang-diags:kbd (Normal)
1 (Apple Boot Variable):run-efi-updater (Normal)
1 (Apple NVRAM Variable):AAPL,PathProperties0000 (Normal)
1 (Apple NVRAM Variable):security-key (Normal)
1 (Apple Wireless Network Variable):preferred-count (Normal)
1 (Apple Wireless Network Variable):preferred-networks (Normal)
1 (EFI Global):Boot0001 (Normal)
1 (EFI Global):Boot0080 (Normal)
1 (EFI Global):BootFFFF (Normal)
1 (EFI Global):BootOrder (Normal)
1 (EFI Global):ConOutDev (Normal)
1 (EFI Global):Lang (Normal)
1 (EFI Global):MemoryConfig (Normal)
1 (EFI Global):MemoryConfih (Normal)
1 (EFI Global):MemoryConfii (Normal)
1 (EFI Global):MemoryConfij (Normal)
1 (EFI Global):PlatformLang (Normal)
1 (MTC variable):MTC (Normal)
1 (OpenCore Variable):OCBt0080 (Normal)
1 (OpenCore Variable):OCBt0081 (Normal)
1 (OpenCore Variable):OCBtFFFF (Normal)
1 (OpenCore Variable):OCBtOrder (Normal)
1 (OpenCore Variable):OCLP-Model (Normal)
1 (OpenCore Variable):OCLP-Settings (Normal)
1 (OpenCore Variable):OCLP-Version (Normal)
1 (OpenCore Variable):revblock (Normal)
1 (OpenCore Variable):revpatch (Normal)
1 (Setup Variable):Setup (Normal)
1 4c024000-2802-4a2a-8880-4a4088108c00:@@AB%` (Normal)
1 62bf9b1c-8568-48ee-85dc-dd3057660863:boot-feature-usage (Normal)
```

<br>

running Syncretic's ScanVSS
```
test_nvram bbs.bin '-scanvss -a'
...Requesting load of /users/user/Library/Application Support/Macschrauber/DirectHW.kext.
/users/user/Library/Application Support/Macschrauber/DirectHW.kext loaded successfully (or already loaded).
(Reading the FlashROM may take several seconds...)
ScanVSS v0.17, Copyright 2022 Syncretic.  All Rights Reserved.
This program comes without any warranty of suitability for any purpose.
-- Found 2 VSS structures.
-- Parsing VSS structures from local flash.

----------------
Signature: 53535624 (Valid)
Size:      0000ffb8 (65464)
Format:    5a (Formatted)
State:     fe (Healthy)
Unk16[0]:  fe (Normal)
Unk16[1]:  01
Unk32:     00000000
----------------
--------
Variable: 8be4df61-93ca-11d2-aa0d-00e098032b8c:MemoryConfii (EFI Global)
StartID:  55aa (Valid)
State:    7f (Normal)
Unknown8: 00
Attr:     00000003 (NON_VOLATILE, BOOT_SERVICE_ACCESS)
NameSize: 26
DataSize: 1990
DataType: looks like Binary
Data:
00000000: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000010: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000020: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000030: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000040: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000050: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000060: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000070: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000080: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000090: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000000a0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000000b0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000000c0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000000d0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000000e0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000000f0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
...
...
00000100: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000110: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000007a0: 01 00 00 00 01 01 11 01 01 00 a4 01 00 00 00 00  ................
000007b0: 00 00 10 01 20 01 01 00 a6 01 00 00 00 00 01 00  .... ...........
000007c0: 00 00 11 01 21 01                                ....!.
--------
--------
Variable: 8be4df61-93ca-11d2-aa0d-00e098032b8c:MemoryConfij (EFI Global)
StartID:  55aa (Valid)
State:    7f (Normal)
Unknown8: 00
Attr:     00000003 (NON_VOLATILE, BOOT_SERVICE_ACCESS)
NameSize: 26
DataSize: 38
DataType: looks like Binary
Data:
00000000: 01 00 a8 01 00 00 00 00 00 00 20 01 ff ff 01 00  .......... .....
00000010: aa 01 00 00 00 00 01 00 34 35 00 00 3a 00 3a 00  ........45..:.:.
00000020: 10 00 20 00 00 00                                .. ...
--------
--------
...
...
```

<br>

Examples test_nvram shell script 18-11-2023
Hardware-Descriptor (base_xx)
```
-------------------------------------------------------------------
4 Fsys store/0 overrides
-------------------------------------------------------------------
Type: Fsys entry
Subtype: Normal
Fixed: Yes
Base: 14800Bh
Header address: FFD4800Bh
Data address: FFD48017h
Offset: Bh
Full size: 67Fh (1663)
Header size: Ch (12)
Body size: 673h (1651)
===================================================================
00000000: 096f 7665 7272 6964 6573 7306            .overridess.
overridess
-------------------------------------------------------------------
ADD_DEVICE    ()    [class="USBPort",type="USB 2.0",location="top-front",speed="480",uhci-id="0x5d100000",ehci-id="0xfd500000"]
ADD_DEVICE    ()    [class="USBPort",type="USB 2.0",location="bottom-front",speed="480",uhci-id="0x3a200000",ehci-id="0xfa400000"]
ADD_DEVICE    ()    [class="USBPort",type="USB 2.0",location="right-rear",speed="480",uhci-id="0x3d100000",ehci-id="0xfd300000"]
ADD_DEVICE    ()    [class="USBPort",type="USB 2.0",location="center-rear",speed="480",uhci-id="0x1a200000",ehci-id="0xfa200000"]
ADD_DEVICE    ()    [class="USBPort",type="USB 2.0",location="left-rear",speed="480",uhci-id="0x1d100000",ehci-id="0xfd100000"]
ADD_DEVICE    ()    [class="FireWirePort",location="rear-right",max-speed="800",port-id="0x01",phy-id="0x00"]
ADD_DEVICE    ()    [class="FireWirePort",location="rear-left",max-speed="800",port-id="0x02",phy-id="0x00"]
ADD_DEVICE    ()    [class="FireWirePort",location="front-top",max-speed="800",port-id="0x01",phy-id="0x01"]
ADD_DEVICE    ()    [class="FireWirePort",location="front-bottom",max-speed="800",port-id="0x02",phy-id="0x01"]
SET_PROPERTY    (class="Processor")    [max-prochots="10000",ptype="iCore7"]
SET_PROPERTY    (class="Sensor"&location="ICAC")    [low-limit="0.1",high-limit="140",type="Current",description="CPU A, Core Low Side (Vcore) Current"]
SET_PROPERTY    (class="Sensor"&location="ICBC")    [low-limit="0.1",high-limit="140",type="Current",description="CPU B, Core Low Side (Vcore) Current"]
SET_PROPERTY    (class="Sensor"&location="Ie1S")    [low-limit="0",high-limit="18",type="Current",description="PCIe Slot 1, 12V Current"]
SET_PROPERTY    (class="Sensor"&location="Ie2S")    [low-limit="0",high-limit="18",type="Current",description="PCIe Slot 2, 12V Current"]
SET_PROPERTY    (class="Sensor"&location="Ie3S")    [low-limit="0",high-limit="18",type="Current",description="PCIe Slot 3, 12V Current"]
SET_PROPERTY    (class="Sensor"&location="Ie4S")    [low-limit="0",high-limit="18",type="Current",description="PCIe Slot 4, 12V Current"]
SET_PROPERTY    (class="Sensor"&location="IeAS")    [low-limit="0",high-limit="18",type="Current",description="PCIe BoostA, 12V Current"]
SET_PROPERTY    (class="Sensor"&location="IeBS")    [low-limit="0",high-limit="18",type="Current",description="PCIe BoostB, 12V Current"]
SET_PROPERTY    (class="Sensor"&location="IH1Z")    [low-limit="0",high-limit="2",type="Current",description="HDD1, 12V Current"]
SET_PROPERTY    (class="Sensor"&location="IH2Z")    [low-limit="0",high-limit="2",type="Current",description="HDD2, 12V Current"]
SET_PROPERTY    (class="Sensor"&location="IH3Z")    [low-limit="0",high-limit="2",type="Current",description="HDD3, 12V Current"]
SET_PROPERTY    (class="Sensor"&location="IH4Z")    [low-limit="0",high-limit="2",type="Current",description="HDD4, 12V Current"]
SET_PROPERTY    (class="Sensor"&location="IO0Z")    [low-limit="0",high-limit="3",type="Current",description="ODD, 12V Current"]
SET_PROPERTY    (class="Sensor"&location="IH5Z")    [low-limit="0",high-limit="12",type="Current",description="HDD+ODD, 5V Current"]
SET_PROPERTY    (class="Sensor"&location="IMAS")    [low-limit="0.1",high-limit="50",type="Current",description="DIMM, PP1V5_S3_MEMA Current"]
SET_PROPERTY    (class="Sensor"&location="IMBS")    [low-limit="0.1",high-limit="50",type="Current",description="DIMM, PP1V5_S3_MEMB Current"]
SET_PROPERTY    (class="Sensor"&location="IN0C")    [low-limit="1",high-limit="40",type="Current",description="IOH Core, PP1V1_S0_IOH Northbridge Current"]
SET_PROPERTY    (class="Sensor"&location="Ip0C")    [low-limit="1",high-limit="80",type="Current",description="PSU, 12V Current (PSMI)"]
SET_PROPERTY    (class="Sensor"&location="ICAB")    [low-limit="0.1",high-limit="40",type="Current",description="PVTT, CPUA Current"]
SET_PROPERTY    (class="Sensor"&location="ICBB")    [low-limit="0.1",high-limit="40",type="Current",description="PVTT, CPUB Current"]
SET_PROPERTY    (class="Sensor"&location="IS1C")    [low-limit="0.25",high-limit="5.0",type="Current",description="PP1V05_S0_SB Current"]
SET_PROPERTY    (class="Sensor"&location="IS2C")    [low-limit="0.25",high-limit="2.3",type="Current",description="PP1V5_S0_SB Current"]
SET_PROPERTY    (class="Sensor"&location="Ip1M")    [low-limit="0.5",high-limit="18",type="Current",description="PP12V_S0 CPUA 240VA Main Current"]
SET_PROPERTY    (class="Sensor"&location="Ip2M")    [low-limit="0",high-limit="18",type="Current",description="PP12V_S0 CPUB 240VA Main Current"]
SET_PROPERTY    (class="Sensor"&location="Ip3M")    [low-limit="0.5",high-limit="18",type="Current",description="PP12V_S0 MEMA 240VA Main Current"]
SET_PROPERTY    (class="Sensor"&location="Ip4M")    [low-limit="0",high-limit="18",type="Current",description="PP12V_S0 MEMB 240VA Main Current"]
SET_PROPERTY    (class="Sensor"&location="Ip5M")    [low-limit="1",high-limit="18",type="Current",description="PP12V_S0 MLB1 240VA Main Current"]
SET_PROPERTY    (class="Sensor"&location="Ip6M")    [low-limit="1",high-limit="18",type="Current",description="PP12V_S0 MLB2 240VA Main Current"]
SET_PROPERTY    (class="Sensor"&location="Ip7M")    [low-limit="0",high-limit="18",type="Current",description="PP12V_S0 PCIE1 240VA Main Current"]
SET_PROPERTY    (class="Sensor"&location="Ip8M")    [low-limit="0",high-limit="18",type="Current",description="PP12V_S0 PCIE2 240VA Main Current"]
SET_PROPERTY    (class="Sensor"&location="TA0P")    [low-limit="5",high-limit="45",type="Temperature",description="System Ambient Temperature"]
SET_PROPERTY    (class="Sensor"&location="TCAC")    [low-limit="1",high-limit="85",type="Temperature",description="CPU A, Core 0 Relative Temperature to ProcHot (PECI)"]
SET_PROPERTY    (class="Sensor"&location="TCAD")    [low-limit="5",high-limit="95",type="Temperature",description="Temperature, CPU A Tdiode"]
SET_PROPERTY    (class="Sensor"&location="TCBC")    [low-limit="1",high-limit="85",type="Temperature",description="CPU B, Core 0 Relative Temperature to ProcHot (PECI)"]
SET_PROPERTY    (class="Sensor"&location="TCBD")    [low-limit="5",high-limit="95",type="Temperature",description="Temperature, CPU B Tdiode"]
SET_PROPERTY    (class="Sensor"&location="TCAH")    [low-limit="5",high-limit="85",type="Temperature",description="CPU A, HeatSink Temperature"]
SET_PROPERTY    (class="Sensor"&location="TCBH")    [low-limit="5",high-limit="85",type="Temperature",description="CPU B, HeatSink Temperature"]
SET_PROPERTY    (class="Sensor"&location="TH1P")    [low-limit="5",high-limit="50",type="Temperature",description="Drive Bay 1, HDD Temperature (On Drive Carrier)"]
SET_PROPERTY    (class="Sensor"&location="TH2P")    [low-limit="5",high-limit="50",type="Temperature",description="Drive Bay 2, HDD Temperature (On Drive Carrier)"]
SET_PROPERTY    (class="Sensor"&location="TH3P")    [low-limit="5",high-limit="50",type="Temperature",description="Drive Bay 3, HDD Temperature (On Drive Carrier)"]
SET_PROPERTY    (class="Sensor"&location="TH4P")    [low-limit="5",high-limit="50",type="Temperature",description="Drive Bay 4, HDD Temperature (On Drive Carrier)"]
SET_PROPERTY    (class="Sensor"&location="TM1P")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM Proximity 1 Temperature (On Riser)"]
SET_PROPERTY    (class="Sensor"&location="TM2P")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM Proximity 2 Temperature (On Riser)"]
SET_PROPERTY    (class="Sensor"&location="TM3P")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM Proximity 3 Temperature (On Riser)"]
SET_PROPERTY    (class="Sensor"&location="TM4P")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM Proximity 4 Temperature (On Riser)"]
SET_PROPERTY    (class="Sensor"&location="TM5P")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM Proximity 5 Temperature (On Riser)"]
SET_PROPERTY    (class="Sensor"&location="TM6P")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM Proximity 6 Temperature (On Riser)"]
SET_PROPERTY    (class="Sensor"&location="TM7P")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM Proximity 7 Temperature (On Riser)"]
SET_PROPERTY    (class="Sensor"&location="TM8P")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM Proximity 8 Temperature (On Riser)"]
SET_PROPERTY    (class="Sensor"&location="TMA1")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM, CPUA, SLOT1, CHA - SPD Temperature"]
SET_PROPERTY    (class="Sensor"&location="TMA2")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM, CPUA, SLOT2, CHB - SPD Temperature"]
SET_PROPERTY    (class="Sensor"&location="TMA3")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM, CPUA, SLOT3, CHC - SPD Temperature"]
SET_PROPERTY    (class="Sensor"&location="TMA4")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM, CPUA, SLOT4, CHC - SPD Temperature"]
SET_PROPERTY    (class="Sensor"&location="TMB1")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM, CPUB, SLOT5, CHA - SPD Temperature"]
SET_PROPERTY    (class="Sensor"&location="TMB2")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM, CPUB, SLOT6, CHB - SPD Temperature"]
SET_PROPERTY    (class="Sensor"&location="TMB3")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM, CPUB, SLOT7, CHC - SPD Temperature"]
SET_PROPERTY    (class="Sensor"&location="TMB4")    [low-limit="5",high-limit="80",type="Temperature",description="DIMM, CPUB, SLOT8, CHC - SPD Temperature"]
SET_PROPERTY    (class="Sensor"&location="TN0D")    [low-limit="5",high-limit="95",type="Temperature",description="Temperature, IOH Tdiode"]
SET_PROPERTY    (class="Sensor"&location="TN0H")    [low-limit="5",high-limit="75",type="Temperature",description="IOH, HeatSink Temperature"]
SET_PROPERTY    (class="Sensor"&location="Tp0C")    [low-limit="5",high-limit="100",type="Temperature",description="PS, AC/DC Supply Temperature 1"]
SET_PROPERTY    (class="Sensor"&location="Tp1C")    [low-limit="5",high-limit="100",type="Temperature",description="PS, AC/DC Supply Temperature 2"]
SET_PROPERTY    (class="Sensor"&location="Te1S")    [low-limit="5",high-limit="95",type="Temperature",description="PCIE slot 1 Temperature"]
SET_PROPERTY    (class="Sensor"&location="Te2S")    [low-limit="5",high-limit="95",type="Temperature",description="PCIE slot 2 Temperature"]
SET_PROPERTY    (class="Sensor"&location="Te3S")    [low-limit="5",high-limit="95",type="Temperature",description="PCIE slot 3 Temperature"]
SET_PROPERTY    (class="Sensor"&location="Te4S")    [low-limit="5",high-limit="95",type="Temperature",description="PCIE slot 4 Temperature"]
SET_PROPERTY    (class="Sensor"&location="Te5S")    [low-limit="5",high-limit="95",type="Temperature",description="PCIE RAID card Temperature"]
SET_PROPERTY    (class="Sensor"&location="VCAC")    [low-limit="0.6",high-limit="1.3",type="Voltage",description="CPU A, Core Voltage"]
SET_PROPERTY    (class="Sensor"&location="VCBC")    [low-limit="0.6",high-limit="1.3",type="Voltage",description="CPU B, Core Voltage"]
SET_PROPERTY    (class="Sensor"&location="Ve1S")    [low-limit="11.4",high-limit="12.6",type="Voltage",description="PCIe Slot 1, 12V Voltage"]
SET_PROPERTY    (class="Sensor"&location="Ve2S")    [low-limit="11.4",high-limit="12.6",type="Voltage",description="PCIe Slot 2, 12V Voltage"]
SET_PROPERTY    (class="Sensor"&location="Ve3S")    [low-limit="11.4",high-limit="12.6",type="Voltage",description="PCIe Slot 3, 12V Voltage"]
SET_PROPERTY    (class="Sensor"&location="Ve4S")    [low-limit="11.4",high-limit="12.6",type="Voltage",description="PCIe Slot 4, 12V Voltage"]
SET_PROPERTY    (class="Sensor"&location="VeAS")    [low-limit="11.4",high-limit="12.6",type="Voltage",description="PCIe BoostA, 12V Voltage"]
SET_PROPERTY    (class="Sensor"&location="VeBS")    [low-limit="11.4",high-limit="12.6",type="Voltage",description="PCIe BoostB, 12V Voltage"]
SET_PROPERTY    (class="Sensor"&location="VH1Z")    [low-limit="11.4",high-limit="12.6",type="Voltage",description="HDD1, 12V Voltage"]
SET_PROPERTY    (class="Sensor"&location="VH2Z")    [low-limit="11.4",high-limit="12.6",type="Voltage",description="HDD2, 12V Voltage"]
SET_PROPERTY    (class="Sensor"&location="VH3Z")    [low-limit="11.4",high-limit="12.6",type="Voltage",description="HDD3, 12V Voltage"]
SET_PROPERTY    (class="Sensor"&location="VH4Z")    [low-limit="11.4",high-limit="12.6",type="Voltage",description="HDD4, 12V Voltage"]
SET_PROPERTY    (class="Sensor"&location="VO0Z")    [low-limit="11.4",high-limit="12.6",type="Voltage",description="ODD, 12V Voltage"]
SET_PROPERTY    (class="Sensor"&location="VH5Z")    [low-limit="4.5",high-limit="5.5",type="Voltage",description="HDD+ODD, 5V Voltage"]
SET_PROPERTY    (class="Sensor"&location="VM1S")    [low-limit="1.43",high-limit="1.57",type="Voltage",description="PP1V5_S3_MEMA Voltage"]
SET_PROPERTY    (class="Sensor"&location="VM2S")    [low-limit="1.43",high-limit="1.57",type="Voltage",description="PP1V5_S3_MEMB Voltage"]
SET_PROPERTY    (class="Sensor"&location="VN0C")    [low-limit="1.07",high-limit="1.13",type="Voltage",description="PP1V1_S0_IOH Northbridge Voltage"]
SET_PROPERTY    (class="Sensor"&location="Vp0C")    [low-limit="11.4",high-limit="12.6",type="Voltage",description="PSU, 12V Voltage"]
SET_PROPERTY    (class="Sensor"&location="VCAB")    [low-limit="1.00",high-limit="1.30",type="Voltage",description="PPVTT_S0_CPUA Voltage"]
SET_PROPERTY    (class="Sensor"&location="VCBB")    [low-limit="1.00",high-limit="1.30",type="Voltage",description="PPVTT_S0_CPUB Voltage"]
SET_PROPERTY    (class="Sensor"&location="VS1C")    [low-limit="1.00",high-limit="1.10",type="Voltage",description="PP1V05_S0_SB Voltage"]
SET_PROPERTY    (class="Sensor"&location="VS2C")    [low-limit="1.43",high-limit="1.58",type="Voltage",description="PP1V5_S0_SB Voltage"]
SET_PROPERTY    (class="Sensor"&location="VS8C")    [low-limit="3.14",high-limit="3.47",type="Voltage",description="PP3V3_S5 Voltage"]
REMOVE_DEVICE    (class="Sensor")    (class="Sensor"&type="?")
REMOVE_DEVICE    !(class="Processor"&location="1")    (class="Sensor"&location="VCBB")
REMOVE_DEVICE    !(class="Processor"&location="1")    (class="Sensor"&location="VCBC")
REMOVE_DEVICE    !(class="Processor"&location="1")    (class="Sensor"&location="ICBB")
REMOVE_DEVICE    !(class="Processor"&location="1")    (class="Sensor"&location="ICBC")
REMOVE_DEVICE    !(class="Processor"&location="1")    (class="Sensor"&location="IMBS")
REMOVE_DEVICE    (class="Memory"&location="DIMM 1"&ecc="FALSE")    (class="Sensor"&location="TMA1")
REMOVE_DEVICE    (class="Memory"&location="DIMM 2"&ecc="FALSE")    (class="Sensor"&location="TMA2")
REMOVE_DEVICE    (class="Memory"&location="DIMM 3"&ecc="FALSE")    (class="Sensor"&location="TMA3")
REMOVE_DEVICE    (class="Memory"&location="DIMM 4"&ecc="FALSE")    (class="Sensor"&location="TMA4")
REMOVE_DEVICE    (class="Memory"&location="DIMM 5"&ecc="FALSE")    (class="Sensor"&location="TMB1")
REMOVE_DEVICE    (class="Memory"&location="DIMM 6"&ecc="FALSE")    (class="Sensor"&location="TMB2")
REMOVE_DEVICE    (class="Memory"&location="DIMM 7"&ecc="FALSE")    (class="Sensor"&location="TMB3")
REMOVE_DEVICE    (class="Memory"&location="DIMM 8"&ecc="FALSE")    (class="Sensor"&location="TMB4")
===================================================================

-------------------------------------------------------------------
4 Fsys store/1 override-version
-------------------------------------------------------------------
Type: Fsys entry
Subtype: Normal
Fixed: Yes
Base: 14868Ah
Header address: FFD4868Ah
Data address: FFD4869Dh
Offset: 68Ah
Full size: 1Bh (27)
Header size: 13h (19)
Body size: 8h (8)
===================================================================
00000000: 106f 7665 7272 6964 652d 7665 7273 696f  .override-versio
00000010: 6e08 00                                  n..
override-version
-------------------------------------------------------------------
00000000: 4261 7365 5f32 3100                      Base_21.
Base_21
===================================================================
```

<br>

IASInstallPhaseList
```
-------------------------------------------------------------------
0 VSS store/97 IASInstallPhaseList
-------------------------------------------------------------------
Type: VSS entry
Subtype: Standard
Text: IASInstallPhaseList
Fixed: Yes
Base: 12D8F1h
Header address: FFD2D8F1h
Data address: FFD2D939h
Offset: D8A9h
Variable GUID: 4D1EDE05-38C7-4A6A-9CC6-4BCCA8B38C14
Full size: 280h (640)
Header size: 48h (72)
Body size: 238h (568)
State: 7Fh
Reserved: 00h
Attributes: 00000007h (NonVolatile, BootService, Runtime)
===================================================================
00000000: aa55 7f00 0700 0000 2800 0000 3802 0000  .U......(...8...
00000010: 05de 1e4d c738 6a4a 9cc6 4bcc a8b3 8c14  ...M.8jJ..K.....
00000020: 4900 4100 5300 4900 6e00 7300 7400 6100  I.A.S.I.n.s.t.a.
00000030: 6c00 6c00 5000 6800 6100 7300 6500 4c00  l.l.P.h.a.s.e.L.
00000040: 6900 7300 7400 0000                      i.s.t...
U(8M8jJKIASInstallPhaseList
-------------------------------------------------------------------
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<array>
<dict>
<key>ConclusionDelay</key>
<integer>0</integer>
<key>InstallPhase</key>
<string>Boot 1</string>
<key>InstallPhasePercentageKey</key>
<integer>58</integer>
</dict>
<dict>
<key>ConclusionDelay</key>
<integer>0</integer>
<key>InstallPhase</key>
<string>Language Chooser</string>
<key>InstallPhasePercentageKey</key>
<integer>42</integer>
</dict>
</array>
</plist>
===================================================================
```

LBSB / BD Sector
```
-------------------------------------------------------------------
LBSN sector
-------------------------------------------------------------------
Type: Section
Subtype: Raw
Fixed: No
Base: 3FFEF0h
Header address: FFFFFEF0h
Data address: FFFFFEF4h
Offset: E90h
Type: 19h
Full size: 110h (272)
Header size: 4h (4)
Body size: 10Ch (268)
===================================================================
00000000: 1001 0019                                ....
-------------------------------------------------------------------
00000000: 0000 0000 0000 0000 0000 0000 ea78 ca39  .............x.9
00000010: 2664 848b xxxx xxxx xxxx xxxx xxxx xxxx  &d..J5xxxxxxxxxx
00000020: 4120 2020 2020 ffff ffff ffff ffff ffff  A     ..........
00000030: ffff ffff ffff ffff ffff ffff ffff ffff  ................
*
00000050: ffff ffff ffff ffff ffff ffff xxxx xxxx  ............xxxx
00000060: xxxx xxxx xxxx xxxx xxxx xxxx 0fff ffff  xxxxxxxx........
00000070: ffff ffff ffff ffff ffff ffff 01ff ffff  ................
00000080: ffff ffff ffff ffff ffff ffff 0000 0000  ................
00000090: 0000 0000 0000 0000 0000 0000 0000 0000  ................
*
000000d0: 0000 0000 0000 0000 0000 0000 bf50 41eb  .............PA.
000000e0: 1d00 0000 0000 0000 0000 0000 ffff ffff  ................
000000f0: ffff ffff ffff ffff e802 ffff 0f09 e9fb  ................
00000100: f200 0000 7856 3412 0000 ffff            ....xV4.....
x9&dJxxxxxxxxBH9A     xxxxxxxxxxxxxPAxV4
===================================================================
```
