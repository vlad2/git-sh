Fork information
===================
    This is a fork from the original git-sh repository at https://github.com/rtomayko/git-sh

    What this fork has different is:

    - mv and rm aren't aliased to git command
    - improved documentation: color.sh.upstream-state is documented in README.markdown
    - add 'git flow' support from https://github.com/taupecat/git-sh/commit/9f696085822415453967e82d8825e917506c328b
    - add 'git worktree' support from https://github.com/selivan/git-sh
    - this README is updated (to show this Fork information section, also the Installation points to this repository)

git-sh
======

A customized bash shell suitable for git work.


The `git-sh` command starts an interactive bash shell tweaked for heavy git
interaction:

  * All git commands available at top-level
    (`checkout master` = `git checkout master`)
  * All git aliases defined in the `[alias]` section
    of `~/.gitconfig` available at top-level.
  * Shawn O. Pearce's excellent bash completion strapped onto
    all core commands and git aliases.
  * Custom prompt with current branch, repository, and
    work tree dirty indicator.
  * Customizable via `/etc/gitshrc` and `~/.gitshrc` config files;
    for creating aliases, changing the prompt, etc.
  * Runs on top of normal bash (`~/.bashrc`) and
    readline (`~/.inputrc`) configurations.

Installation
------------

Install the most recent available version under `/usr/local`:

    $ git clone git://github.com/vlad2/git-sh.git
    $ cd git-sh
    $ make
    $ sudo make install

Start a shell with `git-sh`:

    $ git-sh
    master!git-sh> help

Use the `PREFIX` environment variable to specify a different install location.
For example, under `~/bin`:

    $ make install PREFIX=~

Basic Usage
-----------

Typical usage is to change into a git working copy and then start the shell:

    $ cd mygreatrepo
    $ git sh
    master!mygreatrepo> help

Core git commands and git command aliases defined in `~/.gitconfig` can be
used as top-level commands:

    master!mygreatrepo> checkout -b new
    new!mygreatrepo> log -p
    new!mygreatrepo> rebase -i HEAD~10

It's really just a normal bash shell, though, so all commands on `PATH` and any
aliases defined in `~/.bashrc` are also available:

    new!mygreatrepo> ls -l
    new!mygreatrepo> vim somefile

*IMPORTANT: `diff` is aliased to its git counterpart.  To use system versions,
run `command(1)` (e.g., `command diff`) or qualify the command (e.g. `/bin/diff`).*

Prompt
------

The default prompt shows the current branch, a bang (`!`), and then the relative
path to the current working directory from the root of the work tree.  If the
work tree includes modified files that have not yet been staged, a dirty status
indicator (`*`) is also displayed.

The git-sh prompt includes ANSI colors when the git `color.ui` option is 
enabled. To enable git-sh's prompt colors explicitly, set the `color.sh` config
value to `auto`:

    $ git config --global color.sh auto

Customize prompt colors by setting the `color.sh.branch`, `color.sh.workdir`,
and `color.sh.dirty` git config values:

    $ git config --global color.sh.branch 'yellow reverse'
    $ git config --global color.sh.workdir 'blue bold'
    $ git config --global color.sh.dirty 'red'
    $ git config --global color.sh.dirty-stash 'red'
    $ git config --global color.sh.repo-state 'red'
    $ git config --global color.sh.upstream-state 'yelow'

See [colors in git](http://scie.nti.st/2007/5/2/colors-in-git) for information.

Customizing
-----------

Most `git-sh` behavior can be configured by editing the user or system gitconfig
files (`~/.gitconfig` and `/etc/gitconfig`) either by hand or using
`git-config(1)`. The `[alias]` section is used to create basic command aliases.

The `/etc/gitshrc` and `~/.gitshrc` files are sourced (in that order)
immediately before the shell becomes interactive.

The `~/.bashrc` file is sourced before either `/etc/gitshrc` or `~/.gitshrc`.
Any bash customizations defined there and not explicitly overridden by `git-sh`
are also available.

Copying
-------

Copyright (C) 2008 [Ryan Tomayko](http://tomayko.com/)  
Copyright (C) 2008 [Aristotle Pagaltzis](http://plasmasturm.org/)  
Copyright (C) 2006, 2007 [Shawn O. Pearce](mailto:spearce@spearce.org)

This program is free software; you can redistribute it and/or modify it
under the terms of the GNU General Public License, version 2, as published
by the Free Software Foundation.
