# Day 2 - Linux Basics (2026-06-10)

## Learning Objectives
- Deepen File System operations
- Process Management
- History & Command Line Efficiency

## Key Commands Learned

**File System:**
*On a Linux system, everything is considered to be a file*
*In Linux, on one file system tree under the root*
*A mount point (insert a usb) is a directory on a file system that is logically linked to another file system*
- `df -h` : to find `/dev/sdb` (a mount point)

- `mkdir -p` : Create nested directories
- `ls -lh`  : List files with human-readable sizes
- `cp`, `mv`, `rm -i` : Copy, Move, Safe Remove
- `tree` : Display directory structure 


**Process Management:**
- `ps aux` : Show all running processes
- `top` : Real-time monitoring (press q to quit)
- `pgrep`, `pkill`

**History & Efficiency:**
// "bash_history" only update after logged out 
- cat .bash_history

// "history" saved the command after ran
- `history | grep keyword`
- `!!` : Repeat last command (It is dangerous if we don't confirm it before running it, better to print it out first)
- `Ctrl + R` : Reverse-i-search
- `history -c` : Remove history

//running command without leaving a trace 
- `"HISTCONTROL=ignorespace >> .bashrc"` : set up and save to .bashrc
- ` who` : leaving a space in front, run normally but wont appear in history

**Root vs non-Privileged users**
- non-privileged users : have no special rights on the system
- root (administrator)

- `sudo su` : temporarily become root , `exit` to exit root 

**Absolute vs Relative Paths**
- `cd .` : the current working directory
- `cd ..`: the parent directory
- `cd ~` : the user's home directory 
- `cd -` : last directory
- `cd /` : root
- `cd /path_to_dir` : to path_to_dir
- `pwd` : printing the current working directory

- `cd /home/jason/devops-journey-2026` : absolute path  > start from root '/'
- `cd ~/devops-journey-2026`: (~ > /home/jason) relative path > start from current directory


**File Timestamps**
1. atime : the last time the file was read (`ls -lu`)
2. mtime : the last time the contents was modified  (`ls -l, ls -lt`)
3. ctime : the last time when some metadata related to the file was changed (`ls -lc`)

- `stat /etc/passwd` : showing statistic included timestamps 

How to Changing the timestamps

- `touch linux.txt` : update the atime mtime if file exist & ctime will also update automatically
- `touch -a` :update the atime & ctime will also update automatically
- `touch -m` :update the mtime & ctime will also update automatically

Hacker fail to fake us cause is they can't fake the ctime (fake atime/mtime but ctime is update to current time) 

Sorting File by Timestamps
- `ls -lt` :sorting by mtime
- `ls -ltu`:sorting by atime

**Viewing Files**
- `cat` :display out on terminal window
- `more`:work like `cat`
- `less`:display like man page

-  `cat cat.txt linux.txt > concate.txt`: concatenation two files (cat.txt + linux.txt) to a new file (concate.txt)

- `tail`:reading from the end (usually 10 lines by default/ `-n` number option)
- `head`:similar to tail but start from the beginning
- `watch -n 1 -d ifconfig`:running repeatedly & highlight the changes 

**Creating Files & Directories**
- `touch`: creating a new file or updating the timestamps if file already exist
- `mkdir dir`: creating a new directory
- `mkdir -p mydir1/mydir2/mydir3`: creating a directory and its parents as well

**The cp command**
- `cp file1 dir1/file2`:copy file1 to dir1 as another name file2 
- `cp -i file1 file2`:prompting the user if it overwrites or not *important*
- `cp -p file1 file2`:perserving the file permissions,group and owner, if no owner will change to user who run `cp` *important*
- `cp -r dir1 dir2/`:copy more source files and directories to a destination directory

**The mv command**
- `mv file1 file2`:renaming file1 to file2 
- `mv file1 dir1/`:moving file1 to dir1
- `mv -i file1 dir1/`:prompting the user if it overwites or not
- `mv -n file1 dir1/`:moving only if the source file is newer than destination file or when the destination file is missing

- Moving file within the SAME Filesystem (~/desktop/app.log to ~/Documents/app.log)
1. Inode stays the same.
2. atime & mtime stay identical. Only ctime updates because the file's metadata path changed!

- Moving ACROSS Different Filesystems (USB, NAS, etc..)
1. actually copy the data over and then delete the source file
2. brand new inode number on target Filesystem
3. all timestamps reset to current time

**The rm command**
- `rm file`: removing a file
- `rm -r dir1`:removing a directory
- `rm -ri file1 dir1/`:removing a file and a directory prompting the user for confirmation *important*

- `shred -vu -n 100 file1`:secure removal of a file,`-u` remove from file system after overwirte > size to 0; `-n 100` rewrite with random 0 and 1 100times to prevent recover.

**Piping and Command Redirection**
- Using the *pipe symbol (|)* we can connect two or more commands at a time.

- `ls -lSh /etc/ | head`: seeing the first 10 files by size (`-l` long list, `-S` sorting by size, `h` human readable)
- `ps -ef | grep sshd`: checking if sshd running (`-e` all process, `-f` full format)
- `ps aux --sort=-%mem | head -n 3`:showing the first 3 process by memory consumption

- `cat -n /var/log/auth.log | grep -a "authentication failure" | wc -l`: show log with line `-n`|grep "authentication failure" `-a` treat everything is test (included binary number) | count the total after filter(grep)
>> output = 6

**Command Redirection**
*will overwiter origin content*
- `ps aux > running_processes.txt`
- `who -H > loggedin_users.txt`

*will appending the file*
- `id >> loggedin_users.txt`

*handle error*
- `tail -n 3 /etc/shadow 2> error.txt`: error.txt = Permission denied
- `tail -n 2 /etc/passwd /etc/shadow > output.txt 2>&1`: writing output and error together to output.txt
