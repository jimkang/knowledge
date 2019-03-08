# Find out where on the computer it's getting <header.h> files from

`gcc -print-search-dirs`

If that returns too many directories to look through, you can do `gcc -H thefile.c`, and gcc will print the full path of all of the header files included in thefile.c.
