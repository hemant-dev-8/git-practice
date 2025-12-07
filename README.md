# Git and GitHub Tutorial: From Beginner to Advanced

This tutorial is designed as a comprehensive handbook for learning Git and GitHub. It starts with the basics for absolute beginners and progresses to advanced topics for intermediate developers. We'll use simple language, real-world examples, and practical tips. Each Git command includes a terminal code block with explanations. Diagrams are ASCII-based for clarity. All content reflects modern Git practices as of 2025, including preferences for commands like `git switch` over older alternatives where applicable.

## 1. What is Git (Simple Explanation)

Git is a version control system that tracks changes in your files over time. Think of it like a time machine for your code: it lets you save "snapshots" of your project at different points, so you can go back if something breaks, collaborate with others without overwriting work, and experiment safely. Git was created by Linus Torvalds in 2005 for Linux development and is now the standard for software projects worldwide.

Example: If you're writing a document, Git records every edit as a "commit," allowing you to revert to any previous version.

## 2. Why Developers Use Git

Developers use Git to:
- **Track history**: See who changed what and why.
- **Collaborate**: Multiple people can work on the same project without conflicts.
- **Branch safely**: Experiment with new features without breaking the main code.
- **Backup work**: Your changes are saved in a repository (repo), which can be stored locally or remotely.
- **Integrate with tools**: Git powers platforms like GitHub, GitLab, and Bitbucket for code hosting, reviews, and automation.

Without Git, teams risk losing work or dealing with messy file copies like "project_v1_final_reallyfinal.docx."

## 3. How Git Works Internally (In a Simple Way)

Git stores your project as a series of snapshots (commits) in a hidden `.git` folder. Each commit is a unique hash (like a fingerprint) pointing to file changes.

- **Objects**: Git saves blobs (file contents), trees (directory structures), commits (metadata like author, message), and tags.
- **References**: Branches and tags are pointers to commits.
- **HEAD**: Points to your current working commit.

Simple analogy: Git is like a chain of photos. Each photo (commit) captures the entire project state. Branches are like forking paths in the chain.

Internally, Git uses a directed acyclic graph (DAG) for history, ensuring no cycles and efficient storage via deltas (differences between files).

## 4. Installing Git on Windows, macOS, Linux

- **Windows**: Download from git-scm.com. Run the installer, choose defaults (includes Git Bash for terminal). Verify: Open Git Bash and run `git --version`.
- **macOS**: Install via Homebrew (brew.sh): `brew install git`. Or download from git-scm.com. Verify: `git --version` in Terminal.
- **Linux**: Use package manager. Ubuntu/Debian: `sudo apt update && sudo apt install git`. Fedora: `sudo dnf install git`. Verify: `git --version`.

After installation, Git is ready for use in your terminal.

## 5. First-Time Git Configuration (Name, Email, Default Branch)

