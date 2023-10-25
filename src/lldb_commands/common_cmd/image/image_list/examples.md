# image list举例

## Aweme

```bash
(lldb) image list -o -f
[  0] 0x0000000004874000 /private/var/containers/Bundle/Application/9AB25481-0AD3-435C-A02E-68F9623535BB/Aweme.app/Aweme(0x0000000104874000)
[  1] 0x0000000104b78000 /Users/crifan/Library/Developer/Xcode/iOS DeviceSupport/13.4.1 (17E262)/Symbols/usr/lib/dyld
```
* 另外某次的类似例子的截图
  * ![xcode_lldb_image_list_o_f_aweme_1](../../../../assets/img/xcode_lldb_image_list_o_f_aweme_1.png)
  * ![xcode_lldb_image_list_o_f_aweme_2](../../../../assets/img/xcode_lldb_image_list_o_f_aweme_2.png)
* 说明
  * 第一个是app本身的二进制
    * `/private/var/containers/Bundle/Application/9AB25481-0AD3-435C-A02E-68F9623535BB/Aweme.app/Aweme`
      * 此处`ALSR`的基地址是：`0x0000000004874000`
* 第二个是`dyld`
    * `/Users/crifan/Library/Developer/Xcode/iOS DeviceSupport/13.4.1 (17E262)/Symbols/usr/lib/dyld`

## AwemeCore

```bash
(lldb) image list -o -f | grep AwemeCore
[  0] 0x0000000100adc000 /Users/crifan/Library/Developer/Xcode/DerivedData/Aweme-fswcidjoxbkibsdwekuzlsfcdqls/Build/Products/Debug-iphoneos/Aweme.app/Frameworks/AwemeCore.framework/AwemeCore
```

## Module_Framework

* 带`grep`的

```bash
(lldb) image list -o -f | grep Module_Framework
[  0] 0x0000000104238000 /Users/crifan/Library/Developer/Xcode/DerivedData/youtube-dvlfmmtvybrcdraorwznbwwepoae/Build/Products/Debug-iphoneos/youtube.app/Frameworks/Module_Framework.framework/Module_Framework
```

* 带`grep`输出后，继续计算函数地址和查找相关函数

```bash
(lldb) image list -o -f | grep Module_Framework
[  0] 0x0000000102b50000 /Users/crifan/Library/Developer/Xcode/DerivedData/youtube-dvlfmmtvybrcdraorwznbwwepoae/Build/Products/Debug-iphoneos/youtube.app/Frameworks/Module_Framework.framework/Module_Framework
(lldb) p/x 0x0000000102b50000 + 0x10470B8
(long) $0 = 0x0000000103b970b8
(lldb) im loo -a 0x0000000103b970b8
      Address: Module_Framework[0x00000000010470b8] (Module_Framework.__TEXT.__text + 17051832)
      Summary: Module_Framework`___lldb_unnamed_symbol12565$$Module_Framework
```
