# breakpoint

TODO：

* 【记录】lldb命令使用心得：breakpoint
* 【已解决】Xcode中lldb中b list不是breakpoint list
* 【未解决】Xcode中无法给下一行将要运行的汇编指令加断点
* 【已解决】XCode中如何给符号断点加上判断条件
* 【未解决】XCode和lldb如何根据函数地址加断点

---

* 详见独立子教程
  * [iOS逆向之动态调试：断点](https://book.crifan.org/books/ios_re_debug_breakpoint/website/)

## breakpoint举例

```bash
breakpoint set -a 函数地址

breakpoint set -a ASLR偏移量 + 静态分析的函数地址

breakpoint set -a （image list -o -f看到的库的加载的起始地址） +  （IDA等工具）静态分析的函数地址
```

```bash
(lldb) breakpoint set -a 0x1102d3348
Breakpoint 54: where = AwemeCore`___lldb_unnamed_symbol1462804$$AwemeCore + 480, address = 0x00000001102d3348
(lldb) breakpoint list
Current breakpoints:
…
54: address = AwemeCore[0x000000000ee2b348], locations = 1, resolved = 1, hit count = 0
  54.1: where = AwemeCore`___lldb_unnamed_symbol1462804$$AwemeCore + 480, address = 0x00000001102d3348, resolved, hit count = 0
```

```bash
breakpoint set --name foo --condition '(int)strcmp(y,"hello") == 0'
```

==

```bash
br s -n foo -c '(int)strcmp(y,"hello") == 0'
```

## breakpoint语法

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

### `breakpoint set`语法

```bash
(lldb) help breakpoint set
Sets a breakpoint or set of breakpoints in the executable.

Syntax: breakpoint set <cmd-options>

Command Options Usage:
  breakpoint set [-DHd] -l <linenum> [-G <boolean>] [-C <command>] [-c <expr>] [-i <count>] [-o <boolean>] [-q <queue-name>] [-t <thread-id>] [-x <thread-index>] [-T <thread-name>] [-R <address>] [-N <breakpoint-name>] [-u <column>] [-f <filename>] [-m <boolean>] [-s <shlib-name>] [-K <boolean>]
  breakpoint set [-DHd] -a <address-expression> [-G <boolean>] [-C <command>] [-c <expr>] [-i <count>] [-o <boolean>] [-q <queue-name>] [-t <thread-id>] [-x <thread-index>] [-T <thread-name>] [-N <breakpoint-name>] [-s <shlib-name>]
  breakpoint set [-DHd] -n <function-name> [-G <boolean>] [-C <command>] [-c <expr>] [-i <count>] [-o <boolean>] [-q <queue-name>] [-t <thread-id>] [-x <thread-index>] [-T <thread-name>] [-R <address>] [-N <breakpoint-name>] [-f <filename>] [-L <source-language>] [-s <shlib-name>] [-K <boolean>]
  breakpoint set [-DHd] -F <fullname> [-G <boolean>] [-C <command>] [-c <expr>] [-i <count>] [-o <boolean>] [-q <queue-name>] [-t <thread-id>] [-x <thread-index>] [-T <thread-name>] [-R <address>] [-N <breakpoint-name>] [-f <filename>] [-L <source-language>] [-s <shlib-name>] [-K <boolean>]
  breakpoint set [-DHd] -S <selector> [-G <boolean>] [-C <command>] [-c <expr>] [-i <count>] [-o <boolean>] [-q <queue-name>] [-t <thread-id>] [-x <thread-index>] [-T <thread-name>] [-R <address>] [-N <breakpoint-name>] [-f <filename>] [-L <source-language>] [-s <shlib-name>] [-K <boolean>]
  breakpoint set [-DHd] -M <method> [-G <boolean>] [-C <command>] [-c <expr>] [-i <count>] [-o <boolean>] [-q <queue-name>] [-t <thread-id>] [-x <thread-index>] [-T <thread-name>] [-R <address>] [-N <breakpoint-name>] [-f <filename>] [-L <source-language>] [-s <shlib-name>] [-K <boolean>]
  breakpoint set [-DHd] -r <regular-expression> [-G <boolean>] [-C <command>] [-c <expr>] [-i <count>] [-o <boolean>] [-q <queue-name>] [-t <thread-id>] [-x <thread-index>] [-T <thread-name>] [-R <address>] [-N <breakpoint-name>] [-f <filename>] [-L <source-language>] [-s <shlib-name>] [-K <boolean>]
  breakpoint set [-DHd] -b <function-name> [-G <boolean>] [-C <command>] [-c <expr>] [-i <count>] [-o <boolean>] [-q <queue-name>] [-t <thread-id>] [-x <thread-index>] [-T <thread-name>] [-R <address>] [-N <breakpoint-name>] [-f <filename>] [-L <source-language>] [-s <shlib-name>] [-K <boolean>]
  breakpoint set [-ADHd] -p <regular-expression> [-G <boolean>] [-C <command>] [-c <expr>] [-i <count>] [-o <boolean>] [-q <queue-name>] [-t <thread-id>] [-x <thread-index>] [-T <thread-name>] [-N <breakpoint-name>] [-f <filename>] [-m <boolean>] [-s <shlib-name>] [-X <function-name>]
  breakpoint set [-DHd] -E <source-language> [-G <boolean>] [-C <command>] [-c <expr>] [-i <count>] [-o <boolean>] [-q <queue-name>] [-t <thread-id>] [-x <thread-index>] [-T <thread-name>] [-N <breakpoint-name>] [-O <type-name>] [-h <boolean>] [-w <boolean>]
  breakpoint set [-DHd] -P <python-class> [-k <none>] [-v <none>] [-G <boolean>] [-C <command>] [-c <expr>] [-i <count>] [-o <boolean>] [-q <queue-name>] [-t <thread-id>] [-x <thread-index>] [-T <thread-name>] [-N <breakpoint-name>] [-f <filename>] [-s <shlib-name>]
  breakpoint set [-DHd] -y <linespec> [-G <boolean>] [-C <command>] [-c <expr>] [-i <count>] [-o <boolean>] [-q <queue-name>] [-t <thread-id>] [-x <thread-index>] [-T <thread-name>] [-R <address>] [-N <breakpoint-name>] [-m <boolean>] [-s <shlib-name>] [-K <boolean>]

       -A ( --all-files )
            All files are searched for source pattern matches.

       -C <command> ( --command <command> )
            A command to run when the breakpoint is hit, can be provided more
            than once, the commands will get run in order left to right.

       -D ( --dummy-breakpoints )
            Act on Dummy breakpoints - i.e. breakpoints set before a file is
            provided, which prime new targets.

       -E <source-language> ( --language-exception <source-language> )
            Set the breakpoint on exceptions thrown by the specified language
            (without options, on throw but not catch.)

       -F <fullname> ( --fullname <fullname> )
            Set the breakpoint by fully qualified function names. For C++ this
            means namespaces and all arguments, and for Objective-C this means
            a full functionprototype with class and selector.  Can be repeated
            multiple times to make one breakpoint for multiple names.

       -G <boolean> ( --auto-continue <boolean> )
            The breakpoint will auto-continue after running its commands.

       -H ( --hardware )
            Require the breakpoint to use hardware breakpoints.

       -K <boolean> ( --skip-prologue <boolean> )
            sKip the prologue if the breakpoint is at the beginning of a
            function. If not set the target.skip-prologue setting is used.

       -L <source-language> ( --language <source-language> )
            Specifies the Language to use when interpreting the breakpoint's
            expression (note: currently only implemented for setting
            breakpoints on identifiers). If not set the target.language setting
            is used.

       -M <method> ( --method <method> )
            Set the breakpoint by C++ method names.  Can be repeated multiple
            times tomake one breakpoint for multiple methods.

       -N <breakpoint-name> ( --breakpoint-name <breakpoint-name> )
            Adds this to the list of names for this breakpoint.

       -O <type-name> ( --exception-typename <type-name> )
            The breakpoint will only stop if an exception Object of this type
            is thrown. Can be repeated multiple times to stop for multiple
            object types. If you just specify the type's base name it will
            match against that type in all modules, or you can specify the full
            type name including modules. Other submatches are not supported at
            present.Only supported for Swift at present.

       -P <python-class> ( --script-class <python-class> )
            The name of the class that will manage a scripted breakpoint.

       -R <address> ( --address-slide <address> )
            Add the specified offset to whatever address(es) the breakpoint
            resolves to. At present this applies the offset directly as given,
            and doesn't try to align it to instruction boundaries.

       -S <selector> ( --selector <selector> )
            Set the breakpoint by ObjC selector name. Can be repeated multiple
            times tomake one breakpoint for multiple Selectors.

       -T <thread-name> ( --thread-name <thread-name> )
            The breakpoint stops only for the thread whose thread name matches
            this argument.

       -X <function-name> ( --source-regexp-function <function-name> )
            When used with '-p' limits the source regex to source contained in
            the namedfunctions.  Can be repeated multiple times.

       -a <address-expression> ( --address <address-expression> )
            Set the breakpoint at the specified address.  If the address maps
            uniquely toa particular binary, then the address will be converted
            to a fileaddress, so that the breakpoint will track that
            binary+offset no matter where the binary eventually loads. 
            Alternately, if you also specify the module - with the -s option -
            then the address will be treated as a file address in that module,
            and resolved accordingly.  Again, this will allow lldb to track
            that offset on subsequent reloads.  The module need not have been
            loaded at the time you specify this breakpoint, and will get
            resolved when the module is loaded.

       -b <function-name> ( --basename <function-name> )
            Set the breakpoint by function basename (C++ namespaces and
            arguments will beignored).  Can be repeated multiple times to make
            one breakpoint for multiplesymbols.

       -c <expr> ( --condition <expr> )
            The breakpoint stops only if this condition expression evaluates to
            true.

       -d ( --disable )
            Disable the breakpoint.

       -f <filename> ( --file <filename> )
            Specifies the source file in which to set this breakpoint.  Note,
            by default lldb only looks for files that are #included if they use
            the standard include file extensions.  To set breakpoints on
            .c/.cpp/.m/.mm files that are #included, set
            target.inline-breakpoint-strategy to always.

       -h <boolean> ( --on-catch <boolean> )
            Set the breakpoint on exception catcH.

       -i <count> ( --ignore-count <count> )
            Set the number of times this breakpoint is skipped before stopping.

       -k <none> ( --structured-data-key <none> )
            The key for a key/value pair passed to the implementation of a
            scripted breakpoint.  Pairs can be specified more than once.

       -l <linenum> ( --line <linenum> )
            Specifies the line number on which to set this breakpoint.

       -m <boolean> ( --move-to-nearest-code <boolean> )
            Move breakpoints to nearest code. If not set the
            target.move-to-nearest-codesetting is used.

       -n <function-name> ( --name <function-name> )
            Set the breakpoint by function name.  Can be repeated multiple
            times to makeone breakpoint for multiple names

       -o <boolean> ( --one-shot <boolean> )
            The breakpoint is deleted the first time it stop causes a stop.

       -p <regular-expression> ( --source-pattern-regexp <regular-expression> )
            Set the breakpoint by specifying a regular expression which is
            matched against the source text in a source file or files specified
            with the -f can be specified more than once.  If no source files
            are specified, uses the current default source file.  If you want
            to match against all source files, pass the --all-files option.

       -q <queue-name> ( --queue-name <queue-name> )
            The breakpoint stops only for threads in the queue whose name is
            given by this argument.

       -r <regular-expression> ( --func-regex <regular-expression> )
            Set the breakpoint by function name, evaluating a
            regular-expression to find the function name(s).

       -s <shlib-name> ( --shlib <shlib-name> )
            Set the breakpoint only in this shared library.  Can repeat this
            option multiple times to specify multiple shared libraries.

       -t <thread-id> ( --thread-id <thread-id> )
            The breakpoint stops only for the thread whose TID matches this
            argument.

       -u <column> ( --column <column> )
            Specifies the column number on which to set this breakpoint.

       -v <none> ( --structured-data-value <none> )
            The value for the previous key in the pair passed to the
            implementation of a scripted breakpoint.  Pairs can be specified
            more than once.

       -w <boolean> ( --on-throw <boolean> )
            Set the breakpoint on exception throW.

       -x <thread-index> ( --thread-index <thread-index> )
            The breakpoint stops only for the thread whose index matches this
            argument.

       -y <linespec> ( --joint-specifier <linespec> )
            A specifier in the form filename:line[:column] for setting file &
            line breakpoints.
```
