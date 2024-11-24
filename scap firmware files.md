# .scap files info displaying

Since version 19-4-2024, the Dumper displays basic info for firmware capsule .scap files.

<br>
What are .scap files?   

In summary, .scap files are proprietary firmware capsules, used by Apple to securely package and distribute firmware updates for the low-level system components of Mac computers. Extracting and modifying them requires specialized knowledge and tools.

<br>


As some of these firmware files contain information in their header, the Dumper displays them, if possible.  
<br>
![1](https://raw.githubusercontent.com/Macschrauber/Macschrauber-s-Rom-Dump/main/assets/img_Dumper/scap%20files%20readout.png)
You can also rename them with `test_nvram filename.scap -rename`, with the cli tool, based on IBIOSI or EFI version.

```
$ test_nvram /Users/user/temp/unnamed.scap -rename
===================================================
test_nvram_shell_script 18-Apr-2024 by Macschrauber
scanning: /Users/user/temp/unnamed.scap

$IBIOSI$
  MBP91.88Z.F000.B00.1906131919
Apple Rom Version
  Model:        MBP91
  EFI Version:  228.0.0.0.0
  Built by:     root@saumon
  Date:         Thu Jun 13 19:19:31 PDT 2019
  Revision:     228 (B&I)
  ROM Version:  F000_B00
  Build Type:   Official Build, Release
  Compiler:     Apple clang version 3.0 (tags/Apple/clang-211.10.1) (based on LLVM 3.0svn)
  rename /Users/user/temp/unnamed.scap to MBP91_228.0.0.0.0.scap (1 = yes) ?1
renamed to MBP91_228.0.0.0.0.scap
```
