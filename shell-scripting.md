# Replacing characters in strings

If `title` is `o hay guys`, this

    echo "${title// /\ }"

will replace each space with a `\ ` and print:

    o\ hay\ guys

The double slash right after the variable indicates that all instances should be replaced. The syntax is not quite regex.

# Replacing strings in files

In a shell script, using single quotes will make the script take it literally and not resolve variable references. However, double quotes do not do that while also satisfying `sed` when you need to provide an expression that has spaces in it.

Here is a script that replaces all instances of `__PLACEHOLDER__` with `replacement`, whose value has spaces in it:

    #!/bin/bash

    replacement="o hay guys"

    cleaned="${replacement// /\\ }"

    echo "$cleaned"

    sed -i '' "s/__PLACEHOLDER__/$cleaned/g" test.html
