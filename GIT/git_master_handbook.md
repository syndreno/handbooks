# Git Master Handbook
## Complete Beginner-to-Advanced Learning Guide

> A single-file handbook for learning Git from zero through professional team usage.  
> The goal is not only to memorize commands, but to understand Git's mental model, history graph, collaboration model, recovery tools, and real-world workflows.

---

# Table of Contents

1. What Git Is and Why It Exists
2. Git vs GitHub/GitLab/Bitbucket
3. Core Git Mental Model
4. Installation and Configuration
5. Repositories and `.git`
6. File States and the Daily Workflow
7. `status`, `diff`, and the Staging Area
8. Commits and Commit Messages
9. `.gitignore` and `.gitattributes`
10. Branches and HEAD
11. Merging and Merge Conflicts
12. Remotes, Fetch, Pull, Push, and Upstream
13. Rebase and Interactive Rebase
14. Merge vs Rebase
15. Undo: Restore, Reset, Revert, Amend
16. Reflog and Recovery
17. Stash
18. Cherry-Pick
19. Tags and Releases
20. Detached HEAD and Revision Syntax
21. Git Internals and Object Model
22. Commit Graph and Merge Base
23. File History, Blame, and Search
24. Bisect
25. Worktrees
26. Submodules, Subtree, Git LFS
27. Sparse Checkout and Partial Clone
28. Hooks, Aliases, and Configuration
29. SSH and HTTPS Authentication
30. Forks, Pull Requests, and Code Review
31. Branching Strategies
32. GitFlow
33. GitHub Flow and Trunk-Based Development
34. Releases and Hotfixes
35. Git with CI/CD
36. Semantic Versioning and Conventional Commits
37. Monorepos
38. Security, Secrets, and Signed Commits
39. History Rewriting and Force Push
40. Repository Maintenance and Migration
41. Real-World Scenarios
42. Troubleshooting
43. Common Mistakes
44. Professional Best Practices
45. Command Decision Guide
46. Master Cheat Sheet
47. Practice Roadmap
48. Interview Questions
49. Final Mental Models
50. Git Scenario Q&A — What Command Should I Use?

---

## How to Use This Handbook

You do not need to memorize every command. Learn Git in layers:

1. **Beginner:** `status`, `diff`, `add`, `commit`, `log`, `switch`, `fetch`, `pull`, `push`.
2. **Intermediate:** merge conflicts, rebase, stash, restore, reset, revert, cherry-pick, tags.
3. **Advanced:** reflog, bisect, worktrees, submodules, sparse checkout, partial clone, hooks, history rewriting, and repository maintenance.

Command examples use placeholders such as `<branch>`, `<commit>`, and `<url>`. Replace the whole placeholder, including angle brackets, with a real value. For example:

```bash
git switch <branch>
```

becomes:

```bash
git switch feature/login
```

> **Version note:** Git behavior can be affected by your Git version and configuration. When a command has multiple integration or safety modes, this handbook prefers explicit commands so the intent is clear.

---

# 1. What Git Is and Why It Exists

Git is a **distributed version control system**.

Version control means recording changes to a project so you can answer questions such as:

- What changed?
- Who changed it?
- Why was it changed?
- What did the project look like last week?
- Which change introduced a bug?
- Can two developers work on different features at the same time?
- Can we restore a known-good production version?

Without version control, projects often become:

```text
project/
project-final/
project-final-v2/
project-final-fixed/
project-final-fixed-new/
project-final-real/
```

With Git, history becomes a sequence and graph of commits:

```text
A → B → C → D
```

Each commit represents a meaningful project state.

## Why Git is called distributed

In a typical Git clone, every developer has a local repository containing project history.

That means many operations work locally:

```text
commit
branch
merge
rebase
log
diff
blame
bisect
```

You do not need the remote server for every action.

---

# 2. Git vs GitHub/GitLab/Bitbucket

Git and Git hosting services are different things.

| Name | Meaning |
|---|---|
| Git | Version control software |
| GitHub | Git hosting and collaboration platform |
| GitLab | Git hosting, collaboration, CI/CD and DevOps platform |
| Bitbucket | Git repository hosting and collaboration platform |
| Repository | Version-controlled project |
| Remote | Another Git repository referenced by name |

You can use Git locally without any hosting service:

```bash
git init
git add .
git commit -m "Initial commit"
```

Hosting platforms add features such as:

```text
Pull requests / merge requests
Issue tracking
Code review
Branch protection
CI/CD
Release pages
Security scanning
Permissions
Project management
```

---

# 3. Core Git Mental Model

This is the most important Git concept.

Think in four areas:

```text
Working Directory
      |
      | git add
      v
Staging Area / Index
      |
      | git commit
      v
Local Repository
      |
      | git push
      v
Remote Repository
```

## Working directory

The files you are actively editing.

Example:

```text
src/login.js
```

You change the file. That change exists only in the working tree.

## Staging area

The staging area contains the exact snapshot planned for the next commit.

```bash
git add src/login.js
```

Think:

> "Include this version of `login.js` in my next commit."

## Local repository

A commit saves the staged snapshot into local repository history.

```bash
git commit -m "Fix login validation"
```

## Remote repository

Push sends commits to another repository:

```bash
git push
```

## Full lifecycle

```bash
git status

# edit files

git diff
git add -p
git diff --staged
git commit -m "fix: validate login input"
git push
```

The key question when Git feels confusing is:

```text
Where is my change currently?

Working tree?
Staging area?
Local commit?
Remote branch?
```

---

# 4. Installation and Configuration

Check Git:

```bash
git --version
```

Configure identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Set the default initial branch:

```bash
git config --global init.defaultBranch main
```

Set VS Code as editor:

```bash
git config --global core.editor "code --wait"
```

Inspect configuration:

```bash
git config --list
git config --list --show-origin
```

## Configuration scopes

```text
system  → machine-wide
global  → current user
local   → current repository
```

A local setting overrides global for that repository.

Example:

```bash
git config --local user.email "work@example.com"
```

This is useful if personal and company repositories require different identities.

## Installing Git

The exact installer depends on your operating system. After installation, always verify from a terminal:

```bash
git --version
```

Example output:

```text
git version 2.x.x
```

If the command is not found, Git is either not installed or its executable directory is not on your shell's `PATH`.

## What `user.name` and `user.email` actually do

These values become author/committer identity metadata in commits. They are **not** your Git hosting password and do not by themselves log you in to GitHub, GitLab, or Bitbucket.

Inspect only the identity that applies in the current repository:

```bash
git config user.name
git config user.email
```

Use a repository-local identity when work and personal projects need different addresses:

```bash
git config --local user.name "Work Name"
git config --local user.email "work@example.com"
```

### Common configuration mistake

Do not change global identity just to fix one repository unless you really want the change to affect all repositories for your user account. Prefer `--local` for repository-specific identity.

---

# 5. Repositories and `.git`

Create a repository:

```bash
mkdir demo
cd demo
git init
```

Git creates:

```text
.git/
```

This directory contains repository metadata and history.

Important parts include:

```text
.git/
├── HEAD
├── config
├── index
├── objects/
├── refs/
└── logs/
```

Conceptually:

- `HEAD` → current checked-out reference
- `config` → repository configuration
- `index` → staging area
- `objects` → Git object database
- `refs` → branches/tags
- `logs` → reflog information

Do not casually delete `.git`.

If it is removed, your ordinary project files remain, but that working copy is no longer connected to its local Git history.

## Clone existing repository

```bash
git clone <repository-url>
```

Clone under a different folder name:

```bash
git clone <repository-url> my-project
```

---

# 6. File States and the Daily Workflow

Files can be:

```text
Untracked
Tracked and unchanged
Modified
Staged
Committed
Ignored
```

## Untracked

Git has never started tracking the file.

```text
?? notes.txt
```

Stage it:

```bash
git add notes.txt
```

## Modified

A tracked file differs from the committed/index version.

## Staged

The version prepared for the next commit.

## Committed

Stored in repository history.

## Tracked vs untracked vs ignored

A **tracked** file already exists in Git history or has been staged. An **untracked** file exists in your working directory but Git is not yet tracking it. An **ignored** file matches an ignore rule and is normally hidden from ordinary add/status workflows.

A common state transition is:

```text
new file → untracked → staged → committed → modified → staged → committed
```

Remember that staging stores a snapshot of file content. If you stage a file, edit it again, and then run `git status`, that one file can have both staged and unstaged changes at the same time.

## Recommended daily workflow

```bash
git status
git fetch origin

# edit

git diff
git add -p
git diff --staged
git commit -m "feat: add customer search"
git push
```

---

# 7. `status`, `diff`, and the Staging Area

## `git status`

```bash
git status
```

Short:

```bash
git status --short
```

Possible output:

```text
 M app.js
M  login.js
?? test.txt
```

Interpretation:

```text
 M app.js
```

Modified but not staged.

```text
M  login.js
```

Staged modification.

```text
?? test.txt
```

Untracked file.

## `git diff`

Unstaged changes:

```bash
git diff
```

This roughly compares:

```text
Working tree ↔ Index
```

Staged changes:

```bash
git diff --staged
```

This roughly compares:

```text
Index ↔ HEAD
```

Compare commits:

```bash
git diff <commit1> <commit2>
```

Compare a feature branch with its merge base:

```bash
git diff main...feature/login
```

## Why staging exists

Suppose you changed:

```text
login.js
invoice.js
README.md
```

Only login belongs in the next commit.

Use:

```bash
git add login.js
git diff --staged
git commit -m "fix: validate login request"
```

The other changes stay out of the commit.

## Partial staging

One file may contain multiple unrelated changes.

```bash
git add -p app.js
```

Common responses:

```text
y = stage hunk
n = skip hunk
s = split hunk
q = quit
```

This is extremely useful for creating clean commits.

---

# 8. Commits and Commit Messages

Create:

```bash
git commit -m "Add invoice approval"
```

Open editor:

```bash
git commit
```

## Amend latest commit

Forgot a file:

```bash
git add forgotten-file.js
git commit --amend --no-edit
```

Change message:

```bash
git commit --amend
```

Amending creates a new commit ID, so avoid casually amending history already shared with others.

## Good commit messages

Weak:

```text
update
changes
fix
done
final
```

Better:

```text
Fix duplicate invoice validation
Add payment audit logging
Refactor customer lookup query
```

A good message communicates **intent**, not merely that files changed.

## What `git commit` does and does not do

`git commit` records the **staged snapshot** in the local repository and moves the current branch to the new commit. It does **not** automatically upload the commit to a remote server; `git push` is a separate action.

Useful forms:

```bash
git commit -m "Fix invoice validation"
git commit                 # open configured editor
git commit --amend         # replace the latest commit with a new one
```

`git commit -a` is convenient but easy to misunderstand:

```bash
git commit -am "Fix validation"
```

It automatically stages modifications and deletions of **already tracked files**. It does not add brand-new untracked files. Beginners should usually stage explicitly so they can review exactly what will be committed.

## A useful commit checklist

Before committing:

```bash
git status
git diff --staged
```

Ask:

- Does this commit contain one logical change?
- Did I accidentally stage generated files, secrets, or debug output?
- Does the message explain why the change exists?
- Can this commit be tested or understood independently?

