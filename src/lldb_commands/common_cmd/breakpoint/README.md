# breakpoint

TODO：

* 【记录】lldb命令使用心得：breakpoint
* 【已解决】Xcode中lldb中b list不是breakpoint list
* 【未解决】Xcode中无法给下一行将要运行的汇编指令加断点
* 【已解决】XCode中如何给符号断点加上判断条件
* 【未解决】XCode和lldb如何根据函数地址加断点

---

* 详见独立子教程
  * [iOS逆向之动态调试：断点](https://book.crifan.org/books/ios_re_debug_breakpoint/website/)

## breakpoint举例

```bash
breakpoint set -a 函数地址

breakpoint set -a ASLR偏移量 + 静态分析的函数地址

breakpoint set -a （image list -o -f看到的库的加载的起始地址） +  （IDA等工具）静态分析的函数地址
```

```bash
(lldb) breakpoint set -a 0x1102d3348
Breakpoint 54: where = AwemeCore`___lldb_unnamed_symbol1462804$$AwemeCore + 480, address = 0x00000001102d3348
(lldb) breakpoint list
Current breakpoints:
…
54: address = AwemeCore[0x000000000ee2b348], locations = 1, resolved = 1, hit count = 0
  54.1: where = AwemeCore`___lldb_unnamed_symbol1462804$$AwemeCore + 480, address = 0x00000001102d3348, resolved, hit count = 0
```

```bash
breakpoint set --name foo --condition '(int)strcmp(y,"hello") == 0'
```

==

```bash
br s -n foo -c '(int)strcmp(y,"hello") == 0'
```
