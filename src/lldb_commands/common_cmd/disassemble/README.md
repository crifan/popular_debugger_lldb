# disassemble

TODO：

【记录】lldb命令使用心得：disassemble

---

* disassemble
  * 命令写法
    * `disassemble` == `dis` == `di`
  * 概述
    * 反汇编当前帧的当前函数
      ```bash
      disassemble --frame
      ```
      * =
        ```bash
        di -f
        ```
      * =
        ```bash
        dis
        ```
      * =
        ```bash
        dis -n currentFunctionName
        ```
    * 反汇编某函数，根据函数名
      ```bash
      disassemble --name functionName
      ```
      * =
        ```bash
        di -n functionName
        ```
      * 举例
        ```bash
        dis -n "-[AAUISignInViewController _nextButtonSelected:]"
        ```
    * 反汇编某个地址范围（起始地址~结束地址）
      ```bash
      disassemble --start-address 0x1eb8 --end-address 0x1ec3
      ```
      * =
        ```bash
        di -s 0x1eb8 -e 0x1ec3
        ```
      * 其他例子
        ```bash
        dis --start-address 0x1b30cb978 --end-address 0x1b30cb990
        ```
    * 反汇编一部分=一段代码（起始地址，加上长度）
      ```bash
      disassemble --start-address 0x1eb8 --count 20
      ```
      * =
        ```bash
        di -s 0x1eb8 -c 20
        ```
      * 其他例子
        ```bash
        dis --start-address 0x1b30cb978 --count 10
        ```
    * 对于当前帧的当前函数，显示混合的源码和反汇编代码
      ```bash
      disassemble --frame --mixed
      ```
      * =
        ```bash
        dis --frame --mixed
        di -f -m
        ```
    * 反汇编当前帧的当前函数，显示opcode操作码字节码
      ```bash
      disassemble --frame --bytes
      ```
      * =
        ```bash
        dis --frame --bytes
        di -f -b
        ```
    * 反汇编当前帧的当前源码行
      ```bash
      disassemble --line
      ```
      * =
        ```bash
        di -l
        dis --line
        ```