Long form:

```text
fix: reject duplicate invoice numbers

The API previously accepted repeated submissions with the same
invoice number. Validate uniqueness before persistence.
```

---

# 9. `.gitignore` and `.gitattributes`

## `.gitignore`

Example:

```gitignore
node_modules/
.env
dist/
build/
coverage/
*.log
.idea/
.vscode/
```

Important:

> `.gitignore` does not automatically untrack a file already committed.

Stop tracking but keep locally:

```bash
git rm --cached .env
```

Then commit.

Find ignore rule:

```bash
git check-ignore -v path/to/file
```

## `.gitattributes`

Useful for repository-wide text/binary behavior.

Example:

```gitattributes
* text=auto
*.sh text eol=lf
*.bat text eol=crlf
*.png binary
```

This helps teams avoid inconsistent line-ending behavior.

## Useful `.gitignore` pattern examples

```gitignore
# Ignore one exact file
.env

# Ignore a directory anywhere this pattern applies
node_modules/

# Ignore all log files
*.log

# Ignore build files, but keep one example file
dist/
!important.log
```

Negation rules beginning with `!` can re-include a path, but parent-directory ignore rules can affect whether Git can reach that path. Test confusing rules with:

```bash
git check-ignore -v path/to/file
```

## Repository ignore vs personal ignore

Project-specific ignore rules belong in the repository's `.gitignore`. Personal editor or operating-system files that should not be imposed on every contributor are often better handled with a global excludes file configured through Git.

## Normalizing line endings

When a team introduces or changes `.gitattributes`, existing files may need to be renormalized deliberately. Do this in a dedicated, reviewed change rather than mixing a repository-wide line-ending rewrite with functional code changes.

---

# 10. Branches and HEAD

A branch is mainly a movable reference to a commit.

Initial history:

```text
A---B---C
        ^
        |
       main
```

Create:

```bash
git branch feature/login
```

Now both references point to C.

Switch:

```bash
git switch feature/login
```

Commit twice:

```text
A---B---C main
         \
          D---E feature/login
```

## HEAD

Normally:

```text
HEAD → current branch → current commit
```

Example:

```text
HEAD
 |
 v
feature/login
 |
 v
E
```

Create and switch in one command:

```bash
git switch -c feature/login
```

Delete merged branch:

```bash
git branch -d feature/login
```

Force-delete:

```bash
git branch -D feature/login
```

Rename:

```bash
git branch -m new-name
```

## Inspecting branches

```bash
git branch             # local branches
git branch -r          # remote-tracking branches
git branch -a          # both
git branch -vv         # local branches plus upstream/ahead-behind hints
```

A local branch such as `main` and a remote-tracking ref such as `origin/main` are different references. `origin/main` changes when you fetch from `origin`; it is not a live view that updates by itself.

## Local branch vs upstream branch

After:

```bash
git push -u origin feature/login
```

the local branch normally records `origin/feature/login` as its upstream. After that, commands such as `git pull` and `git push` can often work without naming the remote and branch explicitly.

Check tracking information with:

```bash
git branch -vv
```

---

# 11. Merging and Merge Conflicts

Suppose:

```text
A---B---C main
         \
          D---E feature
```

Merge feature into main:

```bash
git switch main
git merge feature
```

Possible merge commit:

```text
A---B---C-------M main
         \     /
          D---E
```

## Fast-forward

If main did not change:

```text
A---B main
     \
      C---D feature
```

Git can move main directly:

```text
A---B---C---D main
```

Force a merge commit if desired:

```bash
git merge --no-ff feature
```

## Conflict

Example:

```text
<<<<<<< HEAD
tax = 18
=======
tax = 20
>>>>>>> feature/new-tax
```

Git cannot know which business rule is correct.

Resolve manually, remove markers, then:

```bash
git add file
git commit
```

Abort unresolved merge:

```bash
git merge --abort
```

Never resolve a conflict blindly. The result is new code and should be reviewed/tested.

## A safe conflict-resolution workflow

```bash
git status
# open each conflicted file and resolve the intended final code
git add path/to/resolved-file
git status
git diff --staged
git commit              # for a normal merge conflict
```

During a merge, `git status` is your best guide because it tells you which files are still unmerged.

## Merge modes beginners should know

```bash
git merge feature               # normal merge behavior
git merge --ff-only feature     # succeed only if a fast-forward is possible
git merge --no-ff feature       # create a merge commit even when fast-forward is possible
git merge --squash feature      # stage the combined effect; then commit manually
```

`--squash` does not create a true merge commit and does not record the merged branch as a parent. It is useful when a team wants one combined commit, but it changes the history shape and should follow team policy.

### Before starting a merge

Prefer a clean working tree. A merge can sometimes start with local changes present, but aborting becomes harder if those changes overlap with merge work. Commit, stash, or otherwise secure important local changes first.

---

# 12. Remotes, Fetch, Pull, Push, and Upstream

List remotes:

```bash
git remote -v
```

Add:

```bash
git remote add origin <url>
```

Change URL:

```bash
git remote set-url origin <url>
```

## Fetch

```bash
git fetch origin
```

Downloads remote objects/refs without integrating them into your current branch.

Inspect remote changes:

```bash
git log HEAD..origin/main --oneline
git diff HEAD..origin/main
```

## Pull

```bash
git pull
```

Conceptually:

```text
fetch + integrate
```

Explicit merge:

```bash
git pull --no-rebase
```

Explicit rebase:

```bash
git pull --rebase
```

## Push

```bash
git push origin main
```

First push of branch:

```bash
git push -u origin feature/login
```

The `-u` records upstream tracking.

Inspect:

```bash
git branch -vv
```

`origin/main` is a **local remote-tracking ref** representing the last fetched state of remote `origin`'s `main`.

## Fetch vs pull vs push in plain English

| Command | Main direction | Changes current branch immediately? | Typical purpose |
|---|---|---:|---|
| `git fetch` | remote → local object database/remote-tracking refs | No | Inspect remote changes safely |
| `git pull` | remote → current branch | Yes, if integration succeeds | Fetch and integrate upstream work |
| `git push` | local commits → remote | No local history integration | Publish commits |

## Prefer explicit pull behavior

`git pull` is convenient, but its exact reconciliation behavior can depend on Git version and configuration. In team documentation and automation, make the intent obvious:

```bash
git pull --ff-only       # update only when no local divergence exists
git pull --rebase        # fetch, then replay local commits on top
git pull --no-rebase     # fetch, then merge
```

A useful conservative workflow is:

```bash
git fetch origin
git status -sb
git log --oneline --graph --decorate --all
```

Then choose merge or rebase deliberately.

## Ahead and behind

After fetching, this shows a concise branch/upstream summary:

```bash
git status -sb
```

You may see text such as:

```text
## feature/login...origin/feature/login [ahead 2, behind 1]
```

That means your local branch has two commits the fetched remote-tracking branch does not have, while the remote-tracking branch has one commit your local branch does not have. Integrate before pushing.

## Pruning deleted remote branches

A remote-tracking branch can remain locally after its remote branch was deleted. Clean stale remote-tracking references with:

```bash
git fetch --prune
```

This does not delete your ordinary local branches.

---

# 13. Rebase and Interactive Rebase

Before:

```text
A---B---C main
     \
      D---E feature
```

Run:

```bash
git switch feature
git rebase main
```

After:

```text
A---B---C main
         \
          D'---E' feature
```

Rebase **replays** changes and creates new commits.

## Conflict workflow

```bash
git status
# resolve
git add file
git rebase --continue
```

Abort:

```bash
git rebase --abort
```

## Interactive rebase

```bash
git rebase -i HEAD~5
```

Actions:

```text
pick    keep
reword  change message
edit    pause for modification
squash  combine and edit combined message
fixup   combine and discard this message
drop    remove
```

Scenario:

```text
Add payment page
fix typo
fix again
rename var
add test
```

can be cleaned into:

```text
Add payment page
Add payment tests
```

Do this primarily on your own unpublished/unshared history.

## Useful rebase controls

During a conflicted rebase:

```bash
git status
# resolve files
git add <resolved-files>
git rebase --continue
```

Other controls:

```bash
git rebase --abort    # return to the state before the rebase
git rebase --skip     # omit the current rebased commit
```

Use `--skip` only when you intentionally want to drop that commit's change.

For fixup commits, a clean professional workflow is:

```bash
git commit --fixup <target-commit>
git rebase -i --autosquash <base>
```

This can automatically place `fixup!` commits next to their target during interactive rebase. Use it on history you are allowed to rewrite.

## Advanced: move a range of commits to a different base

```bash
git rebase --onto <new-base> <old-base> <branch>
```

This is powerful when a feature was accidentally based on the wrong branch. Because the arguments can be confusing, inspect the graph first and practice in a disposable branch before using it on important work.

---

# 14. Merge vs Rebase

## Merge

```text
A---B---C-------M
     \         /
      D---E---F
```

Pros:

- preserves topology;
- suitable for shared history;
- does not rewrite existing commits.

Cons:

- can produce many merge commits.

## Rebase

```text
A---B---C---D'---E'---F'
```

Pros:

- clean linear history;
- excellent for updating private feature work.

Cons:

- rewrites commits;
- dangerous if collaborators already use those exact commits.

Practical rule:

```text
Private branch → rebase can be excellent.
Shared stable branch → prefer non-destructive integration.
```

---

# 15. Undo: Restore, Reset, Revert, Amend

Before undoing anything, ask:

```text
Where is the mistake?

Unstaged?
Staged?
Latest local commit?
Older local commit?
Already shared?
```

## Discard unstaged tracked edit

```bash
git restore file.txt
```

Destructive to that unstaged edit.

## Unstage

```bash
git restore --staged file.txt
```

Working-tree change remains.

## Fix latest local commit

```bash
git commit --amend
```

## Reset

Soft:

```bash
git reset --soft HEAD~1
```

Effect:

```text
branch moves backward
changes remain staged
```

Mixed/default:

```bash
git reset HEAD~1
```

Effect:

```text
branch moves backward
changes remain unstaged
```

Hard:

```bash
git reset --hard HEAD~1
```

Effect:

```text
branch moves
index resets
tracked working files reset
```

Use hard reset carefully.

## Revert

For shared history:

```bash
git revert <commit>
```

Instead of deleting history, Git creates a new inverse commit.

```text
A---B---C---D---R
```

`R` reverses the selected change.

## Undo decision table

| Problem | Usually use | What happens | Shared-history safe? |
|---|---|---|---:|
| Unstaged edit should be discarded | `git restore <file>` | Working-tree copy is replaced | Yes, but local edit is lost |
| File was staged by mistake | `git restore --staged <file>` | Removes it from staging; working edit stays | Yes |
| Latest private commit needs correction | `git commit --amend` | Replaces latest commit | Only if rewriting is acceptable |
| Private commits should be moved/removed | `git reset ...` | Moves current branch; index/worktree depend on mode | Usually no after sharing |
| Shared commit must be undone | `git revert <commit>` | Adds a new inverse commit | Yes |
| Commit seems lost after reset/rebase | `git reflog` | Finds recent local ref positions | Recovery tool |

