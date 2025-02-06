# Linux Basics
## Directory Hierarchy
- ```/``` - root directory, top level of file system
- ```/home``` - user home directory
- ```/bin``` - essential binary executables
- ```/sbin``` - system administration binaries
- ```/etc``` - configuration files
- ```/var``` - variable data (logs, spool files)
- ```/usr``` - user programs and data
- ```/lib``` - shared libraries
- ```/tmp``` - temporary files

## Vim
- [Learn Vim - iggredible](https://github.com/iggredible/Learn-Vim?tab=readme-ov-file)

## Environment Variables
- Dynamic named values that can affect the behavior of runnning processes in a shell
- Exist in every shell session
- ```evn``` will list all the environment variables in a shell session
- Need to print a specific environment variable? ```echo $PATH``` will show the PATH variable

## Redirects
- Linux is multi-user and multi-tasking. Every process has 3 streams opened:
  - stdin - where the process reads its input from (keyboard)
  - stdout - where the process writes its output to (terminal)
  - stderr - if errors happen, they get sent here (terminal)
- Redirection in Linux allows the user to send the output of a file to another program or file
- ```echo "hello, world!" > helloworld.txt``` will write "hello, world!" to a file called helloworld.txt

## File Permissions
- Rights and privileges are assigned to files and directories in the form of _permissions_
  - Tells us who can read, write, or run them
  - 3 types of users: owners, groups, and others

![permissions cheatsheet](https://github.com/user-attachments/assets/b7a951b3-e2e8-49eb-af8a-3432302f02d6)

## Archiving
- Main tools = ```tar```, ```gzip```, ```bzip2```
- ```tar``` manage / organize files into one archive
- ```gzip``` and ```bzip2``` used for file compression (reduce file size)
```
# To create a tar archive:
tar cvf archive_name.tar directory_to_archive/

# To extract a tar archive:
tar xvf archive_name.tar

# To create a gzip compressed tar archive:
tar cvzf archive_name.tar.gz directory_to_archive/

#To create a bzip2 compressed tar archive:
tar cvjf archive_name.tar.bz2 directory_to_archive/
```
- In Linux, **archiving and compression are separate processes**.

## Copying / Renaming
- ```cp /path/to/file /path/to/copy/it/to``` to copy a file
- ```mv /path/to/file /path/to/new/file``` to move a file
- You can use ```mv``` to rename a file in the same directory

## Soft and Hard Links
- Hard link is a mirror reflection of a file
  - Shares same file data and inode number
  - Displays a different name
  - If the original file is deleted, **the hard link still retains the file data**
- Soft (symbolic) is kind of like a shortcut
  - It has a different inode number
  - File data resides _only_ in the original file
  - If the original file is removed, the link breaks
```
# Create a hard link
ln source_file.txt hard_link.txt

# Create a soft link
ln -s source_file.txt soft_link.txt
```

## Grep
- Finds regular expressions (regex) in a particular file
- Info obtained from [BashSenpai](https://bashsenpai.com/resources/cheatsheets/grep)
### Key Options
- ```-i``` ignore case (treat "abc" and "ABC" as equal)
- ```-v``` invert match (only show lines, not matching patterns)
- ```-r``` recursive search (```-R``` also works)
- ```-l``` shows only names of files containing pattern
- ```-n``` show line numbers of lines containing pattern
- ```-c``` count how many lines match the pattern
- ```-w``` match the whole word

### Examples
- ```grep 'pattern' filename``` search for a pattern within a file
- ```grep 'string1|string2' filename``` search for lines containing string1 or string2
- ```grep -r 'pattern' /dir``` recursive search for pattern in /dir
- ```grep -w 'full word' filename``` search for lines containing "full word"
- ```grep -n 'pattern' filename``` show line numbers of lines w/ the pattern
- ```grep -c 'pattern' filename``` count the lines w/ the pattern
- ```grep --color 'pattern' filename``` highlight the pattern in the output
- ```grep -i 'pattern' filename``` case-insensitive search


