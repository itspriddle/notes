---
title: Git Pro Tips
date: "Wed Oct 30 23:03:28 -0400 2019"
tags: [git]
---

# Git Pro Tips

Here are some of useful git configs and aliases.

Most of these settings are in `~/.gitconfig`, the global git configuration
file.

Note that this duplicates configuration names like `[alias]` in different
sections. Your `~/.gitconfig` file should only include one `[alias]` line, and
all aliases should appear under.

## Default Branch

Recent versions of git use `main` as the branch name when setting up a new
repo. If you prefer to stay with `master`, you can configure it:

```
[init]
  defaultBranch = master
```

## Colors

If you like color everywhere:

```
[color]
  ui = auto
```

You can also customize the colors used for various actions (see `man
git-config` for more info):

```
; Colors for `git status`
[color "status"]
  header    = yellow bold
  added     = green bold
  updated   = green reverse
  changed   = magenta bold
  untracked = red

; Colors for `git diff`
[color "diff"]
  meta       = yellow bold
  frag       = magenta bold
  old        = red bold
  new        = green bold
  whitespace = red reverse
```

## Default `--pretty` format

For things like `git log`, `git show`, etc, you can keep things simple and
concise by setting the following:

```
[format]
  pretty = format:%C(red)%h%Creset%C(yellow)%d%Creset %C(magenta)%an%Creset: %s %C(green)(%ar)%Creset
```

For `git log`, git shows commits on a single line with only the most useful
information present.

You can still use `git show --format=fuller [sha]` to see the _full_ details
of a commit when more context is needed (see the `git showf` alias below).

## Pulling Branches

Ever run `git fetch` and see dozens of remote branches pulled in? If you run
`git branch --remotes` you'll likely see references to old branches that have
already been merged in to master. You can tell git to clean these
automatically, any time you run `git fetch` or `git pull`, with the following
setting:

```
[fetch]
  prune = true
```

Like to handle things manually? You can create a `git prune-branches` alias:

```
[alias]
  prune-branches = !git branch --merged | grep -v '^master$' | grep -v "\\\\*" | xargs -n 1 git branch -d
```

If you want to always `git pull --rebase`, you can configure it with:

```
[pull]
  rebase = true
```

## Pushing Branches

In older versions of git, `git push` without any branch specified would push
_all_ branches to origin. Since this is hardly ever what you'd want, it is now
disabled by default. But if you want to keep safe in case you come cross any
old git versions, you can add the following:

```
[push]
  default = current
```

This makes `git push` operate on the currently checked out branch only.

## Viewing Branches

You may have a few different branches being worked on at once and it can be
useful to see them by the last commit date. The following enables this
behavior by default when running `git branch` commands to list branches:

```
[branch]
  sort = -authordate
```

You can also use the following `git recent-branches` alias to show the 10 most
recent branches, sorted by date:

```
[alias]
  recent-branches = for-each-ref --count=10 --sort=-committerdate --format=\"%(refname:short)\" refs/heads/
```

Need the current branch name? Try a `git branch-name` alias (also try `git
branch-name | pbcopy` on MacOS to copy it to your clipboard):

```
[alias]
  branch-name = rev-parse --abbrev-ref HEAD
```

## Disable advice

Git is nice enough to provide advice on certain commands. For example, `git
status` will show advice on how to `git add` files. You may find some of these
annoying so they can be disabled with the following:

```
[advice]
  statusHints        = false
  pushNonFastForward = false
```

See the `advice.*` section under `man git-config` for more places advice is
printed.

## Nicer `git status`

For a more concise status output, `git status --short --branch` (or `git
status -sb`) can be used. It can be setup by default using:

```
[status]
  short = true
  branch = true
```

Want a verbose status once in a while? Try `git status --no-short`.

## Viewing commits

If you set a `git log` format to be simple as outlined above, you might want a
quicker way to use `git show --format=fuller` to view full details on a single
commit:

```
[alias]
  showf = show --format=fuller
```

_Note:_ `git showf` can optionally have a branch/commit specified. Without
arguments it will use `HEAD` (i.e. that current branch/latest commit). You
could also specify `git showf deadbeef` to see a specific commit.

For a graph view of different branches and their merge points you can setup
`git lg`:

```
[alias]
  lg = log --graph --abbrev-commit --date=relative
```

For when you want full log details there's `git full-log`:

```
[alias]
  full-log = log --format=fuller
```

If you need to see the last commit SHA, perhaps for pasting into GitHub or a
Jira ticket, you can setup `git last-sha`:

```
[alias]
  last-sha = rev-parse --short HEAD
```

You can see the commits you've made to a local branch but haven't yet pushed
upstream with `git pending`:

_Note:_ this requires you pushed with `git push -u` to track your remote.

```
[alias]
  pending = !git --no-pager log @{u}.. && echo
```

You can see the last committer with `git last-committer`:

```
[alias]
  last-committer = !git --no-pager log --pretty="%an" --no-merges -1
```

Or you can see the last commit subject with `git last-subject` (great for
copy/pasting into pull requests/tickets):

```
[alias]
  last-subject = !git --no-pager log --pretty="%s" -1
```

Sometimes you want to see just the filenames that were changed in a commit, and
`git show-files` does this. It can also work on a branch, like `git show-files
master..HEAD` to show everything changed on the current branch vs master. This
is great when you want to run tests or linters on those files (eg
`make-me-pretty $(git ls-files master..HEAD)`):