## Restore a file from another commit

```bash
git restore --source=<commit> -- path/to/file
```

This copies that version into the working tree. Review and commit it normally if that is the result you want.

## Removing untracked files with `git clean`

`git restore` only concerns tracked content. To remove untracked files, Git provides `git clean`, which can permanently delete files that are not committed. Always preview first:

```bash
git clean -nd      # preview untracked files/directories that would be removed
git clean -fd      # remove them after you verified the preview
```

To include ignored files as well, `-x` exists, but this can remove local `.env` files, build caches, or other data. Use it only when you fully understand the consequences.

---

# 16. Reflog and Recovery

Reflog records local ref movement.

```bash
git reflog
```

Example:

```text
abc123 HEAD@{0}: reset: moving to HEAD~1
def456 HEAD@{1}: commit: Important feature
```

If you accidentally reset away a commit:

```bash
git reflog
git branch recovery def456
```

This often rescues work that appears "lost."

Reflog is local and not a substitute for proper backups/remotes.

## Why reflog is not permanent

Reflog entries expire. Default expiration is commonly 90 days for reachable entries and 30 days for entries that are unreachable from the current tip, although configuration can change these values. Garbage collection can eventually remove unreachable objects after their protection expires.

So when you discover lost work, recover it immediately:

```bash
git reflog
git branch recovery/<name> <commit>
```

Creating the branch makes the recovered commit reachable again.

## Useful reflog forms

```bash
git reflog show HEAD
git reflog show main
git show HEAD@{1}
```

A reflog records what happened **in this local repository**. Another developer's clone has its own reflog.

---

# 17. Stash

Temporarily save unfinished work:

```bash
git stash
```

Include untracked:

```bash
git stash -u
```

Named:

```bash
git stash push -m "WIP invoice UI"
```

List:

```bash
git stash list
```

Apply but keep:

```bash
git stash apply
```

Apply and remove:

```bash
git stash pop
```

Specific:

```bash
git stash apply stash@{1}
```

Create branch:

```bash
git stash branch recover-work stash@{0}
```

Scenario:

```text
Working on feature
↓
Urgent production bug
↓
stash
↓
hotfix branch
↓
finish fix
↓
return
↓
stash pop
```

## What is included in a stash?

By default, `git stash` saves changes to tracked files and the index. New untracked files are not included unless you use `-u`/`--include-untracked`. Ignored files require a stronger option and should be handled carefully.

Inspect before applying:

```bash
git stash list
git stash show stash@{0}
git stash show -p stash@{0}
```

Delete one stash you no longer need:

```bash
git stash drop stash@{0}
```

Delete all stash entries:

```bash
git stash clear
```

`clear` is destructive. Do not use it merely to tidy the list unless you are certain nothing is needed.

## `apply` vs `pop`

- `apply` tries to restore the stash and keeps the stash entry.
- `pop` tries to restore it and, when successful, removes it from the stash list.

If you are unsure whether the stash will apply cleanly, `apply` is often the safer first choice.

---

# 18. Cherry-Pick

Apply a particular commit onto the current branch:

```bash
git cherry-pick abc123
```

Scenario:

```text
develop has an urgent bug fix
release branch needs only that fix
```

Use:

```bash
git switch release/2.0
git cherry-pick <fix-commit>
```

Conflict:

```bash
git add file
git cherry-pick --continue
```

Abort:

```bash
git cherry-pick --abort
```

Cherry-pick is useful, but repeated duplicated logical changes can make later history harder to reason about.

## Useful cherry-pick forms

Apply one commit and add a reference to the original commit in the new commit message:

```bash
git cherry-pick -x <commit>
```

`-x` can be valuable for backports because it records where the change came from.

Apply multiple named commits:

```bash
git cherry-pick <commit1> <commit2>
```

Apply a range where you clearly understand the endpoints:

```bash
git cherry-pick <older>..<newer>
```

Revision ranges have precise semantics, so inspect the commits first:

```bash
git log --oneline <older>..<newer>
```

Do not cherry-pick a merge commit casually. Merge commits have multiple parents, and Git may need a mainline parent selection; if you do not understand why that is needed, prefer another integration approach or ask a maintainer.

---

# 19. Tags and Releases

Tags identify important commits.

Lightweight:

```bash
git tag v1.0.0
```

Annotated:

```bash
git tag -a v1.0.0 -m "Release 1.0.0"
```

Inspect:

```bash
git show v1.0.0
```

Push:

```bash
git push origin v1.0.0
```

All:

```bash
git push origin --tags
```

Delete local:

```bash
git tag -d v1.0.0
```

Delete remote:

```bash
git push origin --delete v1.0.0
```

Formal releases usually benefit from annotated/signed tags.

## Lightweight vs annotated tag

A lightweight tag is essentially a named reference. An annotated tag stores a tag object with metadata such as tagger, date, and message, and can also be signed. For releases, annotated tags usually communicate intent better.

List tags:

```bash
git tag
git tag --list "v2.*"
```

Find a human-friendly name near a commit:

```bash
git describe --tags --always
```

A Git tag and a hosting-platform "Release" are related but not identical. Hosting platforms may attach release notes and downloadable assets to a tag.

---

# 20. Detached HEAD and Revision Syntax

Detached HEAD means:

```text
HEAD → commit
```

rather than:

```text
HEAD → branch → commit
```

Enter intentionally:

```bash
git switch --detach <commit>
```

If useful commits are created:

```bash
git switch -c experiment
```

## Revision syntax

```text
HEAD
HEAD~1
HEAD~2
HEAD^
HEAD^2
main
origin/main
v1.0.0
```

`~n` follows first-parent ancestry repeatedly.

`^n` selects a parent, especially useful for merge commits.

## Common revision expressions

| Expression | Meaning |
|---|---|
| `HEAD~1` | first parent of `HEAD` |
| `HEAD~3` | follow first parents three times |
| `HEAD^` | first parent of `HEAD` |
| `HEAD^2` | second parent of a merge commit |
| `A..B` | commits reachable from `B` but not from `A` |
| `A...B` | symmetric-difference commit set in many log contexts; triple-dot diff has merge-base semantics |
| `branch:path/file` | file content at a revision |

Examples:

```bash
git show HEAD~1
git log main..feature --oneline
git show v1.0.0:README.md
```

Revision syntax is powerful enough that it deserves deliberate practice. When using ranges for destructive or publishing operations, inspect the selected commits first.

---

# 21. Git Internals and Object Model

Important object types:

```text
blob
tree
commit
annotated tag
```

## Blob

Stores file content.

## Tree

Represents directory structure and points to blobs/subtrees.

## Commit

Contains references/metadata such as:

```text
tree
parent(s)
author
committer
message
```

## Inspect objects

```bash
git cat-file -t <hash>
git cat-file -p <hash>
```

Git object IDs are content-derived hashes.

Modern Git can support SHA-256 repositories, while SHA-1 repositories remain common, so scripts should avoid unnecessary fixed assumptions about hash format/length.

## How objects connect

A simplified commit snapshot looks like this:

```text
branch ref
   |
   v
commit ----> parent commit(s)
   |
   v
root tree
   |
   +----> subtree ----> blob
   |
   +---------------> blob
```

- A **blob** stores file content, not the filename.
- A **tree** maps names to blobs/subtrees and records modes.
- A **commit** points to one root tree and normally one or more parent commits, plus author/committer metadata and a message.
- A **branch ref** points to a commit and moves as new commits are created.

Git does not need to duplicate identical file content for every snapshot. If a file's content is unchanged, snapshots can refer to the same underlying object. Storage can later be compacted into packfiles for efficiency.

## Useful plumbing-style inspection commands

```bash
git rev-parse HEAD              # resolve a revision to an object ID
git ls-tree HEAD                # inspect a tree
git hash-object <file>          # calculate the object ID for file content
git cat-file -p HEAD            # inspect the commit object
```

These commands are mainly for learning, debugging, scripts, and tooling. Normal daily work should use porcelain commands such as `status`, `add`, `commit`, `switch`, `merge`, and `rebase`.

---

# 22. Commit Graph and Merge Base

Git history is a directed acyclic graph.

```text
A---B---C---F
     \     /
      D---E
```

Normal commit:

```text
one parent
```

Merge commit:

```text
multiple parents
```

Initial commit:

```text
no parent
```

## Merge base

Example:

```text
A---B---C main
     \
      D---E feature
```

Best common ancestor is B.

Find it:

```bash
git merge-base main feature
```

This explains why triple-dot comparisons and merges behave as they do.

---

# 23. File History, Blame, and Search

History of file:

```bash
git log -- app.js
```

With patches:

```bash
git log -p -- app.js
```

Follow rename:

```bash
git log --follow -- app.js
```

Line attribution:

```bash
git blame app.js
```

Use blame to discover context, not to attack people.

Search commit messages:

```bash
git log --grep="invoice"
```

Search when a string's occurrence count changed:

```bash
git log -S "calculateTax"
```

`-S` is useful when you want commits where the number of occurrences of a string changed. Another search mode is `-G`, which searches patch text using a regular expression:

```bash
git log -G "calculate.*Tax" -p
```

Search tracked file contents in the current worktree/index context:

```bash
git grep "calculateTax"
```

Useful log filters:

```bash
git log --author="Name" --oneline
git log --since="2 weeks ago" --oneline
git log --first-parent main --oneline
```

`--first-parent` is especially useful when a main branch contains many merged feature branches and you want a release-oriented view of the main line.

---

# 24. Bisect

`git bisect` performs a binary search for a bad commit.

Start:

```bash
git bisect start
git bisect bad
git bisect good v1.0.0
```

Test the commit Git checks out.

Then repeatedly:

```bash
git bisect good
```

or:

```bash
git bisect bad
```

Finish:

```bash
git bisect reset
```

Automate:

```bash
git bisect run ./test-script.sh
```

This is extremely powerful for regressions in long histories.

## How to choose good and bad points

- **bad** means the bug is present.
- **good** means you have verified the bug is absent.

Your first good commit does not need to be the immediately previous commit; it only needs to be an ancestor far enough back that the behavior is definitely good.

## Automation requirements

For:

```bash
git bisect run ./test-script.sh
```

the script must return exit codes that let Git classify the checked-out commit. Keep the test deterministic; flaky tests produce misleading results. When finished, always run:

```bash
git bisect reset
```

to return to your original checkout.

---

# 25. Worktrees

Worktrees let one repository have multiple checked-out branches in separate directories.

```bash
git worktree add ../project-hotfix hotfix/payment
```

Example:

```text
/project
  feature branch

/project-hotfix
  hotfix branch
```

Useful when you need urgent work without stashing/switching the current directory.

List:

```bash
git worktree list
```

Remove:

```bash
git worktree remove ../project-hotfix
```

## Create a new branch in a new worktree

```bash
git worktree add -b hotfix/payment ../project-hotfix main
```

This creates `hotfix/payment` from `main` and checks it out in the new directory.

## Important worktree rules

