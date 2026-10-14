# Episode 1 — Git and GitHub

## Overview

This session introduces Git and GitHub and explains how developers manage source code, track changes, and collaborate on software projects.

Students will create a repository, work with branches, commit changes, and publish their work to GitHub.

## Learning Objectives

By the end of this session, students will be able to:

- Understand the difference between Git and GitHub.
- Create and manage Git repositories.
- Track changes and create commits.
- Create and switch between branches.
- Push and pull changes between local and remote repositories.
- Merge branches and inspect project history.
- Undo changes safely.

## 1. Git and GitHub

- **Git:** A version control system that tracks changes in files.
- **GitHub:** An online platform for hosting Git repositories and collaborating with other developers.
- **Repository:** A project whose files and history are tracked by Git.
- **Commit:** A snapshot of changes saved in the repository history.
- **Branch:** An independent line of development.
- **Merge:** The process of integrating changes from one branch into another.

## 2. Create a New Repository

Create a new folder for your project and open a terminal inside it.

```bash
git init
```

Create a `README.md` file, then execute:

```bash
git add README.md
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/USERNAME/REPOSITORY.git
git push -u origin main
```

### Command Explanations

- `git init`: Initializes a local repository.
- `git add`: Stages changes for a commit.
- `git commit`: Saves staged changes in the repository history.
- `git branch -M main`: Renames the current branch to `main`.
- `git remote add origin`: Connects the local repository to GitHub.
- `git push -u origin main`: Pushes the branch to GitHub and sets its upstream.

Replace the repository URL with your own GitHub repository URL.

## 3. Clone an Existing Repository

Use `git clone` when you want to download an existing repository for the first time.

```bash
git clone https://github.com/USERNAME/REPOSITORY.git
cd REPOSITORY
```

Check the repository status and remote configuration:

```bash
git status
git remote -v
```

**Important:** `git clone` already initializes the local repository and configures its remote. You do not need to run `git init` or `git remote add origin` again.

## 4. Check and Track Changes

```bash
git status
git add .
git commit -m "Add project files"
git log --oneline
```

- `git status`: Shows the current branch and working-tree changes.
- `git add .`: Stages changes in the current directory and its subdirectories.
- `git commit`: Saves the staged changes.
- `git log --oneline`: Displays a compact commit history.

Inspect file differences:

```bash
git diff
git diff --staged
```

Press `q` to exit the Git pager.

## 5. Configure Git

Configure your author information before making commits.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Check the configuration:

```bash
git config --global --list
```

## 6. Create and Use Branches

Branches allow developers to work on features independently.

Create a feature branch:

```bash
git switch -c feature/add-message
```

Check the current branch:

```bash
git branch
git branch --show-current
```

Create a file named `message.txt`, add some content, and commit it:

```bash
git add .
git commit -m "Add welcome message"
git log --oneline
```

## 7. Push a Branch to GitHub

```bash
git push -u origin feature/add-message
```

The `-u` option sets the upstream branch, allowing you to use `git push` and `git pull` more conveniently in future operations.

## 8. Fetch, Pull, and Push

```bash
git fetch origin
git pull
git push
```

- `git fetch`: Downloads remote updates without integrating them into the current branch.
- `git pull`: Fetches and integrates remote changes into the current branch.
- `git push`: Uploads local commits to the remote repository.

## 9. Merge Branches

After completing a feature, merge it into `main`.

```bash
git switch main
git merge feature/add-message
git log --oneline --graph --all
git push origin main
```

If Git reports a merge conflict, resolve the conflicting files, stage the resolved changes, and complete the merge as instructed by Git.

## 10. Undo Changes

### Discard Unstaged Changes

```bash
git restore filename.py
```

This discards unstaged changes in the specified file.

### Revert a Commit

```bash
git log --oneline
git revert COMMIT_ID
```

`git revert` creates a new commit that reverses the changes introduced by the selected commit.

### Temporarily Save Changes

```bash
git stash
git switch main
git stash pop
```

`git stash` temporarily saves tracked working-tree changes. `git stash pop` reapplies the saved changes and removes the stash entry if successfully applied.

## 11. Hands-on Exercise

### Objective

Create a GitHub repository and practice the complete development workflow.

### Tasks

1. Create a GitHub repository named `git-training`.
2. Clone the repository to your computer.
3. Create a `README.md` describing the project.
4. Commit your changes.
5. Create a branch named `feature/add-message`.
6. Add a `message.txt` file containing a welcome message.
7. Commit and push the feature branch.
8. Switch to `main`.
9. Merge the feature branch into `main`.
10. Push the updated `main` branch to GitHub.
11. Inspect the history using `git log --oneline --graph --all`.

### Challenge

Create a second branch named `feature/add-description`, update the README, commit your changes, and merge the branch into `main`.

## 12. Important Notes

- Git tracks changes locally; GitHub hosts remote repositories.
- A commit does not automatically upload changes to GitHub.
- `git add` stages changes but does not create a commit.
- `git fetch` does not automatically merge remote changes.
- Use feature branches to separate development work.
- Never commit passwords, API keys, or real environment secrets.

## Summary

In this session, students learned how to create repositories, track changes, create branches, merge features, synchronize with GitHub, and inspect project history.

These skills will be used throughout the rest of the course to manage source code and collaborate on projects.