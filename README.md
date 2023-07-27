# envy
A simple bash program to spawn subshells for python venvs

Inspired by the `poetry shell` and `aws-sso exec` commands, this command invokes a subshell and automatically sources `.venv/bin/activate` in the current directory (or searches for a valid venv up the directory tree, for the dozens of us who like using `git worktree`). Also enables creating venvs in one command as well.

No more fumbling with `python -m venv .venv; source .venv/bin/activate`, ain't got time to hit all those keys! I just want a shell that's ready to go!

NOTE: This only supports `bash` at the moment.

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

This utility searched the current directory for a virtual environment
in the current directory, travels up the directory tree (up to the
users home directory) until a virtual env is found, then spawns a
subshell that sources '.bashrc' and the virtual environment (and sets
a value for 'ENVY').

By default, searches for a virtual environment called '.venv', can be
specified in the first argument.

If a virtual environment is not found, a new virtual environment is
created at the current directory and a subshell is invoked.

USAGE:
    codehelp [OPTIONS] [NAME]

ARGS:
    NAME              Virtual env to search/create (default: '.venv')

OPTIONS:
    -h, --help                                     Show documentation
    -n, --new         Skip search and create/activate new virtual env
/home/blake/.local/bin/envy: line 4: .venv-foo: command not found
bash: cannot set terminal process group (124413): Inappropriate ioctl for device
bash: no job control in this shell
stty: 'standard input': Inappropriate ioctl for device
(.venv-foo) [m[1m[36mblake[m [1m[37m@[m [1m[34mbanana[m [1m[37m:[m [1m[32m~/Workspace/repos/envy[m [1m[37m-[m [1m[93mmain *[1m[31m[m
[1m$ [mexit
bash: cannot set terminal process group (124413): Inappropriate ioctl for device
bash: no job control in this shell
stty: 'standard input': Inappropriate ioctl for device
bash: /home/blake/Workspace/repos/envy/foo/bin/activate: No such file or directory
[m[1m[36mblake[m [1m[37m@[m [1m[34mbanana[m [1m[37m:[m [1m[32m~/Workspace/repos/envy[m [1m[37m-[m [1m[93mmain *[1m[31m[m
[1m$ [mexit
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
look for  by using Couldn't find a venv named foo, creating one in current directory
Creating and activating venv (.venv-foo) in current dir).

USAGE:
    envy [OPTIONS] [NAME]

ARGS:
    NAME            Virtual env suffix to search/create (default: '')

OPTIONS:
    -h, --help                                     Show documentation
    -n, --new         Skip search and create/activate new virtual env
```

## TODO
* [ ] zsh and fish support?