- Worktrees share the same underlying repository object database and most repository configuration.
- Git normally prevents the same branch from being checked out in more than one worktree at the same time.
- Removing the folder manually can leave stale worktree metadata. Prefer `git worktree remove`.
- If a linked worktree disappeared unexpectedly, `git worktree prune` can clean stale administrative records after you verify they are no longer needed.

---

# 26. Submodules, Subtree, Git LFS

## Submodules

Record another repository at a specific commit.

```bash
git submodule add <url> libs/shared
```

Clone:

```bash
git clone --recurse-submodules <url>
```

Initialize later:

```bash
git submodule update --init --recursive
```

Mental model:

```text
Parent repo stores:
"child repo should be at commit XYZ"
```

Submodules add complexity, so use them deliberately.

When a superproject records a submodule, it records a specific submodule commit, not simply "whatever is latest on main." After cloning, this is why submodules are commonly checked out at a detached `HEAD` matching the commit expected by the parent repository.

Useful inspection:

```bash
git submodule status
git diff --submodule
```

If the upstream URL in `.gitmodules` changes:

```bash
git submodule sync --recursive
git submodule update --init --recursive
```

A common team mistake is to commit the superproject's new submodule pointer without ensuring teammates/CI can fetch that exact child commit.

## Subtree

A subtree can integrate another project's content directly inside a normal directory of the main repository. Unlike a submodule, users cloning the main repository do not need a separate submodule initialization step for that directory.

`git subtree` is maintained in Git's `contrib/subtree` tooling and may not be installed by every Git distribution. Check first:

```bash
git subtree --help
```

When the command is available, a typical import is:

```bash
git subtree add --prefix=libs/shared <repository-url> main --squash
```

Update that subtree later:

```bash
git subtree pull --prefix=libs/shared <repository-url> main --squash
```

Extract the history of one directory into a branch:

```bash
git subtree split --prefix=libs/shared -b shared-history
```

### Submodule vs subtree

| Question | Submodule | Subtree |
|---|---|---|
| Parent records child as a specific external-repo commit? | Yes | No; files live in parent history |
| Extra clone/init step for users? | Usually yes | No |
| Child keeps clearly separate repository identity? | Yes | Can synchronize/split, but integration is more coupled |
| Parent repository contains child file contents directly? | No | Yes |
| Best when | Independent repositories need explicit version pinning | Consumers should receive dependency contents in a normal clone |

Subtree synchronization can create large or specialized history patterns, especially without `--squash`. Choose it deliberately and document the team's update/push procedure.

## Git LFS

Git LFS is a **separate Git extension**, not the core Git object-storage behavior used for ordinary files. It stores small pointer files in Git while large content is handled through LFS storage. Install Git LFS before using its commands.

For large binary assets:

```bash
git lfs install
git lfs track "*.psd"
git add .gitattributes
git add design.psd
git commit -m "Add design asset via LFS"
```

After configuring a tracking rule, commit the generated `.gitattributes` rule so the whole team uses the same LFS mapping. `git lfs track` affects matching files going forward; converting large files that are already deep in Git history is a separate migration task and can involve history rewriting.

Typical uses:

```text
large media
design files
models
binaries
```

---

# 27. Sparse Checkout and Partial Clone

## Sparse checkout

```bash
git sparse-checkout init --cone
git sparse-checkout set frontend shared
```

Useful when only part of a huge monorepo is needed.

## Partial clone

```bash
git clone --filter=blob:none <url>
```

Avoids downloading all blob content immediately and can fetch objects as needed.

These techniques are valuable for very large repositories.

## Sparse checkout vs partial clone

They solve different resource problems:

| Feature | Reduces files visible in working tree? | Can reduce objects downloaded? |
|---|---:|---:|
| Sparse checkout | Yes | Not by itself |
| Partial clone | Not necessarily | Yes |
| Both together | Yes | Yes, depending on access/server support |

Disable sparse checkout and restore a full working tree:

```bash
git sparse-checkout disable
```

Modern Git documentation still marks sparse checkout behavior as experimental in important respects. Treat it as an advanced workflow, especially when combining it with merges, rebases, external tools, or sparse indexes.

Partial clones may fetch missing objects on demand. That means some commands can unexpectedly require network access later even though the initial clone was smaller.

---

# 28. Hooks, Aliases, and Configuration

## Hooks

Common hooks:

```text
pre-commit
commit-msg
pre-push
post-merge
```

Common uses:

```text
lint
format
tests
commit-message validation
secret detection
```

Critical policy should also be enforced in CI/server controls because local hooks may be bypassed.

Repository-local hooks normally live under `.git/hooks/` unless `core.hooksPath` is configured. Hook files must be executable on systems that use executable permission bits, and the script's interpreter must exist.

Example policy split:

```text
Local pre-commit hook → fast formatting/lint feedback
CI pipeline           → authoritative lint/test/security enforcement
Server protection     → branch/review/push rules
```

Do not put the only copy of an important compliance rule in a developer's local hook.

## Aliases

```bash
git config --global alias.st status
git config --global alias.lg "log --graph --decorate --oneline --all"
```

Then:

```bash
git st
git lg
```

## Helpful configuration

```bash
git config --global fetch.prune true
git config --global rerere.enabled true
```

`rerere` means "reuse recorded resolution" and can reuse previous conflict resolutions.

---

# 29. SSH and HTTPS Authentication

## SSH

Generate a modern key where supported:

```bash
ssh-keygen -t ed25519 -C "you@example.com"
```

Private key:

```text
id_ed25519
```

Never share or commit it.

Public key:

```text
id_ed25519.pub
```

Add the public key to the hosting service.

A common test form is:

```bash
ssh -T git@<host>
```

## HTTPS

Remote:

```text
https://host/company/project.git
```

Modern hosting commonly uses:

```text
personal access token
credential manager
browser/OAuth login
```

instead of ordinary account passwords.

## SSH troubleshooting checklist

```bash
git remote -v
ssh -T git@<host>
```

If authentication fails, check:

1. The remote URL uses the protocol you intended.
2. The public key is registered with the hosting account.
3. Your SSH client is offering the correct private key.
4. The repository account actually has read/write permission.

## HTTPS credential storage

Do not place access tokens directly inside repository URLs, shell scripts, or committed configuration. Prefer the operating system's supported credential manager/helper or the hosting provider's login flow.

Authentication proves who you are to the server; authorization determines whether that identity is allowed to read or push a particular repository/branch.

---

# 30. Forks, Pull Requests, and Code Review

## Fork workflow

Typical remotes:

```text
origin   → your fork
upstream → original project
```

Add upstream:

```bash
git remote add upstream <original-url>
```

Update:

```bash
git fetch upstream
git switch main
git rebase upstream/main
```

## PR/MR lifecycle

```text
Issue
 ↓
Branch
 ↓
Commits
 ↓
Push
 ↓
Pull/Merge Request
 ↓
CI
 ↓
Code Review
 ↓
Approval
 ↓
Merge
```

Good PR description explains:

```text
Problem
Solution
Important design decisions
Testing
Screenshots
DB/migration impact
Deployment impact
Rollback concerns
```

Good review checks:

```text
correctness
security
readability
maintainability
performance
tests
edge cases
architecture
```

Small focused PRs are easier and safer to review.

---

# 31. Branching Strategies

Common strategies:

```text
Feature branches
GitFlow
GitHub Flow
Trunk-based development
Release branches
Fork workflow
```

No strategy is universally best.

## Quick comparison

| Strategy | Typical branch lifetime | Release style | Best fit | Main risk |
|---|---|---|---|---|
| Short feature branches / GitHub-style flow | Short | Continuous/frequent | Most product teams with CI | PR queue/integration delay |
| Trunk-based development | Very short or direct-to-trunk | Continuous | Strong CI, feature flags, disciplined teams | Broken trunk if controls are weak |
| GitFlow | Longer-lived develop/release branches | Scheduled/versioned | Products with formal release trains | Merge overhead and branch drift |
| Release branches | Release lifetime | Maintained versions | Products supporting multiple versions | Backport duplication |
| Fork workflow | Contributor-controlled | Project dependent | Open source / restricted write access | Keeping fork synced |

The branch names themselves do not create a process. CI rules, review policy, release automation, permissions, and team habits are what make a branching model work.

Choose according to:

```text
team size
release frequency
CI maturity
deployment style
compliance
support requirements
risk tolerance
```

---

# 32. GitFlow

Typical branches:

```text
main
develop
feature/*
release/*
hotfix/*
```

Typical path:

```text
feature → develop → release → main
```

Hotfix:

```text
main → hotfix → main
          \
           develop
```

Advantages:

- explicit release structure;
- useful for scheduled/versioned releases.

Disadvantages:

- more long-lived branches;
- more merge overhead;
- slower integration.

## What each GitFlow branch is for

| Branch | Purpose | Typical source/destination |
|---|---|---|
| `main` | released/production history | receives release and hotfix work |
| `develop` | integration line for the next release | receives completed features |
| `feature/*` | isolated feature development | starts from and returns to `develop` |
| `release/*` | stabilization for an upcoming version | starts from `develop`, finishes into release lines |
| `hotfix/*` | urgent fix to released code | starts from `main`, then propagated to other active lines |

Git itself does not enforce these names or transitions. A team must define who may merge, how CI runs, how release branches are retired, and how hotfixes are propagated.

## When not to choose GitFlow

If a team deploys many times per day, has strong automated testing, and can hide incomplete work behind feature flags, the overhead of long-lived `develop`/`release` branches may add more friction than value.

---

# 33. GitHub Flow and Trunk-Based Development

## GitHub-style flow

```text
main
  \
   short-lived feature
        |
        PR
        |
       main
```

Main should generally remain deployable.

## Trunk-based development

Developers integrate frequently with:

```text
small changes
short-lived branches
strong CI
automated tests
feature flags
```

Why?

Long-lived branches diverge and become expensive to merge.

## GitHub-style flow step by step

A common pattern is:

```text
1. update main
2. create short feature branch
3. commit small changes
4. push branch
5. open PR/MR
6. run CI and review
7. merge
8. deploy from main according to team automation
9. delete feature branch
```

This is simple because there is one principal long-lived integration branch.

## Trunk-based development is more than "everyone commits to main"

Trunk-based development depends on fast feedback and small integrations. Teams commonly use:

- short-lived branches or controlled direct-to-trunk commits;
- automated tests before/after integration;
- feature flags for incomplete behavior;
- small changes that are easy to review and revert;
- branch protection or merge queues when appropriate.

Without these controls, direct work on trunk can increase risk rather than reduce it.

## Choosing between the two

Use GitHub-style short feature branches when PR review is the normal unit of collaboration. Move closer to trunk-based development when the team can integrate extremely frequently without keeping long-lived branches and has the automation to keep trunk healthy.

---

# 34. Releases and Hotfixes

## Release branch

```bash
git switch -c release/2.5 main
```

Stabilize, test, then tag:

```bash
git tag -a v2.5.0 -m "Release 2.5.0"
```

## Hotfix

Production bug:

```bash
git switch main
git pull --ff-only
git switch -c hotfix/payment-null
```

Fix, test, commit:

```bash
git add .
git commit -m "fix: handle null payment reference"
git push -u origin hotfix/payment-null
```

After review/merge:

```text
deploy
tag if appropriate
propagate fix to active release/development lines
```

