# expression

TODO：

* 【记录】lldb命令使用心得：expression
* 【记录】lldb命令使用心得：p和po
  * 【整理】Xcode中lldb命令对比：po和p

---

## p和po

* `p` == `expression --`
* `po` == `expression -O --`

## expression语法

```bash
(lldb) help expression
Evaluate an expression on the current thread.  Displays any returned value with
LLDB's default formatting.  Expects 'raw' input (see 'help raw-input'.)

Syntax: expression <cmd-options> -- <expr>

Command Options Usage:
  expression [-AFLORTgp] [-f <format>] [-G <gdb-format>] [-a <boolean>] [-j <boolean>] [-X <source-language>] [-v[<description-verbosity>]] [-i <boolean>] [-l <source-language>] [-t <unsigned-integer>] [-u <boolean>] [-d <none>] [-S <boolean>] [-D <count>] [-P <count>] [-Y[<count>]] [-V <boolean>] [-Z <count>] -- <expr>
  expression [-AFLORTgp] [-a <boolean>] [-j <boolean>] [-X <source-language>] [-i <boolean>] [-l <source-language>] [-t <unsigned-integer>] [-u <boolean>] [-d <none>] [-S <boolean>] [-D <count>] [-P <count>] [-Y[<count>]] [-V <boolean>] [-Z <count>] -- <expr>
  expression [-r] -- <expr>
  expression <expr>

       -A ( --show-all-children )
            Ignore the upper bound on the number of children to show.

       -D <count> ( --depth <count> )
            Set the max recurse depth when dumping aggregate types (default is
            infinity).

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

       -X <source-language> ( --apply-fixits <source-language> )
            If true, simple fix-it hints will be automatically applied to the
            expression.

       -Y[<count>] ( --no-summary-depth=[<count>] )
            Set the depth at which omitting summary information stops (default
            is 1).

       -Z <count> ( --element-count <count> )
            Treat the result of the expression as if its type is an array of
            this many values.

       -a <boolean> ( --all-threads <boolean> )
            Should we run all threads if the execution doesn't complete on one
            thread.

       -d <none> ( --dynamic-type <none> )
            Show the object as its full dynamic type, not its static type, if
            available.
            Values: no-dynamic-values | run-target | no-run-target

       -f <format> ( --format <format> )
            Specify a format to be used for display.

       -g ( --debug )
            When specified, debug the JIT code by setting a breakpoint on the
            first instruction and forcing breakpoints to not be ignored (-i0)
            and no unwinding to happen on error (-u0).

       -i <boolean> ( --ignore-breakpoints <boolean> )
            Ignore breakpoint hits while running expressions

       -j <boolean> ( --allow-jit <boolean> )
            Controls whether the expression can fall back to being JITted if
            it's not supported by the interpreter (defaults to true).

       -l <source-language> ( --language <source-language> )
            Specifies the Language to use when parsing the expression.  If not
            set the target.language setting is used.

       -p ( --top-level )
            Interpret the expression as a complete translation unit, without
            injecting it into the local context.  Allows declaration of
            persistent, top-level entities without a $ prefix.

       -r ( --repl )
            Drop into Swift REPL

       -t <unsigned-integer> ( --timeout <unsigned-integer> )
            Timeout value (in microseconds) for running the expression.

       -u <boolean> ( --unwind-on-error <boolean> )
            Clean up program state if the expression causes a crash, or raises
            a signal. Note, unlike gdb hitting a breakpoint is controlled by
            another option (-i).

       -v[<description-verbosity>] ( --description-verbosity=[<description-verbosity>] )
            How verbose should the output of this expression be, if the object
            description is asked for.
            Values: compact | full

Single and multi-line expressions:

    The expression provided on the command line must be a complete expression
    with no newlines.  To evaluate a multi-line expression, hit a return after
    an empty expression, and lldb will enter the multi-line expression editor.
    Hit return on an empty line to end the multi-line expression.

Timeouts:

    If the expression can be evaluated statically (without running code) then
    it will be.  Otherwise, by default the expression will run on the current
    thread with a short timeout: currently .25 seconds.  If it doesn't return
    in that time, the evaluation will be interrupted and resumed with all
    threads running.  You can use the -a option to disable retrying on all
    threads.  You can use the -t option to set a shorter timeout.

User defined variables:

    You can define your own variables for convenience or to be used in
    subsequent expressions.  You define them the same way you would define
    variables in C.  If the first character of your user defined variable is a
    $, then the variable's value will be available in future expressions,
    otherwise it will just be available in the current expression.

Continuing evaluation after a breakpoint:

    If the "-i false" option is used, and execution is interrupted by a
    breakpoint hit, once you are done with your investigation, you can either
    remove the expression execution frames from the stack with "thread return
    -x" or if you are still interested in the expression result you can issue
    the "continue" command and the expression evaluation will complete and the
    expression result will be available using the "thread.completed-expression"
    key in the thread format.

Examples:

    expr my_struct->a = my_array[3]
    expr -f bin -- (index * 8) + 5
    expr unsigned int $foo = 5
    expr char c[] = \"foo\"; c[0]
     
     Important Note: Because this command takes 'raw' input, if you use any
     command options you must use ' -- ' between the end of the command options
     and the beginning of the raw input.
```
