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
| -1 |  | List one item per line different from -l |


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

17. `less` is replacement for `more`. `less` falls into the class of program called pagers, it allows easy viewing of long text file in page-by-page manner. Whereas `more` only allowed forward page, `less` allows forward as well as backward page.

18. If you are using a mouse, you can double-click a filename to copy it and middle-click to paste it into commands.

19. If we accidentally attempt to view a non-text file and it scrambles the terminal window, we can recover by entering the `reset` command.

20. Directories found on linux systems
| Directory | Comments |
|-----------|----------|
| `/` | Root directory, everything begins here  |
| `/bin` | Contains binaries that must be present for the system to boot & run |
| `/boot` | Contains linux kernel, initial RAM disk image(for drivers needed at boot time) and boot loader. */boot/grub/grub.conf*, or *menu.lst* used to configure boot loader, */boot/vmlinuz*, linux kernel |
| `/dev` | This is a special directory that contains device nodes. *“Everything is a file”* also applies to devices. Here is where the kernel maintains a list of all the devices it understands. |
| `/etc` | The */etc* directory contains all the system-wide configuration files. It also contains a collection of shell scripts that start each of the system services at boot time. Everything in this directory should be readable text. While everything in */etc* is interesting, here are some all-time favorites: */etc/crontab*, a file that defines when automated jobs will run; */etc/fstab*, a table of storage devices and their associated mount points; and */etc/passwd*, a list of the user accounts. |
| `/home` | In normal configurations, each user is given a directory in */home*. Ordinary users can write files only in their home directories. This limitation protects the system from errant user activity. |
| `/lib` | Contains shared library files used by the core system programs. These are similar to dynamic link libraries (DLLs) in Windows.|
| `/lost+found` | Each formatted partition or device using a Linux file system, such as ext3, will have this directory. It is used in the case of a partial recovery from a file system corruption event. Unless something really bad has happened to your system, this directory will remain empty. |
| `/media` | On modern Linux systems, the */media* directory will contain the mount points for removable media such as USB drives, CD-ROMs, and so on, that are mounted automatically at insertion. |
| `/mnt` | On older Linux systems, the */mnt* directory contains mount points for removable devices that have been mounted manually.|
| `/opt` | The */opt* directory is used to install “optional” software. This is mainly used to hold commercial software products that might be installed on the system. |
| `/proc` | The */proc* directory is special. It’s not a real file system in the sense of files stored on your hard drive. Rather, it is a virtual file system maintained by the Linux kernel. The *“files”* it contains are peepholes into the kernel itself. The files are readable and will give you a picture of how the kernel sees your computer. |
| `/root` | This is the home directory for the root account. |
| `/sbin` | This directory contains *“system”* binaries. These are programs that perform vital system tasks that are generally reserved for the superuser. |
| `/tmp` | The */tmp* directory is intended for the storage of temporary, transient files created by various programs. Some configurations cause this directory to be emptied each time the system is rebooted. |
| `/usr` | The */usr* directory tree is likely the largest one on a Linux system. It contains all the programs and support files used by regular users.|
| `/usr/bin` | */usr/bin* contains the executable programs installed by your Linux distribution. It is not uncommon for this directory to hold thousands of programs. |
| `/usr/lib` | The shared libraries for the programs in */usr/bin*. |
| `/usr/local` | The */usr/local* tree is where programs that are not included with your distribution but are intended for system-wide use are installed. Programs compiled from source code are normally installed in */usr/local/bin*. On a newly installed Linux system, this tree exists, but it will be empty until the system administrator puts something in it. |
| `/usr/sbin` | Contains more system administration programs. |
| `/usr/share` | */usr/share* contains all the shared data used by programs in */usr/bin*. This includes things such as default configuration files, icons, screen backgrounds, sound files, and so on. |
| `/usr/share/doc` | Most packages installed on the system will include some kind of documentation. In */usr/share/doc*, we will find documentation files organized by package. |
| `/var` | With the exception of */tmp* and */home*, the directories we have looked at so far remain relatively static; that is, their contents don’t change. The */var* directory tree is where data that is likely to change is stored. Various databases, spool files, user mail, and so forth, are located here. |
| `/var/log` | */var/log* contains log files, records of various system activity. These are important and should be monitored from time to time. The most useful ones are */var/log/messages* and */var/log/syslog*. Note that for security reasons on some systems, you must be the superuser to view log files. |

