# image list

* 输出加载的镜像image列表
  ```bash
  image list -o -f
  ```
* 输出加载的镜像image列表，只输出特定二进制
  ```bash
  image list -o -f | grep moduleName
  ```
  * 举例
    ```bash
    image list -o -f | grep AwemeCore
    image list -o -f | grep Module_Framework
    ```
