# image

TODO：

* 【已解决】lldb命令使用心得：image

---

* image核心子命令
  * [image lookup](../../../lldb_commands/common_cmd/image/image_lookup/README.md)
  * [image list](../../../lldb_commands/common_cmd/image/image_list/README.md)
  * [image dump](../../../lldb_commands/common_cmd/image/image_dump/README.md)

## image命令语法

```bash
(lldb) help image
Commands for accessing information for one or more target modules.

Syntax: image

'image' is an abbreviation for 'target modules'
(lldb) help target modules
Commands for accessing information for one or more target modules.

Syntax: target modules <sub-command> ...

The following subcommands are supported:

      add          -- Add a new module to the current target's modules.
      dump         -- Commands for dumping information about one or more target
                      modules.
      list         -- List current executable and dependent shared library
                      images.
      load         -- Set the load addresses for one or more sections in a
                      target module.
      lookup       -- Look up information within executable and dependent
                      shared library images.
      search-paths -- Commands for managing module search paths for a target.
      show-unwind  -- Show synthesized unwind instructions for a function.

For more help on any particular subcommand, type 'help <command> <subcommand>'.
```
