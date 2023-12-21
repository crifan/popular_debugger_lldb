# watchpoint

TODO：

* 【已解决】Xcode中lldb中如何给watchpoint加上条件判断过滤
* 【已解决】Xcode中lldb的条件watchpoint报错：error user expression indirection requires pointer operand long invalid
* 【已解决】Xcode的lldb中如何监控结构体变量值的变化
* 【未解决】研究YouTube逻辑：监控NSArray的_allTrackRenderers值被改动
* 【未解决】YouTube的HAMPlayerInternal的playerLoop中监控_currentTime变量值变化
* 【未解决】iOS逆向：watchpoint添加失败报错：error Watchpoint creation failed sending gdb watchpoint packet failed

---

## watchpoint举例

### 默认：type=write

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

### type=read

```bash
(lldb) watchpoint set expression -w read -- 0x10b121828
Watchpoint created: Watchpoint 1: addr = 0x10b121828 size = 8 state = enabled type = r
    watchpoint spec = '0x10b121828'
    new value: 4476770681
```

### 控制watchpoint

关闭所有：

```bash
(lldb) watchpoint disable
All watchpoints disabled. (4 watchpoints)
```

开启所有：

```bash
(lldb) watchpoint enable
All watchpoints enabled. (4 watchpoints)
```
