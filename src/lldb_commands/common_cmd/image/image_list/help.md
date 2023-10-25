# image list的help语法

```bash
(lldb) help image list
List current executable and dependent shared library images.

Syntax: target modules list <cmd-options> [<shlib-name> [<shlib-name> [...]]]

Command Options Usage:
  target modules list [-ghou] [-a <address-expression>] [-A[<width>]] [-b[<width>]] [-d[<width>]] [-f[<width>]] [-m[<width>]] [-p[<none>]] [-r[<width>]] [-s[<width>]] [-S[<width>]] [-t[<width>]] [<shlib-name> [<shlib-name> [...]]]

       -A[<width>] ( --arch=[<width>] )
            Display the architecture when listing images.

       -S[<width>] ( --symfile-unique=[<width>] )
            Display the symbol file with optional width only if it is different
            from the executable object file.

       -a <address-expression> ( --address <address-expression> )
            Display the image at this address.

       -b[<width>] ( --basename=[<width>] )
            Display the basename with optional width for the image object file.

       -d[<width>] ( --directory=[<width>] )
            Display the directory with optional width for the image object
            file.

       -f[<width>] ( --fullpath=[<width>] )
            Display the fullpath to the image object file.

       -g ( --global )
            Display the modules from the global module list, not just the
            current target.

       -h ( --header )
            Display the image base address as a load address if debugging, a
            file address otherwise.

       -m[<width>] ( --mod-time=[<width>] )
            Display the modification time with optional width of the module.

       -o ( --offset )
            Display the image load address offset from the base file address
            (the slide amount).

       -p[<none>] ( --pointer=[<none>] )
            Display the module pointer.

       -r[<width>] ( --ref-count=[<width>] )
            Display the reference count if the module is still in the shared
            module cache.

       -s[<width>] ( --symfile=[<width>] )
            Display the fullpath to the image symbol file with optional width.

       -t[<width>] ( --triple=[<width>] )
            Display the triple when listing images.

       -u ( --uuid )
            Display the UUID when listing images.
     
     This command takes options and free-form arguments.  If your arguments
     resemble option specifiers (i.e., they start with a - or --), you must use
     ' -- ' between the end of the command options and the beginning of the
     arguments.

'image' is an abbreviation for 'target modules'
```
