# 调试控制

* 源码级别的=Source Level
  * 单步执行 = step over
    ```bash
    thread step-over
    ```
      * = 
        ```bash
        next
        ```
      * =
        ```bash
        n
        ```
  * 单独进入 = step into
    ```bash
    thread step-in
    ```
      * = 
        ```bash
        step
        ```
      * =
        ```bash
        s
        ```
* 指令级别的=Instruction Level
  * 指令级单独进入 = step instruction into
    ```
    bashthread step-inst
    ```
      * =
        ```bash
        si
        ```
  * 指令级单步执行 = step instruction over
    ```
    thread step-inst-over
    ```
      * =
        ```bash
        ni
        ```
* 跳出当前函数
  ```bash
  thread step-out
  ```
    * =
      ```bash
      finish
      ```
