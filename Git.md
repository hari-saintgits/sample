# Welcome, Everyone!
Git & GitHub Essentials

## Today, We'll cover
- What's Git and Github
- How to setup `git`
- How to push to our first repo

---

# Git
`git` is a *version control system* that helps you track changes in your code over time. Think of it as a digital notebook where you can save and revisit different versions of your work.

# Github
GitHub is a web-based platform that provides hosting for Git repositories. It's a popular place for developers to share their code, collaborate on projects, and discover open-source software.

---

# Getting Started
1. Navigating GitHub
- Create an account
- Create a repository

2. Installing `git`
- Windows
    `winget install --id Git.Git -e --source winget`
    `winget install -e --id GitHub.cli`
- Linux
    `sudo apt install git gh`
- Mac
    `brew install git gh`

---

# Setting up `git`
1. Setup your `username`

`git config --global user.name "yourusername"`

2. Setup your `email`

`git config --global user.email "youremail"`

---

# `git` Commands

1. Tell git to track all the files
`git add .`

2. Save a snapshot (commit) of current change, with message
`git commit -m "updated something"`

3. Push local changes to GitHub
`git push`

4. Pull changes from GitHub
`git pull`