{{< youtube bbmWOjuFmgA >}}

21. Symbolic Links are used to refer to a file. It is also called *sym links* or *softlink*.
```bash
lrwxrwxrwx 1 root root 11 2018-08-11 07:34 libc.so.6 -> libc-2.6.so
```
When `ls -l` is used, symbolic links are denonted by first-letter `l`. One usecase of symbolic links are that if you want to refer one file with multiple names. For Example, suppose we have binary `python-3.12` then we can create a symlink named `python` & use that in our script. If we want to update python version to `python-3.18` we can simply update the symlink instead of updating name in each & every script.

22. Just like softlinks there is hard links, they vary from softlink because they use the same inode of the file, whereas softlink uses different inode than original file. In most cases softlink should be used.

23. Softlinks are created using `ln -s` command.
```bash
user@hostname:~$ ln -s /path/to/original/file /path/to/softlink
```
Always use absolute pathnames for original files while creating links. Symlinks can be copied from one drive to another unlike hardlinks due to inode. If `-s` is removed in above command it will create hardlink.
```bash
user@hostname:~$ ln /path/to/original/file /path/to/softlink
```

24. If original file is deleted the softlink stops working, it throws error "No such file or directory. Whereas hardlink will still work & show the content of original file. Hardlinks are dependent on indone & each drive has it own inode numbers due to this reason copying hardlinks to different drives can cause issues while softlinks work just fine.

25. In Linux there are many important files that are plain human-readable text. Unlike many proprietary systems, Linux makes everything available for examination and study.



## Chapter 4 - Manipulating files & directories

1. Five most used commands:-
    - `cp` copy files & directories
    - `mv` move or rename files & directories
    - `mkdir` create directories
    - `rm` remove files & directories
    - `ln` create hard & symbolic links

2. Using special characters help in specifying filenames. These characters called *wildcards*. Using wildcards(a.k.a. *globbing*) allows you to select filenames based on characters.

| Wildcard | Meaning |
|:---------|:--------|
| `*` | Matches any characters |
| `?` | Matches any single character |
| `[characters]` | Matches any character that is a member of the set *characters* |
| `[!characters]` | Matches any character that is not a member of the set *characters* |
| `[[:class:]]` | Matches any character that is a member of the specified *class* |

3. Commonly used character class
| Character Class | Meaning |
|:----------------|:--------|
| `[:alnum:]` | Matches any alphanumeric characters |
| `[:alpha:]` | Matches any alphabetic character |
| `[:digit:]` | Matches any numeral |
| `[:lower:]` | Matches any lowercase letter |
| `[:upper:]` | Matches any uppercase letter |

4. *Wildcards* can used to select some complex filenames.
Examples:-

| Pattern | Matches |
|:--------|:--------|
| `*` | All files |
| `g*` | Any file beginning with *g* |
| `b*.txt` | Any file beginning with *b* followed by any characters and ending with *.txt* |
| `Data???` | Any file beginning with Data followed by exactly three characters |
| `[abc]*` | Any file beginning with either an *a, a b,* or *a c* |
| `BACKUP.[0-9][0-9][0-9]` | Any file beginning with *BACKUP*. followed by exactly three numerals |
| `[[:upper:]]*` | Any file beginning with an uppercase letter |
| `[![:digit:]]*` | Any file not beginning with a numeral |
| `*[[:lower:]123]` | Any file ending with a lowercase letter or the numerals 1, 2, or 3 |

5. Wildcards work in GUI too. App like *nautilus* in gnome or *Dolphin* in KDE supports wildcards.

6. [A-Z] or [a-z] character ranges don't work as expected sometimes in linux. Hence, it's adviced to use character class instead.

7. `mkdir directory...` command is used to create directories.
```bash
user@hostname:~$ mkdir dir1
user@hostname:~$ mkdir dir2 dir3 dir4
```

8. `cp items dest` copies files or directories to destination(file or directory)
```bash
user@hostname:~$ cp item1 item2
user@hostname:~$ cp item2 item3 item4 directory
```