># README.md — Git Learning Journey

This document explains all the steps I followed while learning and practicing Git through this project. I describe the commands I used, the reasoning behind each action, and the problems I faced along the way.

---

>## Checking the Status of the Repository

- **initializes a new Git repo in the current directory.:**
```sh
git init
```
  It creates a .git/ directory where Git stores all its configuration.

- **Check current repository status:**  
```sh
git status  
```
  Shows which files are staged, unstaged, or untracked.

- **See more detailed changes:**  
```sh
git status -v  
```
  Helpful to see exactly what changes exist in the working tree.

---

>## Staging and Committing Changes

- **Stage a file for commit:**  
```sh
git add <file_name>  
```
  Prepares files for committing.

- **Stage interactively to review changes before staging:**  
```sh
git add -p <file_name>  
```
  Useful to control which changes are included.

- **Commit staged changes with a message:**  
```sh
git commit -m "<commit_message>"
```
  Saves changes in Git history.

---

>## Viewing Commit History

- **View full history:**  
```sh
git log  
```

- **View condensed one-line history:**  
```sh
git log --oneline
```

- **View last 2 commits from the last 5 minutes:**  
```sh
git log --oneline -n 2 --since="5 minutes ago"
```

- **Personalized log format (hash, date, message, branch, author):**  
```sh
git log --pretty=format:"* %h %ad | %s (%d) [%an]" --date=short
```

---

>## Restoring Previous Versions

- **Find the first commit:**  
```sh
git log --oneline --reverse
```

- **Restore a file to the first snapshot:**  
```sh
git checkout <first_commit_hash> -- <file_name>
```

- **Restore to a more recent snapshot:**  
```sh
git checkout <second_commit_hash> -- <file_name>
```

- **Return to the latest committed version:**  
```sh
git restore <file_name>
```

---

>## Tagging Versions

- **Tag the current version:**  
```sh
git tag v1
```

- **Tag the previous commit without using a hash:**  
```sh
git tag v1-beta HEAD~1
```

- **Switch between tagged versions:**  
```sh
git checkout <tag_name>
```

- **List all tags:**  
```sh
git tag
```

---

>## Undoing Changes

- **Revert the last commit without removing it from history:**  
```sh
git revert HEAD
```

- **Reset to a previous tag and remove later commits:**  
```sh
git reset --hard <tag_name>
```

- **Discard staged changes:**  
```sh
git restore --staged <file_name>
```

- **Expire old references and clean unreachable commits:**  
```sh
git reflog expire --expire=now --all  

git gc --prune=now --aggressive
```

- **Amend the last commit without changing content:**  
```sh
git commit --amend --no-edit
```

---

>## Moving Files and Directories

- **Move a file and stage the change:**  
```sh
git mv <file> <destination>
```

- **Create a Makefile and commit changes:**  
```sh
git add Makefile  

git commit -m "Add Makefile to run lib/hello.sh"
```

---

>## Exploring Git Internals

- `.git/` — hidden folder storing all Git data  
- `objects/` — stores commits, trees, and blobs  
- `refs/` — stores branch and tag references  
- `config` — repository settings  
- `HEAD` — points to the current branch  

- **Show commit object details:**  
```sh
git cat-file commit <hash>
```

- **Show the directory tree of a commit:**  
```sh
git ls-tree HEAD
```

- **Show content of a file from a specific commit:**  
```sh
git show HEAD:<file_path>
```

---

>## Branching, Merging, and Rebasing

- **Create a branch:**  
```sh
git branch <branch_name>
```

- **Switch to a branch:**  
```sh
git checkout <branch_name>
```

- **Compare differences between branches:**  
```sh
git diff <branch1> <branch2> <files>
```

- **Visualize commit tree:**  
```sh
git log --graph --oneline --all
```

- **Merge a branch into the current branch:**  
```sh
git merge <branch>
```

- **Rebase current branch on top of another branch:**  
```sh
git rebase <branch>  

git rebase --continue
```

**Notes:**  
- Merge creates a commit combining histories.  
- Rebase creates a linear history by replaying commits.  
- Fast-forward occurs when the current branch has no new commits, so Git moves the pointer forward.

**Conflict Example:**  
While merging main into greet, Git could not automatically merge because both branches modified the same lines. I manually resolved the conflict by keeping the desired content.

---

>## Remote Repositories and Bare Repos

- **Create a bare repository:**  
```sh
git clone --bare hello hello.git
```

- **Add a remote to the bare repository:**  
```sh
git remote add shared ../hello.git
```

- **Remove a remote:**  
```sh
git remote remove shared
```

- **Pull changes from a remote:**  
```sh
git pull <remote_name> <branch_name>
```

---

>## Problems Faced and Lessons Learned

- Conflicts happen when multiple branches modify the same lines — solved manually.  
- Forgetting to stage changes before committing caused errors — learned to always check git status.  
- Git keeps all history; garbage collection and reflog management are necessary for cleanup.  
- Understanding bare repositories clarified how shared repositories work in collaboration.
