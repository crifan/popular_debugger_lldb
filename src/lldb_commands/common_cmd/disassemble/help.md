# disassemble的help语法

```bash
(lldb) help disassemble
Disassemble specified instructions in the current target.  Defaults to the
current function for the current thread and stack frame.

Syntax: disassemble [<cmd-options>]

Command Options Usage:
  disassemble [-bmr] -s <address-expression> [-A <arch>] [-C <num-lines>] [-e <address-expression>] [-F <disassembly-flavor>] [-P <plugin>]
  disassemble [-bmr] -s <address-expression> [-A <arch>] [-C <num-lines>] [-c <num-lines>] [-F <disassembly-flavor>] [-P <plugin>]
  disassemble [-bmr] [-A <arch>] [-C <num-lines>] [-c <num-lines>] [-F <disassembly-flavor>] [-n <function-name>] [-P <plugin>]
  disassemble [-bfmr] [-A <arch>] [-C <num-lines>] [-c <num-lines>] [-F <disassembly-flavor>] [-P <plugin>]
  disassemble [-bmpr] [-A <arch>] [-C <num-lines>] [-c <num-lines>] [-F <disassembly-flavor>] [-P <plugin>]
  disassemble [-blmr] [-A <arch>] [-C <num-lines>] [-F <disassembly-flavor>] [-P <plugin>]
  disassemble [-bmr] [-a <address-expression>] [-A <arch>] [-C <num-lines>] [-c <num-lines>] [-F <disassembly-flavor>] [-P <plugin>]

       --force
            Force dissasembly of large functions.

       -A <arch> ( --arch <arch> )
            Specify the architecture to use from cross disassembly.

       -C <num-lines> ( --context <num-lines> )
            Number of context lines of source to show.

       -F <disassembly-flavor> ( --flavor <disassembly-flavor> )
            Name of the disassembly flavor you want to use. Currently the only
            valid options are default, and for Intel architectures, att and
            intel.

       -P <plugin> ( --plugin <plugin> )
            Name of the disassembler plugin you want to use.

       -a <address-expression> ( --address <address-expression> )
            Disassemble function containing this address.

       -b ( --bytes )
            Show opcode bytes when disassembling.

       -c <num-lines> ( --count <num-lines> )
            Number of instructions to display.

       -e <address-expression> ( --end-address <address-expression> )
            Address at which to end disassembling.

       -f ( --frame )
            Disassemble from the start of the current frame's function.

       -l ( --line )
            Disassemble the current frame's current source line instructions if
            there is debug line table information, else disassemble around the
            pc.

       -m ( --mixed )
            Enable mixed source and assembly display.

       -n <function-name> ( --name <function-name> )
            Disassemble entire contents of the given function name.

       -p ( --pc )
            Disassemble around the current pc.

       -r ( --raw )
            Print raw disassembly with no symbol information.

       -s <address-expression> ( --start-address <address-expression> )
            Address at which to start disassembling.
```
