# breakpoint

* 概述
  * 用`b`或`breakpoint`加断点
    * 添加方式
      * 通过地址
        ```bash
        b <someAddress>
        breakpoint set -a <someAddress>
        breakpoint set --address <someAddress>
        ```
        * 举例
          ```bash
          breakpoint set -a 0x1102d3348
          breakpoint set --address 0x1830c6a80
          ```
      * 通过函数名
        ```bash
        b <someFunctionName>
        breakpoint set -n <someFunctionName>
        breakpoint set --name <someFunctionName>
        ```
        * 举例
          ```bash
          b objc_alloc_init
          breakpoint set --name "-[NSString stringByAppendingString:]"
          breakpoint set --name "-[AAUISignInController _performAuthenticationForAccount:serviceType:inViewController:completion:]"
          ```
    * 额外条件 = 辅助条件
      * 条件判断
        ```bash
        breakpoint set --name <someFunctionName> --condition <someConditionExpression>
        ```
        * 举例
          ```bash
          breakpoint set --name foo --condition '(int)strcmp(y,"hello") == 0'
          br s -n foo -c '(int)strcmp(y,"hello") == 0'
          br s -n "objc_alloc_init" -c '(bool)[NSStringFromClass($x0) isEqualToString: @"AADeviceInfo"]'
          br s -n "objc_alloc_init" -c '(int)strcmp((char *)class_getName($x0),"AADeviceInfo")==0'
          br s -n "objc_alloc_init" -c '(int)strcmp((char *)object_getClassName($x0),"AADeviceInfo")==0'
          ```
      * 指定模块=库
        ```bash
        br s -n <someFunctionName> -s <libFileName>
        br s -n <someFunctionName> --shlib <libFileName>
        ```
        * 举例
          ```bash
          br s -n "___lldb_unnamed_symbol972" -s libMobileGestalt.dylib
          br s -n "___lldb_unnamed_symbol972" --shlib libMobileGestalt.dylib
          ```
    * 语法
      * [breakpoint的help语法 · iOS逆向之动态调试：断点](https://book.crifan.org/books/ios_re_debug_breakpoint/website/cmd_lldb/br_help.html)
* 详解
  * [iOS逆向之动态调试：断点](https://book.crifan.org/books/ios_re_debug_breakpoint/website/)
