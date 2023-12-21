# watchpoint的help语法

## `help watchpoint`

```bash
(lldb) help watchpoint
Commands for operating on watchpoints.
Syntax: watchpoint <subcommand> [<command-options>]
The following subcommands are supported:
      command -- Commands for adding, removing and examining LLDB commands
                 executed when the watchpoint is hit (watchpoint 'commands').
      delete  -- Delete the specified watchpoint(s).  If no watchpoints are
                 specified, delete them all.
      disable -- Disable the specified watchpoint(s) without removing it/them. 
                 If no watchpoints are specified, disable them all.
      enable  -- Enable the specified disabled watchpoint(s). If no watchpoints
                 are specified, enable all of them.
      ignore  -- Set ignore count on the specified watchpoint(s).  If no
                 watchpoints are specified, set them all.
      list    -- List all watchpoints at configurable levels of detail.
      modify  -- Modify the options on a watchpoint or set of watchpoints in
                 the executable.  If no watchpoint is specified, act on the
                 last created watchpoint.  Passing an empty argument clears the
                 modification.
      set     -- Commands for setting a watchpoint.
For more help on any particular subcommand, type 'help <command> <subcommand>'.
```

## `help watchpoint set`

```bash
(lldb) help watchpoint set
Commands for setting a watchpoint.
Syntax: watchpoint set <subcommand> [<subcommand-options>]
The following subcommands are supported:
      expression -- Set a watchpoint on an address by supplying an expression.
                    Use the '-l' option to specify the language of the
                    expression. Use the '-w' option to specify the type of
                    watchpoint and the '-s' option to specify the byte size to
                    watch for. If no '-w' option is specified, it defaults to
                    write. If no '-s' option is specified, it defaults to the
                    target's pointer byte size. Note that there are limited
                    hardware resources for watchpoints. If watchpoint setting
                    fails, consider disable/delete existing ones to free up
                    resources.  Expects 'raw' input (see 'help raw-input'.)
      variable   -- Set a watchpoint on a variable. Use the '-w' option to
                    specify the type of watchpoint and the '-s' option to
                    specify the byte size to watch for. If no '-w' option is
                    specified, it defaults to write. If no '-s' option is
                    specified, it defaults to the variable's byte size. Note
                    that there are limited hardware resources for watchpoints.
                    If watchpoint setting fails, consider disable/delete
                    existing ones to free up resources.
For more help on any particular subcommand, type 'help <command> <subcommand>'.
```

## `help watchpoint set expression`

```bash
(lldb) help watchpoint set expression
Set a watchpoint on an address by supplying an expression. Use the '-l' option
to specify the language of the expression. Use the '-w' option to specify the
type of watchpoint and the '-s' option to specify the byte size to watch for.
If no '-w' option is specified, it defaults to write. If no '-s' option is
specified, it defaults to the target's pointer byte size. Note that there are
limited hardware resources for watchpoints. If watchpoint setting fails,
consider disable/delete existing ones to free up resources.  Expects 'raw'
input (see 'help raw-input'.)
Syntax: watchpoint set expression <cmd-options> -- <expr>
Command Options Usage:
  watchpoint set expression [-w <watch-type>] [-s <byte-size>] [-l <source-language>] -- <expr>
  watchpoint set expression <expr>
       -l <source-language> ( --language <source-language> )
            Language of expression to run
       -s <byte-size> ( --size <byte-size> )
            Number of bytes to use to watch a region.
            Values: 1 | 2 | 4 | 8
       -w <watch-type> ( --watch <watch-type> )
            Specify the type of watching to perform.
            Values: read | write | read_write
Examples:
watchpoint set expression -w write -s 1 -- foo + 32
    Watches write access for the 1-byte region pointed to by the address 'foo +
    32'
     
     This command takes options and free-form arguments.  If your arguments
     resemble option specifiers (i.e., they start with a - or --), you must use
     ' -- ' between the end of the command options and the beginning of the
     arguments.
```
