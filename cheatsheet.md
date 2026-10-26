# Cheatsheet — Terminal & Git basics

## Terminal

| Command | Does |
|---|---|
| `pwd` | where am I? |
| `ls`, `ls -la` | list files (incl. hidden, with details) |
| `cd <dir>`, `cd ..`, `cd ~`, `cd -` | change directory / up / home / back |
| `mkdir -p a/b/c` | create directories |
| `touch f` | create an empty file |
| `cat f`, `less f` | show a file / page through it (`q` quits) |
| `cp a b`, `cp -r dirA dirB` | copy file / directory |
| `mv a b` | move or rename |
| `rm f`, `rm -r dir` | delete (**no trash can!**) |
| `cmd > f`, `cmd >> f` | write output to a file / append |
| `cmd1 \| cmd2` | pipe output of cmd1 into cmd2 |
| `grep text f` | lines containing "text" |
| `man cmd`, `cmd --help` | help |

**Keys:** `Tab` complete · `↑/↓` history · `Ctrl+R` search history · `Ctrl+C` cancel · `Ctrl+L` clear · `Ctrl+A/E` start/end of line

**Shell config:** `~/.zshrc` (zsh) / `~/.bashrc` (bash) · reload with `source ~/.zshrc`
```bash
alias ll='ls -la'
mkcd() { mkdir -p "$1" && cd "$1"; }
export EDITOR=nano
```

## Git setup (once per computer)

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.org"
git config --global init.defaultBranch main
git config --global pull.rebase false
ssh-keygen -t ed25519 -C "you@example.org"
cat ~/.ssh/id_ed25519.pub          # → paste into your host's SSH key settings
ssh -T git@github.com              # or gitlab.com / codeberg.org
```

## Git basics

| Command | Does |
|---|---|
| `git init` / `git clone <url>` | new repo / copy a repo |
| `git status` | **what's going on?** |
| `git diff` / `git diff --staged` | unstaged / staged changes |
| `git add <file>`, `git add .` | stage |
| `git commit -m "msg"` | commit staged changes |
| `git log --oneline --graph --all` | history as a graph |
| `git remote add origin <url>` | connect a remote (once) |
| `git remote -v` | show remotes |
| `git push -u origin main` | first push of a branch |
| `git push` | every push after that |

## Branches

| Command | Does |
|---|---|
| `git branch` | list branches (`*` = current) |
| `git branch -a` | including the branches on the remote |
| `git switch -c <b>` | create + go to branch |
| `git switch <b>` | go to branch |
| `git push -u origin <b>` | first push of branch `<b>` |

**The loop:** `git switch -c <b>` → edit → `git add` → `git commit` → `git push -u origin <b>`
