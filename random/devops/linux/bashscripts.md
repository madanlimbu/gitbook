# Bashscripts

#### Exit status

```text
set -e  # Exit immediately if a command exits with a non-zero status.
```

[Shell scripts](https://en.wikipedia.org/wiki/Shell_script) typically execute commands and capture their exit statuses.

For the shell’s purposes, a command which exits with a zero exit status has succeeded. A nonzero exit status indicates failure.

#### Dirname & $0

```text
dirname $0 - relative path to script from where script is ran
```

#### Source / Dot Operator

`source filename [arguments]` or `.`  - executes the content of file passed as argument in the current shell. \( which means we can import variable / function / script from another script file \)

  

[http://linuxcommand.org/lc3\_man\_pages/seth.html](http://linuxcommand.org/lc3_man_pages/seth.html)

