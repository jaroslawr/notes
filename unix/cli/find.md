# find

List files, skipping .git directory:

    find . -path ./.git -prune -o -ls

List files, null-separated:

    find . -type f -print0 | xargs -0 -n1 echo

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

- `%p` file name
- `%l` symlink target, if symlink
