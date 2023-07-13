# watchpoint

TODO：

* 【已解决】Xcode中lldb中如何给watchpoint加上条件判断过滤
* 【已解决】Xcode中lldb的条件watchpoint报错：error user expression indirection requires pointer operand long invalid
* 【已解决】Xcode的lldb中如何监控结构体变量值的变化
* 【未解决】研究YouTube逻辑：监控NSArray的_allTrackRenderers值被改动
* 【未解决】YouTube的HAMPlayerInternal的playerLoop中监控_currentTime变量值变化

---

## watchpoint举例

```bash
(lldb) watchpoint set expr 0x000000011ceb5818
Watchpoint created: Watchpoint 1: addr = 0x11ceb5818 size = 8 state = enabled type = w
    new value: 0
```

触发时打印：

```bash
Watchpoint 1 hit:
old value: 0
new value: 0
```

关闭所有：

```bash
(lldb) watchpoint disable
All watchpoints disabled. (4 watchpoints)
```

打开所有：

```bash
(lldb) watchpoint enable
All watchpoints enabled. (4 watchpoints)
```

## watchpoint语法

```bash
(lldb) help watchpoint
Commands for operating on watchpoints.

Syntax: watchpoint <subcommand> [<command-options>]

The following subcommands are supported:

      command -- Commands for adding, removing and examining LLDB commands
                 executed when the watchpoint is hit (watchpoint 'commands').
      delete  -- Delete the specified watchpoint(s).  If no watchpoints are
                 specified, delete them all.
      disable -- Disable the specified watchpoint(s) without removing it/them. 
                 If no watchpoints are specified, disable them all.
      enable  -- Enable the specified disabled watchpoint(s). If no watchpoints
                 are specified, enable all of them.
      ignore  -- Set ignore count on the specified watchpoint(s).  If no
                 watchpoints are specified, set them all.
      list    -- List all watchpoints at configurable levels of detail.
      modify  -- Modify the options on a watchpoint or set of watchpoints in
                 the executable.  If no watchpoint is specified, act on the
                 last created watchpoint.  Passing an empty argument clears the
                 modification.
      set     -- Commands for setting a watchpoint.

For more help on any particular subcommand, type 'help <command> <subcommand>'.
```
