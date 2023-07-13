# register

TODO：

【记录】lldb命令使用心得：register

---

## register举例

```bash
(lldb) reg r x0 x1 x2 x3
      x0 = 0x000000029e100ea0
      x1 = 0x0000000000000000
      x2 = 0x0000000292566f00
      x3 = 0x0000000289d922e0
```

```bash
(lldb) reg r x8
      x8 = 0x0000000107e2fef8  Module_Framework`vtable for video_streaming::OnesieRequestProto + 16
```

## register语法

```bash
(lldb) help register
Commands to access registers for the current thread and stack frame.

Syntax: register [read|write] ...

The following subcommands are supported:

      read  -- Dump the contents of one or more register values from the
               current frame.  If no register is specified, dumps them all.
      write -- Modify a single register value.

For more help on any particular subcommand, type 'help <command> <subcommand>'.
```

### register read语法

```bash
(lldb) help register read
Dump the contents of one or more register values from the current frame.  If no
register is specified, dumps them all.

Syntax: register read <cmd-options> [<register-name> [<register-name> [...]]]

Command Options Usage:
  register read [-A] [-f <format>] [-G <gdb-format>] [-s <index>] [<register-name> [<register-name> [...]]]
  register read [-Aa] [-f <format>] [-G <gdb-format>] [<register-name> [<register-name> [...]]]

       -A ( --alternate )
            Display register names using the alternate register name if there
            is one.

       -G <gdb-format> ( --gdb-format <gdb-format> )
            Specify a format using a GDB format specifier string.

       -a ( --all )
            Show all register sets.

       -f <format> ( --format <format> )
            Specify a format to be used for display.

       -s <index> ( --set <index> )
            Specify which register sets to dump by index.
     
     This command takes options and free-form arguments.  If your arguments
     resemble option specifiers (i.e., they start with a - or --), you must use
     ' -- ' between the end of the command options and the beginning of the
     arguments.
```
