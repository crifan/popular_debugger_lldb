# memory read的help语法

```bash
(lldb) help memory read
Read from the memory of the current target process.

Syntax: memory read <cmd-options> <address-expression> [<address-expression>]

Command Options Usage:
  memory read [-drd] [-f <format>] [-c <count>] [-G <gdb-format>] [-s <byte-size>] [-l <number-per-line>] [-o <filename>] <address-expression> [<address-expression>]
  memory read [-dbrd] [-f <format>] [-c <count>] [-s <byte-size>] [-o <filename>] <address-expression> [<address-expression>]
  memory read [-AFLORTdrd] -t <name> [-f <format>] [-c <count>] [-G <gdb-format>] [-E <count>] [-o <filename>] [-d <none>] [-S <boolean>] [-D <count>] [-P <count>] [-Y[<count>]] [-V <boolean>] [-Z <count>] <address-expression> [<address-expression>]
  memory read -t <name> [-x <source-language>] <address-expression> [<address-expression>]

       -A ( --show-all-children )
            Ignore the upper bound on the number of children to show.

       -D <count> ( --depth <count> )
            Set the max recurse depth when dumping aggregate types (default is
            infinity).

       -E <count> ( --offset <count> )
            How many elements of the specified type to skip before starting to
            display data.

       -F ( --flat )
            Display results in a flat format that uses expression paths for
            each variable or member.

       -G <gdb-format> ( --gdb-format <gdb-format> )
            Specify a format using a GDB format specifier string.

       -L ( --location )
            Show variable location information.

       -O ( --object-description )
            Display using a language-specific description API, if possible.

       -P <count> ( --ptr-depth <count> )
            The number of pointers to be traversed when dumping values (default
            is zero).

       -R ( --raw-output )
            Don't use formatting options.

       -S <boolean> ( --synthetic-type <boolean> )
            Show the object obeying its synthetic provider, if available.

       -T ( --show-types )
            Show variable types when dumping values.

       -V <boolean> ( --validate <boolean> )
            Show results of type validators.

       -Y[<count>] ( --no-summary-depth=[<count>] )
            Set the depth at which omitting summary information stops (default
            is 1).

       -Z <count> ( --element-count <count> )
            Treat the result of the expression as if its type is an array of
            this many values.

       -b ( --binary )
            If true, memory will be saved as binary. If false, the memory is
            saved save as an ASCII dump that uses the format, size, count and
            number per line settings.

       -c <count> ( --count <count> )
            The number of total items to display.

       -d <none> ( --dynamic-type <none> )
            Show the object as its full dynamic type, not its static type, if
            available.
            Values: no-dynamic-values | run-target | no-run-target

       -f <format> ( --format <format> )
            Specify a format to be used for display.

       -l <number-per-line> ( --num-per-line <number-per-line> )
            The number of items per line to display.

       -o <filename> ( --outfile <filename> )
            Specify a path for capturing command output.

       -r ( --force )
            Necessary if reading over target.max-memory-read-size bytes.

       -s <byte-size> ( --size <byte-size> )
            The size in bytes to use when displaying with the selected format.

       -t <name> ( --type <name> )
            The name of a type to view memory as.

       -x <source-language> ( --language <source-language> )
            The language of the type to view memory as.

       -d ( --append-outfile )
            Append to the file specified with '--outfile <path>'.
     
     This command takes options and free-form arguments.  If your arguments
     resemble option specifiers (i.e., they start with a - or --), you must use
     ' -- ' between the end of the command options and the beginning of the
     arguments.
```
