# memory

TODO：

* 【记录】lldb命令使用心得：memory
* 【已解决】iOS逆向：Xcode中lldb从内存中导出二进制数据

---

## memory举例

### 查看内存中的数据

```bash
(lldb) x/16gx 0x0000000109117438
0x109117438: 0x0000000000000000 0x0000000000000000
0x109117448: 0x00000001052b6a88 0x00000001052b6ad8
0x109117458: 0x000000010521b03c 0x00000001052b5758
0x109117468: 0x00000001052b5850 0x00000001052b5980
0x109117478: 0x00000001052b5ab0 0x00000001052b6638
0x109117488: 0x00000001052b6674 0x000000010521b40c
0x109117498: 0x00000001052b65fc 0x00000001052b6a10
0x1091174a8: 0x00000001052b6a4c 0x00000001052b5a74
```

### （把内存中某段数据）导出到文件

```bash
memory read --binary --force --outfile /Users/crifan/dev/tmp/lldb_mem_dump/akd_func2540_arm64e.bin 0x10485d98c 0x1048600dc
```

* 参数解释
  * `--outfile /Users/crifan/dev/tmp/lldb_mem_dump/akd_func2540_arm64e.bin`
    * 注意：此处输出文件路径是PC端（此处Mac端），不是移动端（iPhone端）
  * `--binary`
    * 以二进制格式导出
      * 否则默认以txt文本格式导出
  * `--force`
    * 强制导出大量数据
    * 注：
      * 默认最多只能导出`1K`=`1024`个字节
      * 不加此参数，会出现警告
        ```bash
        error: Normally, 'memory read' will not read over 1024 bytes of data.
        error: Please use --force to override this restriction just once.
        error: or set target.max-memory-read-size if you will often need a larger limit.
        ```
      * 如果经常导出（超过`1K`的）大量数据，则再去设置：
        ```bash
        set target.max-memory-read-size
        ```

## memory语法

```bash
(lldb) help memory
Commands for operating on memory in the current target process.

Syntax: memory <subcommand> [<subcommand-options>]

The following subcommands are supported:

      find    -- Find a value in the memory of the current target process.
      history -- Print recorded stack traces for allocation/deallocation events
                 associated with an address.
      read    -- Read from the memory of the current target process.
      region  -- Get information on the memory region containing an address in
                 the current target process.
      write   -- Write to the memory of the current target process.

For more help on any particular subcommand, type 'help <command> <subcommand>'.
```

### memory read语法

```bash
(lldb) help memory read
Read from the memory of the current target process.

Syntax: memory read <cmd-options> <address-expression> [<address-expression>]

Command Options Usage:
  memory read [-drd] [-f <format>] [-c <count>] [-G <gdb-format>] [-s <byte-size>] [-l <number-per-line>] [-o <filename>] <address-expression> [<address-expression>]
  memory read [-dbrd] [-f <format>] [-c <count>] [-s <byte-size>] [-o <filename>] <address-expression> [<address-expression>]
  memory read [-AFLORTdrd] -t <name> [-f <format>] [-c <count>] [-G <gdb-format>] [-E <count>] [-o <filename>] [-d <none>] [-S <boolean>] [-D <count>] [-P <count>] [-Y[<count>]] [-V <boolean>] [-Z <count>] <address-expression> [<address-expression>]
  memory read -t <name> [-x <source-language>] <address-expression> [<address-expression>]

       -A ( --show-all-children )
            Ignore the upper bound on the number of children to show.

       -D <count> ( --depth <count> )
            Set the max recurse depth when dumping aggregate types (default is
            infinity).

       -E <count> ( --offset <count> )
            How many elements of the specified type to skip before starting to
            display data.

       -F ( --flat )
            Display results in a flat format that uses expression paths for
            each variable or member.

       -G <gdb-format> ( --gdb-format <gdb-format> )
            Specify a format using a GDB format specifier string.

       -L ( --location )
            Show variable location information.

       -O ( --object-description )
            Display using a language-specific description API, if possible.

       -P <count> ( --ptr-depth <count> )
            The number of pointers to be traversed when dumping values (default
            is zero).

       -R ( --raw-output )
            Don't use formatting options.

       -S <boolean> ( --synthetic-type <boolean> )
            Show the object obeying its synthetic provider, if available.

       -T ( --show-types )
            Show variable types when dumping values.

       -V <boolean> ( --validate <boolean> )
            Show results of type validators.

       -Y[<count>] ( --no-summary-depth=[<count>] )
            Set the depth at which omitting summary information stops (default
            is 1).

       -Z <count> ( --element-count <count> )
            Treat the result of the expression as if its type is an array of
            this many values.

       -b ( --binary )
            If true, memory will be saved as binary. If false, the memory is
            saved save as an ASCII dump that uses the format, size, count and
            number per line settings.

       -c <count> ( --count <count> )
            The number of total items to display.

       -d <none> ( --dynamic-type <none> )
            Show the object as its full dynamic type, not its static type, if
            available.
            Values: no-dynamic-values | run-target | no-run-target

       -f <format> ( --format <format> )
            Specify a format to be used for display.

       -l <number-per-line> ( --num-per-line <number-per-line> )
            The number of items per line to display.

       -o <filename> ( --outfile <filename> )
            Specify a path for capturing command output.

       -r ( --force )
            Necessary if reading over target.max-memory-read-size bytes.

       -s <byte-size> ( --size <byte-size> )
            The size in bytes to use when displaying with the selected format.

       -t <name> ( --type <name> )
            The name of a type to view memory as.

       -x <source-language> ( --language <source-language> )
            The language of the type to view memory as.

       -d ( --append-outfile )
            Append to the file specified with '--outfile <path>'.
     
     This command takes options and free-form arguments.  If your arguments
     resemble option specifiers (i.e., they start with a - or --), you must use
     ' -- ' between the end of the command options and the beginning of the
     arguments.
```
