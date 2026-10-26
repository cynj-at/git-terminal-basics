# 03 — Configuring your shell

**Goals:** understand where the shell reads its settings, and add your own aliases, functions and variables in a clean, organised way.

## The config file: your shell's "startup script"

Every time a new shell starts, it reads a config file and runs the commands in it. Everything you put there is available in every new terminal.

| Shell | File | Notes |
|---|---|---|
| zsh (macOS default) | `~/.zshrc` | |
| bash (Linux) | `~/.bashrc` | |
| bash (Git Bash on Windows) | `~/.bashrc` | loaded via `~/.bash_profile`, see the box below |

The leading dot makes the file **hidden**, so you need `ls -a` to see it.

> **Windows (Git Bash):** Git Bash reads `~/.bash_profile` at startup. If your `~/.bashrc` doesn't seem to be loaded, add this line to `~/.bash_profile`:
> ```bash
> if [ -f ~/.bashrc ]; then source ~/.bashrc; fi
> ```

### Open it in an editor

```bash
code ~/.zshrc        # VS Code (if the `code` command is installed)
nano ~/.zshrc        # simple terminal editor: Ctrl+O save, Enter, Ctrl+X quit
```

(Use `~/.bashrc` instead if you're on bash.) If the file doesn't exist yet, the editor creates it.

### Changes only apply to *new* shells

After you edit the file, either open a new terminal or reload the file in the current one:

```bash
source ~/.zshrc      # or: source ~/.bashrc
```

`source` means "run this file in **my current** shell". That's also how one config file can load another.

## Aliases — short names for long commands

```bash
alias ll='ls -la'
alias ..='cd ..'
alias gs='git status'
```

Now `ll` runs `ls -la`. Rules:
- **No spaces around `=`.**
- Use single quotes around the command.
- Type `alias` on its own to list all aliases. `type ll` shows what `ll` is.

## Functions — little programs with arguments

An alias can't take arguments in the middle. A function can. `$1` is the first argument, `$2` the second, and so on.

```bash
mkcd() {
  mkdir -p "$1" && cd "$1"
}
```

`mkcd new-project` creates the folder **and** changes into it. The `&&` means "only run the second command if the first one succeeded".

## Variables and `PATH`

```bash
export EDITOR=nano                       # programs (like git) ask $EDITOR which editor to use
export PATH="$HOME/bin:$PATH"            # also look for programs in ~/bin
echo $PATH                               # show the search path
```

`PATH` is a list of directories, separated by `:`. When you type a command like `git`, the shell searches these directories in order. `which git` shows you which one it found.

## Keeping it tidy: split your config into several files

Over time your config grows. A common pattern is one main file that **sources** smaller, topic-based files:

```
~/.zshrc                      ← main file, stays short
~/.config/shell/aliases.sh    ← all aliases
~/.config/shell/functions.sh  ← all functions
```

Add this to the end of your `~/.zshrc` (or `~/.bashrc`):

```bash
for f in ~/.config/shell/*.sh; do
  [ -r "$f" ] && source "$f"
done
```

This loads every `.sh` file in that folder. Want a new topic? Create a new file, with no need to touch `.zshrc` again. Because the files use only features that bash and zsh share, you can use the **same files with both shells**, and even copy them to a new computer or keep them in a git repository ("dotfiles").

> ▶️ **Exercise E3 — Make the shell yours** · [open exercise](exercises-1-terminal.md#e3--make-the-shell-yours)

## Try it

→ Exercise **E3** in [exercises-1-terminal.md](exercises-1-terminal.md).

## Pitfalls

- **`alias ll = 'ls -la'`** (with spaces) doesn't work. No spaces around `=`.
- **"Nothing changed":** you forgot `source ~/.zshrc` or to open a new terminal.
- **zsh: `no matches found: ~/.config/shell/*.sh`:** the folder is empty or missing. Create at least one `.sh` file in it first.
- **Edited the wrong file:** check `echo $SHELL`. zsh doesn't read `.bashrc` and bash doesn't read `.zshrc`.
- **Broken config, the terminal shows errors on start:** open the file in an editor and comment out (`#`) your last change. As a last resort, rename it: `mv ~/.zshrc ~/.zshrc.broken`.
