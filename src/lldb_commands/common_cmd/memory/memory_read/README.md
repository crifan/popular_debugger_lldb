# memory read

## 心得

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
