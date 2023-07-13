# po

TODO：

* 【整理】iOS逆向心得：当iPhone锁屏时Xcode中lldb的po会卡死
* 【整理】iOS逆向心得：po异常时NSString的字符串无法像char*一样打印出来
* 【整理】iOS逆向调试心得：po不是对象实例但可以看到是哪个类

---

* `po` == `expression -O --`

## po举例

```bash
(lldb) po $x1
8203662366

(lldb) po (SEL)$x1
"stringByAppendingString:"

(lldb) po $x2
<nil>

(lldb) po $x3
{(
    executing
)}

(lldb) po $arg3
<nil>
```

```c
(lldb) reg r x1 x2 x3
      x1 = 0x000000010a328d0a  
      x2 = 0x0000000281f79160
      x3 = 0x000000016b4b8ea8
(lldb) po 0x000000010a328d0a
4466052362

(lldb) po 0x0000000281f79160
<AWELazyRegisterHandler: 0x281f79160>

(lldb) po 0x000000016b4b8ea8
6095081128
```