Run these global configs once:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main  # Sets default branch to 'main' instead of 'master'
```

View configs: `git config --list`. These set your commit authorship and modern defaults.

## 6. How Repositories Work

A repository (repo) is a folder containing your project files plus the `.git` directory for history.

- Initialize: Create a new repo in an empty folder.
- Clone: Copy an existing repo.
- Files states: Untracked (new), modified (changed), staged (ready for commit), committed (saved).

Repos can be bare (no working files, for servers) or standard.

## 7. Local Repo vs Remote Repo

- **Local repo**: On your machine. All operations (commits, branches) happen here fast and offline.
- **Remote repo**: Hosted online (e.g., GitHub). Acts as a shared backup and collaboration hub. Push/pull to sync.

Example: Work locally on features, push to remote for team review.

## 8. Git Basic Workflow

1. Modify files in your working directory.
2. Stage changes (add to staging area).
3. Commit staged changes to history.
4. Push to remote if collaborating.

Repeat: Edit → Stage → Commit → Push.

## 9. Staging Area Concept

The staging area (index) is a "prep zone" between your working files and commits. It lets you select which changes to include in the next commit, keeping commits focused.

Example: Edit three files, but stage only two for a commit about "bug fix," leaving the third for later.

## 10. Main Git Commands

Here are key commands with examples. Assume you're in a repo directory.

- **git init**: Creates a new local repo.

```bash
git init  # Initializes .git in current folder
```

- **git clone**: Copies a remote repo locally.

```bash
git clone https://github.com/user/repo.git  # Clones into a new folder
```

- **git status**: Shows working directory status (modified, staged, untracked files).

```bash
git status
```

- **git add**: Stages files/changes.

```bash
git add file.txt  # Stages one file
git add .  # Stages all changes
```

- **git commit**: Saves staged changes as a commit.

```bash
git commit -m "Initial commit"  # -m for message
```

- **git log**: Views commit history.

```bash
git log  # Full log
git log --oneline --graph  # Compact with graph
```

- **git diff**: Shows changes.

```bash
git diff  # Unstaged changes
git diff --staged  # Staged changes
git diff HEAD~1  # Vs last commit
```

- **git reset**: Unstages or resets commits (use carefully).

```bash
git reset file.txt  # Unstage file
git reset --hard HEAD~1  # Discard last commit and changes
```

- **git restore**: Restores files (modern alternative to checkout for files).

```bash
git restore file.txt  # Discard changes in file
git restore --staged file.txt  # Unstage file
```

- **git rm**: Removes files from repo and working dir.

```bash
git rm file.txt  # Stages removal
git rm --cached file.txt  # Remove from repo but keep locally
```

- **git mv**: Renames/moves files.

```bash
git mv old.txt new.txt  # Renames and stages
```

- **git branch**: Manages branches.

```bash
git branch  # List branches
git branch new-branch  # Create
git branch -d old-branch  # Delete
```

- **git switch**: Switches branches (modern, safer than checkout).

```bash
git switch main  # Switch to main
git switch -c new-branch  # Create and switch
```

- **git checkout**: Older command for switching (use switch instead for branches).

```bash
git checkout main  # Legacy switch
git checkout -b new-branch  # Legacy create and switch
```

- **git merge**: Merges branches.

```bash
git switch main
git merge feature-branch  # Merges into main
```

- **git rebase**: Reapplies commits on new base.

```bash
git switch feature
git rebase main  # Rebase feature onto main
```

- **git push**: Sends local commits to remote.

```bash
git push origin main  # Push main to origin remote
git push -u origin main  # Set upstream tracking
```

- **git pull**: Fetches and merges from remote.

```bash
git pull origin main  # Fetch + merge
```

- **git fetch**: Downloads remote changes without merging.

```bash
git fetch origin  # Update local tracking branches
```

- **git stash**: Temporarily saves changes.

```bash
git stash  # Stash changes
git stash pop  # Apply and remove stash
git stash list  # View stashes
```

- **git tag**: Marks commits (e.g., releases).

```bash
git tag v1.0  # Lightweight tag
git tag -a v1.0 -m "Release v1.0"  # Annotated
git push origin v1.0  # Push tag
```

## 11. Branching and Merging Explained with Diagrams

Branching creates parallel histories. Main is stable; features go on branches.

ASCII Diagram: Simple Branching

```
* main (initial commit)
 \
  * feature (new commit)
```

Merging integrates branches.

Diagram: Merge

```
* main --- * --- * (merge commit)
            /
           * feature
