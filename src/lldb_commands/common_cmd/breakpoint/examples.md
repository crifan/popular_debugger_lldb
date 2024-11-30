# 举例

* 说明
  * 此处只是列出一些简单的例子
    * 完整教程和例子，详见
      * [iOS逆向之动态调试：断点](https://book.crifan.org/books/ios_re_debug_breakpoint/website/)

## 通过地址添加断点

* 语法
  ```bash
  breakpoint set -a 函数地址

  breakpoint set -a ASLR偏移量 + 静态分析的函数地址

  breakpoint set -a （image list -o -f看到的库的加载的起始地址） +  （IDA等工具）静态分析的函数地址
  ```
* 举例
  ```bash
  (lldb) breakpoint set -a 0x1102d3348
  Breakpoint 54: where = AwemeCore`___lldb_unnamed_symbol1462804$$AwemeCore + 480, address = 0x00000001102d3348
  (lldb) breakpoint list
  Current breakpoints:
  …
  54: address = AwemeCore[0x000000000ee2b348], locations = 1, resolved = 1, hit count = 0
    54.1: where = AwemeCore`___lldb_unnamed_symbol1462804$$AwemeCore + 480, address = 0x00000001102d3348, resolved, hit count = 0
  ```

## b

```bash
(lldb) b 0x10104F698
Breakpoint 4: where = mobileactivationd`getPcrt_1000075C0 + 216, address = 0x000000010104f698
```

## 条件判断

```bash
breakpoint set --name foo --condition '(int)strcmp(y,"hello") == 0'
```

==

```bash
br s -n foo -c '(int)strcmp(y,"hello") == 0'
```