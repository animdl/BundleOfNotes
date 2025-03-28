# Setup

```
// Check if identity is already set
git config --list
git config --get user.<name | email>

// Remove a configuration value
git config --unset <key>
git config --unset-all <key>

// Remove a section of key, value pairs
git config --remove-section "section name"

// Set your identity
git config --add --global user.name "username"
git config --add --global user.email "email"

// Set default branch name
git config --add --global init.defaultBranch <master | main>
```

## Locations
Git configs can be stored in multiple locations:
- system: `/etc/gitconfig`, all users on the system
- global: `~/.gitconfig`, all projects of a user
- local: `.git/config`, a specific project
- worktree: `.git/config.worktree`, a part of a project

# Commands
```
// Create a new repo
git init

// Shows branch status; file changes and untracked files
git status

// Stage a file (add it to the index) to be committed later
// (without staging, every file would be included in every commit)
git add <path-to-file | pattern>

// Commit all your staged files
// (commit is a snapshot of the rep at a given point in time)
git commit -m "commit message"

// Shows a history of commits, and their author and date
git [--no-pager] log [-n <number of commits to show>]
```

```
// Displays the contents of a commit from the object files stored in .git/objects
// The tree hash will return the contents of the blob object (files committed)
git cat-file -p <commit hash | tree hash>

// 

```