## Backporting a hotfix

If a production fix also belongs in an older or parallel maintained release line, identify the exact fix commit and apply it deliberately:

```bash
git switch release/2.4
git cherry-pick -x <fix-commit>
```

The `-x` reference is useful in many backport workflows because the new commit message records the original commit. Always test the target release separately; dependency/API context may differ.

## Release checklist

A Git release process commonly needs more than a tag:

```text
version update
release notes/changelog
CI green
migrations reviewed
security checks
artifact build
deployment/rollback plan
annotated or signed tag if policy requires
post-release verification
```

Keep release mechanics in versioned CI/CD configuration or documented automation where possible instead of relying on one person's manual terminal history.

---

# 35. Git with CI/CD

Git often triggers automation.

```text
Commit
 ↓
Push / PR
 ↓
CI
 ├── Install
 ├── Lint
 ├── Build
 ├── Unit tests
 ├── Integration tests
 └── Security checks
 ↓
Review/Merge
 ↓
Deployment pipeline
```

Possible conventions:

```text
develop → development
release/* → staging/UAT
main → production
tag v* → production release
```

Important:

> A Git branch is not inherently an environment. The mapping is implemented by team policy and CI/CD configuration.

## Common Git events used by CI/CD

Pipelines are often triggered by events such as:

```text
push to a branch
pull/merge request opened or updated
tag pushed
manual approval
scheduled job
```

The exact event names and YAML syntax depend on the CI platform. Git itself only provides the repository history and refs; the CI system decides what to run.

## What a healthy pull-request pipeline should answer

Before merge, automation should make it easy to answer:

- Does the code build?
- Do automated tests pass?
- Do lint/format rules pass?
- Are migrations/schema changes valid?
- Did secret/security scanning find a problem?
- Is the change safe for the target runtime/version?

## Keep generated credentials out of Git

CI tokens, cloud keys, signing secrets, and deployment passwords belong in the CI platform's secret store or another dedicated secret manager. Repository files should reference secret names/variables, not embed production values.

## Reproducibility matters

A useful pipeline should be tied to a specific commit/tag so you can answer exactly which source produced an artifact. For releases, prefer promoting a tested artifact through environments rather than rebuilding different source states manually at each stage.

---

# 36. Semantic Versioning and Conventional Commits

## Semantic Versioning

```text
MAJOR.MINOR.PATCH
```

Example:

```text
2.4.1
```

Typical interpretation:

```text
MAJOR → incompatible change
MINOR → backward-compatible feature
PATCH → backward-compatible bug fix
```

Pre-release:

```text
2.0.0-beta.1
```

## Conventional Commits

Pattern:

```text
type(scope): description
```

Examples:

```text
feat(auth): add password reset
fix(invoice): reject duplicate invoice
docs(readme): add deployment guide
refactor(api): simplify validation
test(payment): add refund tests
chore(deps): update packages
ci(pipeline): add security scan
```

This can power automated changelogs and release tooling.

---

# 37. Monorepos

Example:

```text
repo/
├── apps/
│   ├── web/
│   ├── admin/
│   └── api/
└── packages/
    ├── ui/
    └── shared/
```

Advantages:

```text
atomic cross-project changes
shared tooling
consistent standards
easy dependency visibility
```

Challenges:

```text
repository size
CI duration
permissions
ownership
coupling
```

Useful techniques:

```text
path-based CI
build caching
sparse checkout
partial clone
CODEOWNERS
```

---

# 38. Security, Secrets, and Signed Commits

Never commit:

```text
passwords
API keys
private keys
cloud credentials
database passwords
production .env files
access tokens
```

If a secret enters history:

```text
1. Treat it as compromised
2. Revoke/rotate it
3. Remove it from current code
4. Rewrite history if necessary
5. Coordinate with collaborators
6. Update CI/deploy secrets
```

Deleting the file in a later commit does not remove it from earlier history.

## First response to a leaked secret

Rotation/revocation comes before history cleanup. Rewriting Git history may reduce future exposure, but it cannot make an already copied credential safe again.

After rotation:

- remove the secret from source/configuration;
- add appropriate ignore or secret-management rules;
- decide whether history rewriting is required;
- coordinate force-updates and fresh clones if history is rewritten;
- inspect CI logs, artifacts, caches, package registries, and deployment systems for copies.

Use dedicated secret-management systems or CI secret stores instead of committing production credentials.

## Signed commits

Example:

```bash
git commit -S -m "Release security patch"
```

Signed annotated tag:

```bash
git tag -s v2.0.0 -m "Release 2.0.0"
```

Verification:

```bash
git verify-commit <commit>
git verify-tag v2.0.0
```

---

# 39. History Rewriting and Force Push

History rewriting changes commit IDs.

Use cases:

```text
clean private feature history
remove secrets
remove huge files
change metadata in migrations
```

A commonly used modern history-rewrite tool is:

```text
git filter-repo
```

## Force push

Dangerous:

```bash
git push --force
```

Safer when rewriting an allowed personal branch:

```bash
git push --force-with-lease
```

Why safer?

It checks that the remote ref still matches the state you expect, reducing accidental overwrites of other people's new work.

Avoid force-pushing important shared branches except during intentionally coordinated exceptional maintenance.

`--force-with-lease` is safer than plain `--force`, but it is not magic. Its protection depends on the expected remote state. Background fetches can update remote-tracking refs and weaken the intuitive "nobody changed it since I saw it" assumption. On high-risk branches, use branch protection/server policy instead of relying only on client-side force-push flags.

---

# 40. Repository Maintenance and Migration

Integrity:

```bash
git fsck
```

Object statistics:

```bash
git count-objects -vH
```

Optimize:

```bash
git gc
```

Prune stale remote-tracking refs:

```bash
git fetch --prune
```

Most maintenance is automatic.

Run maintenance commands because you have a reason, not as a daily ritual. `git gc` can repack objects and clean repository data according to Git's retention rules; `git fsck` checks object connectivity/validity but is not a repair button for every problem.

Before aggressive cleanup or repository surgery, make sure important refs exist on a reliable remote or backup and understand which unreachable objects may eventually be removed.

## Migration

Mirror clone:

```bash
git clone --mirror <old-url>
```

Mirror push:

```bash
git push --mirror <new-url>
```

`--mirror` is powerful and can also delete destination refs to match the source, so use it carefully.

---

# 41. Real-World Scenarios

## Scenario 1: You forgot to update before coding

Your feature has local commits, and main advanced.

```bash
git fetch origin
git rebase origin/main
```

Or merge based on team policy:

```bash
git merge origin/main
```

Resolve conflicts, test, push.

---

## Scenario 2: Push rejected because remote changed

Do not immediately force-push.

Inspect:

```bash
git fetch origin
git log --graph --oneline --decorate --all
```

Then integrate:

```bash
git rebase origin/<branch>
```

or merge.

---

## Scenario 3: Committed on the wrong branch

Assume commit is still local.

Create correct branch at current commit:

```bash
git branch feature/correct-place
```

Move original branch back:

```bash
git reset --hard HEAD~1
```

Switch:

```bash
git switch feature/correct-place
```

Your commit remains on the new branch.

---

## Scenario 4: Need one fix from another branch

```bash
git cherry-pick <commit>
```

---

## Scenario 5: Need to stop current work for urgent issue

```bash
git stash -u
git switch main
git switch -c hotfix/urgent
```

Later:

```bash
git switch original-feature
git stash pop
```

---

## Scenario 6: Lost commit after hard reset

```bash
git reflog
```

Find the old hash:

```bash
git branch recovery <hash>
```

---

## Scenario 7: Feature branch history is messy

If the branch is your own and rewriting is permitted:

```bash
git rebase -i origin/main
```

Clean with:

```text
squash
fixup
reword
drop
```

Then:

```bash
git push --force-with-lease
```

---

## Scenario 8: Bad commit already reached shared main

Prefer:

```bash
git revert <commit>
git push
```

This preserves shared history.

---

## Scenario 9: Need to compare feature against current main

```bash
git fetch origin
git diff origin/main...HEAD
```

---

## Scenario 10: A bug appeared sometime in the last 200 commits

Use:

```bash
git bisect
```

instead of manually testing commits one by one.

---

## Scenario 11: Production hotfix while feature work is open

Instead of stashing, use worktree:

```bash
git worktree add ../hotfix main
```

Then create/fix in the second directory.

---

## Scenario 12: Merge conflict contains two valid business changes

Do not simply select one side.

Example:

Branch A:

```javascript
validateInvoiceNumber();
```

Branch B:

```javascript
validateVendorStatus();
```

Correct resolution may be:

```javascript
validateInvoiceNumber();
validateVendorStatus();
```

Conflict resolution is software development, not just marker deletion.

---

# 42. Troubleshooting

## `fatal: not a git repository`

You are outside a Git repository.

```bash
pwd
ls -a
```

Navigate into the project or initialize the intended directory.

## `nothing to commit, working tree clean`

No uncommitted change requires a commit.

## `non-fast-forward`

The remote contains history your local branch does not contain.

```bash
git fetch origin
git log --graph --oneline --all
```

Integrate before pushing.

## `src refspec main does not match any`

Possible:

```text
wrong branch name
no commits yet
typo
```

Check:

```bash
git branch
git status
git log --oneline
```

## Detached HEAD

If work should be kept:

```bash
git switch -c my-work
```

## Merge or rebase says there are unresolved conflicts

Check:

```bash
git status
```

Do not start another merge/rebase on top. Resolve each unmerged path, stage the result, and then continue the operation:

```bash
git add <resolved-files>
git merge --continue
# or
git rebase --continue
```

Use the matching `--abort` command if you intend to cancel the operation.

## `index.lock` already exists

First make sure no Git process, IDE Git operation, or commit editor is still running. A stale lock can remain after a crash. Do **not** automatically delete `.git/index.lock` while another Git process may still be active, because the lock protects repository state from concurrent writes.

## `refusing to merge unrelated histories`

This often means the two histories do not share an ancestor, such as when a local repository and a separately initialized remote both contain independent initial commits. Do not immediately add `--allow-unrelated-histories`. First confirm that joining two independent repositories is actually what you intend.

## Wrong author name/email in a local latest commit

Correct configuration, then amend if the commit is still safe to rewrite:

```bash
git config user.name "Correct Name"
git config user.email "correct@example.com"
git commit --amend --reset-author
```

If the incorrect commit is already shared, coordinate before rewriting history.

## Authentication error

Check:

```bash
git remote -v
```

Then inspect:

```text
SSH key
credential manager
token
repository permission
remote URL
```

---

# 43. Common Mistakes

1. Running `git add .` without reviewing.
2. Force-pushing shared branches.
3. Rebasing history others are using.
4. Committing secrets.
5. Using `reset --hard` without checking status.
6. Resolving conflicts blindly.
7. Creating huge unrelated commits.
8. Keeping feature branches open for too long.
9. Pulling without understanding whether merge or rebase will be used.
10. Treating `origin/main` as if it automatically updates without fetch.
11. Assuming `.gitignore` removes already tracked files.
12. Committing generated dependency folders such as `node_modules`.
13. Using Git as the only disaster-recovery strategy.
14. Deleting branches before confirming work is merged/reachable.
15. Changing line-ending settings mid-project without team coordination.

