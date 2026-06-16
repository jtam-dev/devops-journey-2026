# Day 4 - Linux Basics (2026-06-12)

## Learning Objectives
- Searching for String in Binary Files
- The Basics of VIM text Editor
- Compressing & Archiving
- The Inode Structure


## Source
- a:`ifconfig > a`
- b:`ifconfig > b`
- c:`who >c`
- d.txt:`ls -li > d.txt`
- `cp /etc/ssh/sshd_cofig .`: copy sshd_config to current directory


## Problems Encountered & Solutions
*Searching Files* 
- `cmp a b`: binary or text files, fast comparison of whether files are identical or different at byte level 
output: a b differ: byte 285, line 5
- `cmp /user/bin/ls .ls`: no output is good (same file)
- `sha256sum /usr/bin/ls ./ls`: binary or text files, compare the *integrity* of files by verifying their checksums, ensuring identical across different locations 
output: two same hash code displayed. (identical same = 100% same!)
- `diff a b`: comparing text files line by line with detailed output, useful for *source code* and *configuration files*.
output: display the different between two text files


*VIM text editor*
- `vi output.txt`: open vim editor
Normal Mode (Esc -> confirm no --INSERT--)
- `:wq`: quit & save vim editor ; `:w` = save ; `:q` = quit
- `/ssh` : searching text ; pressing `n` to highlight the next result
- `!ifconfig`,`!ls`: forced to run something; go back to terminal for a moment and run `ifconfig / ls` (still in the vim)
- `%s/no/XXX/g`: `%` whole file; `s` substitute; `/no/`  to `XXX` ; `g` Global (one line -> all 3 `no` sub to `XXX`)
- `:e!`:force reload to last saved moment
- `u`: type "u" in commad to undo last step
- `dd` : to cut a line and copied to the clipboard; `10dd`: cut *ten* lines and copied to the clipboard
- `p`: paste the line from the clipboard
- `v` + arrow up & down: select a word ; `V` + arrow up & down: select a line
- `set nonu` : Don't display line number; `set nu`: Display line number
- `:100` move to line 100
- `shift + g` : move to the end of the file
- `gg`/`:1`: move to the begin of the file
Insert Mode 
- `i` :insert before the cursor; `I`: insert at the beginning of the line
- `a` :insert after the cursor; `A`: insert at the end of the line
- `o` :insert on the next line
How to change setting? 
- `vim ~/.vimrc`:vim configuration (vim will run ".vimrc" everytime)
- `i`:Insert Mode->`:set nu` ->next line `:syntax on`-> `ESC`:Normal mode -> `:wq!`
How to handle two files at the same time?
- `vi a c`: open a & c at the same time
- `:n`:move to the next file
- `:prev`:move from file c to the prev file a
- `vi -o a c`:open two files in a split window; `Ctrl + w`: to move around this two files
- `vi -d a b`:open two files in a split window to compare the different

*Compressing & Archiving*
- Archiving : 10 100 kilobytes files archive to 1 1000 kilobytes file (same size->easier to move)
- Compressing: 10 100 kilobytes files -> 200 kilobytes maybe(differnt compress ratio)

- `man tar`: manpage for tar
- `tar -c`: create a archive
- `tar -x`: extract a archive
- `tar -t`: display a table of content
- `tar -z`: gzip 
- `tar -v`: showing the archive process
- `sudo tar -czvf etc.tar.gz /etc/`:  create`-c` a gzip`-z` (showing archive process`-v`) file named`-f` etc.tar.gz(zipped archived file) from the directory */etc/* 
- Archived file also call *tarballs*
- `sudo tar -czvf /tmp/etc.tar.gz /etc/`: we can specify the directory */tmp/*
- `tar -czvf archive.tar.gz /etc/passwd /etc/group /var/log/dmesg /etc/ssh/`: we can archive multiple files in to a file
- `tar --exclude='*.mkv' --exclude='.config' --exclude='.cache' -czvf myhome.tar.gz ~`:we can exclude some file types
- `tar -xzvf etc.tar.gz`:extract the archived file
- `tar -xjvf etc.tar.bc2 -C my_backup/`:extract the archived file to a specify directory
- `sudo tar -cjvf etc-$(date +%F).tar.bz2 /etc/`: a trick to create a backup file with date (etc-2026-05-03.tar.bz2)

*The Inode Structure*
- Each file on the disk has a data structure called *index node* or *inode* associated with it
- This structure stores metadata information about the file such as the type, file's permission, file's owner and group owner, timestamp information , file size and so on
- *It is actually contains all file information except the file contents and the name*
- Each inode is uniquely identified by an integer number call inode number(ls -i)
- `ls -i`:display inode number ; `ls -li`:display inode number and long list
To create two hard link(ln)
- `ln d.txt e.txt`:two file shard the same hardlink, if we change d.txt, e.txt will be also changed 
- `ls -li`: checking the result 
output:276654 -rw-rw-r-- 2 jaosn jason 821 16 Jun 22:00 d.txt |276654 -rw-rw-r-- 2 jaosn jason 821 16 Jun 22:00 e.txt(same details)
- `find . -inum 276654`: find the files sharing the same inode number(hardlink)
output:
./my_backup/d.txt
./e.txt

- Hardlink: can make us easy to access within different directories without copy one by one

- Softlink/Symlink: is just a reference to another file (shortcut) *use more often*
- We can create a softlink to a directory but hardlink can't
- Also, softlink can cross the file system(different disk),but hardlink cant (belong to it's own inode structure)
- softlink only contain the path of the original file;hardlink have same inode structure and inode number
- `ln -s /etc/passwd ./pswd`: */etc/passwd* create a shortcut call *./pswd*