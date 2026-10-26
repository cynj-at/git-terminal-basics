# Terminal & Git — the basics, for self-study

This is the self-study version of the course *Terminal & Git*: everything from "what is a terminal?" to your first commits, pushed to GitHub / GitLab / Codeberg, on `main` and on a branch. No prior knowledge required.

Plan about **3–4 hours**, ideally spread over two sittings (chapters 01–04, then 05–06).

## Before you start

Work through **[00-preparation.md](00-preparation.md)**: install git, open a terminal (Git Bash on Windows), create an account on a git host.

## The path

| Step | Read | Then do |
|---|---|---|
| 1 | [01 — Terminal basics](01-terminal-basics.md) | the *Try it* box |
| 2 | [02 — Navigating and working with files](02-navigation-files.md) | [E1](exercises-1-terminal.md#e1--scavenger-hunt-navigation), [E2](exercises-1-terminal.md#e2--pipes-and-redirection) |
| 3 | [03 — Configuring your shell](03-shell-config.md) | [E3](exercises-1-terminal.md#e3--make-the-shell-yours) |
| 4 | [04 — Setting up git and SSH](04-git-setup.md) | [E4](exercises-1-terminal.md#e4--check-your-git-configuration), [E5](exercises-1-terminal.md#e5--ssh-end-to-end) |
| 5 | [05 — How git thinks](05-git-concepts.md) | — |
| 6 | [06 — Git basics: commit, push, branch](06-git-basics.md) | [S1](exercises-2-git.md#s1--my-first-repository), [S2](exercises-2-git.md#s2--work-on-a-branch-and-push-it) |

Inside the chapters, a ▶️ box tells you when it's time for an exercise.

At the end you can:
- move around in a terminal and work with files,
- customise your shell with aliases and functions,
- connect to your git host via SSH,
- `init` a repository, `add` and `commit` changes, connect it with `git remote add` and `push` it,
- create a branch, commit on it and push it.

Keep the [cheatsheet](cheatsheet.md) open while you work.

## How to read the material

- Code blocks are commands for you to type (or paste) into the terminal. Lines that start with `#` are comments that explain things. Don't type them.
- `<something-in-angle-brackets>` is a placeholder. Replace the whole thing, brackets included, e.g. `<username>` → `alex`.
- Boxes labelled **macOS**, **Windows (Git Bash)** or **Linux** apply only to that system.
- Solutions are hidden in collapsible blocks. Try it yourself first.
- Stuck? Every chapter ends with **Pitfalls**: the most common problems and their fixes.