---

# 44. Professional Best Practices

1. Use `git status` constantly.
2. Review `git diff` before staging.
3. Review `git diff --staged` before committing.
4. Make small logical commits.
5. Use meaningful messages.
6. Keep feature branches short-lived.
7. Fetch/sync regularly.
8. Protect important branches.
9. Require passing CI.
10. Require review for important changes.
11. Never commit secrets.
12. Tag releases consistently.
13. Prefer `--force-with-lease` over `--force`.
14. Do not rewrite shared history casually.
15. Learn reflog before you need it.
16. Test conflict resolutions.
17. Use `.gitattributes` for repository consistency.
18. Automate lint/tests/security checks.
19. Delete merged feature branches when appropriate.
20. Document branching and release policy.
21. Keep commits independently understandable.
22. Use feature flags for incomplete trunk-based features.
23. Separate formatting-only changes from behavior changes when practical.
24. Avoid checking huge binaries into normal Git history.
25. Practice recovery in disposable repositories.

---

# 45. Command Decision Guide

| Situation | Usually use |
|---|---|
| See repository state | `git status` |
| See unstaged changes | `git diff` |
| See staged changes | `git diff --staged` |
| Stage selected hunks | `git add -p` |
| Unstage file | `git restore --staged file` |
| Discard unstaged tracked edit | `git restore file` |
| Fix latest private commit | `git commit --amend` |
| Undo shared commit | `git revert <commit>` |
| Move private history backward | `git reset` |
| Recover lost commit | `git reflog` |
| Temporarily store WIP | `git stash` |
| Apply one specific commit | `git cherry-pick` |
| Integrate branches preserving topology | `git merge` |
| Replay private work onto new base | `git rebase` |
| Find bug-introducing commit | `git bisect` |
| Mark release | `git tag` |
| Inspect remote without integrating | `git fetch` |
| Update only if fast-forward is possible | `git pull --ff-only` or fetch + `git merge --ff-only` |
| Update local commits on top of fetched upstream | `git pull --rebase` or fetch + `git rebase` |
| Publish and set upstream | `git push -u origin <branch>` |
| Preview untracked cleanup | `git clean -nd` |
| Remove verified untracked files/directories | `git clean -fd` |
| Find which ignore rule applies | `git check-ignore -v <path>` |
| See local/remote branch tracking | `git branch -vv` |
| Compare feature to merge base with main | `git diff main...feature` |
| Work on two branches simultaneously | `git worktree add ...` |
| Update nested submodules to recorded commits | `git submodule update --init --recursive` |
| Restore a file from a specific commit | `git restore --source=<commit> -- <file>` |

---

# 46. Master Cheat Sheet

## Setup

```bash
git --version
git config --global user.name "Name"
git config --global user.email "email@example.com"
git config --list --show-origin
```

## Repo

```bash
git init
git clone <url>
git status
```

## Changes

```bash
git diff
git add file
git add .
git add -p
git diff --staged
git commit -m "message"
git commit --amend
```

## History

```bash
git log
git log --oneline
git log --oneline --graph --decorate --all
git show <commit>
git reflog
```

## Branches

```bash
git branch
git switch branch
git switch -c branch
git branch -d branch
git branch -D branch
git branch -m new-name
```

## Remote

```bash
git remote -v
git fetch origin
git pull
git push
git push -u origin branch
```

## Merge/Rebase

```bash
git merge branch
git merge --abort
git rebase branch
git rebase --continue
git rebase --abort
git rebase -i HEAD~5
```

## Undo

```bash
git restore file
git restore --staged file
git reset --soft HEAD~1
git reset HEAD~1
git reset --hard HEAD~1
git revert <commit>
```

## Stash

```bash
git stash
git stash -u
git stash list
git stash apply
git stash pop
```

## Cherry-pick

```bash
git cherry-pick <commit>
git cherry-pick --continue
git cherry-pick --abort
```

## Tags

```bash
git tag
git tag -a v1.0.0 -m "Release"
git push origin v1.0.0
```

## Investigation

```bash
git blame file
git log -- file
git log -p -- file
git log -S "text"
git bisect start
git grep "text"
git log -G "regex" -p
git log --first-parent main --oneline
```

## Cleanup safety

```bash
git clean -nd              # preview untracked cleanup
git clean -fd              # remove after review
git fetch --prune          # remove stale remote-tracking refs
```

## Advanced

```bash
git worktree list
git submodule update --init --recursive
git sparse-checkout init --cone
git fsck
git gc
```

---

# 47. Practice Roadmap

## Level 1 — Beginner

Practice:

```text
init
status
add
commit
log
diff
restore
.gitignore
```

Exercise:

1. Create a repository.
2. Add `README.md`.
3. Commit it.
4. Modify it.
5. Inspect diff.
6. Stage it.
7. Inspect staged diff.
8. Commit it.
9. Make an unwanted edit.
10. Restore the file.

## Level 2 — Branching

Create:

```text
main
feature/login
feature/profile
```

Practice:

```text
switch
merge
branch deletion
merge conflicts
```

Create an intentional conflict and resolve it.

## Level 3 — Remote collaboration

Practice with a test remote:

```text
clone
fetch
pull
push
tracking branches
```

## Level 4 — Recovery

In a disposable repository:

```text
reset
revert
reflog
stash
```

Intentionally lose a commit and recover it.

## Level 5 — History manipulation

Practice:

```text
rebase
interactive rebase
cherry-pick
```

## Level 6 — Debugging

Create 20 commits and insert a bug around commit 12.

Find it with:

```bash
git bisect
```

## Level 7 — Team simulation

Simulate:

```text
main
develop
feature/*
release/*
hotfix/*
```

Perform a feature, release, conflict, urgent hotfix, and release tag.

## Level 8 — Advanced repository

Experiment with:

```text
worktree
submodule
LFS
sparse checkout
hooks
signed commits
```

---

# 48. Interview Questions

## Beginner

### What is Git?

A distributed version control system that tracks project history through commits and references.

### Git vs GitHub?

Git is version-control software; GitHub is a hosted collaboration platform built around Git repositories.

### What is the staging area?

The index containing the exact snapshot intended for the next commit.

### What is a branch?

A movable reference to a commit.

### What is HEAD?

A reference representing the currently checked-out position, normally the current branch.

## Intermediate

### Fetch vs pull?

Fetch downloads remote information. Pull fetches and then integrates changes.

### Merge vs rebase?

Merge combines histories without rewriting existing commits. Rebase replays commits onto another base and therefore rewrites those commits.

### Reset vs revert?

Reset moves references and can change index/working state. Revert creates a new inverse commit and is safer for shared history.

### What is `origin/main`?

A local remote-tracking reference representing the last fetched state of `main` from `origin`.

### Why does Git have staging?

To let developers construct focused commits containing exactly the intended changes.

## Advanced

### What is reflog?

A local record of reference movements useful for recovery.

### Why is rebase dangerous on shared branches?

It creates new commit identities and changes ancestry, which can conflict with collaborators' existing history.

### Why is `--force-with-lease` safer than `--force`?

It checks whether the remote reference changed unexpectedly before overwriting it.

### What is a merge base?

A best common ancestor used for merge and comparison logic.

### What object types does Git use?

Primarily blobs, trees, commits, and annotated tag objects.

### What is detached HEAD?

HEAD points directly to a commit instead of a branch.

### What is bisect?

A binary-search mechanism for identifying the commit that introduced a regression.

### Why are branches cheap?

A branch is mainly a lightweight reference rather than a full copy of project files/history.

---

# 49. Final Mental Models

## Model 1 — Local state

```text
Working Tree
    |
    | add
    v
Index
    |
    | commit
    v
Repository
```

## Model 2 — Remote collaboration

```text
Remote
  |
  | fetch
  v
Remote-tracking refs
  |
  | merge/rebase
  v
Local branch
  |
  | push
  v
Remote
```

## Model 3 — Branch = movable reference

```text
A---B---C
        ^
        |
       main
        ^
       HEAD
```

A branch is not a folder or a second full project.

## Model 4 — History = graph

```text
A---B---C---F
     \     /
      D---E
```

The graph explains:

```text
merge
rebase
reset
revert
cherry-pick
bisect
reflog
```

## Model 5 — Undo depends on whether history is shared

```text
Private history
    ↓
amend / reset / rebase may be appropriate

Shared history
    ↓
revert / new corrective commits are usually safer
```

## Model 6 — Git is snapshot-oriented

Do not think:

```text
Git just saves files.
```

Think:

```text
Git records project states and relationships between them.
```

---

# Recommended Professional Daily Workflow

```bash
git status
git fetch origin
git switch -c feature/my-feature

# edit

git diff
git add -p
git diff --staged
git commit -m "feat: implement my feature"
git push -u origin feature/my-feature
```

Then:

```text
Open PR/MR
↓
Run CI
↓
Code review
↓
Address feedback
↓
Merge
↓
Delete feature branch when appropriate
```

---

# What to Learn Next

After mastering this handbook, continue with:

```text
GitHub/GitLab branch protection
CODEOWNERS
merge queues
CI/CD pipelines
GitOps
semantic-release
automated changelogs
dependency scanning
secret scanning
SAST
supply-chain security
monorepo build systems
feature flags
deployment strategies
repository governance
```

---


# Core Handbook Summary

The commands worth understanding deeply are:

```text
status
diff
add
commit
log
branch
switch
fetch
pull
push
merge
rebase
restore
reset
revert
reflog
stash
cherry-pick
tag
bisect
```

Do not simply memorize them.

For every Git operation, ask:

```text
What state does this command read?
What state does it modify?
Does it rewrite history?
Can it destroy work?
Does it affect collaborators?
Can it be recovered?
```

Once you can answer those questions reliably, you are not merely memorizing Git commands—you understand Git.

A final recovery habit worth memorizing is:

```bash
git status
git reflog
```

When something looks wrong, stop making destructive changes, inspect state first, and protect important commits with a temporary branch before trying to repair history.

---

# 50. Git Scenario Q&A — What Command Should I Use?

This section is designed for the question beginners ask most often:

> **"I am in this situation. What Git command should I use now?"**

The answers use simple English and prefer safe, inspect-first workflows. Replace placeholders such as `<branch>`, `<commit>`, and `<file>` with real values.

## A. Starting, cloning, and checking a repository

### Q1. I have a normal folder. How do I start using Git in it?

```bash
git init
git status
```

`git init` creates the repository metadata. It does not automatically commit your files.

### Q2. I want a copy of an existing remote repository. What do I use?

```bash
git clone <url>
```

Use `clone` instead of `init` when the project already exists as a Git repository elsewhere.

### Q3. I want to clone the repository into a different local folder name.

```bash
git clone <url> my-folder
```

### Q4. I do not know whether my current folder is inside a Git repository.

```bash
git status
```

For the repository root path:

```bash
git rev-parse --show-toplevel
```

### Q5. I want to know my Git version.

```bash
git --version
```

This matters when documentation describes behavior introduced or changed in newer Git versions.

