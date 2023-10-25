# image lookup的help

```bash
(lldb) help image lookup
Look up information within executable and dependent shared library images.

Syntax: target modules lookup <cmd-options> [<filename> [<filename> [...]]]

Command Options Usage:
  target modules lookup [-Av] -a <address-expression> [-o <offset>] [<filename> [<filename> [...]]]
  target modules lookup [-Arv] -s <symbol> [<filename> [<filename> [...]]]
  target modules lookup [-Aiv] -f <filename> [-l <linenum>] [<filename> [<filename> [...]]]
  target modules lookup [-Airv] -F <function-name> [<filename> [<filename> [...]]]
  target modules lookup [-Airv] -n <function-or-symbol> [<filename> [<filename> [...]]]
  target modules lookup [-Av] -t <name> [<filename> [<filename> [...]]]

       -A ( --all )
            Print all matches, not just the best match, if a best match is
            available.

       -F <function-name> ( --function <function-name> )
            Lookup a function by name in the debug symbols in one or more
            target modules.

       -a <address-expression> ( --address <address-expression> )
            Lookup an address in one or more target modules.

       -f <filename> ( --file <filename> )
            Lookup a file by fullpath or basename in one or more target
            modules.

       -i ( --no-inlines )
            Ignore inline entries (must be used in conjunction with --file or
            --function).

       -l <linenum> ( --line <linenum> )
            Lookup a line number in a file (must be used in conjunction with
            --file).

       -n <function-or-symbol> ( --name <function-or-symbol> )
            Lookup a function or symbol by name in one or more target modules.

       -o <offset> ( --offset <offset> )
            When looking up an address subtract <offset> from any addresses
            before doing the lookup.

       -r ( --regex )
            The <name> argument for name lookups are regular expressions.

       -s <symbol> ( --symbol <symbol> )
            Lookup a symbol by name in the symbol tables in one or more target
            modules.

       -t <name> ( --type <name> )
            Lookup a type by name in the debug symbols in one or more target
            modules.

       -v ( --verbose )
            Enable verbose lookup information.
     
     This command takes options and free-form arguments.  If your arguments
     resemble option specifiers (i.e., they start with a - or --), you must use
     ' -- ' between the end of the command options and the beginning of the
     arguments.

'image' is an abbreviation for 'target modules'
```
