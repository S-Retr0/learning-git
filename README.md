# How To Use Git

This is a simple guide I'm creating while I'm trying to learn Git since I'm new to it.
I'm just looking and adding content from different books, blogs and docs and trying to write something that will help me out to become familiar with Git.

## What is Git?

Git a collection of command line utilities that track and record changes in file (most often source code, but you track anything you wish). With Git you can restore old version of your project, compare, analyse, merge changes and more. This process is referred to as VERSION CONTROL.

Git is decentralized, which means that it doesn't depend on a central server to keep old versions of your files. Instead it works fully locally by storing this data as a folder on your hard drive, which we call a REPOSITORY. However you can store a copy of your repository online, which makes it easy for multiple people to collaborate and work on the same code. This is what websites like "Github" and "BitBucket" are used for.

## How to install and configure Git

On macOS we first need to install [Homebrew](https://brew.sh/ "Homebrew"), which is a package managaer for macOS.
Copy and paste the following line in the terminal:
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
Follow the instructions and once you have successfully installed homebrew, you're ready to install Git:
``` 
$ brew install git
```

### How to add autocomplete
If you try autocompletion with the tab you'll see that it doesn't work with Git. Let's fix it!
First we must install `bash-complition`
```
$ brew install bash-complition
```
Now we add it to `~/.bash_profile` and refresh the terminal:
We will use `cat` to append some lines at the end of `~/.bash_profile` (you can nano or any text editor)
```
$ cat >> ~/.bash_profile
```
Now copy and paste the following lines:
```
if [ -f $(brew --prefix)/etc/bash_completion ]; then
  . $(brew --prefix)/etc/bash_completion
fi
```
Use `ctrl+c` to end the `cat` command, then refresh the terminal:
```
$ source ~/.bash_profile
```
Done. Now you have autocomplition for git. Let's test it.
Type `git`, hit the spacebar then tab and you will get the list of all the available commands git offers.
```
$ git
add                  format-patch         repack
am                   fsck                 replace
annotate             gc                   request-pull
apply                get-tar-commit-id    reset
archive              grep                 revert
bisect               gui                  rm
blame                help                 send-email
branch               init                 shortlog
bundle               instaweb             show
checkout             interpret-trailers   show-branch
cherry               log                  stage
cherry-pick          merge                stash
citool               mergetool            status
clean                mv                   submodule
clone                name-rev             subtree
commit               notes                svn
config               p4                   tag
describe             pull                 verify-commit
diff                 push                 whatchanged
difftool             rebase               worktree
fetch                reflog
filter-branch        remote
```

### How to Configure Git
Let's finish setting Git by adding a username and email. We use the `--global` setting which allows these configurations to be applied to any other repository that we work on locally.
```
$ git config --global user.name "Username"
$ git config --global user.email email@example.com
```
To check all the configuartion settings for the repository you're in, type:
```
$ git config --list
```
If you want to edit any of your configuration settings, you can do so by editing the `~/.gitconfig` file.

### Making Atom the Deafult Text Editor for Git
By default, Git uses VIM, which is... well, I don't like it at all. I prefer nano while using the terminal or [atom.io](https://atom.io/ "Atom.io") for every day use.
So I'm going to make atom my default text editor, feel free to keep Vim or use whatever text editor you're confortable with.
```
$ git config --global core.editor "atom --wait"
```

## Understanding the Git Workflow
Let's learn the basics of the Git Workflow with a practical example. We will create a local repository, check its status, make some changes and then save them (commit).

### Create a New Repo (git init)
Let's create a new directory, and initialize it. 
```
$ mkdir space-x-project
$ cd space-x-project/
$ git init
```
`git init` will initialize our folder and create a hidden `.git` directory where the repository and configurations will be stored.

### Checking the Repo Status (git status)
Running `git status` will return information about the current state of our repo, like if we have new files, new changes made, if everything is up to date, which is the current branch and much more.
```
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```
As we can see our repo is empty, let's create a file and check it again:
```
$ touch README.md
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.md

nothing added to commit but untracked files present (use "git add" to track)
```
Now `git status` tells us that we have an untracked file (`README.md`).

### Staging (git add)
Git has the concept of a "staging area". You can think of this like a blank canvas, which holds the changes which you would like to commit. It starts out empty, but you can add files to it (or even single lines and parts of files) with the `git add` command, and finally **COMMIT** everything **(CREATE A SNAPSHOT)** with `git commit`.

We have different methods to add files:
* We can add a single file `git add <file>`:
   ```
   $ git add README.md
   ```
* Multiple files `git add <file1> <file2> <file3>`

* We can add all tracked files with `-u`option
   ```
   $ git add -u
   ```
* Or we can add everything with the `-A` option. (It's a good habit to only add the files you need, don't abuse `-A`)
   ```
   $ git add -A
   ```
To learn more about the `add` command run:
```
$ git add --help
```
Now our files are ready to be commited. Running again `git status` will tell us that we have a new file ready to be committed.

#### Whas is `.gitignore`?
Git only tracks the files you ask it to, but you might ask it to track some files by mistake (if you use `git add .` for example, it will track all the files in the current direcory).
Sometimes you want Git to not track some particular files, so you need to hide them from it, here is where the `.gitignore` file comes to your help, which is a file added to the root directory of the repository, and it lists files you don't want Git to track or display as part of `git status`. Let's add one to make some practice:
1. Create a file called `.gitignore`
   ```
   $ touch .gitignore
   ```
2. Use an editor and write down the files/folder you don't want Git to track
   ```
   $ cat >> .gitignore
   secret_idea.txt
   secret_folder/
   *.log
   ```
3. Now stage the `.gitignore` file
   ```
   $ git add .gitignore

### Commiting (git commit)
A commit represents the state of our repository at a given point in time. It's like snapashot, which we can go back to see how things were when we took it. To create a new commit we need to have at least one change added to the staging area and run the following:
```
$ git commit -m "First Commit"
```
The `-m`option specifies that you are going to add a message within the command. Otherwise you can just type `git commit`, which will open up a text editor (in our case Atom since we set it as the default one) and ask you to enter a commit message.

### See changes made to tracked files (git diff)
The `diff` command shows the changes that have been made to the tracked files in the repository since the last commit.
Our `README.md` file is empty for now, add some text to it and use `git diff` to check what changed, for example I added some stupid lines and here is the output:
```
$ git diff
diff --git a/README.md b/README.md
index 8b13789..eb2665f 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,4 @@

+Adding some text.
+Adding more text.
+Aye. Chocolate Rain...
```
We can see that we have 3 new lines, the `+` (green) indicates it's been added while `-` (red) it's been removed, but since our file was empty we don't have any red `-`.
Go ahead, stage and commit the changes.

### Commit History (git log)
To view the history of a project, we use the `git log` command, you should get something like this:
```
commit 82ee81ef3e6129033e4e1a5d1234516a305e6ff
Author: S-Retr0 <retr0@mail.com>
Date:   Sat Apr 21 18:30:02 2018 +0200

    Updated README

commit d266a610418dff012345c3e4bc9d1abad8dd4096
Author: S-Retr0 <retr0@mail.com>
Date:   Sat Apr 21 18:27:52 2018 +0200

    Added problems.txt
```
Each commit has a unique hash, author, timestamp and commit message.

## Remote Repository

For now our repository is local, but we may need to share it with someone for collaboration.
We will copy our repo in a centralized server, in this case GitHub (this new copy is called a **remote**).

### Connect to a Remote Repository (git remote add)
(*In order to upload something to GitHub you must have an account, and create your repo on it. I assume you already did this two things, so let's keep going.*)

We first have to establish a connection to the repository we created on GitHub.
```
$ git remote add origin https://github.com/user-name/repository-name.git
```
A project may have many remote repositories at the same time. To be able to tell them apart we give them different names. Traditionally the main remote repository in git is called `origin`.

### Uploading to a Server (git push)
Our remote repository should be empty now, while our local repo has the `README.md` file, so let's transfer out local commits to the server. This process is called **PUSH**.
```
$ git push -u origin master
```
The `git push` command takes two parameters:
1. The name of the repository, in our case it's called `origin`;
2. The name of the branch to push to, `master`is the default branch for every repo.

The `-u` option stands for “upstream”. It links your repository to an upstream repository for future reference. When you add commits later, Git will show the status of your local copy in relation to the upstream repository.

### Cloning a Repository (git clone)
Now that your repository is online, people can see its content and clone it to their local computer.

Say for example a friend of yours need to have a copy of your repo (so he can help with the project), all he needs to do is:
```
$ git clone https://github.com/your-username/project-name.git
```
And just like that a new local repository is automatically created in his computer, with the github version configured as a remote.

### Getting Updates from the Server (git pull)
If you make updates to your repository, your friend can get updates by first downloading the new changes `git fetch`, then merging it to the appropriate branch `git merge`. An alternative is to use `pull`, which is runs the fetch followed by a merge.
```
$ git pull origin master
```

## Branching

When developing a new feature, it is considered a good practice to do it on a copy of the original project, called a **BRANCH**. Branches have their own history and isolate their changes from one another, until you decide to **MERGE** them back together.
This is done for a couple of reasons:
- An already working, stable version of the code won't be broken;
- Many features can be safely developed at once by different people;
- Developers can work work on their own branch, without the risk of their codebase changing due to someone else's work;
- When unsure what's best, multiple versions of the same feature can be developed on separate branches and then compared.

### Creating a New Branch (git branch)
For now, we only have one branch, which is the default called `master`. Let's check if it's true
```
$ git branch
* master
```
If we use the `-a` option we can check the remote branches too
```
$ git branch -a
* master
  remotes/origin/master
```
Let's add a new branch to work on and call it `test_branch`
```
$ git branch test_branch
```
