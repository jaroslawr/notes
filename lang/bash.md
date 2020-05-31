# bash

## Parsing

### Order of expansions

Bash processes input by performing the following expansions in the order listed:
- brace expansion
- tilde expansion
- parameter and variable expansion
- arithmetic expansion
- command substitution (done in a left-to-right fashion)
- process substitution
- word splitting
- globbing (referred to as "filename expansion" in bash manual)
- quote removal

<https://www.gnu.org/software/bash/manual/html_node/Shell-Expansions.html>

### Quoting

- `''` Constructs literal string, no interpolation
- `$''` Understand basic escapes like `\n`, `\t` and `\'`
- `""` Does variable interpolation, command substitution etc.

Quoting prevents arguments from undergoing word splitting.

### Command substitution

Command substitution is done using `$()` or `\`\``.

`$()` is generally preferred since it can be nested without quoting.

### Word splitting

The IFS variable controls how raw input string will be split into separate
arguments.

By default IFS includes newline, tab and space.

## Functions

POSIX way of defining functions is:

    do_thing() { ... }

Bash additionally permits:

    function do_thing() { .... }

Function arguments are accessed as `$1`, `$2`, ...

## Control structures

### for x in y loops

for x in y expands y like command line arguments and makes x assume the value of
each individual argument in turn. 

### while read loops

<https://stackoverflow.com/questions/2746553/read-values-into-a-shell-variable-from-a-pipe>

### Looping over files

With a for loop:

    for f in ./*; do
       [command] "$f"
    done

The `./` in the `./\*` glob prevents filenames starting with `-` to be
interpreted as options (since they will be expanded as `./-something`). The
`"` in `"$f"` prevent word splitting from acting on the file name.

`find` and a `while read` loop give more control over which files to process:

    find . -print0 | while IFS= read -r -d'' file; do
        mv "$file" "$file.bak"
    done

`-print0` makes find delimit the file names with a null byte. `-d ''` argument
to read causes null byte to be used as record separator, and setting a blank IFS
makes sure that the record is not word-split - whole file name ends up in `file`
variable.

## Tests

- `[[]]` is non-POSIX. Contents of `[[]]` have their own specific parsing rules,
  for example they do not undergo word splitting. `[[]]` also has extra features
  compared to regular `[]` like regex matching.

- `[]` is POSIX, uses `test` builtin to do the testing. Contents of `[]` are
  parsed like a regular command invocation.

- `(())` is non-POSIX, does arithmetic tests.

### `[[]]` tests

### `[]` tests

### `(())` tests

## Subshells

## Here documents

## Redirection of file descriptors

## Misc

### Standard readline keybindings 

### Changing directories

- `cd` go to home directory
- `cd -` go to previous directory

### History expansion

- `!!` last command
- `!^` first arg of last command
- `!$` last arg of last command
- `!:n` nth arg of last command
- `!\*` args of last command

### Special variables

- `$PWD` - current working directory
- `$?` - exit code of last command

### Builtins

- `help x` - display help for `x` builtin
- `read x` - read into variable `x`
    - `-r` disables interpreting backslash escapes
    - `-d` specifies the record delimiter
    - `IFS` specifies the field delimiter

## Personal coding style

- Use `""` quoting as much as possible
- Use braces in variable references, always write `${FOO}`
- Use `[[]]` for tests
- Use `$()` for command substitution
- Declare functions as `fun() {...}`
