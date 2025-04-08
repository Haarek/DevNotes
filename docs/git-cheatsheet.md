# Git Command Line Cheat Sheet

A quick reference to the most commonly used Git commands.

## 📦 Repository Management

| Task                           | Command                                       |
|--------------------------------|-----------------------------------------------|
| Clone a repository             | `git clone <repo-url>`                        |
| Initialize a repository        | `git init`                                    |
| View remote URLs               | `git remote -v`                               |
| Add a remote                   | `git remote add origin <url>`                 |
| Remove a remote                | `git remote remove origin`                    |

## 📄 Staging & Committing

| Task                           | Command                                       |
|--------------------------------|-----------------------------------------------|
| Check status                   | `git status`                                  |
| Stage file(s)                  | `git add <file>` or `git add .`              |
| Unstage file                   | `git reset <file>`                            |
| Commit changes                 | `git commit -m "Your message"`                |
| Amend last commit              | `git commit --amend`                          |

## 🔄 Branching & Merging

| Task                           | Command                                       |
|--------------------------------|-----------------------------------------------|
| List branches                  | `git branch`                                  |
| Create a new branch            | `git checkout -b <branch-name>`               |
| Switch branches                | `git checkout <branch-name>`                  |
| Merge branch                   | `git merge <branch-name>`                     |
| Delete branch                  | `git branch -d <branch-name>`                 |

## 📤 Pushing & Pulling

| Task                           | Command                                       |
|--------------------------------|-----------------------------------------------|
| Pull latest changes            | `git pull`                                    |
| Push current branch            | `git push`                                    |
| Push new branch                | `git push -u origin <branch-name>`            |

## 🔍 Logs & Diffs

| Task                           | Command                                       |
|--------------------------------|-----------------------------------------------|
| View commit history            | `git log`                                     |
| One-line history               | `git log --oneline --graph --all`             |
| Show changes (unstaged)        | `git diff`                                    |
| Show staged changes            | `git diff --cached`                           |
| Show changes for a file        | `git log -p <file>`                           |

## 🧹 Clean Up & Reset

| Task                           | Command                                       |
|--------------------------------|-----------------------------------------------|
| Discard changes (unstaged)     | `git checkout -- <file>`                      |
| Remove untracked files         | `git clean -f`                                |
| Reset to last commit           | `git reset --hard`                            |

## 🧠 Useful Tips

- Use `git stash` to temporarily save changes.
- Use `git rebase -i` for interactive rebase and cleanup.
- Use `.gitignore` to exclude files from version control.