### Q6. I want to see which username and email this repository will use for commits.

```bash
git config user.name
git config user.email
```

### Q7. I use one email for work and another for personal repositories.

Inside the work repository:

```bash
git config --local user.name "Your Work Name"
git config --local user.email "work@example.com"
```

Local configuration overrides global configuration for that repository.

## B. Understanding current changes

### Q8. I changed files. What should I run first?

```bash
git status
```

Then inspect actual unstaged changes:

```bash
git diff
```

### Q9. I want a short one-line-style status.

```bash
git status --short
```

Or with branch/upstream information:

```bash
git status -sb
```

### Q10. I want to see changes I have not staged yet.

```bash
git diff
```

### Q11. I want to see exactly what will go into my next commit.

```bash
git diff --staged
```

### Q12. One file contains two unrelated changes. I want to stage only one part.

```bash
git add -p <file>
```

Review each hunk and stage only the pieces that belong to the commit.

### Q13. I staged a file and then edited it again. Why does Git show it twice?

The staged snapshot and the newest working-tree version are now different. Inspect both:

```bash
git diff --staged
git diff
```

Stage the newer edit too only if it belongs in the same commit.

### Q14. I want to know why Git is ignoring a file.

```bash
git check-ignore -v <file>
```

It shows the ignore rule and file that caused the match.

## C. Staging and committing

### Q15. I want to stage one file.

```bash
git add <file>
```

### Q16. I want to stage several known files.

```bash
git add file1 file2 file3
```

### Q17. I want to stage all current changes, but I want to review first.

```bash
git status
git diff
git add .
git diff --staged
```

Do not treat `git add .` as a substitute for review.

### Q18. I staged the wrong file. I want to unstage it but keep my edit.

```bash
git restore --staged <file>
```

The working-tree edit remains.

### Q19. I want to commit the staged files.

```bash
git commit -m "Describe the change"
```

### Q20. I want to write a longer commit message in my editor.

```bash
git commit
```

### Q21. I committed but forgot one file, and the commit is still private.

```bash
git add <forgotten-file>
git commit --amend --no-edit
```

This replaces the latest commit with a new commit ID.

### Q22. My latest private commit message is wrong.

```bash
git commit --amend
```

Edit the message, save, and exit the editor.

### Q23. I want to add a small fix that will later be squashed into an earlier commit.

```bash
git commit --fixup <target-commit>
git rebase -i --autosquash <base>
```

Use this only when rewriting the affected history is allowed.

### Q24. I used `git commit -am`, but my new file was not committed. Why?

`-a` handles modifications/deletions of tracked files, not new untracked files. Stage the new file:

```bash
git add <new-file>
git commit
```

## D. Branches and switching

### Q25. I want to see my local branches.

```bash
git branch
```

### Q26. I want to see local and remote-tracking branches.

```bash
git branch -a
```

### Q27. I want to create a new branch and switch to it.

```bash
git switch -c feature/my-feature
```

### Q28. I want to switch to an existing branch.

```bash
git switch <branch>
```

### Q29. Git refuses to switch branches because my local edits would be overwritten.

Choose one action: commit the work, stash it, or discard it if truly unwanted. For temporary storage:

```bash
git stash push -u -m "WIP before branch switch"
git switch <branch>
```

### Q30. I want to rename my current branch.

```bash
git branch -m <new-name>
```

### Q31. I want to delete a local branch that is already merged.

```bash
git branch -d <branch>
```

`-d` is intentionally safer than `-D` because Git can refuse when it believes commits are not merged.

### Q32. I really want to delete an unmerged local branch.

First inspect it:

```bash
git log <branch> --oneline
```

If you are certain:

```bash
git branch -D <branch>
```

### Q33. I want to know what upstream branch my local branch tracks.

```bash
git branch -vv
```

## E. Remotes, fetching, pulling, and pushing

### Q34. I want to see configured remote repositories.

```bash
git remote -v
```

### Q35. I want to add a remote called `origin`.

```bash
git remote add origin <url>
```

### Q36. The remote URL changed.

```bash
git remote set-url origin <new-url>
```

### Q37. I want to download remote changes without changing my current branch.

```bash
git fetch origin
```

This is one of the safest ways to inspect remote progress.

### Q38. I want to update remote-tracking branches and remove stale ones whose remote branches were deleted.

```bash
git fetch --prune
```

### Q39. I want to update my branch only when it can fast-forward.

```bash
git pull --ff-only
```

This refuses a divergent-history integration instead of choosing merge/rebase for you.

### Q40. I want my local commits replayed on top of the newest upstream commits.

```bash
git pull --rebase
```

Use this when your team allows rebasing your local/private commits.

### Q41. I want `pull` to integrate by merge instead of rebase.

```bash
git pull --no-rebase
```

### Q42. I want to push a new branch for the first time and set its upstream.

```bash
git push -u origin <branch>
```

### Q43. My push was rejected because the remote branch has new commits.

Do not force-push immediately. Inspect first:

```bash
git fetch origin
git status -sb
git log --graph --oneline --decorate --all
```

Then follow team policy, for example:

```bash
git rebase origin/<branch>
```

or:

```bash
git merge origin/<branch>
```

Then push normally.

### Q44. I rebased my own already-published feature branch and now a normal push is rejected.

After fetching and confirming nobody else's unexpected work is on the branch:

```bash
git push --force-with-lease
```

Do not use this casually on shared/protected branches.

### Q45. I want to delete a remote branch.

```bash
git push origin --delete <branch>
```

## F. Merge scenarios

### Q46. I want to merge `feature/login` into `main`.

```bash
git switch main
git merge feature/login
```

Run tests before pushing the result.

### Q47. I want the merge to succeed only if it can be fast-forwarded.

```bash
git merge --ff-only <branch>
```

### Q48. I want a merge commit even if fast-forward is possible.

```bash
git merge --no-ff <branch>
```

Use this only if the team's history policy prefers explicit merge commits.

### Q49. I want one combined commit from a feature branch, not a true merge commit.

```bash
git merge --squash <branch>
git diff --staged
git commit -m "Add feature"
```

This does not record the feature branch as a merge parent.

### Q50. A merge has conflicts. What do I do?

```bash
git status
```

Open conflicted files, create the correct final content, then:

```bash
git add <resolved-files>
git diff --staged
git commit
```

Test the resolved code.

### Q51. I started a merge and want to cancel it.

```bash
git merge --abort
```

This is safest when you started from a clean working tree.

### Q52. A conflict shows both sides contain useful code.

Do not choose "ours" or "theirs" blindly. Manually combine the business logic, remove conflict markers, test it, then stage the resolved file.

## G. Rebase scenarios

### Q53. My feature branch is behind `main`. I want a linear feature history.

```bash
git fetch origin
git switch <feature>
git rebase origin/main
```

Resolve any conflicts, test, and continue.

### Q54. Rebase stopped on a conflict.

```bash
git status
# resolve files
git add <resolved-files>
git rebase --continue
```

### Q55. I want to cancel the rebase completely.

```bash
git rebase --abort
```

### Q56. Git is replaying a commit I intentionally do not want during rebase.

```bash
git rebase --skip
```

Use this only when you really mean to omit that commit's change.

### Q57. My last five private commits are messy. I want to reorder, squash, or rename them.

```bash
git rebase -i HEAD~5
```

Use `reword`, `squash`, `fixup`, `drop`, or reorder lines as needed.

### Q58. My feature was based on the wrong branch.

Advanced option:

```bash
git rebase --onto <correct-base> <old-base> <feature>
```

Make a backup branch and inspect the graph before doing this on important work.

## H. Undoing file changes

### Q59. I changed a tracked file and want to throw away the unstaged edit.

```bash
git restore <file>
```

This destroys that unstaged edit. Inspect `git diff <file>` first if you may need it.

### Q60. I want the version of a file from an older commit.

```bash
git restore --source=<commit> -- <file>
```

Review the resulting working-tree change and commit it if appropriate.

### Q61. I accidentally deleted a tracked file locally and want it back.

```bash
git restore <file>
```

### Q62. I have an untracked file that Git cannot restore because it was never committed.

Git cannot recover content it never stored. If you simply want to delete untracked files, preview first:

```bash
git clean -nd
```

Then, only if correct:

```bash
git clean -fd
```

## I. Undoing commits safely

### Q63. I want to undo my latest local commit but keep all changes staged.

```bash
git reset --soft HEAD~1
```

### Q64. I want to undo my latest local commit and keep changes unstaged.

```bash
git reset HEAD~1
```

### Q65. I want to remove my latest local commit and discard its tracked changes completely.

```bash
git reset --hard HEAD~1
```

This is destructive. Check `git status` and consider creating a backup branch first.

### Q66. A bad commit is already on shared `main`. What is the normal safe fix?

```bash
git revert <bad-commit>
git push
```

This adds a new commit that reverses the selected change.

### Q67. I need to revert a range of shared commits.

There are several valid ways depending on history and whether merges are involved. First inspect the range:

```bash
git log --oneline <older>..<newer>
```

Then revert deliberately. Do not run a bulk range command until you understand the commit ordering and whether merge commits are included.

### Q68. I reset too far and my commit disappeared.

```bash
git reflog
```

Find the old commit, then protect it:

```bash
git branch recovery/my-work <commit>
```

### Q69. I rebased and now I want the branch position from before the rebase.

```bash
git reflog
```

Locate the pre-rebase branch tip and create a recovery branch before doing more destructive operations.

## J. Stash scenarios

### Q70. I have unfinished tracked work and need a clean working tree temporarily.

```bash
git stash push -m "WIP"
```

### Q71. I also have new untracked files that must be stashed.

```bash
git stash push -u -m "WIP"
```

### Q72. I want to see all stashes.

```bash
git stash list
```

### Q73. I want to inspect a stash before applying it.

```bash
git stash show -p stash@{0}
```

### Q74. I want to apply a stash but keep it as a backup.

```bash
git stash apply stash@{0}
```

### Q75. I want to apply the latest stash and remove it when successful.

```bash
git stash pop
```

### Q76. A stash is old and I am sure I no longer need it.

```bash
git stash drop stash@{0}
```

### Q77. A stash does not apply cleanly to my current branch.

Try a dedicated recovery branch:

```bash
git stash branch recover-stash stash@{0}
```

This can be easier when the original base has moved significantly.

## K. Cherry-pick and backport scenarios

### Q78. I need exactly one fix from another branch.

```bash
git cherry-pick <commit>
```

### Q79. I am backporting a fix and want the new commit message to mention the original commit.

```bash
git cherry-pick -x <commit>
```

### Q80. Cherry-pick stopped on a conflict.

```bash
git status
# resolve files
git add <resolved-files>
git cherry-pick --continue
```

### Q81. I want to cancel the cherry-pick.

```bash
git cherry-pick --abort
```

## L. Tags and release scenarios

### Q82. I want to mark the current commit as release `v1.0.0`.

Preferred for a formal release:

```bash
git tag -a v1.0.0 -m "Release 1.0.0"
```

### Q83. I created a local tag. How do I publish it?

```bash
git push origin v1.0.0
```

### Q84. I want to list only version-2 tags.

```bash
git tag --list "v2.*"
```

