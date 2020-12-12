# Oh, a new Unix shell

## Why oh?

Oh is a reimagining of the Unix shell as a programming language.

Oh's goal is a language that is not only more powerful and more regular
but one that works with and within the interactive constraints and
conventions established by the Unix shell over the last half-century.

## Getting started

### Installing oh

The easiest way to try oh is to download a precompiled binary. There
are oh binaries for Linux, macOS, DragonflyBSD, FreeBSD, OpenBSD and
Solaris/Illumos.

[TODO: Add link to binaries for current release]

Alternatively, oh can be build from source. With a recent version of
Go installed, type,

    go get github.com/michaelmacinnis/oh

to install oh.

### Configuring oh

When oh starts it attempts to read a file called `.oh-rc` in the home
directory of the current user. This path can be overridden by setting
the OH_RC environment variable to an alternative file's full path
before invoking oh.

The oh rc file is useful for setting environment variables and defining
custom commands. It's also a good place to override oh's default prompt.
The commands below replaces oh's default make-prompt method with one that
displays the current date.

    define make-prompt: method (suffix) {
        return `(date)$suffix
    }
    
    define old-make-prompt: replace-make-prompt $make-prompt

Oh also provides a searchable command history. This history is stored
in a file called `.oh-history` in the home directory of the current
user. This path can also be overridden but setting the OH_HISTORY
environment variable to the full path of an alternative location before
invoking oh.

## Comparing oh to other Unix shells

Oh is a Unix shell. If you've used other Unix shells, oh should feel
familiar. Below are some specific differences you may encounter.

### Clobbering

When redirecting output oh will not overwrite an existing file. To force
oh to overwrite (clobber) and existing file add a pipe, `|`, character
immediately after the redirection operator. For example,

    command >| out.txt

### Command substitution

Many Unix shells support command substitution using the historical
backtick syntax,

    `command`

or the POSIX syntax,

    $(command)

Oh has one syntax for command substitution,

    `(command)

This syntax is both nestable and unambiguous.

### Here documents

Oh does not have heredocs. It does however allow strings to span lines
and provides a here command that takes a string argument and serves a
similar purpose. For example,

    # Build oh for supported BSD platforms
    here "
    dragonfly amd64
    freebsd 386
    freebsd amd64
    freebsd arm
    freebsd arm64
    openbsd 386
    openbsd amd64
    openbsd arm
    openbsd arm64
    " | mill (o a) {
        echo ${o}/${a}
        GOOS=${o} GOARCH=${a} go build -o oh_${o}_${a}
    }

### Variables and implicit concatenation

Like other shells, oh implicitly concatenates adjacent string/symbol
values. Unlike other shells, oh allows is more generous when it comes to
the characters that can appear in a symbol. What this means, is that it
is that when implicit concatenation is being used variable names should
be enclosed in curly braces, `{}`, to avoid unexpected behavior.

### More information

For a detailed comparison to other Unix shells see: [Comparing oh to other Unix Shells](https://htmlpreview.github.io/?https://raw.githubusercontent.com/michaelmacinnis/oh/master/doc/comparison.html)

## Using oh

For more information on using oh, see: [Using oh](doc/manual.md)

## License

[MIT](LICENSE)

