# 00 — Preparation (do this first)

Takes about 15 minutes. The goal is to have **a terminal, git, a text editor and an account on a git host** ready when we start.

## 1. Install git and open a terminal

**macOS**
1. Open *Terminal* (Spotlight: `Cmd + Space`, type "Terminal").
2. Type `git --version` and press Enter.
3. If git is missing, macOS offers to install the *Command Line Developer Tools*. Click *Install* and wait.

**Windows**
1. Download and install **Git for Windows** from <https://git-scm.com/download/win>.
   The defaults are fine. When asked for the default editor, choose *Nano* or *Visual Studio Code* (not Vim, unless you know it).
2. Open **Git Bash** from the start menu. **We use Git Bash for the whole course**, not PowerShell or cmd, so the commands are the same for everyone.
3. Type `git --version`.

> Advanced Windows users can use WSL (Windows Subsystem for Linux) instead. Then follow the Linux instructions.

**Linux**
1. Open your terminal emulator.
2. `git --version`. If it's missing, install it with your package manager, e.g.
   `sudo apt install git` (Debian/Ubuntu), `sudo dnf install git` (Fedora), `sudo pacman -S git` (Arch).

✅ **Check:** `git --version` prints something like `git version 2.4x.x`.

## 2. A text editor

Any code editor works. If you don't have one, install **Visual Studio Code**: <https://code.visualstudio.com> or **vscodium**.

## 3. An account on a git host

Create a free account on **one** of these:

- GitHub — <https://github.com>
- GitLab — <https://gitlab.com>
- Codeberg — <https://codeberg.org> (non-profit, based in Germany)

Write down your **username** and the **email address** you used. You'll need both.

## 4. Checklist

- [ ] I can open a terminal (Git Bash on Windows)
- [ ] `git --version` works
- [ ] I have a text editor
- [ ] I have an account on GitHub, GitLab or Codeberg and know my username

If something doesn't work, don't worry. Check the *Pitfalls* sections in the chapters, or ask in the course chat.
