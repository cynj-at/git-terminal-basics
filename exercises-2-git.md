# Exercises — Git basics

Two exercises that build on each other. Do them in order, in the same folder.

> **Before you start:**
> - You've worked through [04](04-git-setup.md) (git config + SSH) and [06](06-git-basics.md).
> - zsh users (macOS): run `setopt interactivecomments` so you can paste commands with `# comments`.
> - If git opens an editor: in **nano** save with `Ctrl+O`, `Enter`, quit with `Ctrl+X`. In **Vim** type `Esc`, then `:wq`, `Enter`.
> - **`git status` is always allowed.** Use it after every step.

| # | Scenario | Commands you'll learn |
|---|---|---|
| S1 | My first repository | `init`, `add`, `commit`, `.gitignore`, `remote add`, `push` |
| S2 | Work on a branch and push it | `branch`, `switch -c`, `add`, `commit`, `push -u origin <branch>` |

---

## S1 — My first repository

*You're putting together the program for a concert and want to track it with git, and back it up online.*

**Tasks:**
1. Create the folder `~/git-course/concert-program`, go into it and turn it into a git repository.
2. Create a `README.md` with a heading and one sentence about the project.
3. Create a fake audio file: `echo "fake" > rehearsal.wav`. Audio exports should **not** be committed. Create a `.gitignore` that ignores all `.wav` files.
4. Check `git status`. Which files does git see? Is `rehearsal.wav` listed?
5. Stage and commit `README.md` and `.gitignore` with a good message.
6. Look at your history with `git log --oneline`.
7. On your git host, create a **new, empty** repository called `concert-program`. **Don't** tick "Add a README" (your repo already has a history).
8. Connect your local repo to it and push. The host shows you the commands. Use the **SSH** URL.
9. Refresh the web page. Your README is online. 🎉

> **No account / SSH not working yet?** Use a "fake server" on your own disk instead and take this path in step 8:
> ```bash
> git init --bare -b main ~/git-course/remote.git
> git remote add origin ~/git-course/remote.git
> git push -u origin main
> ```

<details>
<summary>Solution</summary>

```bash
mkdir -p ~/git-course/concert-program
cd ~/git-course/concert-program
git init

printf "# Concert program\n\nProgram and notes for the spring concert.\n" > README.md
echo "fake" > rehearsal.wav
echo "*.wav" > .gitignore

git status                     # shows README.md and .gitignore, NOT rehearsal.wav
git add README.md .gitignore
git commit -m "Add README and ignore audio exports"
git log --oneline

git remote add origin git@<your-host>:<username>/concert-program.git
git push -u origin main
```

If `git push` complains about `master` vs `main`: your branch is called `master` because `init.defaultBranch` wasn't set. Rename it with `git branch -m main`.
</details>

---

## S2 — Work on a branch and push it

*You want to draft the concert program, but `main` should stay as it is until the program is final. So you work on a branch.*

Continue in `~/git-course/concert-program` from S1.

**Tasks:**
1. Which branch are you on? (`git branch`)
2. Create a branch `program-draft` and switch to it in one command.
3. Create `program.md` with three pieces. Check `git status`, then `add` and `commit` it.
4. Look at the history with `git log --oneline --graph --all`. Where does `main` point, where does `program-draft` point?
5. Push the branch to your remote. It's the branch's first push, so you need `-u origin <branch>`.
6. On the website, open the branch dropdown (it says `main`) and switch to `program-draft`. `program.md` is there, but not on `main`.
7. Back in the terminal: switch to `main` and run `ls`. Where is `program.md`? Switch back to `program-draft` and check again.
8. Bonus: go to `main`, create a second branch `readme-update`, add a line to `README.md`, commit and push it. Then run `git branch -a`.

> **Using the "fake server" from S1?** Instead of the website, check step 6 with `git branch -r` (lists the branches on the remote).

<details>
<summary>Solution</summary>

```bash
cd ~/git-course/concert-program
git branch                                  # 1: * main

git switch -c program-draft                 # 2
printf "1. Bach - Cello Suite 1\n2. Chopin - Ballade 1\n3. Ravel - Bolero\n" > program.md
git status                                  # 3: program.md is untracked
git add program.md
git commit -m "Add first draft of the program"

git log --oneline --graph --all             # 4: program-draft is one commit ahead of main

git push -u origin program-draft            # 5

git switch main                             # 7
ls                                          #    no program.md: it only exists on the branch
git switch program-draft
ls                                          #    there it is again

git switch main                             # 8
git switch -c readme-update
echo "Rehearsals are on Tuesdays." >> README.md
git commit -am "Mention rehearsal day in README"
git push -u origin readme-update
git branch -a                               #    local branches + remotes/origin/... branches
```

Nothing is lost when you switch branches. Git just shows you the files as they are on that branch. Before switching, commit your changes (or git refuses to switch).

**What's next?** Bringing `program-draft` back into `main` is called *merging* (`git switch main`, `git merge program-draft`). On GitHub / GitLab / Codeberg you'd usually do that with a *pull request* / *merge request* in the browser.
</details>

---

## Clean up

When you're done:
```bash
rm -rf ~/git-course
```
(The repository on your git host remains. Delete it on the website if you like.)
