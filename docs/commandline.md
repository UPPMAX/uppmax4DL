---
hide:
  - footer
---

# The command-line on Bianca

!!! info "Objectives"
    - We'll use the commands and investigate the Bianca environment
    - Tips and tricks for Bianca users

!!! warning

    - We assume that you have already covered the Command-line material and tested on Rackham
        - [LINUX](https://uppmax.github.io/uppmax_intro/linux.html)
        - [Basic toolkit](https://uppmax.github.io/uppmax_intro/linux_basics.html)

## Command-line intro

       
### Navigation and file management

1. `pwd`  &emsp; present directory
1. `ls`  &emsp;list content
1. `cd`  &emsp;change directory
1. `mkdir`  &emsp;make directory
1. `cp`  &emsp;copy
1. `scp`  &emsp;securely remotely copy
1. `mv`  &emsp;move
1. `rm`  &emsp;remove
1. `rmdir`  &emsp;remove empty directory

### Read files and change file properties

10. `cat`  &emsp;print content on screen
11. `head`  &emsp;print first part
12. `tail`  &emsp;print last part
13. `less`  &emsp;browse content
14. `tar`  &emsp;compress or extract file
15. `chmod`  &emsp;change file permissions
16. `man`  &emsp;info about a command

## Type along

### Navigating Bianca

- Check the path to your $HOME folder

```
$ cd ~
$ pwd
$ pwd -P
```

??? answer
    ```
    /home/$USER
    /castor/project/home/bjornc
    ```

- Check the path to your projects

```
$ cd /proj
$ ls
$ pwd
$ pwd -P
```

??? answer
    ```
    /proj
    /proj
    ```
```
$ cd /sensXXX
$ pwd
$ pwd -P
```
??? answer
    ```
    /proj/sensXXX
    /castor/project/proj
    ```

## Aliases on your desktop

1. Be logged in with ThinLinc.
2. Open a terminal.
3. Run `cd Desktop\`
4. Make shortcuts to your heart's content:
  - `PROJ=sens2023531`
  - `ln -s /proj/$PROJ/ proj`
  - `ln -s /proj/$PROJ/nobackup nobackup`
  - `ln -s /proj/$PROJ/nobackup/wharf/<yourusername>/<yourusername-$PROJ> wharf`

You can also make aliases to executables, like the convenient `interactive`-job starting script in `proj/useful_files`.

## The terminal and the GUI are friends

On a clean terminal, try typing `cd` and then dragging a folder from the GUI to the terminal.

It types the absolute path for you!

## Use `chmod` to protect important files

Most projects rely on data that should in principle never be changed. Run `chmod -R -w data/` to remove write permissions on everything inside the `data` directory. 

Note that e.g. `rm --force` can still delete files, and you can overwrite or delete data by confirming when Bash prompts (if you own the files). However, this will protect you from most programmatic mistakes, the mistakes of others, and give you an opportunity to regret a typo.

Some people use an alias for `rm` that causes it to always prompt for confirmation. I don't recommend this because it detracts from the effectiveness of write-protecting your own files.
