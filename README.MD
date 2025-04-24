
# MAKESHARE

An OpenVMS command-line utility that creates a DCL command procedure to link
a shared imaged from an object library.

---

### Usage

This utility must be executed via a global symbol:
```
    $ MAKESHARE:==$DISK:[DIRECTORY]MAKESHARE.EXE
```
### Options
```
    $ MAKESHARE -l <library> [-e <location>] [-s <suffix>] [-q]
                             [-m] [-sql] [-sd <n>] [-sp <n>]

    -l <library>     The name of the object library to create a shared image
                     from. Disk and directory names, and logical names may be
                     used.

    -e <location>    Specifies a location in which to create the shared image
                     executable. Specify a directory or logical name including
                     a colon.

    -s <suffix>      Specifies a suffix for the shared image executable name

    -xd              Add support for xfServerPlus debugging

    -m               Generate a linker map file

    -sql             Link against the SQL Connection shared image

    -tk              Link against the UI Toolkit shared image

    -sd <n>          Include n spare symbol vector positions for data

    -sp <n>          Include n spare symbol vector positions for procedures

    -q               Quiet mode, don't display file created message
```
### Example 1
```
    $ makeshare -l MYLIB.OLB

         Creates a command procedure named MYLIB.COM which can be used to link
         a shared image named MYLIB.EXE. The object library must be in the
         current directory, and the resulting command procedure and shared image
         will also be created in the current directory. No linker map file will
         be created, and there will be no spare slots in the symbol vector for
         either data or procedures.
```
### Example 2
```
    $ makeshare -l LIB:MYLIB.OLB -e EXE: -s _SH -sql -sd 10 -sp 100 -m

         Creates a command procedure named MYLIB.COM which can be used to link
         a shared image named EXE:MYLIB_SH.EXE. The object library will be
         located in the directory referenced by the LIB: logical name. The
         shared image will be created in the directory referenced by the EXE:
         logical name, and its name will be suffixed with _SH. The resulting
         shared image will be linked against the SQL Connection API shared image
         and will have 10 spare slots in the symbol vector for additional data
         items and 100 spare slots for additional procedures. A linker map file
         named MYLIB_SH.MAP will be created in the current directory.
```
