If you encounter an error regarding an unknown developer when attempting to open the Dumper, macOS displays a message stating: 'macOS cannot verify the developer of.'

To allow the system to open the Dumper, perform a Ctrl-click on it and select <open>.


If you receive a message indicating that either the app or the disk image (.dmg) is damaged:

If this dialog persists, you can resolve it using Terminal with the following command:
xattr -cr "/path/to/RomDump Macschrauber.app"



Alternatively, you can:

Execute the script named "RomDump Macschrauber is damaged fix."
Use the included Downloader to obtain a copy with no quarantine flag set.

in case the Downloader is not included:
https://www.dropbox.com/s/t5k7j4gxj8n9pj2/Download%20Macschrauber%27s%20CMP%20Rom%20Dump.zip?dl=1 


These issues arise from the presence of Flashrom in the package, which is flagged as potentially harmful by some malware scanners.

——————————————————



Yes, you can indeed disable parts of SIP while leaving others enabled.

If you run csrutil status, even while booted normally, you will see the component parts of it. Each of these can be selectively disabled by running one of the following commands while booted into Recovery mode:

	•	csrutil enable --no-internal
	•	csrutil enable --without kext
	•	csrutil enable --without fs
	•	csrutil enable --without debug
	•	csrutil enable --without dtrace
	•	csrutil enable --without nvram

You can disable two or more components by structuring the command as follows:
csrutil enable --without kext  --without nvram


for running RomDump Macschrauber csrutil enable --without kext is enough



———————————————————————————————————————————————

Special thanks to:
	•	tsialex for investigating the Mac bootrom and sharing the information.
 
	•	Syncretic for scanvss.
 
	•	LongSoft for UEFIExtract.
 
	•	joevt for rebuilding DirectHW.kext for all Mac OS versions.
 
	•	startergo for help with compiling issues.
 
	•	Dayo for assistance with English grammar and spelling, as well as his excellent RefindPlus bootloader.
 
	•	Takaaki Naganoya@Piyomaru Software for the scrollable dialog "displaytextview"


———————————————————————————————————————————————


I have a youtube channel: https://www.youtube.com/channel/UCx5HT0rwmVaKNraMHW-Z3bQ


If you require assistance with a damaged boot ROM, feel free to contact me in English or German at tigerpost@gmx.de
