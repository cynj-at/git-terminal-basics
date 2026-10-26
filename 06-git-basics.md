# 06 — Git basics: commit, push, branch

**Goals:** create a repository, save changes with `add` and `commit`, connect it to your git host with `git remote add` and `push` it. Then do the same on a **branch**.

## Starting a repository

Either **start locally**:

```bash
mkdir my-project && cd my-project
git init
```

…or **copy an existing one** from a server (this also downloads the whole history):

```bash
git clone git@<your-host>:<username>/<repo>.git
cd <repo>
```

## The core loop: `status` → `add` → `commit`

```bash
git status                  # 1. what changed?
git diff                    # 2. show the exact changes (not yet staged)
git add notes.md            # 3. stage a file
git add .                   #    ...or everything in this folder and below
git diff --staged           # 4. what will go into the commit?
git commit -m "Add rehearsal notes for Tuesday"   # 5. save the snapshot
```

> 💡 **Rhythm:** `status` → `add` → `status` → `commit`. Run `git status` before and after each step until it becomes a habit. It tells you what to do next.

## Good commit messages

- Short summary line (≤ ~50 characters), written as a command: *"Add intro section"*, *"Fix typo in bar 12"*.
- Explain **why**, not just what. The *what* is in the diff.
- One commit = one logical change. "Fix bar 12 and reformat everything and add new piece" is three commits.

`git commit` without `-m` opens your editor for a longer message: the first line is the summary, then an empty line, then details. (In **nano**: save with `Ctrl+O`, `Enter`, quit with `Ctrl+X`. Stuck in **Vim**? `Esc`, then `:wq`, `Enter`.)

## Looking at the history

```bash
git log                         # full history (q to quit)
git log --oneline               # one line per commit
git log --oneline --graph --all # all branches, drawn as a graph
git show HEAD                   # what changed in the latest commit?
```

## Ignoring files: `.gitignore`

Some files should never be committed: temporary files, large audio exports, passwords. List them in a file called `.gitignore` in the project root:

```gitignore
# macOS / Windows junk
.DS_Store
Thumbs.db

# exports and temporary files
*.wav
*.tmp

# secrets
.env
```

Ignored files no longer show up in `git status`. Commit the `.gitignore` itself.

> ⚠️ Never commit passwords, tokens or private keys. Even if you delete them later, **they stay in the history.**

## Remotes: `git remote add` and `git push`

Your repository lives on your computer. To back it up on GitHub / GitLab / Codeberg (or share it), you connect it to a **remote**, which is conventionally called `origin`:

```bash
git remote add origin git@<your-host>:<user>/<repo>.git   # once per repository
git remote -v                                             # check: which remotes exist?
git push -u origin main                                   # first push of main
git push                                                  # every push after that
```

`-u` ("upstream") connects your local `main` to `origin/main`, so from then on a plain `git push` knows where to go.

> ▶️ **Exercise S1 — My first repository** · [open exercise](exercises-2-git.md#s1--my-first-repository)

## Branches: work on something without touching `main`

A branch is a separate line of work (see [05](05-git-concepts.md#branches-are-just-pointers)). Typical use: try something out, or prepare a change, while `main` stays clean.

```bash
git branch                       # list branches, * marks the current one
git switch -c new-intro          # create a branch "new-intro" and switch to it
# ... edit files ...
git add intro.md
git commit -m "Rewrite intro"    # the commit lands on new-intro, not on main
git push -u origin new-intro     # first push of this branch: same -u as for main
git switch main                  # back to main: your files change to main's version
```

On your git host you'll now see **two branches** (usually in a dropdown that says `main`). Bringing a branch back into `main` (*merging*) is the next step after this course.

> ▶️ **Exercise S2 — Work on a branch and push it** · [open exercise](exercises-2-git.md#s2--work-on-a-branch-and-push-it)

## Old commands you'll see in tutorials

Older tutorials use `git checkout` for branches. Git added a clearer command:

| Old | New (use these) |
|---|---|
| `git checkout <branch>` | `git switch <branch>` |
| `git checkout -b <new-branch>` | `git switch -c <new-branch>` |

`checkout` still works, so don't be confused when you see it.

## Pitfalls

- **`fatal: not a git repository`:** you're not inside your project folder. `pwd`, then `cd` into it.
- **`nothing added to commit`:** you forgot `git add`.
- **`error: src refspec main does not match any`:** there's no commit yet, or your branch is called `master`. Make a commit first, or rename the branch with `git branch -m main`.
- **`Permission denied (publickey)`:** SSH isn't set up yet. Go back to [04](04-git-setup.md).
- **Push rejected because the remote already has commits** (you ticked "Add a README" when creating the repo online): run `git pull --allow-unrelated-histories`, save the merge message, then `git push`. Next time create the online repo **empty**.
- **`error: Your local changes would be overwritten` on `git switch`:** commit your changes first, then switch.
