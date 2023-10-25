# image lookup

* `image lookup`的典型写法举例
  * `-a`
    ```bash
    image lookup -a 0x114fb69c4

    image lookup -v -a 0x112d57730
    image lookup -va 0x0000000195d31f14
    im loo -va 0xa916260182319ea0

    image lookup -a 0x00000000009e8000+0x0000001008f83b8
    ```
  * `-n`
    ```bash
    image lookup -n statfs
    image lookup -n ___lldb_unnamed_symbol2575$$akd
    image lookup -n "+[UMUserManager sharedManager]"

    image lookup -name getInt

    image lookup -r -n objc_msgSend
    image lookup -r -n accountsWithAccountType
    image lookup -r -n "accountsWithAccountType:"
    image lookup -rn initWithURL
    image lookup -rn "AADeviceInfo"
    image lookup -rn "setValue:forHTTPHeaderField:"
    image lookup -rn "AADeviceInfo udid"
    im loo -rn SetRequestPriority

    image lookup -vn ___lldb_unnamed_symbol2575$$akd
    image lookup -vn "-[AALoginAccountRequest urlRequest]"
    image lookup -vn "-[AKAppleIDAuthenticationContextManager shouldContinueWithAuthenticationResults:error:forContextID:completion:]"
    image lookup -vn "+[AADeviceInfo(Deprecated) udid]"
    image lookup -vn "+[AADeviceInfo udid]"
    image lookup -vn "-[AADeviceInfo udid]"

    image lookup -vrn "AADeviceInfo udid"
    ```
  * `-s`
    ```bash
    image lookup -s statfs

    image lookup -r -s objc_msgSend
    image lookup -r -s statfs
    image lookup -r -s handlePressGesture
    image lookup -r -s _nextButtonSelected
    image lookup -r -s "authenticationContext"

    image lookup -vs SecTrustEvaluateFastAsync
    image lookup -vs "AADeviceInfo"
    image lookup -vs "___lldb_unnamed_symbol972"

    image lookup -v -s SSLHandshake
    ```
  * `-t`
    ```bash
    image lookup -type Person
    image lookup -type NSObject
    ```

---

* `image lookup`的主要参数
  * 根据不同类型去搜
    * address=地址
      * `-a <address-expression>`=`--address <address-expression>`
        * 作用：Lookup an address in one or more target modules
    * name=名称
      * `-n <function-or-symbol>`=`--name <function-or-symbol>`
        * 作用：Lookup a function or symbol by **name** in one or more target modules
          * searches **debug** symbols
    * symbol=符号
      * `-s <symbol>`=`--symbol <symbol>`
        * 作用：Lookup a symbol by name in the **symbol** tables in one or more target modules
          * searches **non-debug** symbols
    * type=类型
      * `-t <name>`=`--type <name>`
        * 作用：Lookup a type by name in the debug symbols in one or more target modules
  * 其他辅助参数
    * 输出详细信息
      * `-v`=`--verbose`
        * 作用：Enable verbose lookup information
    * 以正则表达式的方式去搜
      * `-r`= `--regex`
        * 作用：The `<name>` argument for name lookups are regular expressions.

以及：

* lldb支持命令的缩写
  * 常见的缩写
    * `image` -> `img`、`im`
    * `lookup` -> `loo`
* lldb支持字母合在一起
  * `-v -a` -> `-va`
  * `-r -n` -> `-rn`

所以就有多种常见写法：

* 基本参数的写法
  * `image lookup -a` == `im loo -a`
  * `image lookup -n` == `im loo -n`
  * `image lookup -s` == `im loo -s`
* 如果加上`-v`，则是：
  * `image lookup -v -a` == `im loo -v -a`
    * == `image lookup -va` == `im loo -va`
  * `image lookup -v -n` == `im loo -v -n`
    * == `image lookup -vn` == `im loo -vn`
  * `image lookup -v -s` == `im loo -v -s`
    * == `image lookup -vs` == `im loo -vs`
