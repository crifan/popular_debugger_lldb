# 命令缩写

lldb命令的缩写：所有命令都支持任意前缀字符的缩写，只要不产生混淆

lldb中的命令，可以缩写

比如：

```bash
print
```

常见缩写是：

```bash
p
```

但其实底层逻辑是：

从第一个字母`p`到最后一个字母`t`，缩写到任意位置都是可以的

前提是，只要不（和其他命令的前缀）产生混淆

## 举例

### print

* `print`
  * `p`
    * 是`lldb`专门为`print`**保留**的`p`，所以可以用`p`
      * 否则按道理，也会和其他`process`等命令产生冲突，也不能把`print`缩写为`p`
  * `pr`
    * 和`process`的`pr`是一样的前缀字符
      * `lldb`无法确定是哪个，所以就属于会产生**冲突**、**混淆**
      * 所以**不**能用`pr`
  * `pri`
    * 可以
  * `prin`
    * 可以
  * `print`
    * 可以
所以总体结论就是：
* `print`
  * 可以用特定的缩写：`p`
  * 也可以用其他普通的，不产生冲突的缩写：`pri`、`prin`、`print`

### breakpoint

断点de的命令

```bash
breakpoint
```

可以缩写/简写为：

```bash
breakpoin
breakpoi
breakpo
breakp
break
brea
bre
br
```

而不能用：

* `b`
  * 特殊：属于lldb中专门保留的特定的缩写
    * 含义是：以某种特定的格式去添加断点

-》有了上面的缩写逻辑，则普通的：

```bash
breakpoint list
```

就可以写为：

```bash
breakpoin list
breakpoi list
breakpo list
breakp list
break list
brea list
bre list
br list
```

都是可以的，都是等价的

#### 子命令也支持缩写

当然命令的子命令，参数，也是同样支持缩写

比如此处

```bash
br list
```

的`list`也可以缩写：

```bash
br lis
br li
br l
```

只要不产生冲突即可

此处就是`breakpoint`的子命令中，上述缩写不会冲突混淆即可。

注：

此处可以用`help breakpoint`去查看，`breakpoint`有哪些子命令

```bash
(lldb) help breakpoint
Commands for operating on breakpoints (see 'help b' for shorthand.)

Syntax: breakpoint <subcommand> [<command-options>]

The following subcommands are supported:

      clear   -- Delete or disable breakpoints matching the specified source
                 file and line.
      command -- Commands for adding, removing and listing LLDB commands
                 executed when a breakpoint is hit.
      delete  -- Delete the specified breakpoint(s).  If no breakpoints are
                 specified, delete them all.
      disable -- Disable the specified breakpoint(s) without deleting them.  If
                 none are specified, disable all breakpoints.
      enable  -- Enable the specified disabled breakpoint(s). If no breakpoints
                 are specified, enable all of them.
      list    -- List some or all breakpoints at configurable levels of detail.
      modify  -- Modify the options on a breakpoint or set of breakpoints in
                 the executable.  If no breakpoint is specified, acts on the
                 last created breakpoint.  With the exception of -e, -d and -i,
                 passing an empty argument clears the modification.
      name    -- Commands to manage name tags for breakpoints
      read    -- Read and set the breakpoints previously saved to a file with
                 "breakpoint write".  
      set     -- Sets a breakpoint or set of breakpoints in the executable.
      write   -- Write the breakpoints listed to a file that can be read in
                 with "breakpoint read".  If given no arguments, writes all
                 breakpoints.

For more help on any particular subcommand, type 'help <command> <subcommand>'.
```

其中可见，`breakpoint`的子命令：

* `clear`
* `command`
* `delete`
* `disable`
* `enable`
* `modify`
* `name`
* `read`
* `set`
* `write`

不会和上面的缩写`lis`、`li`、`l`，有冲突和混淆

-》所以你会看到，很多人常把：

```bash
breakpoint list
```

写成：

```bash
br l
```

就是这个目的：

* 尽量用缩写
  * -》减少输入的字符数
    * -》提高调试效率

### 其他常见缩写

其他常用缩写：

* `expression` -> `e`、 `exp`
* `disassemble` -> `dis`
* `register` -> `reg`
  * `register read` -> `reg r`
* `image` -> `im`
  * `image lookup` = `im loo`
* `memory` -> `mem`
