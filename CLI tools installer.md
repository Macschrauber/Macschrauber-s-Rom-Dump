# Installer for using the CLI tools in Terminal
## this is optional if you want to use the additional options `test_nvram` provides
### `test_nvram` is used by the Dumper as well.

This script installs the `test_nvram` shell script as a system-wide available command, along with the helper tools in `/usr/local/bin`  
You can just double click it, below is an example output of `install_test_nvram_cli_tool`.  
```
 ~ % /Volumes/Macschrauber\'s\ CMP\ Rom\ Dump/Readme\ \&\ other\ tools/Installer\ for\ the\ CLI\ tools\ \(optional\)/install_test_nvram_cli_tool
=============================================================================
Installer for Macschrauber's test_nvram CLI command and accompanying tools.
This installer may require admin privileges and prompt you for your password.
Using either the .App contents in same directory or 2 levels back.
Or you provide the App path as an argument
like -/my/path/RomDump\ Macschrauber.app.
=============================================================================
Found RomDump Macschrauber.app.
Need administrator password for copying the cli tools to /usr/local/bin
Password:
test_nvram -> /usr/local/bin/test_nvram
findhex -> /usr/local/bin/findhex
macserial -> /usr/local/bin/macserial

/usr/local/bin/UEFIExtract not overwritten
/usr/local/bin/scanvss not overwritten
/usr/local/bin/flashrom097r1711 not overwritten
/usr/local/bin/gfxutil not overwritten
/usr/local/bin/gfxutil180b not overwritten

~/Library/Application Support/Macschrauber exists

~/Library/Application Support/Macschrauber/DirectHW.kext exists

done
```
Examples of what can be done with `test_nvram` are in:  
https://github.com/Macschrauber/Macschrauber-s-Rom-Dump/blob/main/shell%20script%20examples.md
