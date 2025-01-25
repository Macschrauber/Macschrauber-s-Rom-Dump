### AVX2 Scanner

What is AVX/AVX2?
<br>
An enhaced command set what Xeon CPUs in Mac Pro 1,1 to 6,1 does not have. Mac OS newer than Monterey is compiled with AVX/AVX2 switched on. Also many Apps from that era, on. So knowing, if an App or component contains this code is useful.
<br>

It disassembles the executables and scans for `AVX/AVX2` command strings, it needs installing the `command line tools`.
<br>
<br>
There will be a dialog, asking for this install, if you run the script the first time.
<br>
<br>
Don't mind, if installing the tools will tell, it takes an insane (days) amount of time. This is pretty normal and goes back to a an hour or so.
<br>
<br>
Tested with Massive X, `-c` argument is optional for counting the commands, what is much slower:
<br>
<br>
`% ~/Downloads/avx2 /Library/Audio/Plug-Ins/VST3 -c
Macschrauber's AVX/AVX2 Scanner 16-1-2025 F
Scanning directory: /Library/Audio/Plug-Ins/VST3/Massive X.vst3/
Executable with 6037 AVX and AVX2 commands: /Library/Audio/Plug-Ins/VST3/Massive X.vst3/Contents/PkgInfoMacOS/Massive X
AVX and AVX2 code found.`
<br>
<br>
If copied to `/Downloads`, prepare the bash script:
<br>
`xattr -c ~/Downloads/avx2`
<br>
`chmod +x ~/Downloads/avx2`
<br>
and run the bash script with (Preview as an example):
<br>
`~/Downloads/avx2 /System/Applications/Preview.app`
<br>
The script will need some time, as it disassembles a lot of code.
<br>
<br>
<br>
Also the same bash script, wrapped in a simple AppleScript, for those who prefer a GUI to select what to scan.
<br>
![Screenshot](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_avx2/AVX2%20GUI%201%20select%20type.png)
![Screenshot](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_avx2/AVX2%20GUI%202%20select%20app.png)
![Screenshot](https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/assets/img_avx2/AVX2%20GUI%203%20terminal.png)


