# 导出结果到文件

lldb调试期间，对于命令：

```bash
disassemble -f
```

的结果，想要输出/导出到文件，可以：

## 方法1：`session save`

* 方法1：`session save`
  * 优点：
    * 方便，无需引入额外命令
    * （对部分人是优点）可以把session的所有内容都保存输出到文件
  * 缺点：没有针对性（针对自己想要的特定的代码的输出结果）

不借助外部脚本和命令，直接用：

```bash
session save /Users/crifan/dev/tmp/sub_1000A0460.txt
```

即可：

把当前会话session == 当前这次lldb的调试，自动启动开始，到现在的输出的内容

都输出到文件中

其中就包括，之前刚已运行的命令的输出结果了。

## 方法2：用`lldb`的（`python`）脚本

* 方法2：用`lldb`的（`python`）脚本
  * 缺点：要额外新引入lldb的脚本
  * 优点：可以有针对性的，只输出单个命令的结果到文件
    * 而不用保存当前session的所有内容

比如：

[4iar/lldb-write: Write the output of an lldb command to file (github.com)](https://github.com/4iar/lldb-write)

用法：

先安装：

下载代码

```bash
git clone https://github.com/4iar/lldb-write.git
```
```
然后去加到lldb启动脚本中：

```bash
vi ~/.lldbinit
```

加上：

```bash
command script import /{change_to_your_path}/lldb-write/write.py
```

重启lldb后，可以看到提示：

`The "write" command has been loaded and is ready for use.`

然后即可使用：

```bash
write /some/path/outputFile.txt yourOriginLldbCommand
```

比如：

```bash
write /Users/crifan/dev/tmp/lldb_akd_symbol2575_disassemble.txt dis -f
```

即可把当前lldb命令的输出结果，导出到文件中。

同时：当前lldb终端中，仍能正常看到结果。还是很好用的。
