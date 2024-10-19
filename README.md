# envy
A simple bash program to spawn subshells for python venvs

Inspired by the `poetry shell` and `aws-sso exec` commands, this command invokes a subshell and automatically sources `.venv/bin/activate` in the current directory (or searches for a valid venv up the directory tree, for the dozens of us who like using `git worktree`). Also enables creating venvs in one command as well.

TLDR: Replace `$ python -m venv .venv; source .venv/bin/activate` with `$ envy`. No more fumbling with stupid typos, ain't got time to hit all those keys! I just want a shell that's ready to go!

NOTE: This only supports `bash` and `zsh` at the moment.

## Installation
Use your preferred way of installing an executable to your `PATH`. I suggest using `curl`:
```bash
$ mkdir -p ~/.local/bin
$ [[ ":$PATH:" != *":~/.local/bin:"* ]] && PATH="~/.local/bin:${PATH}"
$ curl https://raw.githubusercontent.com/BlakeJC94/envy/main/envy --output ~/.local/bin/envy
$ chmod a+x ~/.local/bin/envy
```

## Usage
Documentation can be viewed with `$ envy --help`:
```
envy
Subshell spawner for Python

This utility searches the current directory for a virtual environment
in the current directory, travels up the directory tree (up to the
users home directory) until a virtual env is found, then spawns a
subshell that sources '.bashrc' and the virtual environment (and sets
a value for 'ENVY').

By default, searches for a virtual environment called '.venv', can be
specified in the first argument.

If a virtual environment is not found, a new virtual environment is
created at the current directory and a subshell sourcing the new venv
is invoked.

Different venvs can be targeted/created via first positional arg (e.g.
look for '.venv-foo' by using 'envy foo').

USAGE:
    envy [OPTIONS] [NAME]

ARGS:
    NAME            Virtual env suffix to search/create (default: '')

OPTIONS:
    -h, --help                                     Show documentation
    -n, --new         Skip search and create/activate new virtual env
```

## Oh My Zsh! Compatibility

Ensure that the `virtualenv` plugin in enabled
```zsh
# ~/.zshrc
plugins=(... virtualenv)
```

And make sure to use a theme with `virtualenv` support. To modify the default robbyrussell
theme:
```diff
# ~/.oh-my-zsh/themes/robbyrussell.zsh-theme
-PROMPT="%(?:%{$fg_bold[green]%}%1{➜%} :%{$fg_bold[red]%}%1{➜%} ) %{$fg[cyan]%}%c%{$reset_color%}"
+PROMPT='$(virtualenv_prompt_info) '
+PROMPT+="%(?:%{$fg_bold[green]%}%1{➜%} :%{$fg_bold[red]%}%1{➜%} ) %{$fg[cyan]%}%c%{$reset_color%}"
 PROMPT+=' $(git_prompt_info)'

+ZSH_THEME_VIRTUALENV_PREFIX="("
+ZSH_THEME_VIRTUALENV_SUFFIX=")"
+
 ZSH_THEME_GIT_PROMPT_PREFIX="%{$fg_bold[blue]%}git:(%{$fg[red]%}"
 ZSH_THEME_GIT_PROMPT_SUFFIX="%{$reset_color%} "
 ZSH_THEME_GIT_PROMPT_DIRTY="%{$fg[blue]%}) %{$fg[yellow]%}%1{✗%}"
```

## TODO
* [x] zsh and fish support?
