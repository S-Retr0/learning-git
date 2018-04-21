# How To Use Git  (macOS)

This is a simple guide I'm creating while I'm trying to learn Git since I'm new to it.
I'm just looking and adding content from different books, blogs and docs and trying to write something that will help me out to become familiar with Git.

### What is Git?

Git a collection of command line utilities that track and record changes in file (most often source code, but you track anything you wish). With Git you can restore old version of your project, compare, analyse, merge changes and more. This process is referred to as VERSION CONTROL.

Git is decentralized, which means that it doesn't depend on a central server to keep old versions of your files. Instead it works fully locally by storing this data as a folder on your hard drive, which we call a REPOSITORY. However you can store a copy of your repository online, which makes it easy for multiple people to collaborate and work on the same code. This is what websites like "Github" and "BitBucket" are used for.

### How to install Git and configure it

On macOS we first need to install [Homebrew](https://brew.sh/ "Homebrew"), which is a package managaer for macOS.
Copy and paste the following line in the terminal:
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
Follow the instructions and once you have successfully installed homebrew, you're ready to install Git:
``` 
$ brew install git
```
If you try autocompletion with the tab you'll see that it doesn't work with Git. Let's fix it!
First we must install `bash-complition`
`$ brew install bash-complition`
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
Use `ctrl+c` to end the `cat` command