```

Fast-forward merge (no conflicts, linear):

```
* main --- * feature (main moves forward)
```

Three-way merge creates a new commit with two parents.

## 12. When to Use Merge and When to Use Rebase

- **Merge**: Preserves history, good for shared branches. Creates merge commits showing collaboration. Use for integrating completed features into main.
- **Rebase**: Rewrites history for a linear timeline. Moves your commits atop the base. Use for cleaning local branches before sharing (e.g., before PR). Avoid on public branches to prevent history rewrites.

Example: Rebase your feature branch on main before merging to keep history clean.

## 13. Resolving Merge Conflicts (Step-by-Step)

Conflicts happen when same lines are edited differently.

1. Run `git merge` or `git pull` – Git marks conflicts in files with `<<<<<<<`, `=======`, `>>>>>>>`.
2. Open the file, edit to resolve (keep desired changes).
3. Stage resolved file: `git add file.txt`.
4. Commit: `git commit -m "Resolved conflicts"`.

Example conflicted file:

```
<<<<<<< HEAD
Your change
=======
Their change
>>>>>>> branch
```

Tools like VS Code or Git mergetool help visually.

## 14. How Pull Requests Work (GitHub)

Pull Requests (PRs) are GitHub's way to propose changes.

1. Fork or branch from repo.
2. Commit changes on branch.
3. Push branch to GitHub.
4. Open PR: Compare branch to base (e.g., main), add description.
5. Reviewers comment, request changes.
6. Update via pushes.
7. Merge PR (squash, merge commit, or rebase).

PRs enable code reviews, discussions, and CI checks.

## 15. Forking Workflow (Open-Source Style)

For contributing to others' repos:

1. Fork the repo on GitHub (creates your copy).
2. Clone your fork locally: `git clone your-fork-url`.
3. Add upstream remote: `git remote add upstream original-url`.
4. Create feature branch, commit changes.
5. Push to your fork: `git push origin feature`.
6. Open PR from your fork to upstream.

Sync fork: `git fetch upstream; git rebase upstream/main`.

## 16. GitHub Issues, Actions, Projects Overview

- **Issues**: Track bugs, features, tasks. Label, assign, milestone. Use Markdown for descriptions.
- **Actions**: Automate workflows (CI/CD). YAML files in `.github/workflows` for builds, tests on push/PR.
- **Projects**: Kanban boards for organizing issues/PRs. Automate columns (e.g., move on close).

Example: Create issue for bug, link to PR that fixes it.

## 17. Practical Git Workflows

- **Feature Branch Workflow**: Create branch per feature, develop, PR to main. Simple for small teams.
- **Gitflow Workflow**: Branches: main (releases), develop (integration), feature/*, release/*, hotfix/*. Complex for large projects with releases.
- **Trunk-Based Development**: Short-lived branches, frequent merges to main. Emphasizes CI, reduces merge hell.
- **Release Management**: Use tags (v1.0), branches for maintenance (release/v1). GitHub Releases for artifacts.

Choose based on team size: Feature branch for most.

## 18. Everyday Git Usage Examples

- **Creating New Features**: `git switch -c feature/new-ui`; edit files; `git add .`; `git commit -m "Add UI components"`; push; open PR.
- **Fixing Bugs**: Branch from main: `git switch -c bugfix/crash`; fix; commit; PR.
- **Updating from Main**: On feature branch: `git fetch origin; git rebase origin/main`.
- **Reviewing Code with PRs**: Comment on lines, suggest changes, approve/merge.
- **Writing Good Commit Messages**: Use imperative: "Fix login bug" not "Fixed...". Body for details.
- **Version Management with Tags**: After merge: `git tag -a v1.1 -m "Stable release"; git push origin v1.1`.
- **Stashing Temporary Work**: Mid-feature: `git stash`; switch branches; later `git stash pop`.

## 19. Real-World Mistakes Beginners Make (and How to Avoid Them)

- **Committing everything at once**: Avoid by staging selectively; review `git diff --staged`.
- **Pushing without pulling**: Causes conflicts; always `git pull` first.
- **Working on main**: Use branches; set repo policy to protect main.
- **Bad commit messages**: Follow "50/72 rule" – short subject, detailed body.
- **Forgetting .gitignore**: Add early for build files, secrets.
- **Force pushing public branches**: Breaks others' work; use `--force-with-lease`.
- **Ignoring conflicts**: Resolve immediately; don't skip.

Tip: Use `git status` often.

## 20. Advanced Topics

- **Interactive Rebase (git rebase -i)**: Edit history. `git rebase -i HEAD~3` – pick/squash/edit commits interactively.
- **Squash Commits**: In rebase: mark 's' to combine. Cleans messy history before PR.
- **Amend Commits**: `git commit --amend` – edit last commit message or add files.
- **Cherry-Pick**: Apply specific commit: `git cherry-pick commit-hash`.
- **Clean Untracked Files**: `git clean -fd` (dry run: -n) – removes untracked.
- **Worktrees**: Multiple working dirs: `git worktree add ../new-tree branch`.
- **Git Hooks**: Scripts in .git/hooks (e.g., pre-commit for linting). Use tools like Husky.
- **.gitignore Deep Explanation**: File listing patterns to ignore (e.g., *.log, /build/). Global: `~/.gitignore`. Nested for subdirs. ! to negate. Check with `git check-ignore -v file`.

## 21. Git Security Basics

- **Avoid Committing Secrets**: Use .gitignore for .env, keys. Scan with git-secrets tool.
- **How to Rotate Credentials**: If leaked, generate new (e.g., API keys), update repos, commit without old ones.
- **Using SSH Keys vs HTTPS**: SSH for secure, key-based auth (no passwords). Generate: `ssh-keygen`; add to GitHub. Clone: git@github.com:user/repo.git. HTTPS for simplicity but requires PATs (Personal Access Tokens).

Prefer SSH for frequent use.

## 22. Daily Best Practices Every Developer Should Follow

- **Commit small, logical changes**: Easier to review/revert.
- **Always write meaningful commit messages**: Subject <50 chars, body explains why/how.
- **Always pull before pushing**: Avoid conflicts.
- **Keep branches short-lived**: Merge/delete after 1-2 days.
- **Never commit directly to main**: Use PRs for reviews.
- **Rebase your feature branches before PR**: For clean history.
- **Delete merged branches regularly**: `git branch -d branch`; remote: `git push origin --delete branch`.
- **Keep your repo clean (.gitignore, naming)**: Consistent files/folders.
- **Review your diff before committing**: `git diff --staged`.
- **Use tags for releases**: Semantic versioning (v1.2.3).
- **Stash WIP instead of committing junk**: For temporary switches.

## 23. A Final Summary as a Cheat-Sheet

### Most Used Commands
- Setup: `git init`, `git clone url`, `git config --global ...`
- Daily: `git status`, `git add .`, `git commit -m "msg"`, `git push`, `git pull`
- Branches: `git switch -c branch`, `git branch -d branch`
- History: `git log --oneline --graph`, `git diff`
- Fixes: `git restore file`, `git stash`, `git rebase main`

### Common Workflows
- New feature: Branch → Edit → Commit → Rebase main → Push → PR → Merge.
- Bug fix: Similar, but from latest main.
- Open-source: Fork → Clone → Branch → Commit → Push → PR to upstream.

### Best Practices
- Small commits with good messages.
- Pull before push; rebase before PR.
- Use branches; protect main.
- .gitignore secrets; review diffs.
- Tag releases; clean branches.
