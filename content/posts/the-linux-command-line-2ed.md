---
title: 'The Linux Command Line 2ed'
date: 2024-08-01T19:37:59+05:30
tags: ["linux", "bash", "The Linux Command Line", "William E. Shott"]
draft: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
draft: false
---

## Chapter 1 - What is shell?

1. Shell is program which takes input from keyboard & passes them to OS. There are various types of shell like *bash*, *sh*, *zsh* etc.

2. Terminal Emulators are which helps to interact with shells like konsole from KDE, gnome-terminal from GNOME etc.

```bash
user@hostname:~$ 
```
3. 👆 This is *shell prompt*. Appears when shell is ready to accept input. (#) represent running shell as superuser, ($) represent normal user. Usually is *username@hostname* followed by current directory. It can be changed via editing *PS1* variable in *~/.bashrc*.

4. By default last 1,000 commands are saved by the linux distribution. `HISTFILESIZE` & `HISTSIZE` can be used to change the limit in *~/.bashrc* file.

5. Up & Down arrow keys are used to iterate between last commands. Left & Right arrow keys are used to move cursor left or right to edit command.

6. `CTRL+C` & `CTRL+V` is used to perform **not** used to perform copy & paste. Insteas
selecting text with left mouse button copies the text & pressing middle button pastes the text at cursor location.

7. Linux GDE(graphical desktop environment) follows “focus follows mouse” instead of “click to focus” like in windows. Still have to click to bring window to foreground but it will receive input.

```sh
user@hostname:~$ date
Thu Aug  1 08:25:09 PM UTC 2024
```
8. `date`  shows current date & time.

```bash
user@hostname:~$ cal
    August 2024
Su Mo Tu We Th Fr Sa
             1  2  3
 4  5  6  7  8  9 10
11 12 13 14 15 16 17
18 19 20 21 22 23 24
25 26 27 28 29 30 31

```bash
9. `cal` shows the calendar for current month. Ensure *ncal* package is installed.

10. We can access virtual consoles using `CTRL-ALT-F1` to `CTRL-ALT-F6`.

```bash
user@hostname:~$ df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.1M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv   12G  6.3G  4.4G  60% /
tmpfs                              984M     0  984M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          2.0G  182M  1.7G  10% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000
```
11. `df -h` shows current free space on drives. *-h* make shows data in human redable format.

```bash
user@hostname:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       388Mi       1.2Gi       1.1Mi       530Mi       1.5Gi
Swap:          2.3Gi          0B       2.3Gi
```
12. `free -h` shows free memory.

```bash
user@hostname:~$ exit
```
13. `exit` ends the current terminal session, similar to `CTRL-D` or directly closing the window.

## Chapter 2 - Navigation

1. Three following commands is mainly used for navigation:-
    - `pwd` prints current directory
    - `ls` lists items in directory
    - `cd` changes directory

2. Linux organizes its files in *hierarchial directory structure*. The first directory is called *root directory*.

3. Unlike Windows, which has a seperate file system tree for each storage device, Linux have a single file system tree, regardless how many drives are attached. Drives are mounted at various points on the tree.

4. Imagine that the file system is a maze shaped like an upside-down tree and we are able to stand in the middle of it. At any given time, we are inside a single directory, and we can see the files contained in the directory and the pathway to the directory above us (called the parent directory) and any subdirectories below us. The directory we are standing in is called the current working directory. To display the current working directory, we use the pwd (print working directory) command.
```bash
user@hostname:~$ pwd
/home/user
```

5. Whenever user logs in for first time the terminal opens into *home directory* of the user.

6. Each user account is given its own home directory, and it is the only place a regular user is allowed to write files.

7. `ls` command is used to list the items in any directory. If directory is not provided then it list item in current directory.
```bash
user@hostname:~$ ls
Desktop Documents Music Pictures Public Templates Videos
```

8. To change working directory use `cd` command followed by the path of the directory. Pathname can be defined in 2 ways: *absolute pathname* & *relative pathname*

9. Absolute pathnames begins with the root directory and follows the tree branch by branch until the desired directory or file is reached.

10. For Example, */usr/bin* means that root contains a directory *usr* which contains a directory *bin*. The initial */* represents the root path.
```bash
[me@linuxbox ~]$ cd /usr/bin
[me@linuxbox bin]$ pwd
/usr/bin
[me@linuxbox bin]$ ls
...Listing of many, many files ...
```

11. Absolute pathname always starts from root directory but relative pathname start from current directory.

12. Relative pathname uses special notation such as .(dot) for current directory & ..(dot dot) for parent directory is used.

13. For Example, *./page1/css* means current directory contains *page1* directory which contains *css*. *./* from the starting of the pathname can be removed and it will still work in same way.

14. *../router/contact* means that the parent directory contains *router* directory which contains *contact* directory.

15. Filenames or directory starting from period character is hidden by default. To list them use `ls -a`.

16. Filenames & commands are case-sensitive meaning *file1* & *File1* are 2 different files.

17. Linux supports long filenames with punctuation characters, limit punctuation character to period, dash & underscore. Do not use space in names instead use underscore.

18. Linux has no concept of file extension. Though many software use extensions in their filenames.

19. Shortcuts to change current working directory
    - `cd` changes working directory to home directory
    - `cd -` changes working directory to previous working directory
    - `cd ~user_name` changes working directory to home directory of *user_name*



## Chapter 3 - Exploring the System

1. Commands used in this chapter:
    - `ls` list directory contents
    - `file` Determine file type
    - `less` View file content

2. To print items in current working directory we can simply use `ls`
```bash
[me@linuxbox ~]$ ls
Desktop Documents Music Pictures Public Templates Videos
```

3. To list items in different directory we can provide pathname as arguments to `ls`
```bash
[me@linuxbox ~]$ ls /usr
bin games include lib local sbin share src
```

4. `~` symbolizes home directory of current user.

5. We can even list multiple directories at once.
```bash
[me@linuxbox ~]$ ls ~ /usr
/home/me:
Desktop Documents Music Pictures Public Templates Videos
/usr:
bin games include lib local sbin share src
```

6. We can add `-l` to command to change output format to long format.
```bash
[me@linuxbox ~]$ ls -l
total 56
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Desktop
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Documents
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Music
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Pictures
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Public
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Templates
drwxrwxr-x 2 me me 4096 2017-10-26 17:20 Videos
```

7. Commands are often followed by one or more options that modify their behavior and, further, by one or more arguments, the items upon which the command acts. 
```bash
command -options arguments
```

8. Many commands, however, including those from the GNU Project, also support long options, consisting of a word preceded by two dashes. Also, many commands allow multiple short options to be strung together. In the following example, the ls command is given two options, which are the `l` option to produce long format output, and the `t` option to sort the result by the file’s modification time.
```bash
[me@linuxbox ~]$ ls -lt
```

9. `--reverse` reverses the order of the sort.
```bash
[me@linuxbox ~]$ ls -lt --reverse
```

10. Common options for `ls` command
| Option | Long Option | Description |
|:---:|---|---|
| -a | --all | List all files, even those which begins with period(normally hidden). |
| -A | --almost-all | Like -a but doesn't list .(current dir) & ..(parent dir) |
| -d | --directory | Normally ls will list contents of directory, this will only list the directory use with -l to see details about the directory |
| -F | --classify | Appends indicator character at the end of the items e.g. (/) slash at end of directories |
| -h | --human-readable | In long listing, displays file size in human redable format rather than byte |
| -l |  | Display result in long format |
| -r | --reverse | Display result in reverse order. Normally displays in ascending alphabetical order. |
| -S |  | Sort result by file size |
| -t |  | Sort by modification time |


11. Explaining the output of long format
```bash
-rw-r--r-- 1 root root 32059 2017-04-03 11:05 oo-cd-cover.odf
-rw-r--r-- 1 root root 27837 2017-04-03 11:05 oo-maxwell.odt
-rw-r--r-- 1 root root 98816 2017-04-03 11:05 oo-trig.xls
-rw-r--r-- 1 root root 453764 2017-04-03 11:05 oo-welcome.odt
-rw-r--r-- 1 root root 358374 2017-04-03 11:05 ubuntu Sax.ogg
```
| Field | Meaning |
|-------|---------|
|-rw-r--r--| Access right to file. First character indicates file type, `-` for file & `d` for directory. Next 3 are right for file owner, then next 3 for group & last 3 for others. |
| 1 | File's number of hard links |
| root | username of file owner |
| root | name of the group that owns the file |
| 32059 | Size of file in bytes |
| 2017-04-03 11:05 | date & time for last modification |
| oo-cd-cover.odf | name of the file |

12. `file filename` commands is used to determine the type of file. In Linux it is not necessary for file to have an extension.
```bash
user@hostname:~$ file picture.jpg
picture.jpg: JPEG image data, JFIF standard 1.01
```

13. In Linux one of the common idea is  *everything is a file*.

14. Linux contains lot of text files. They are different from MS Word or Libre Writer files. These text files only contains only text like ASCII. They are mainly used for configuration, scripts & logs.

15. `less filename` is used to view the these text files.
```bash
user@hostname:~$ less /etc/passwd
```

16. Commands to navigate `less`
| Command | Action |
|---------|--------|
| Page Up or b | Scroll back one page |
| Page Down or space | Scroll down one page |
| Up Arrow | Scroll back one line |
| Down Arrow | Scroll Down one line |
| G | Move to the end of file |
| 1G or g | Move to the start of file |
| /characters | Find next occurence of characters |
| n | Search next occurence of previous search |
| h | Display help screen |
| q | Quit less |