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
