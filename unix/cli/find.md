# find

List files, skipping .git directory:

    find . -path ./.git -prune -o -ls

List files, null-separated:

    find . -type f -print0 | xargs -0 -n1 echo

List open files of process 123:

    find /proc/123/fd -printf "%p %l\n"

List pids sorted by number of open files:

    find /proc/ -regex "/proc/[0-9]+/fd/[0-9]+" -printf "%p\n" |
        cut -d'/' -f3 |
        uniq -c |
        sort -k1,1rn

If the path given to find is relative, find will also print relative
paths, but prefixed with "./". Otherwise find will print out absolute
paths. This is true even when using -printf.

Regexes in find are Emacs-style regexes, unless `-regextype` is
specified.

## Options

### Tests

- `-type <type>` `type` is `f` for regular files, `d` for directories,
  `l` for symlinks - types can be combined with comma
- `-name <glob>` file name matches `glob`
- `-iname <glob>` file name matches `glob`, case-insensitively
- `-path <glob>` file path matches `glob`
- `-ipath <glob>` file path matches `glob`, case-insensitively
- `-regex <regex>` file path matches `regex`
- `-iregex <regex>` file path matches `regex`, case-insensitively

### Actions

- `-print0` print filename terminated with null byte
- `-printf <format>` print file information given by `format`
- `-ls` print file information in ls-like format
- `-exec <cmd> \;`
- `-exec <cmd> {} \;`
- `-exec <cmd> {} \+`
- `-execdir <cmd> \;`

### Printf format strings

- `%p` file path
- `%P` file path, with the starting point removed
- `%f` file name
- `%l` file symlink target, if symlink
- `%Tc` file last modification date, in locale format
- `%u/%g` file owner username/groupname
- `%U/%G` file owner uid/gid
