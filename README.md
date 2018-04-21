# How To Use Git  (macOS)

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

## Understanding the Git Workflow
Let's learn the basics of the Git Workflow with a practical example. We will create a local repository, check its status, make some changes and then save them (commit).

### Create a New Repo (`git init`)
Let's create a new directory, and initialize it. 
```
$ mkdir space-x-project
$ cd space-x-project/
$ git init
```
`git init` will initialize our folder and create a hidden `.git` directory where the repository and configurations will be stored.

### Checking the Repo Status (`git status`)
x