* 如果加上`-r`，则是：
  * `image lookup -r -n` == `im loo -r -n`
    * == `image lookup -rn` == `im loo -rn`
  * `image lookup -r -s` == `im loo -r -s`
    * == `image lookup -rs` == `im loo -rs`

## image lookup的高级用法

### 限定在某个二进制Module内部查找

`lldb`中`image lookup`的基本用法：

```bash
image lookup -a 0x1000
```

如果要限定在某个`二进制文件`=`库`=`模块`=`Module`中的话，语法是：

```bash
image lookup -a 0x1000 a.out
```
  * 其中`a.out`是二进制文件名

#### 举例

##### AppleAccount

```bash
im loo -rn didReceiveData AppleAccount
```
* 参数说明
  * `AppleAccount`文件（此处调试时的路径是）
    * `/Users/crifan/Library/Developer/Xcode/iOS DeviceSupport/15.1 (19B74) arm64e/Symbols/System/Library/PrivateFrameworks/AppleAccount.framework/AppleAccount`
* 完整输出
  ```bash
  (lldb) im loo -rn didReceiveData AppleAccount
  3 matches found in /Users/crifan/Library/Developer/Xcode/iOS DeviceSupport/15.1 (19B74) arm64e/Symbols/System/Library/PrivateFrameworks/AppleAccount.framework/AppleAccount:
          Address: AppleAccount[0x0000000192f4cf34] (AppleAccount.__TEXT.__text + 1000)
          Summary: AppleAccount`-[_AAURLSessionDelegate URLSession:dataTask:didReceiveData:]        Address: AppleAccount[0x0000000192f4cff4] (AppleAccount.__TEXT.__text + 1192)
          Summary: AppleAccount`-[AAURLSession URLSession:dataTask:didReceiveData:]        Address: AppleAccount[0x0000000192f83d88] (AppleAccount.__TEXT.__text + 225852)
          Summary: AppleAccount`-[AARequester connection:didReceiveData:]
  ```

##### AppleStoreCore

```bash
image lookup -rn initialize AppleStoreCore
```
* 完整输出
  ```bash
  (lldb) image lookup -rn initialize AppleStoreCore
  3 matches found in /Users/crifan/Library/Developer/Xcode/DerivedData/Jolly-fbcdzphrbokcgxhejxlslydrdyaa/Build/Products/Debug-iphoneos/Jolly.app/Frameworks/AppleStoreCore.framework/AppleStoreCore:
          Address: AppleStoreCore[0x000000000049a6bc] (AppleStoreCore.__TEXT.__text + 4807496)
          Summary: AppleStoreCore`initializeAvailabilityCheck        Address: AppleStoreCore[0x000000000049a6c4] (AppleStoreCore.__TEXT.__text + 4807504)
          Summary: AppleStoreCore`_initializeAvailabilityCheck        Address: AppleStoreCore[0x00000000000a8010] (AppleStoreCore.__TEXT.__text + 668828)
          Summary: AppleStoreCore`static AppleStoreCore.User.initialize() -> ()
  (lldb) image lookup -rs initialize AppleStoreCore
  4 symbols match the regular expression 'initialize' in /Users/crifan/Library/Developer/Xcode/DerivedData/Jolly-fbcdzphrbokcgxhejxlslydrdyaa/Build/Products/Debug-iphoneos/Jolly.app/Frameworks/AppleStoreCore.framework/AppleStoreCore:
          Address: AppleStoreCore[0x000000000049a6bc] (AppleStoreCore.__TEXT.__text + 4807496)
          Summary: AppleStoreCore`initializeAvailabilityCheck        Address: AppleStoreCore[0x000000000049a6c4] (AppleStoreCore.__TEXT.__text + 4807504)
          Summary: AppleStoreCore`_initializeAvailabilityCheck        Address: AppleStoreCore[0x00000000004d0430] (AppleStoreCore.__TEXT.__stubs + 11844)
          Summary: AppleStoreCore`symbol stub for: swift_deallocUninitializedObject        Address: AppleStoreCore[0x00000000000a8010] (AppleStoreCore.__TEXT.__text + 668828)
          Summary: AppleStoreCore`static AppleStoreCore.User.initialize() -> ()
  ```