```
[alias]
  show-files = !git --no-pager show --name-only --format=
```

On MacOS or a system with Ruby's webrick gem installed, `git web` will spawn a
web interface for browsing (close with `git web --close`):

```
[alias]
  web = instaweb --httpd=webrick -b open
```

## Undoing things

For when you've run `git add` on files and you want to back out, `git unstage`
does the job (`git unstage -- .` to unstage everything, or `git unstage --
file1` to specify files):

```
[alias]
  unstage = reset HEAD -- ...
```

If you've already committed, you can setup `git undo` to undo the commit
(which can then be unstaged with `git unstage`):

```
[alias]
  undo = reset --soft HEAD^
```

If you've made a typo and haven't pushed yet, `git amend` can be setup to
amend the last commit. You might `git amend -a` or `git add changed-file;
git amend`. You might want to reset the date as well so that the commit shows
up as expected in views sorting by date:

```
[alias]
  amend = !git commit --amend --date=\"$(date)\" -C HEAD
```

## Per-System overrides

If you keep your personal git life and work git life separate, you can keep
default settings in `~/.gitconfig` and overrides in a separate file.

For example you might default to using your personal email in `~/.gitconfig`:

```
[user]
  email = josh@josh.fail
```

In `~/.gitconfig` you can specify a local include, with system specific
configuration file:

```
[include]
  path = ~/.gitconfig.local
```

Then in _that_ `~/.gitconfig.local` file, specific customizations are made:

```
[user]
  email = work@josh.fail
```

## Customizing Your GIT_EDITOR

For git commands like `git commit` or `git tag` where you might want to use a
text editor to draft the associated message, you can set the `$GIT_EDITOR`
environment various or the `core.editor` git config.

To use the environment variable, add to `~/.zprofile` for ZSH or
`~/.bash_profile` for Bash:

```
export GIT_EDITOR=vim
```

Or to set via `~/.gitconfig`:

```
[core]
  editor = vim
```

Want to use VS Code instead?

```
export GIT_EDITOR="code --wait"
```

Or in `~/.gitconfig`:

```
[core]
  editor = code --wait
```

## Directory-based Git Author

A directory-based alternative to override your git author is to use [direnv][]
to configure author/committer git environment variables while under a certain
directory.

If you just need to change your email, you could setup a `.envrc` file in the
root directory where you keep your A2 projects cloned -- for example
`~/work/a2/.envrc`.

```
export GIT_AUTHOR_EMAIL=work@josh.fail
export GIT_COMMITTER_EMAIL=work@josh.fail
```

If you want to change your name too for some reason:

```
export GIT_AUTHOR_NAME="Josh Danger Priddle"
export GIT_COMMITTER_EMAIL="Josh Danger Priddle"
```

With that in place, any time you `cd ~/work/a2` (or any subdirectory), `git
commit` will automatically use the values you've set.

[direnv]: https://direnv.net

## "Local" gitignore

If you need to ignore files or directories in your own copy of a cloned repo,
you can add ignore rules to `.git/info/exclude`. For example, if you kept some
personal scripts in `_my_scripts/` you could add `_my_scripts/*` to
`.git/info/exclude` to tell git to ignore it without it impacting other
developers.

_Note:_ Use this feature sparingly and with caution. If multiple developers
need to ignore the same files, you should use a regular `.gitignore` file.

## Utilities

When you first setup a new repo you need to make a first commit. You can
setup `git msg` to allow committing with no content and just a message:

```
[alias]
  msg = commit --allow-empty -m
```

Use `git msg "First commit"` then checkout a new branch with your code.

If you need a way to determine the root directory of a project, you can setup
`git root`:

```
[alias]
  root = rev-parse --show-toplevel
```

Want to scan for TODO/FIXME comments? You can setup `git todo`:

```
[alias]
  todo = grep -wniI -e TODO -e FIXME
```

Need the last commit sha from the previous pull?

```
[alias]
  last-pull-sha = !"git reflog | awk '/: pull / { if (l == 1) { print $1; exit }; l+=1 }'"
```

Rollback with `git checkout "$(git last-pull-sha)"`.

## Bonus: Bash/ZSH aliases

These shell aliases cover very common git operations. They can be added to
`~/.bashrc` for Bash users or `~/.zshrc` for ZSH users.

The obvious ones:

```
alias gb='git branch'
alias gbd='git branch -d'
alias gco='git checkout'
alias gd='git diff'
alias gdc='git diff --cached'
alias gs='git status'
```

For when you've deleted a lot of files from a repo you can use `grm` to remove
them from git as well:

```
alias grm="git status --porcelain | awk '\$1 == \"D\" {print \$2}' | xargs git --git-dir=\$(git rev-parse --git-dir) rm --ignore-unmatch"
```

Finally, `gcomp` and `gcomp-` (mnemonic: **g**it **c**heckout **m**aster
**p**ull). `gcomp` checks out master and pulls, `gcomp-` checks out master and
pulls, _then_ checks out the previous branch. Any time you're about to push up
a new pull request you can run `gcomp- && git rebase master` to make sure
you're up to date.

```
alias gcomp='git checkout master; git pull'
alias gcomp-='git checkout master; git pull; git checkout -'
```