### Q85. I tagged the wrong commit and the tag is only local.

```bash
git tag -d <tag>
```

Then recreate the tag at the correct commit. If the tag was already published, coordinate before replacing it.

### Q86. I want Git to describe the current commit using the nearest suitable tag.

```bash
git describe --tags --always
```

## M. History and investigation

### Q87. I want a compact graph of all branches.

```bash
git log --graph --oneline --decorate --all
```

### Q88. I want to see one specific commit.

```bash
git show <commit>
```

### Q89. I want the history of one file.

```bash
git log -- <file>
```

With patches:

```bash
git log -p -- <file>
```

### Q90. The file was renamed. I still want its earlier history.

```bash
git log --follow -- <file>
```

### Q91. I want to know which commit last changed each line.

```bash
git blame <file>
```

Use it to find context, then inspect the relevant commits.

### Q92. I want to find commits whose messages mention `invoice`.

```bash
git log --grep="invoice"
```

### Q93. I want to find when the number of occurrences of a string changed.

```bash
git log -S "calculateTax" -p
```

### Q94. I want commits whose patches match a regular expression.

```bash
git log -G "calculate.*Tax" -p
```

### Q95. I want to search tracked files for text.

```bash
git grep "search text"
```

### Q96. I want to compare two commits.

```bash
git diff <commit1> <commit2>
```

### Q97. I want to see what my feature changed since it diverged from `main`.

```bash
git diff main...<feature>
```

Fetch first if you really mean the latest remote main:

```bash
git fetch origin
git diff origin/main...HEAD
```

## N. Finding a bug with bisect

### Q98. A bug exists now but did not exist in an old release. How can I find the first bad commit?

```bash
git bisect start
git bisect bad
git bisect good <known-good-commit-or-tag>
```

Test each selected commit and mark it `good` or `bad`. When done:

```bash
git bisect reset
```

### Q99. I have an automated test that can identify good and bad revisions.

```bash
git bisect run ./test-script.sh
```

Use a deterministic test script with appropriate exit status behavior.

## O. Worktree scenarios

### Q100. I am halfway through a feature and need to fix production without stashing.

Create another working tree:

```bash
git worktree add -b hotfix/urgent ../project-hotfix main
```

Now your existing directory can stay on the feature while the second directory handles the hotfix.

### Q101. I want to list all linked worktrees.

```bash
git worktree list
```

### Q102. I finished with a linked worktree.

```bash
git worktree remove ../project-hotfix
```

Prefer this over deleting the directory manually.

## P. Submodule scenarios

### Q103. I cloned a project and its submodule directories are empty or incomplete.

```bash
git submodule update --init --recursive
```

### Q104. I want to clone a repository and initialize submodules immediately.

```bash
git clone --recurse-submodules <url>
```

### Q105. I want to see which submodule commits the project is using.

```bash
git submodule status
```

### Q106. A submodule URL changed upstream.

```bash
git submodule sync --recursive
git submodule update --init --recursive
```

### Q107. I am inside a submodule and see detached HEAD. Is that always an error?

No. A superproject commonly checks out the exact recorded submodule commit, which can leave the submodule detached. Create/switch to a real submodule branch before making work you intend to develop and publish there.

## Q. Large files and Git LFS

### Q108. My repository needs large binary files. What should I consider?

Install Git LFS, then configure matching file types, for example:

```bash
git lfs install
git lfs track "*.psd"
git add .gitattributes
```

Then add and commit the large file normally. Confirm your remote hosting supports the required LFS storage/quota.

### Q109. I already committed a huge binary years ago. Will `git lfs track` remove it from old history?

No. Tracking affects how matching files are handled going forward. Cleaning existing historical blobs is a migration/history-rewrite problem and requires coordination.

## R. Sparse checkout and partial clone

### Q110. The monorepo is huge and I only need two directories in my working tree.

```bash
git sparse-checkout init --cone
git sparse-checkout set frontend shared
```

Treat sparse checkout as an advanced workflow and test your tools with it.

### Q111. I want to return from sparse checkout to the full working tree.

```bash
git sparse-checkout disable
```

### Q112. I want to reduce initial blob download in a huge repository.

```bash
git clone --filter=blob:none <url>
```

This is a partial clone. Missing objects can be fetched later when needed, so network access may still occur during later commands.

### Q113. Do sparse checkout and partial clone mean the same thing?

No. Sparse checkout controls which tracked files are populated in the working tree. Partial clone controls which objects are initially downloaded. They can be used separately or together.

## S. Authentication scenarios

### Q114. I use an SSH remote and want to test whether authentication works.

```bash
ssh -T git@<host>
```

The exact success message depends on the hosting provider.

### Q115. My remote uses HTTPS and password authentication fails.

Many hosting platforms use tokens, browser/OAuth flows, or credential managers instead of ordinary account passwords. Check your hosting provider's current authentication requirements and use a secure credential helper rather than embedding a token in the repository URL.

### Q116. I can authenticate but cannot push.

Authentication and permission are different. Check repository/branch authorization, protected-branch rules, and whether you have write access.

## T. Fork and open-source contribution scenarios

### Q117. I forked a project. What remote names are common?

```text
origin   → your fork
upstream → original project
```

Add the original repository if needed:

```bash
git remote add upstream <original-url>
```

### Q118. I want to update my fork's local `main` from the original project.

```bash
git fetch upstream
git switch main
git rebase upstream/main
```

A merge is also valid if that project prefers merge-based synchronization.

### Q119. I want to contribute a feature without pushing directly to upstream `main`.

Typical flow:

```bash
git switch -c feature/my-change
git add -p
git commit -m "feat: describe change"
git push -u origin feature/my-change
```

Then open a pull/merge request according to the hosting platform.

## U. Release and hotfix scenarios

### Q120. Production is broken. I need an urgent hotfix branch from the deployed main line.

```bash
git fetch origin
git switch main
git pull --ff-only
git switch -c hotfix/issue-name
```

Fix, test, commit, push, review, merge, and propagate the fix to any other maintained lines.

### Q121. The same fix is needed in an older supported release branch.

If the fix is a clean self-contained commit, a backport may use:

```bash
git switch release/older
git cherry-pick -x <fix-commit>
```

Test the older release independently because context/dependencies may differ.

## V. Cleanup and maintenance scenarios

### Q122. My working directory has lots of generated untracked files. How do I see what Git would delete?

```bash
git clean -nd
```

### Q123. The preview is correct. How do I remove those untracked files and directories?

```bash
git clean -fd
```

### Q124. I want to remove ignored build artifacts too.

Preview first:

```bash
git clean -ndx
```

Only if correct:

```bash
git clean -fdx
```

This can delete ignored local configuration such as `.env`, so treat it as highly destructive.

### Q125. I want to check repository object integrity.

```bash
git fsck
```

This is a diagnostic integrity check, not a universal repair command.

### Q126. I want to see repository object storage statistics.

```bash
git count-objects -vH
```

### Q127. I want to request Git repository optimization.

```bash
git gc
```

Most repositories do not need this manually as a routine daily command.

## W. Repository migration scenarios

### Q128. I need to migrate all refs from one Git server to another.

A mirror workflow can be appropriate:

```bash
git clone --mirror <old-url>
cd <repo>.git
git push --mirror <new-url>
```

`--mirror` is powerful and can delete destination refs to match the source. Verify the destination and test the migration plan before running it on an important server.

### Q129. I only need an ordinary working copy on a new remote, not a full mirror migration.

Add/change the remote and push the intended branches/tags explicitly rather than using `--mirror`.

## X. Common error-message scenarios

### Q130. Git says `fatal: not a git repository`.

Check where you are:

```bash
pwd
ls -a
```

Move into the repository directory or initialize the intended directory with `git init`.

### Q131. Git says `nothing to commit, working tree clean`.

There are no uncommitted tracked/staged changes. If you expected a new file, check whether it is untracked or ignored:

```bash
git status --short
git check-ignore -v <file>
```

### Q132. Git says `src refspec main does not match any`.

Check branch and commit existence:

```bash
git branch
git status
git log --oneline
```

Common causes are a different branch name, no initial commit yet, or a typo.

### Q133. Git says `refusing to merge unrelated histories`.

Stop and confirm whether you are intentionally joining two independently initialized histories. Do not use `--allow-unrelated-histories` merely to silence the error.

### Q134. Git reports an `index.lock` file.

First close/finish any running Git operations or IDE actions. Only treat the lock as stale after confirming no Git process is using it.

### Q135. I am in detached HEAD and made commits I want to keep.

Create a branch immediately:

```bash
git switch -c keep-my-work
```

### Q136. I accidentally checked out an old commit only to inspect it. How do I return?

Switch back to your branch:

```bash
git switch <branch>
```

## Y. Team-safety scenarios

### Q137. A teammate says, "Just force-push main." Should I?

Normally no. Protected/shared branches should use reviewed corrective commits or a coordinated maintenance procedure. If a bad shared commit needs undoing, `git revert` is usually safer.

### Q138. Should I rebase a branch other teammates are actively using?

Usually not without coordination. Rebase changes commit identities. Prefer merge or agree on a history-rewrite process with the team.

### Q139. I see a secret in an old commit. Can I just delete the file now?

No. First revoke/rotate the credential. Then remove it from current files and decide whether coordinated history rewriting is required.

### Q140. I have a huge pull request with formatting, refactoring, and a feature mixed together. What should I do next time?

Use focused commits and, where practical, separate formatting-only changes from behavior changes. Before committing, use:

```bash
git add -p
git diff --staged
```

### Q141. I am unsure whether a Git command may destroy my work. What is the safest general process?

Use this order:

```text
1. git status
2. git diff / git diff --staged
3. git log --graph --oneline --decorate --all
4. create a backup branch if history will move
5. use dry-run/preview when available
6. run the command
7. git status again
8. test the project
```

For a commit you are worried about losing:

```bash
git branch backup/before-change
```

A cheap backup reference is often the best protection before learning an advanced history command.

## Z. Which command family should I think about?

When you still do not know the exact command, first classify the problem:

| Your question | Think about | First safe command |
|---|---|---|
| "What changed?" | status/diff | `git status` |
| "What was committed?" | log/show | `git log --oneline` |
| "What will I commit?" | staging | `git diff --staged` |
| "How do I move between lines of work?" | branch/switch | `git branch -vv` |
| "What changed on the server?" | fetch/remote refs | `git fetch` |
| "How do I combine histories?" | merge/rebase | inspect graph first |
| "How do I undo this?" | restore/reset/revert | identify whether it is working tree, index, private history, or shared history |
| "Where did my commit go?" | reflog | `git reflog` |
| "I need this one commit elsewhere" | cherry-pick | `git show <commit>` first |
| "I need temporary storage" | stash | `git stash push -m "..."` |
| "Which commit caused the bug?" | bisect | identify known-good and known-bad points |
| "I need two branches open at once" | worktree | `git worktree list` |
| "Why is a file ignored?" | ignore rules | `git check-ignore -v <file>` |
| "Can I delete these generated files?" | clean | `git clean -nd` first |

The safest Git habit is not memorizing the most powerful command. It is **identifying which state you are changing before you change it**.

---
