# rcov.el

`rcov.el` allows you to use rcov from Emacs conveniently.

* Run unit tests and jump to uncovered code by <code>C-x `</code>
* Run unit tests and save the current coverage status.
* Run unit tests and jump to uncovered code introduced since the last run.
* View cross-reference annotated code.

## Installation

Copy <tt>rcov.el</tt> to the appropriate directory, which is in load-path then require it.

`(require 'rcov)`

## Usage

There are some commands to run RCov in Emacs.  All of them will display RCov window, whose `major-mode` is `compilation-mode`.  This allow you to jump to uncovered code using C-x `. rcov-command-line, rcovsave-command-line, and rcovdiff-command-line define command line to run rcov. If you do not use RCov from Rake, you must modify them.

### Finding uncovered code

Type the following while editing your program:
  
`M-x rcov`
  
### Setting the reference point

RCov's `--text-coverage-diff` mode compares the current coverage status against the saved one. It therefore needs that information to be recorded before you write new code (typically right after you perform a commit) in order to have something to compare against. You can save the current status with the `--save` option. Type the following to save the current status in Emacs:

`M-x rcovsave`

If you do not use RCov from Rake, you must modify `rcovsave-command-line` variable.

### Finding new uncovered code

Type the following to save the current status in Emacs:
  
`M-x rcovdiff`

### Viewing cross-reference annotated code

If you read cross-reference annotated code, issue

`rake rcov RCOVOPTS='-a'`

at the beginning.  This command creates a `coverage` directory and many `*.rb` files in it.  Filenames of these Ruby scripts are converted from original path.  You can browse them by normally `C-x C-f`.  You can think of `-a` option as `--xrefs` option and output format is Ruby script.  After `find-file-ed` annotated script, the `major-mode` is `rcov-xref-mode`,
which is derived from `ruby-mode` and specializes navigation.

* `Tab` and `M-Tab` goes forward/backward links.
* `Ret` follows selected link.

This feature is useful to read third-party code or to follow control flow.
