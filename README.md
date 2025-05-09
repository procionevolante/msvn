msvn
====

msvn stands for _my svn_ and is an svn wrapper to ease using svn in a terminal.

Contrarily to git, svn is not so console-friendly out of the box: for example,
output is not paginated or colored, it just goes straight out to the terminal.

This wrapper tries to fix this and adds a bunch of quality of life commands on
top of it.

Since it was initially used on a windows machine, it can also be sourced by a
windows `bash` (eg. cygwin, git-bash, MSYS64, ...) and its main function,
`mysvn`, aliased to `svn`.
Windows is slow at starting new processes but in this way invoking `msvn` gets
somewhat faster.

Features
--------

Listed from more basic to more complex:
* pipe output of many commands to `less -F`, like on git
* include line numbers in `blame` output (and use a pager, duh)
* new command `bat`: like `svn cat` but with syntax highlighting
* colored `diff` output
* new command `dst`|`dstat`: diff with stats similar to `git diff --stat`
* new command `ddi`|`ddiff`: wordwise diff with syntax-highlighting
* new command `sddi`: same as `ddi` but side-by-side
* new command `slog` (short-log): output similar to `git log --oneline` using
  [`short-log`](short-log)
* repo path expansion: if path starts with "`/`" msvn will try to figure out the
  true root of the repo within remote.
  Useful if the same server is used to host multiple repos and you can't use the
  already present "`^`" svn shortcut.  
  Example: if current checked out dir is `^/nucular-launch-codes/branches/Mario`
  and you call `msvn diff /branches/Luigi` it will get converted to
  `svn diff ^/nucular-launch-codes/branches/Luigi`
* new command `sr` (set root):
  output command to set the `$sr` shell variable to the true root of the repo.  
  Use alternatively to the `/` path expansion of the previous point by
  running `eval $(msvn sr)` and then the cmd that relies on `$sr`
  (ex. `msvn di "$sr/branches/Mario"`)
* improved bash completion script with support for changelists.
  Use it by running `eval "$(msvn completions)"` in your `~/.bashrc` file or
  similar
* support for pre-commit hooks similarly to git: place a `pre-commit` executable
  in `.svn/hooks/` in your repo.
  It will be invoked in the current working directory with all arguments
  following `svn commit` as `argv`.
  If the program returns with an error the commit is aborted.  
  An example `pre-commit` file is provided

Installation
------------

1. Clone the repo to `~/src/msvn` or another dir.
(A couple commands -`completions`, `slog`- rely on the repo being checked out
there: If you use another dir, edit the script to point to the real dir)
2. Add the `msvn` script to `PATH`.
3. (optional) alias `msvn` to `svn` in your shell

Dependencies
------------

* [bat](https://github.com/sharkdp/bat)
* [diffstat](https://invisible-island.net/diffstat/)
* [delta](https://github.com/dandavison/delta)

<!--
vim: tw=80
-->
