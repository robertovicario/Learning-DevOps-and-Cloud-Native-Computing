# Git

## Overview

Git is a distributed version control system used to track changes in source code during software development. It allows multiple developers to work on a project simultaneously, manage versions of the codebase, and collaborate efficiently.

## Repositories

A Git repository is a storage space where your project files and their revision history are kept. It can be local (on your machine) or remote (on a server).

## Branches

Branches in Git allow you to diverge from the main line of development and continue to work without affecting the main branch. They enable parallel development and are crucial for feature development, bug fixing, and experimentation.

## Operations

Common operations in Git include:

- **Clone:** Copy an existing Git repository.
- **Commit:** Record changes to the repository.
- **Push:** Upload local repository content to a remote repository.
- **Pull:** Fetch and integrate changes from a remote repository.
- **Merge:** Combine changes from different branches.
- **Rebase:** Move or combine a sequence of commits to a new base commit.
- **Checkout:** Switch between branches or restore working tree files.

## Git CLI

The Git Command Line Interface (CLI) is a powerful tool that allows you to interact with Git repositories directly from your terminal.

- **Commands:** [git-scm.com/book/en/v2/Getting-Started-The-Command-Line](https://git-scm.com/book/en/v2/Getting-Started-The-Command-Line)

## Git Objects

Git stores its data in a structure known as a Git object, which includes commits, trees, blobs, and tags. These objects are identified by unique SHA-1 hashes.

### Commits

A commit in Git is an object that represents a snapshot of your repository at a specific point in time. It includes the following information:

- **SHA-1 Hash:** A unique identifier for the commit.
- **Parent Commit(s):** Reference to the previous commit(s) in the history.
- **Author Information:** Name and email of the author.
- **Committer Information:** Name and email of the person who committed the changes (can be different from the author).
- **Commit Message:** A message describing the changes made in the commit.
- **Tree Object:** A snapshot of the working directory.

### Tags

Tags in Git are used to mark specific points in history as being important. They are commonly used to mark release points (e.g., v1.0, v2.0). There are two types of tags:

- **Lightweight Tag:** A simple pointer to a commit.
- **Annotated Tag:** A full object in the Git database that contains metadata such as the tagger name, date, and a message.
