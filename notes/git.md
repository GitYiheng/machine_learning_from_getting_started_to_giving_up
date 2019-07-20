# Git

Git helps you manage your code.

## Install Git on Ubuntu 18.04

Open a terminal window by pressing `ctrl` + `alt` + `t` simultaneously and type

```
sudo apt-get install git
```

## Setup User Information

```
git config --global user.name "<user_name>"
git config --global user.email <user_email@gmail.com>
```

## 3 Places for Code

1. Working directory (on your computer): you can edit this directly
2. Staging area (on your computer): this acts as a buffer
3. Git repository (online): code in the cloud

## Create a Local Copy of Existing Repository

Copy a git repository (online) as a working directory (on your computer):

```
git clone https://github.com/<user_name>/<repo_name>.git
```

## Add, Commmit and Push

Sync the staging area (on your computer) with the git repository (on your computer):

```
git add <filename>
```

Comment your modification:

```
git commit -m "<user_comments>"
```

Sync the Git repository (online) with the staging area (on your computer):

```
git push
```

## Pull

Sync the working directory and the staging area (in your computer) with the Git repository (online):

```
git pull
```
