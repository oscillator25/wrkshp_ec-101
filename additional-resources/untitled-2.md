---
description: >-
  What follows is a list of Unix commands that every user should be familiar
  with.
---

# Fundamental Unix Commands

### man

"man" displays the manual for any command. If you are not sure how to use a given command or are curious as to what else it might be able to do, just type "man COMMAND". When viewing man pages, you can page forward by pressing the spacebar and Enter. Jumping to a specific page is possible by typing the page number and Enter. It's also possible to search an opened man page by typing a forward slash "/" followed by a regular expression and pressing Enter. Type the Q key and Enter to quit and return to the command prompt.

Run the following command:

`man man`

### ls

"ls" lists the contents of the current directory. Since you are in your home directory, running ls now will show you every file and sub-directory contained there.

Run the following command:

`ls -l`

"ls -l" and "ls -la" are important variations of ls; try running them and see if you can tell what the difference is. Confirm your hypothesis by checking "man ls".

### cat

"cat" concatenates a list of files and prints their contents to the shell. Very often cat is used to quickly display the contents of a single file.

Run the following command:

`cat .sh_history`

### more

"more" is used to browse the contents of a file. While cat is useful to view short files, it doesn't work well with long files. more to the rescue! The navigation inside more is very much like that of man, so you can use the same navigation tricks you just learned about for moving around inside the file. Use more to view the .sh\_history file now.

Run the following command:

`more .sh_history`

### cp

"cp" is used to copy a file or directory from one location to another.

`man cp`

### echo

"echo" displays a given line of text. This is useful for prompting users for input or for displaying the contents of environment variables. For example, there is an environment variable named $USER that contains your user ID. Let's have Unix say hello to you.

Run the command:

`echo Hello $USER`

Note that $USER is in all CAPS.

## Relative vs. Absolute Paths <a id="partone_unix_paths"></a>

Every location or node in the Unix file system can be indicated by a path. For example, the path to your home directory is "/z/z99999", where Z99999 is your user ID. This is called an absolute path because it describes a path that begins at "/", or the file system root directory. The path then goes into the z directory, inside which the z99999 directory is found. Note that your user ID in USS is all lowercase, including your home directory name.

Another way to describe locations in Unix is with a relative path. At any given time, there is always a "current working directory". A single period "." is a shorthand way to indicate the current working directory and two periods ".." describes the parent directory. If you ever wish to refer to a file or directory inside your current working directory, you can prefix the path with "./" \(dot-slash\). Likewise, if you wish to reference a file in the parent directory you would prefix the path with "../" \(dot-dot-slash\). Using relative paths enable you to traverse the file system quickly without having to always express the full path.

Note: The absolute path to the current working directory can always be known by checking the $PWD environment variable, or by running the pwd command.

## File Permissions and the $PATH Variable <a id="partone_unix_permissions"></a>

Time for another new command:

### which

"which" will report the absolute path to any executable file that the shell can find.

Run the following commands:

  
 `which java`

How does the shell know where to search for executable files? Introducing the $PATH. The $PATH variable contains a colon-separated list of paths to various directories in the file system that contain executable files. Take a look at the contents of the $PATH variable now.

`echo $PATH`

Whenever you enter a command, Unix searches each one of the directories in the $PATH list, in order, until it finds the command or reaches the end of the list. If a command exists in more than one PATH directory, the first directory in the list is used.

Let's take a moment to discuss how Unix file permissions work.

Each file and directory in Unix has three user-based permission groups:

* owner: The owner permissions apply only to the single user that owns the file.
* group: The group permissions apply to all users in the group that owns the file.
* others: The other permissions apply to everyone else on the system.

There are three types of permissions:

* r = Read: Permission to view the contents of a file
* w = Write: Permission to alter the contents of a file
* x = eXecute: Permission to run a file

Each of these three groups can have any combination of the three types of permissions. The command ls -l will display the file permissions for all files and directories in the current directory, along with the owning user and group.

For example:

```text
-rw-r--r--.  1 Z99999  GROUP1      270 Aug  1 20:50 .sh_history
  ^  ^  ^
  |  |  |__: Other
  |  |_____: Group
  |________: Owner
```

Here, the Z99999 is the owner, and GROUP1 is the group. Z99999 has permission to read and write the file, but the group and other access is limited to read-only.

