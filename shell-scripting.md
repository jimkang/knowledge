# Replacing characters in strings

If `title` is `o hay guys`, this

    echo "${title// /\ }"

will replace each space with a `\ ` and print:

    o\ hay\ guys

The double slash right after the variable indicates that all instances should be replaced. The syntax is not quite regex.
