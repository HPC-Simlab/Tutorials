# Table of Contents
1. [Description](#desc)
2. [Install Git bash on Windows](#installgitwindows)
3. [Install Git on Ubuntu](#installgitubuntu)
4. [Git configuration](#gitconfig)
    1. [Global configuration](#globalconfig)
    2. [Local configuration](#localconfig)
5. [Track an existing project](#track)
6. [Git on SIMLAB](#gitonsimlab)

## Description <a name="desc"></a>
Git Bash is an application for Microsoft Windows environments which provides an emulation layer for a Git command line
experience.

## Install Git bash on Windows <a name="installgitwindows"></a>

To install **git bash** on windows

1. Download  from https://git-scm.com/download/win
2. Double click the downloaded file.
3. Proceed with the installation.

## Install Git on Ubuntu <a name="installgitubuntu"></a>

```sh
sudo apt-get install git
```

## Git configuration <a name="gitconfig"></a>

### Global configuration: <a name="globalconfig"></a>


```sh
git config --global user.name "FIRST_NAME LAST_NAME"
git config --global user.email "NAME@example.com"
```

### Local configuration: <a name="localconfig"></a>


```bash
git config user.name "FIRST_NAME LAST_NAME"
git config user.email "NAME@example.com"
```

*Note that you can use git config for futher customization*

## Track an existing project <a name="track"></a>

- To start tracking an existing project use the following commands


```bash
cd yourproject
git init .
git add *
git commit -m "commit message"
```

- To make it vailable in github, create a new repository in github then run

```bash
git remote add origin https://github.com/username/new_repo
git push
```

## Git on SIMLAB <a name="gitonsimlab"></a>

To setup your environment for working with git please follow these steps in a simlab machine:

- List available versions:
```sh
$ module avail git
---------------------------- /cm/shared/modulefiles ----------------------------
git/2.23.0-GCCcore-9.3.0-nodocs  
```
- Load git (version 2.23.0):
```sh
module load git/2.23.0-GCCcore-9.3.0-nodocs
```
- List modules loaded with git:
```sh
$ module list
Currently Loaded Modulefiles:
1) GCCcore/9.3.0                  7) ncurses/6.2-GCCcore-9.3.0        
2) zlib/1.2.11-GCCcore-9.3.0      8) gettext/0.20.1-GCCcore-9.3.0     
3) cURL/7.69.1-GCCcore-9.3.0      9) libreadline/8.0-GCCcore-9.3.0    
4) expat/2.2.9-GCCcore-9.3.0     10) DB/18.1.32-GCCcore-9.3.0         
5) XZ/5.2.5-GCCcore-9.3.0        11) Perl/5.30.2-GCCcore-9.3.0        
6) libxml2/2.9.10-GCCcore-9.3.0  12) git/2.23.0-GCCcore-9.3.0-nodocs
```
