# image

TODO：

* 【记录】lldb命令使用心得：image
* 【已解决】lldb命令使用心得：image
  * 【已解决】lldb命令使用心得：image lookup

---

## image用法举例

* `image list`

```bash
(lldb) image list -o -f | grep AwemeCore
[  0] 0x0000000100adc000 /Users/crifan/Library/Developer/Xcode/DerivedData/Aweme-fswcidjoxbkibsdwekuzlsfcdqls/Build/Products/Debug-iphoneos/Aweme.app/Frameworks/AwemeCore.framework/AwemeCore
```

```bash
(lldb) image list -o -f | grep Module_Framework
[  0] 0x0000000104238000 /Users/crifan/Library/Developer/Xcode/DerivedData/youtube-dvlfmmtvybrcdraorwznbwwepoae/Build/Products/Debug-iphoneos/youtube.app/Frameworks/Module_Framework.framework/Module_Framework
```

```bash
(lldb) image list -o -f | grep Module_Framework
[  0] 0x0000000102b50000 /Users/crifan/Library/Developer/Xcode/DerivedData/youtube-dvlfmmtvybrcdraorwznbwwepoae/Build/Products/Debug-iphoneos/youtube.app/Frameworks/Module_Framework.framework/Module_Framework
(lldb) p/x 0x0000000102b50000 + 0x10470B8
(long) $0 = 0x0000000103b970b8
(lldb) im loo -a 0x0000000103b970b8
      Address: Module_Framework[0x00000000010470b8] (Module_Framework.__TEXT.__text + 17051832)
      Summary: Module_Framework`___lldb_unnamed_symbol12565$$Module_Framework
```

* `image lookup -N functionNameOrClassName`

```bash
(lldb) image lookup -n transformOtherModelToSuit:
1 match found in /Users/crifan/Library/Developer/Xcode/DerivedData/DiDi-cwpbvvyvqmeijmcjnneothzuthsy/Build/Products/Debug-iphonesimulator/DiDi.app/DiDi:
        Address: DiDi[0x0000000100293d60] (DiDi.__TEXT.__text + 2693664)
        Summary: DiDi`+[FW_BetFunction transformOtherModelToSuit:] at FW_BetFunction.m:107
```

* `image lookup -a address` = `im loo -a address`

```bash
(lldb) image lookup -a 0x10f04f810
      Address: AwemeCore[0x000000000c587810] (AwemeCore.__BD_TEXT.__text + 113653776)
      Summary: AwemeCore`___lldb_unnamed_symbol1023498$$AwemeCore + 32

(lldb) im loo -a 0x00000001091694a4
      Address: Module_Framework[0x0000000003df94a4] (Module_Framework.__TEXT.__text + 64967844)
      Summary: Module_Framework`___lldb_unnamed_symbol171165$$Module_Framework
```

* `image lookup -v -a address`

```bash
(lldb) image lookup -v -a 0x10f04f810
      Address: AwemeCore[0x000000000c587810] (AwemeCore.__BD_TEXT.__text + 113653776)
      Summary: AwemeCore`___lldb_unnamed_symbol1023498$$AwemeCore + 32
       Module: file = "/Users/crifan/Library/Developer/Xcode/DerivedData/Aweme-fswcidjoxbkibsdwekuzlsfcdqls/Build/Products/Debug-iphoneos/Aweme.app/Frameworks/AwemeCore.framework/AwemeCore", arch = "arm64"
       Symbol: id = {0x0014c028}, range = [0x000000010f04f7f0-0x000000010f04f844), name="___lldb_unnamed_symbol1023498$$AwemeCore"
```

## image命令语法

```bash
(lldb) help image
Commands for accessing information for one or more target modules.

Syntax: image

'image' is an abbreviation for 'target modules'
(lldb) help target modules
Commands for accessing information for one or more target modules.

Syntax: target modules <sub-command> ...

The following subcommands are supported:

      add          -- Add a new module to the current target's modules.
      dump         -- Commands for dumping information about one or more target
                      modules.
      list         -- List current executable and dependent shared library
                      images.
      load         -- Set the load addresses for one or more sections in a
                      target module.
      lookup       -- Look up information within executable and dependent
                      shared library images.
      search-paths -- Commands for managing module search paths for a target.
      show-unwind  -- Show synthesized unwind instructions for a function.

For more help on any particular subcommand, type 'help <command> <subcommand>'.
```
