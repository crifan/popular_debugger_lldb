# image dump

* Dump all sections from the main executable and any shared libraries. 
  ```bash
  image dump sections
  ```
* Dump all sections in the a.out module
  ```bash
  image dump sections a.out
  ```
* Dump all symbols from the main executable and any shared libraries
  ```bash
  image dump symtab
  ```
* Dump all symbols in a.out and liba.so
  ```bash
  image dump symtab a.out liba.so
  ```
