# memory

TODO：

* 【记录】lldb命令使用心得：memory
* 【记录】lldb命令使用心得：memory read
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
