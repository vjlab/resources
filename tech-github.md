# Using Github for Project Management

### Why Github?

Github is actually for process control during the software development stage: when different developers are working on the same project, Github allows management of contributions from different developers to differents part a project, or different versions of the same code (i.e. a senior engineer will pick one). For internal lab use, the way we use it is less involved because we'll almost never have code conflicts, and there's very little chance that we'll be developing on different versions of the same project, so there's almost no need to deal with multiple forks or multiple branches. 

Other advantages are:
 - You can store all your project files online so that you can access them anywhere
 - A relatively easy collaboration platform (not having to manage conflicting content makes things a lot easier)
 - Enforced documentation standards via the `readme.md` file
 - Easily published
 - Easily synced and presented on a website via Trevor's `blotter` website template
 - If you're writing code, you can "git-save" your libraries onto Github.
 
Disadvantages
 - The learning curve is slighty steeper than, say, sharing on a Google drive. But it's still nothing that you can't learn in under an hour.

You can use the browser interface, or the command line. 

### Some Basic Commands
Version (to check if git’s successfully installed). Run this from anywhere:
```
git —-version
```

Set global config values
```
git config --global user.name "my_name"
git config --global user.email "my_email@gmail.com"
```

To see what config values you've already set:
```
git config --list
```

You'll be adding more config values over time as and when the need arises. 

For help:

```
git <verb> --help
```
e.g.
```
git config --help
```

## To Create A Repo From An Existing Folder On Your Local Machine
```
cd my_local_proj_folder
git init
```

You'll see something like:

```
> Initialized empty Git repository in /users/username/...../my_local_proj_folder.git
```

This process creates a .git file, which is actually a folder containing everything related to the repo.
To delete that .git file:
```
rm -rf git
```

Check status:
```
git status
```

Specify files to ignore:
```
touch .gitignore
```

In the gitignore file, you can have something like:
```
.DS_Store
.project
*.pyc
```

(the "*.pyc" tells `git` to ignore all files with a .pyc extension)


## Staging Area
Think of this as an intermediary area between your working directory/version. and the .git directory(repo).

working dir --(stage fix)--> staging area --(commit)--> .git repo

 - A stage fix pushes stuff from your working dir to the staging area.
 - A commit pushes stuff from the staging area to the .git dir.
 - Checking out the project pulls stuff from the .git dir to your working dir.

You can see what files are in the staging area using:
```
cd my_repo
git status
```

These will be in the section "Changes to be committed". 

To add all files to the staging area:
```
git add -A
```

Or to add individual files, e.g. a gitignore file:
```
git add .gitignore
```

To remove all files from the staging area:
```
git reset
```

## Commit
Commit all files in the staging area with -m "my_message" (m for message)
```
git commit -m "Initial commit"
```

If you run

```git status
```

This should now show "nothing to commit".

To publish:
```
git push
```

## Log
To see what you've done:
```
git log
```
