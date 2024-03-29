- Learning to navigate **files, create files, delete and copy files** 
  Best article to refer - [Filesystem](https://www.digitalocean.com/community/tutorials/basic-linux-navigation-and-file-management)
- **Linux Basic Commands**
  collapsed:: true
	- `ln` Link (Unix) command
		- The ln command is standard Unix command utility used to create ^^hard link^^ or ^^soft link^^ (symlink) to an existing file or directory.
			- Hard link - Simply known as links are objects that associate the filename with the ^^inode^^ A given file on disk could have multiple links scattered through the directory hierarchy, with all of the links being equivalent, since they all associate with the same ^^inode^^. Creating a link therefore does not copy the contents of the file but merely causes another name to be associated with the same contents. Each time a hardlink is created, a link counter that is part of inode structure gets incremented; a file is not deleted until its reference count reaches zero.
			  `ln source_file targetlink`
			- Symbolic links : Symbolic links are special files which, when encountered during pathname resolution, modify the pathname resolution to be taken to the location which the symbolic link contains. The content of the symbolic link is therefore the destination path string, which can also be examined using the readlink command line utility. The symbolic link may contain an arbitrary string which does not refer to the location of an existing file. Such a symbolic link will fail until a file is created at the location which is contained by the symbolic link. By contrast, a symbolic link to an existing file will fail if the existing file is moved to a different location (or renamed)
			  `ln -s targetfile shortcut`
			- Also  - You cannot link directories or files in different filesystems when doing Hardlinks however since Softlinks are just like path pointing to original file, you can link folders as well as files in different file systems
			-
	- `cp` : Copy command
		- cp is a Linux shell command to copy files and directories.
		  Syntax  $ cp [options] source dest.
		- cp command options
			- `cp main.c bak` Copy single file to directory
			- `cp main.c def.h /home/usr/rapid/` Copy 2 files main.c and def.h to absolute path directory
			- `cp *.c bak` Copy all .C files to directory
			- `cp src /home/usr/rapid/` Copy directory src to absolute path directory
			- `cp -R dev bak` Copy files recursively to subdirectory bak
			- `cp -f test.c bak` Force copy files
			- `cp -i test.c bak` Interactive prompt before file overwrite
			- `cp -u * bak` Copy only newer files to destination _directory_ bak
			-
	- `cat` : Cat command
		- `cat` is a standard Unix utility that reads files sequentially, writing them to standard output (STDOUT). Name derived from concatenate files.
		- `cat [options] [file_names]`
		- `cat file1.txt` Displays contents of files
		- `cat file1.txt file2.txt` Concatenate two text files and display result in the terminal
		- `cat file1.txt file2.txt > newcombinedfile.txt` Concatenate two text files and create new file
		- `cat >newfile.txt` Create a file called newfile.txt. Type desired input and press CTRL+D to finish
		- `cat file1.txt > file2.txt` Copy the contents of file1.txt to file2.txt
		- `cat file1.txt >> file2.txt` Append content of file1.txt to file2.txt
		- `cat file1.txt file2.txt file3.txt | sort > test4` Concatenate the files, sort the complete set of lines and write the output to new file
		- `cat file1.txt | grep example` Highlight instances of the word example in file1.txt
		-
		- Do not use useless cat commands. e.g. cat "$file" | grep "$pattern" can be written as grep "$pattern" "$file"
	- `find` : find command
		- Finding a File in Linux by Name or Extension
		  card-last-interval:: 4
		  card-repeats:: 1
		  card-ease-factor:: 2.6
		  card-next-schedule:: 2022-04-25T13:04:14.947Z
		  card-last-reviewed:: 2022-04-21T13:04:14.954Z
		  card-last-score:: 5
			- `find /home/username/ -name "*.err"`
			- `find /home/username/ -iname ".err"` _ignorecase here_
		- Using command `find` commands and syntax to find file in linux
		  card-last-interval:: 4
		  card-repeats:: 2
		  card-ease-factor:: 2.6
		  card-next-schedule:: 2022-04-25T13:04:17.945Z
		  card-last-reviewed:: 2022-04-21T13:04:17.945Z
		  card-last-score:: 5
			- `find options starting/path expression`
			- `find -03 -L /var/www/ -name ".html"`
		- Finding file with modification time and accessed time.
		  card-last-score:: 5
		  card-repeats:: 1
		  card-next-schedule:: 2022-04-24T09:48:44.767Z
		  card-last-interval:: 4
		  card-ease-factor:: 2.6
		  card-last-reviewed:: 2022-04-20T09:48:44.768Z
			- `find / -name "*conf" -mtime -7`
			- `find /home/example/user -name "*conf" -mtime -3`
			- `find / -mtime +50 -mtime -100`   _50days back and less than 100 days_
			- `find / -atime 50`
		- Using `grep` to Find a File in Linux Based on content.
		  card-last-score:: 5
		  card-repeats:: 1
		  card-next-schedule:: 2022-04-25T13:04:16.963Z
		  card-last-interval:: 4
		  card-ease-factor:: 2.6
		  card-last-reviewed:: 2022-04-21T13:04:16.963Z
			- `find . -type f -exec grep "example" '{}' \; -print`
			  This searches every object in the current directory hierarchy (.) that is a file (-type f) and then runs the command grep "example" for every file that satisfies the conditions. The files that match are printed on the screen (-print). The curly braces ({}) are a placeholder for the find match results. The {} are enclosed in single quotes (') to avoid handing grep a malformed file name. The -exec command is terminated with a semicolon (;), which should be escaped (\;) to avoid interpretation by the shell.
		- How to find and process a File in Linux.
		  card-last-score:: 5
		  card-repeats:: 1
		  card-next-schedule:: 2022-04-24T09:49:01.501Z
		  card-last-interval:: 4
		  card-ease-factor:: 2.6
		  card-last-reviewed:: 2022-04-20T09:49:01.501Z
			- `find . -name "rc.conf" -exec chmod o+r '{}' \;`
		- How to find and delete a file in Linux.
		  card-last-score:: 5
		  card-repeats:: 1
		  card-next-schedule:: 2022-04-24T09:48:51.127Z
		  card-last-interval:: 4
		  card-ease-factor:: 2.6
		  card-last-reviewed:: 2022-04-20T09:48:51.127Z
			- `find . -name "*.bak" -delete`
		- Find files with permission e.g. 777.
		  card-last-score:: 5
		  card-repeats:: 1
		  card-next-schedule:: 2022-04-24T09:48:03.779Z
		  card-last-interval:: 4
		  card-ease-factor:: 2.6
		  card-last-reviewed:: 2022-04-20T09:48:03.781Z
			- `find . -type f -perm 0777 -print`
			- `find . -type f ! -perm 777`
		- Find files by size.
		  card-last-score:: 3
		  card-repeats:: 2
		  card-next-schedule:: 2022-04-29T07:40:36.410Z
		  card-last-interval:: 4
		  card-ease-factor:: 2.46
		  card-last-reviewed:: 2022-04-25T07:40:36.412Z
			- `find / -size +50M -size -100M`   _files greater than 50MB and less than 100 MB_
			- `find path -size +MoreThanM -size -LessthanM`
	- `ls` : Ls command or List command
		- List files and directories in current working directory or path given.
		- `-l` long format, permissions, number of hardlinks, owner, group, size etc
		- `-F` append a "/" to a directory and a "*" to executable files
		- `-g` display group but not owner
		- `-o` display owner but not group (when combined with -g suppresses both owner and group )
		- `-d` shows information about a symbolic link or directory rather than about the links target or listing the contents of a directory
		- `-h` output sizes in human readable format. (e.g. 1K, 235M, 2G etc. ) This option not part of POSIX standard
		- Additional options of how files are displayed
			- `-f` do not sort
			- `-t` sort the list of files by modification time
			- `-1` force output to be one entry per line
			- `-R` recursively list files in subdirectories and their subdirectories
			- `-u` List files last access time instead of last modified time
			- `--full-time` to show times with seconds and milliseconds instead of down to minute
	- `chown` : Linux chown command.
	  collapsed:: true
		- There are three major types of permissions :
			- User permissions
			- Group permissions
			- Other premissions
		- Syntax
		  chown [-c|--changes] [-v|--verbose] [-f|--silent|--quiet] [--dereference]
		        [-h|--no-dereference] [--preserve-root]
		        [--from=currentowner:currentgroup] [--no-preserve-root]
		        [-R|--recursive] [--preserve-root] [-H] [-L] [-P]
		        {new-owner|--reference=ref-file} file ...
		- Ways to format new-owner
			- `user` The name of the user to own the file. In this format, the colon (:) and the group is omitted. The owning group is not altered
			- `user:group` The user and group to own the file, separated by a colon
			- `:group` The group to own the file
			- `user:` If  group is omitted, but a colon follows user, the owner is changed to user and owning group is changed to login group of user
			- `:` Specifying a colon with no user or group is accepted, but ownership is not changed.
		- Examples
			- `sudo chown myuser myfile.txt` to change owner
			- `sudo chown notme:notmygroup myfile.txt` to change owner and group
			- `sudo chown -R myuser:mygroup otherfiles` Change the ownership of directory and all its contents recursively
		- Groups in Linux
			- In Linux, a user is a member of multiple groups but it has only ^^one current group^^. The user's current group is user's group identity or **GID**.
			- When user creates a new file, the file's ownership is set to user's UID (user identity) and GID (group identity). So when a user _myuser_ creates a file, its owned by _myuser_ and also by its current group. _myuser_ can change the file's group ownership with **chown** but only **root** can change the owner to someone else
			- Each user has a configurable login group which can be any of user groups. Command to change login group is **usermod** with `-g` option
			  `sudo usermod -g newlogingroup myuser`
			- By default every Linux user has a private group, with that user as the only member.
		- Note : Only root user can change owner user of file. So use sudo 
		  `sudo chown aaron:family family_dog.jpg`
	- `mkdir` : make directory 
	  collapsed:: true
		- `mkdir -p /tree/branch/leaves`
		- `mkdir tree`
		-
	- `SGID`, `SUID` and `sticky` bit
	  collapsed:: true
		- SGID is setting group id
		- SUID is setting user id
		- Sticky bit is setting sticky bit `t` for any directory
			- Example you want access to /tmp or /var/log folders to create files but not to delete. You can set a sticky bit
	- `sed` - also supports regular expressions.
	  collapsed:: true
		- `s`:  Stream editor, it will preview what command will do without executing it where we want to replace one text with another.
		- `-i` : --in-place , will make it final
		-
	- `cut`
	  collapsed:: true
		- cut -d ' ' -f 1 userinfo.txt
		- cut -d ',' -f 1 userinfo.txt
	- `uniq` : remove repeating lines which are adjacent only
	- `sort` : sorts
- Searching with `grep` with simple patterns
	- Syntax : grep [options] 'search_pattern' file
	- grep 'CentOS' /etc/os-release
	- grep -i 'centos' /etc/os-release             //i stands for ignore case
	- Searching for all files grep -r 'Centos' /etc/        // r stands for recursive
	- grep -ir 'centos' /etc/
	- remember to use sudo :    $sudo grep -ir 'centos' /etc
	- grep -ivr 'centos' /etc/os-release                // invert search
	- grep -wi                                                      // matches only words with `w` option
	- grep -oi 'centos' /etc/os-release             // matches only words and displays only matches
	-
- **Regular expressions** - Used to search with complex search conditions.
	- Grep is original Grep and it understands basic regular expressions and basic patterns. Glob or wild card.
	- When we grep sometimes we get a lot of other details were the pattern is present.
	- Here we will discuss all characters in basic expressions.
	- Line begins with, use character `^`
		- grep '^PASS' /etc/login
		- only gives options that start with that pattern exactly and no other lines
	- Line ends with, use operator `$`
		- grep 'sam$' /etc/login
		- only gives lines that end with sam
	- Match ^^any one^^ character, use operator `.`
		- grep -r 'c.t' /etc
		- grep -wr `c.t` /etc  //matches only word, no partial word matches
		- What if I want to match the character which is a regex operator. ? Escape \
			- you cannot search for (.) using grep '.' /etc/login.txt as it will match all characters.
			- User operator \ : Escaping special characters
				- e.g. grep -wr '\\.' /etc/login.txt
				-
	- Match the ^^previous Element 0 (zero) or More^^ Times: Use character '\*'. Element before it is optional to exist.
		- e.g. let* == le_ttt_
	- Match ^^The Previous Element 1 or More Times^^ use character `+`
		- To use + as an operator : 
		  $ grep -r '0\\+' /etc/
		- By default grep uses basic regular expressions. So for using meta characters to use their special meaning, use backslash before it. Hence use egrep or **Extended regular expression to avoid back slash on regex operators.**
	-
	-
- **Extended Regular expressions**. refer documenation at https://regexr.com
  $ grep -Er '0+' /etc/ == $ egrep r '0+' /etc/
	- ^^Previous Element can exist this many times^^ :  `{}` parenthesis brackets
		- egrep -r '0{3}' /etc : matches exactly 3 0s
		- egrep -r '0{3,}' /etc/ : matches 3 0s at least
		- egrep -r '10{,3}' /etc/ : matches 1 followed by atmost 3 0s. Which means it will also include 1 followed by no 0s in results as well.
	- ^^Make Previous Element options^^ : `?` Question mark
	  collapsed:: true
		- find all text that contains disable or disabled. This means d is optional
			- egrep -r 'disabled?' /etc
	- ^^Previous element can exist this many times^^ use {min,max}
	  collapsed:: true
		- egrep -r '0{3,5}' /etc/         // {min,max} matches zero 3,4 or 5 times
	- Match one thing or other : |
	  collapsed:: true
		- egrep -r `enabled|disabled` /etc
		- egrep -r 'enabled? | disabled?' /etc
	- Range or sets : []
		- to find cat or cut use - egrep -r 'c[au]t' /etc/login
		- `$ egrep -r '/dev/.*' /etc/`             -> . is any character, * any number of characters plus previous one any. Its greedy gives various results not ideal.
		- `$ egrep -r '/dev/[a-z]*' /etc/`                -> Cannot catch digits here
		- `$ egrep -r '/dev/[a-z]*[0-9]' /etc`               -> Good enough. but ends with a digit only, what if more?
		- `$ egrep -r '/dev/[a-z]*[0-9]?' /etc/`              -> End with digit is optional , which means its okay if its not present hence using question mark
		- Common used sets [a-z] [0-9] [abz954]
	- Subexpressions : ()
	  collapsed:: true
		- 1+2\*3 = 9 but (1+2)*3 = 9, we can do same with regular expressions and have different results.
	- Negated Range or Sets : [^]
		- Elements in this range should NOT be matched
		- egrep -r 'http[\^s]' /etc/
- **TAR**. `tar` : To create Tape Archives.
  collapsed:: true
	- Packing Files and Directories with tar.
	- `$ tar --list --file archive.tar`
	- `$ tar -tf archive.tar`
	- remember to add --file or -f option when pointing to tar files
	- To create archive file use command `tar --create --file archive.tar file1` == `tar cf archive.tar file1`
	- To append files to this tar ball use command `$ tar --append --file archive.tar file2` == `$ tar rf archive.tar file1`
	- Before extracting from tar archive , always use --list option
		- `tar --list --file archive.tar` == `tar tf archive.tar`
		- `tar --extract --file archive.tar` == `tar xf archive.tar`
		- To extract to OTHER directories than ones listed in tar use `$ tar --extract --file archive.tar --directory /tmp/` = `$ tar xf archive.tar -C /tmp` --> Use Capital C to extraCt elsewhere.
		- To preserve permission use sudo
- How to **compress and de-compress** files in Linux
  collapsed:: true
	- Most Unix have three compression utilities already installed gzip, bzip2 or xz
	- Typical command `$ gzip file1`
	- To decompress -> gunzip OR bunzip OR unxz. Also similar can be option --decompress
	- When compressed OG file is deleted.
	- To keep original file use --keep or -k option with any of above utilities
	- To check contents or compressed files we can do `$ gzip --list file.gz`
	- `$ zip archive file1` = `$ zip archive.zip file1`
	- `$ zip -r archive.zip Pictures/ `
	- `$ unzip archive.zip `
	- Zip supports both packing and compression.
	- Telling tar to do both things - create archive and compress it 
	  collapsed:: true
		- `$ tar --create --gzip --file archive.tar.gz file` -> `$ tar czf archive.tar.gz file1`
		- `$ tar --create --bzip --file archive.tar.bz2 file1` -> `$ tar cjf archive.tar.bz2 file1`
		- `$ tar --create --xz --file archive.tar.xz file1` -> `tar cJf archive.tar.xz` file1
		- ^^AutoCompress^^ `$ tar --create --autocompress --file archive.tar.gz file1`   // depending on the extension compression utility is autoselected.
		- Also can be written as `$ tar caf archive.xz file1`
		-
	-
	-
- **Backup Tools** in Linux - Common
  collapsed:: true
	- `Rsync`
		- Backup to a remote system
		- [[draws/2022-05-13-15-49-07.excalidraw]]
		- `rsync` -a Pictures/ aaron@9.9.9.9:/home/aaron/Picures
		- you can do local to remote, remote to remote remote to local or local to local
	- Disk Imaging
		- `$ sudo dd if=/dev/vda of=diskimage.raw bs=1M status=progress`
		- To restore disk image , just reverse the if and of labels
- **Redirection** in Linux
	- If a program knows its input, it needs to know where to send its output
	- Output is of two types, successful and unsuccessful output (errors,warnings etc. )
	- StdIn < , Stdout 1> , Stderr 2>
	-
- **Reboot and shutdown**
  collapsed:: true
	- `$ systemctl reboot`
	- `$ sudo systemctl reboot`            //for normal users
	- `$ sudo systemctl poweroff`    // to shtudown
	- `$ sudo systemctl reboot --force`  //forcefully reboot
	- `$sudo systemctl poweroff --force` //forcefully poweroff
	- `$sudo systemctl reboot --force --force` //abrupt reboot and same for poweroff.
	- `$ sudo shutdown 02:00` // shutdown 24 clock timer
	- `$ sudo shutdown +15` //after 15 mins shutdown
	- `$sudo shutdown -r 02:00`  //reboot at specific time
	- `$ sudo shutdown -r +15 'wall message'` //reboot in specific time
- **Boot and changing diff. Operating Modes. Boot Targets** (??)
  collapsed:: true
	- To get current Boot target use `systemctl get-default`. Can be set at graphical.target
	- **Multi-User.Target** : Everything text based, mutliple users can login and use system at same time
	  collapsed:: true
		- `sudo systemctl set-default multi-user.target` // makes Linux boot normally, but graphical user interface is skipped. Multiple users can log in. It also turns on internet services. But have to reboot.
	- Immediately switch target without reboot
	  collapsed:: true
		- ^^`$ sudo systemctl isolate graphical.target`^^
		- This method does not change default target.
	- Other useful targets
	  collapsed:: true
		- **Emergency Target** `sudo systemctl isolate emergency.target` -> few programs as possible. Useful for debugging. Like safe mode. Root file system is mounted as read-only
		- **Rescue Target** `sudo systemctl isolate rescue.target` -> a bit fewer programs than emergency target. DB troubleshooting.
		- For both above targets we need root credentials (with password)
	- **Installing and troubleshooting Bootloaders** (?)
	  collapsed:: true
		- Bootloader is used to start Linux kernel
		- Popular bootloader is GRUB -> Grand Unified Boot Loader.
		- Say there is a problem with Boot loader and OS does not boot.
		- choose Rescue mode.
		- system files are mounted under mnt/root
		- Generate a grub configuration file -> `grub2-mkcofnig -o /boot/grub2/grub.cfg`
		- command to show all block devices -> `lsblk`
		- Grub should be installed on boot disk
		- `grub2-install /dev/sda` -> where /boot was present
		- dnf reinstall
- **Startup Processes** || **systemctl**
  collapsed:: true
	- `$sudo systemctl status sshd.service`
	- To stop a service `$ sudo systemctl stop sshd.service`
	- `$ sudo systemctl start sshd.service` -> Manually start the service
	- After config for a service is changed, to pick up new settings. `$sudo systemctl restart sshd.service`
	- But this is abrupt restart
	- For gentle restart - `$ sudo systemctl reload sshd.service`
	- Can also use - `$ sudo systemctl reload-or-restart sshd.service`
	- Want to disable sshd login, disable the service -> `$ sudo systemctl disable sshd.service`
	- To enable `$ sudo systemctl enable sshd.service`
	- Usually after installing a new application or DB server or app of any kind, we need to set up to auto start on boot
		- `systemctl enable sshd.service`
		- `systemctl start sshd.service`
		- `system enable --now sshd.service`        // tells system to enable and start service now
		- `system disable --now sshd.service`  // tells system to stop and disable service now
	- Sometimes some process can still start even if stopped or disabled, since other services can interfere. There is a **BRUTEFORCE** way to stop these services from every staring -> **mask**
		- `$ sudo systemctl mask atd.service`     //wont start even if enabled or started
		- `$ sudo systemctl unmask atd.service` // undo mask
	- To find all services installed -> **sudo systemctl list-units --type service --all**  //sometimes we install apps but their service names are completely different
	-
- **Manage & Diagnosing processes**
  collapsed:: true
	- commonly used command to inspect processes is PS
	- ps supports both UNIX and BSD style syntaxes and hence has different outputs. E.g. `ps -a and ps a are different outputs`
	- `ps aux` // a and x lists all process including all terminals and u is uniform or good format
	- ps only shows state of process when command was executed
	- for live monitoring of process - use `top` command
	- For checking process run by a user use `-U` option. E.g. `ps -U swapnil`
	- search name specific logs -> use `pgrep`
	- E.g. `pgrep -a syslog`
	- Process Niceness -> how nice a process is to other processes. Lower number less nice it is, means it has higher priority.
		- At launch time, we can launch with a nice value -> `nice -n 11 bash`
		- Use `-l` in ps to check nice values. `NI` column in process
		- A regular user can assign values from 0-19
		- Negative values can be assigned by root user only or SUDO
		- To renice syntax -> ` sudo renice 7 8209` ---> renice _nicevalue_ _pid_
		- As a regular user you can lower nice value only once.
	- To see which processes are parents of other process, use `f`
		- `ps aufx `
	- **SIGNALS**
		- **SIGSTOP** and **SIGKILL** -> These cannot be ignored by any process.
		- **SIGSTOP** , will stop the process unless they receive **SIGCONT** (sigcontinue)
		- **SIGKILL** is last resort
		- kill -L -> give list of Numeric values and associated signal names.
		- only send process to owned by current user.
		- `sudo kill -SIGHUP 1147` // sudo for sending signal to process not owned, signal, PID
		- also ok to skip SIG command looks like `sudo kill -HUP 1147`
		- `pkill -KILL bash`  -> search with name and kill them (to just search use pgrep)
		- background vs foreground
			- command - `jobs` -> lists jobs running in backgroun
			- to bring to foreground - `fg 1`  //1 is PID
			- Press CTRL+Z to pause from running command
			- to make it resume progress ->`bg 1`
		- to find what files a process is using use `lsof`
			- `lsof -p 8401`  --> ls is list, of is open files
			- `lsof /var/log/messages` -> list processes that use this file.
			- work with sudo gives result.
- **Locate and Analyze log files in Linux**
  collapsed:: true
	- Everything important happened in a linux system is saved somewhere in log text files.
	- Status messages, errors, warning messages. -> These are generated by applications and processes. Its job of logging daemons to collect, organize and store them into files
	- rsyslog = rocket-fast system for log processing. /var/log -> location
	- **Finding the file** Where to find ssh logs? We can search **all files** that contain the word ssh.
	  collapsed:: true
		- `$ grep -r 'ssh' /var/log`
		- ssh logs are stored in /var/log/secure -> you found this from above command
		-
	- **Following the log files**
	  collapsed:: true
		- tail -F /var/log/secure `-F` follow mode
	- **Journal** daemon - smarter way to collect data, `journalctl` helps organize logs easily
	  collapsed:: true
		- which sudo -> /bin/sudo   //here we found where the command is located
		- `journalctl /bin/sudo`       // Using Journal daemon to find logs of above command. It opens in less pager
		- `journal -u sshd.service`   //if we know name of service we can use journalctl, -u tells daemon journal to display logs by this UNIT.
		- `journalctl -e`                        // end of journalctl
		- `journalctl -f`                     // follow mode
		- Types of alerts  : **info**, **warning**, **err**, **crit**
		  id:: 6284c29d-7f30-4f03-b20f-f87ff53d3caa
		- We can use `-p` command to find the priority errors e.g. `$ journalctl -p err`
		- There are many priority switches to use
		- **Examples of JournalCtl**
			- $ journalctl -p `TAB` `TAB`
			- $ journalctl -p 
			  emerg    alert    crit     err      warning  notice   info     debug
			- $ journalctl -p err -g '^b'               // -g is for grep, we pass grep expression for lines that begin with b. Begin ^
			- $ journalctl -S 02:00            // -S stands for Since
			- $ journalctl -S 01:00 -U 02:00 //between 1.00 AM to 2:00 AM
			- $ journalctl -S '2021-11-15 12:04:55'            //date and time format supported
			- $ journalctl -b 0                // boot options , current boot use 0
			- $ journalctl -b -1               // previous boot
			- mkdir /var/log/journal
			-
			-
		- Who logged in last
			- last
			- lastlog
	-
- **Scheduling JOB : CRONTABS | ANACRON **
	- Three main tools to set up scheduled Tasks 1. CRON 2. ANACRON (only works with days) 3. AT
	- 1. **CRON**
	  `cat /etc/crontab` --> Below is what you would see
		- Syntax :
		- [[draws/2022-05-18-19-48-36.excalidraw]]
		- Below is list of other expression used with the Syntax
		  * (*) = matches all possible values
		  
		  * , = matches mutliple values 15,45
		  * - = range of values (i.e. 2-4)
		  * / = specifies the step (i.e. *//)
		- Useful commands to remember
			- `crontab -l `      // -lists users crontab
			- `sudo crontab -l`
			- `sudo crontab -e -u jane`  // -e edit crontab , -u for any specific user
			- `sudo crontab -r -u jane`  // -r remove crontab for specific user
			- Alternate way to set up cronjobs - > special directories, however dont use extensions for files before copying it to folders
			- daily = /etc/cron.daily
			- hourly = /etc/cron.hourly
			- monthly = /etc/cron.monthly
			- weekly = /etc/cron.monthly
	- 2. **ANACRON**
		- To check syntax `sudo vim /etc/anacrontab`
		- Syntax is which day  delay in minutes user and command
		- to force run all anacron jobs -> `sudo anacron -n -f`
		- Read more about this online
		- (?) read more about `systemd-cat` utility
	- 3. **AT**
		- at 15:00
		- at 'August 20 2022'
		- at '2:30 August 20 2022'
		- at 'now + 30 minutes'
		- at 'now + 3 hours'
		- at 'now + 3 months'
		- at 'now + 3 weeks'
		- `sudo grep atd /var/log/cron` --> to check for logs of AT cron
		- to remove jobs use command - `atrm` -> will remove jobs of current user
		- to see list of running jobs by AT use command `atq`
		- doesn't give us useful details , use systemd-cat command to capture more, how to do it? --> | systemd-cat --identifier=at_scheduled
		- then search using `journalctl | grep at_scheduled`
		- Same can be done from **ANACRON**
		-
- **Update Software** & **Manage Software**
  collapsed:: true
	- Upgrading with the Package Manager
	- Centos - `dnf check-upgrade`
	- `sudo dnf upgrade` -->  dnf is the package manager for CentOs
	- Most software Linux is managed by package manager
	- Old Centos used `YUM` as package manager, new ones use `dnf`
	- Software repository  - All files, updates etc. that bring functionality
	- `sudo dnf repolist` -> huge list of repositories that give you packages
	- `sudo dnf repolist -v` --> more verbose
	- official repositories might not include all packages we need, we can use
	- `$ sudo dnf repolist --all`
	- To enable an optional repository listed by above command use -> `sudo dnf config-manager --enable powertools`  // powertools is name of repo id
	- to disable use `sudo dnf config-manager --disable powertools`
	- Add an external repository (other than official or optional) use this command to add --> `sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo`   // adds external docker repo
	- To remove 3rd party repository -> use verbose list `sudo dnf repolist -v`
	- Check the value of `Repo-filename` : /etc/yum.repos.d/docker-ce.repo   // since we added docker above
	- To remove, simply remove the file `sudo rm /etc/yum.repos.d/docker-ce.repo`
	- Not sure exact name of package ?
	- To search use `sudo dnf search web server`   -> searches all that matches keywords web server
	- `sudo dnf search 'web server'` -> exact search
	- `sudo dnf info 'nginx'`
	- To install use `sudo dnf install nginx -y`
	- To **reinstall** -> `sudo dnf reinstall nginx`
	-
	- To **remove** package -> `sudo dnf remove nginx`
	-
	- **Another way to install software** - >
	- `sudo dnf group list`  ---> `$ sudo dnf group install 'Server with GUI`  // installs all important packages from that group
	- To add even optional packages to above just --with-optional so the command would look like --> `$ sudo dnf group install --with-optional 'Server with GUI'`
	- To remove group of packages -> `sudo dnf group remove 'Group name'`
	-
	- **Download RPM package and install**
	  collapsed:: true
		- wget _link of RPM package_
		- `sudo dnf install ./rpm package name`    // . is current directory
		- sudo dnf remove _name of package_
		-
		-
	- **To automatically remove dependencies**
		- `sudo dnf autoremove`
		- To see history ->`sudo dnf history`
	- **Provides/Lists files details for installed packages**
		- `dnf provides /etc/anacrontab`  --> to find from where the utility came from which package
		- `dnf provides docker`  --> even if package is not installed , we can find which package provides the utility
		- `dnf repoquery --list nginx`   --> say you installed nginx but dont know where its config files are --> `dnf repoquery --list nginx | grep conf`
	-
	-
- **Integrity and availability of resources**
  collapsed:: true
	- _Verify available storage space_ -> How do we know we are running out of storage space
	- use `df` OR disk free option here. Output difficult to read so make `-h` for human readable format.
	- Ignore filesystems `tmpfs` only exist in computer's memory
	-
	- How much space is used by directory -> 
	  collapsed:: true
		- du -sh /bin/ -->  diskusage command s is summarize (don't go insde directories) and -h human readable.
	- How to find free memory --> `free -h` , Mi, Gi format; check available column.
	- How to check Load Average / processor used -> use command `uptime` // output is min, 5 min and 15 min load average
	-
	- `lscpu` --> Read more
	- `lscpi` --> Read more
	-
	- **Integrity of file systems**
	  collapsed:: true
		- Unmount filesystem first
		- To verify xfs file system -> `sudo xfs_repair -v /dev/vdb1`
		-
		- To check and repair extf4
		- `sudo fsck.extf -v -f -p /dev/vdb2`    --> verbose , -f and -p are optional, use -p always
		-
	- **How to determine key processes are running fine**
	  collapsed:: true
		- `systemctl list-dependencies`
	-
- **Change Kernel runtime parameters, persistent and non-persistent**
  collapsed:: true
	- `sysctl -a`
	- `sudo sysctl -a`
	- sudo sysctl -w _parameteridentifiedabove_=1
	- But this is **non-persistent** change, reboot and gone
	- **How do we make change persistent?**
		- man sysctl.d
		- location /etc/sysctl.d/*conf
		- `sysctl -a | grep vm`   --> see parameters related to VM
		- choose for example vm.swappiness=30 , high value will use disk sooner than required, low value will use disk unless necessary.
		- create a file for example swap-less.conf in /etc/sysctl.d
		- and add vm.swapiness=29
		- Will take effect on next reboot.
		- Want to make it immediate without reboot use command -> `sudo sysctl -p /etc/sysctl.d/swap-less.conf`    // don't know why p but remember we use p to make permanent
		-
		-
	-
- **SELinux** (Read more - course insufficient)
- **User Management**
  collapsed:: true
	- Manage Local User Accounts
	- Each user should have separate user account protected by proper permissions. Can allow to have special permissions and security and custom config
	- **How to create new user in Linux**
		- `sudo useradd john`   --> A new user is added to system, a new group john is also created, a home directory is create /home/john , default shell is set to /bin/bash, all files from /etc/skel will be copied to home directory of user. 
		  You can check content using `ls -a /etc/skel` -> #skel
		- Explore defaults given to each user added  ->`useradd --defaults`  == `useradd -D`
		- `cat /etc/login.defs` -> another way to check these default settings
		- No password is set to set password use -> `sudo passwd john`
		- To delete user john use -> `sudo userdel john` -> this will delete user may delete john group as well but not home/john directory
		- but if we want to delete home directory as well use -> `sudo userdel --remove john` == `sudo userdel -r john`
		- What if we want to change defaults -> Say change default shell to something else use following command
		  `sudo useradd --shell /bin/othershelllocation --home-dir /home/otherdirectory john`
		- also can be written as `sudo useradd -s /bin/othershell -d /home/otherdirectory/ john`
		- All details id, gid, home, shell etc are stored at **/etc/passwd**
		- do `cat /etc/passwd` ---> output below
		- `swapnil:x:1000:1000:,,,:/home/swapnil:/bin/bash` --> first 1000 is userid (uid), next number 1000 is group id (guid) followed by home directory and default shell.
		- Say you want other userid , use command --> `sudo useradd --uid 1100 smith` OR `sudo useradd -u 1100 smith` (group id of smith, smith will also have 1100)
		- what to do if **passwd** file completes.
	- **How to create delete and modify groups and group memberships**
	  collapsed:: true
		- Its like assigning roles to user accounts. Is a developer or not and based that on they get permissions.
		- Special group provides special permissions. Example WHEEL group -> sudo group and docker group
		- Primary group, is also called login group. It is the group assigned when user logs in.
		- `sudo groupadd developers`
		- To add user in group -> g password utility -> don't be confused, group password are almost never used to change group passwords. This is used now to add and delete users from group
		- `sudo gpasswd --add john developers` **or** `sudo gpasswd -a john developers`
		- `groups john`  -> first value is primary group
		- To delete from group -> `sudo gpasswd --delete john developers` **or** `sudo gpasswd -d john developers`
		- `sudo usermod -g developers john` **or** `sudo usermod --gid developers john` -> Used only to change _PRIMARY_ group.
		- `sudo groupmod --new-name programmers developers`
		- sudo groupmod -n programmers developers
		- `sudo groupdel programmers` --> cannot delete group if its someone's primary group. Secondary groups can be deleted easily even if it has users
		- Learn following examples -> Lock account, unlock, expire, unexpire, create system account,
		- read about `chage` - > to change age of account expiration to 0
		-
	- **Manage system-wide environment profiles**
	  collapsed:: true
		- printenv = $env
		- `etc/profile.d/lastlogin.sh`
		- type `$ echo $HOME` will print home directory for current login
		- If user wants to add their own environment variables, uses can edit this file - `.bashrc` present in their home directory
		- To set some `variable and its value for ALL Users` that log on to the system we can add them to --> this file `/etc/environment`
		- To do complex stuff like running commands when user logs in you can use location `/etc/profile.d/` and add scripts or files here
	- **Managing Template USER Environment**
	  collapsed:: true
		- Imagine you want to inform new users of default policy , what we can do is add custom
		  add information to /etc/skel ---> adds anything here to new users created
		- You can use sudo and edit .`bashrc` file for user as well -> `sudo vim /home/trinity/.bashrc`
		- if you say want to add special login bash files for all users edit file at skel -> `$ sudo vim /etc/skel/.bashrc`
	- **LDAP (?)**
	-
- **User Resource Limits**
  collapsed:: true
	- A lot of users logging into a system, impose limits on resources a user can use.
	- To set such limits -> `sudo vim /etc/security/limits.conf`
	- File has following info -> <domain> -> usually a user name, for groups use @group_name or use * to match everything (every user) its a way to set default limit because using * means limits that apply to users not mentioned in limits
	- <type> --> hard limit, soft limit (its startup value, if user has soft limit 10 upto whatever is mentioned their hard limit, so they can get slight increase if required) and dash (-) type, means its both soft and hard limit.
	- <item> ---> decides what this limit is for, e.g. nproc (max no. of processes for user) , fsize (maximum file size that can be created), cpu (cpu time in minutes).
	- `$ sudo ulimit -a`
	- user can only decrease and not raise over hard limit. but only once they can raise even if hard limit allows it. Cannot raise twice
- **Manage User Permissions**
  collapsed:: true
	- adding users to sudoers file
	- command `sudo visudo`
	- To run commands as different user -> `sudo -u trinity ls /home/trinity`
	- sudoers file format
		- user/group ALL=(ALL) ALL
		- first field user or grou, second is users third is commands
- **Manage Access to Root Account**
  collapsed:: true
	- To login to root user use $ `sudo --login` OR $ `sudo -i`
	- If you know root password -> `su -l` or `su`
	- when _root is locked_ , we can still use `sudo --login` but not `su -`
	- if it had not a password set we can use `sudo passwd root` set a new password
	- If root had a password set, but root is locked we can unlock it `sudo passwd --unlock root`
	- and then we use `su -`
	- Imagine - we can login as root and this is insecure ; to lock root `sudo passwd --lock root`
	- Kernel level -> when you don't have any login and need to change root password -> https://phoenixnap.com/kb/how-to-change-root-password-linux
	-
- **PAM** - Pluggable Authentication Module
  collapsed:: true
	- Gives flexibility on how we want certain utilities of Linux on how to authenticate.
	- PAM related files -> `etc/pam.d/`
	- edit su file here
	- Syntax of a PAM file -> service type control-flag module module-arguments
	-
- **Networking**
  collapsed:: true
	- Configure network and hostname statically or dynamically.
	- DHCP provides dynamic IP , Static IP is assigned manually.
	- `ip link show` -> This shows interfaces on system. Shorter form`ip l`
	- to see ip address -> `ip addresses show` or short form `ip a`
	- We can view routing table using `ip route show` or `ip r`
		- default via is IP address of default gateway.
	- To check DNS resolvers -> check fine`/etc/resolv.conf`
	- Every entry with nameserver is valid DNS resolver, fairly normal to see two or more dns resolver name servers.
	- Usually auto-configured via DHCP maybe, When operating system boots.
	- `/etc/sysconfig/network-scripts/` -> this directory has files names like _ifcfg-ethernetadaptername_ and route-adaptername
	- cat this file ifcfg , we can confirm multiple network configuration settings here.
	- Check BOOTPROTO, if it says equals to DHCP, server will use DHCP.
	- Network Manager Text User Interface (NMTUI)
		- `sudo nmtui`
		- it asks us to pick an option -> pick edit a connection
		- see your available network interface, choose that one
		- With that you move to different fields and clicks using tab and arrow keys.
		- Profile name can be anything, Device name can be interface name only.
		- Here you can add IP addresses, DNS names, DNS servers, Gateways, search domains etc.
		- Hybrid configuration is also possible, we can keep it dynamic for IP configuration and still provide another Static IP address
		- new settings won't be automatically applied, it needs reboot
		- Too get them applied -> `nmcli device reapply _nameofnetworkinterface_`
	- Hostnames - if we type google.com -> data goes to some ip address and you receive response.
		- `/etc/hosts file` -> static dns resolution
		- format is ipaddress hostname you want it to be resolved as
	- Starting Network services at boot
		- How to configure network services to start at boot
		- `systemctl status NetworkManager.service` --> check if service is running
		- you can install NetworkManager -> `dnf install NetworkManager`
		- Use this command to enable it so as it starts at boot -> `sudo systemctl enable NetworkManager`
		- nmcli connection show -> shows all connection
		- To modify -> `sudo nmcli connection modify connection name autocnnect yes` -> to connect at boot time.
	- **Starting** **Stopping** and **checking** network services.
		- Two utilities -> `ss` and `netstat`
		- To see programs waiting for incoming network connections ->`$ sudo ss -ltunp`
		- `-l` is listening / scanning for incoming connection, t flag is tcp , u is udp connections, n is numeric values (portnumbers), p flag shows processes. or `ss -tunlp`
		- Check Local address and port column in output.
		- Look for entries like 0.0.0.0 -> means it will accept connections from any IP address
		- Any entries like [::], means its looking for IPv6 connections
		- Under processes you can see process utilizing these ports
		- `ss` command also shows PID
		- `netstat` almost uses same options, `netstat -tunlp`
		-
	- **Packet Filtering**
		- How to implement packet filtering in Linux?
			- To enhance security firewalls are set up in order to allow packets. 
			  Red hat has default firewall called FIREWALLD.
			- Normally default Zone is used Public, everything is dropped except of what we allow. Other zones are DROP and TRUSTED.
			- How to check -> `$ firewall-cmd --get-default-zone`
			- To change default zone `$ firewall-cmd --set-default-zone=public`
			- To see all firewall rules --> `$ sudo firewall-cmd --list-all`
			- To see incoming connections see the services: line of above output
			- Say the service name was `cockpit`, to see ports of this service allowed use --> `$ sudo firewall-cmd --info-service=cockpit`
			- To allow traffic to http service (say we install a http server) -> use `$ sudo firewall-cmd --add-service=http` OR `$ sudo firewall-cmd --add-port=80/tcp`
			- To remove a service from list of accepted connections, we can do -> `$ sudo firewall-cmd --remove-service=http` OR `$ sudo firewall-cmd --remove-port=80/tcp`
			- In public zone logic is simple, all traffic is denied and allowed only to exceptions add.
			- Instead of above logic , we can choose to allow traffic from Trusted Zones using command -> `$ sudo firewall-cmd --add-source=10.11.12.0/24 --zone=trusted`
			- Trusted zone allows all connections from this zone.
			- `$ firewall-cmd --get-active-zones`
			- To remove policies based on zones or IP addresses -> `$ sudo firewall-cmd --remove-source=10.11.12.0/24 --zone=trusted`
			- All rules added here not permanent, once rebooted all are lost.
			- How to make permanent? add temporary as above , once we are satisfied with result, we can turn current set of rules to permanent --> `sudo firewall-cmd --runtime-to-permanent`
			- 2nd method to make permanent ---> `$ sudo firewall-cmd --add-port=1234/tcp --permanent`
		-
	- **Statically route IP Traffic**]
		- `sudo ip route add 192.168.0.0/24 via 10.0.0.100`
		- Above is how you route traffic to 192 network via 10.0 interface you have.
		- Say you have multiple interfaces (possibly with diff IP addresses) -> `$ sudo ip route add 192.168.0.0/24 via 10.11.12.100 dev enp0s3`
		- To delete previous route -> `$ sudo ip route del 192.168.0.0/24`
		- Adding default route -> `$ sudo ip route add default via 10.0.0.100`
		- To delete default route -> `$ sudo ip route del default via 10.0.0.100`
		- Routes added are temporary if we reboot all is lost.
		- Want to make permanent?
		- `nmcli connection show`
		- `sudo nmcli connection modify enps03 +ipv4.routes "192.168.0.0/24 10.0.0.100"`
		- `ip route show` --> shows all routes added
		- To delete permanent routes -> `sudo ncmli connection modify epns03 -ipv4.routes "192.168.0.0/24 10.0.0.100"`
		- Then reapply settings -> `sudo nmcli device reapply epns03`
		- GUI command -> `sudo nmtui`
		- Then reapply -> `sudo nmcli device reapply epns03`
		-
	- **Synchronize Time**
	  collapsed:: true
		- Drift happens in Clocks, server time drifts
		- Keeping accurate time is important.
		- Special software -> chrony daemon.
		- `systemctl status chronyd.service`
		- `timedatectl`
		- Say chronyd is not installed
			- ensure Timezone is set coorectly -> `sudo timedatectl set-timezone America/New_York`
			- To see all list `sudo timedatectl list-timezones`
			- Install Chrony daemon -> `sudo dnf install chrony`
			- start and enable it == `sudo systemctl start chronyd.service` `sudo systemctl enable chronyd.service`
			- `timedatectl`
			- `sudo systemctl set-ntp true`
			-
- **Service Configuration**
  collapsed:: true
	-
	- Configuring a caching DNS server
	- Why is DNS caching useful -> A computer needs to find out how it can reach website e.g. google.com
	  Goes to ISP's DNS server (say this was server launched 2secs ago it does not know anything)
	  Query goes to next DNS and next and next, once IP address is found it sends downstream and is cached.
	- Next Time -> When launched again -> we find the cached entry quicker.
	- Consider same locally, for high intensity caching to reduce delay, we want to enable our own caching server.
	- **bind** is a popular DNS utility
	- To install **bind** -> `sudo dnf install bind bind-utils` //two software packages bind and bind-utils , utils has extra programs.
	- bind config file is located at `/etc/named.conf/`. There are 100s of options to use, Focus on essential
	- For more refer `man named.conf`
	- Check current IP address of server -> `ip a`
	- To make changes to bind config -> `sudo vim /etc/named.conf`
		- listen-on port 53 {127.0.01;};               // bind is configured to listen on loopback address. This means it will accept connections from local host only, for other connections change to
		- listen-on port 53 {127.0.0.1; 192.168.17;};
		- for any network --> listen-on port 53 {any;};
		- allow-query {localhost;};                  //for programs on local host only requesting DNS information local connections only, for others ->
		- allow-query {localhost; 192.168.0.0/24;};             //local and other network
		- allow-query {any;};                                               // for any network
		- recursion yes;                                    // set to yes by default, helps bind server to get data from other DNS servers
	- Next start bind and it auto starts after reboot by --> `sudo systemctl start bind.service` & sudo `systemctl enable bind.service`
	- Add firewall rule -> `sudo firewall-cmd --add-service=dns`      // this is temporary
	- Add firewall rule -> `sudo firewall-cmd --add-service=dns --permanent`      // this is permanent
	- To check -> `dig @127.0.0.1 google.com` ==`dig @localhost google.com`
		- first time query time check ; run it again, query time will be 0 seconds. because now the data is cached.
		- In its default configuration, it automatically caches. we do not give explicit instructions
	- **Maintaining a DNS zone**
	  collapsed:: true
		- DNS server is also called name server
		- Consider we bough DNS example.com
		- A zone can group DNS data of specific domain, we can have zone for example.com and other for other domain
		- Edit bind main config file -> `sudo vim /etc/named.conf`
			- Go to end of file.
			- check for block starting with zone
			- add zone "example.com" IN {
			      type master;                                        // this is our master server
			      file "example.com.zone";
			  };
			- Save the file and add the zone file.
			- sudo ls /var/named/ --> we can see a file called named.localhost
			- `sudo cp --preserve=ownership /var/named/named.localhost /var/named/example.com.zone`
			- Edit the zone file now
			- `sudo vim /var/named/example.com.zone`
			- TTL is set to 1D, can change to 1H // 1 Day to 1 Hour
			- example.com.  A  203.20.113.30
			- @ IN SOA @ administrator.example.com.                     // . in end is not required for relative domain names. IN stands for INTERNET, can be omitted, its IN class.
			- @ (two tabs) NS ns1.example.com.                   // we are telling world what is our NameServer for example.com domain for DNS entries
			- @ (two tabs) NS ns2.example.com.
			- Devices do not know where ns2.example.com are located , so we add A records for these entries
			- ns1 (two tabs) A(two tabs) 10.11.12.9
			- ns2 (two tabs) A (two tabs)10.11.12.10              //relative domain names do not need .
			- @ (two tabs) A (two tabs) 203.0.113.15
			- www (two tabs) A (two tabs) 203.0.113.15
			- www CNAME 203.0.113.15                              // CNAME is like a redirection. Keep CNAME only not both www entries.
			- example.com. (two tabs) MX 10 mail.example.com
			                                             MX 20 mail2.example.com                 // 10, 20 are priorities
			- mail (two T.) A 203.0.113.80
			- mail2 (two T) A 203.0.113.81
			- server1 (two tabs)AAAA 2001:DB8:10::1
			- example.com.    TXT    "Can write anything here"
			- For bind to recognize above changes -> `sudo systemctl restart named.service`
			- `dig @localhost`
	- **Configuring EMAIL aliases**
	  collapsed:: true
		- Setting an entire email infra is complicated
		- Easy to setup a PoC to check how aliases work
		- `sudo dnf install postfix` and start and enable it // postfix is an email service
		- To test -> `sendmail aaraon@localhost <<< "Hello, Test email"`
		- To check where email is stored `cat /var/spool/mail/aaron`
		- Now to configure aliases to aarons mail box
			- Defined in `/etc/aliases`
			- `sudo nano /etc/aliases`
			- add this --> `advertising: aaron`
			- Save the file
			- Inform postfix of added new aliases - > `sudo newaliases`
			- `sendmail advertising@localhost <<< "Hello new "`
			- can also have a clone for three different mailboxes by
			  adding this entry in /etc/aliases 
			  `contact: aaron,john,jane`
			- To forward somewhere else add this entry 
			  `advertising:aaron@somecompany.com`
		-
	- **Configuring IMAP and IMAPS service**
	  collapsed:: true
		- Once we receive an email , we need to read it.
		- Internet Messages Access Protocol, need to read it via Oulook or similar apps
		- Client server synchronization
		- IMAP does not encrypt, IMAPS is IMAP over SSL, all network traffic is encrypted.
		- Install -> `sudo dnf install dovecot`
		- Now start using `systemctl start dovecot` and enable `systemctl enable dovecot`
		- `sudo firewall-cmd --add-service=imap`
		- `sudo firewall-cmd --add-service=imaps`
		- `sudo firewall-cmd --runtime-to-permanent`
		- check all config files at `/etc/dovecot/conf.d`
	- **Configuring SSH Servers Clients**
	  collapsed:: true
		- Server already runs OpenSSH daemon
		- Config file `/etc/ssh/sshd_config` -> **d refers to daemon**, there is also a ssh config file for client, that can be found `/etc/ssh/ssh_config`
		- `sudo nano /etc/ssh/sshd_config`
		- first important setting -> port number on which ssh daemon accepts incoming
		- `Port 22` -> commented , want to change uncomment it and change to whichever port you want
		- check man sshd_config , use search /Family , go to AddressFamily
		- if we want to only accept IPV4 connections, uncomment `AddressFamily` and use inet4
		- By default it listens for all available IPs
		- we can change to Listen to as well ->`ListenAddress 10.11.12.9`
		- search man page for `PermitRootLogin` -> default value is yes.
		- `PasswordAuthentication yes` is default , can change to no by uncommenting. Users can only login with SSH keys which is more secure.
		- To make single exception add this line below it
		- ```
		  Match User aaron
		         PasswordAuthentication yes
		  ```
		- search for x11forarding , default is set to yes, we can disable it globally.
		- sudo systemctl reload sshd.service
	- **What about Client configuration ?**
	  collapsed:: true
		- Client keeps some file in .ssh directory in home
		- ls -a goto  `~/.ssh`    --> Unix like systems directory
		- Windows its `C:\Users\aaron/.ssh`
		- man ssh_config
		- create a new file in ~/.ssh/ directory called config
			- Host centos
			           Hostname 10.11.12.9
			           Port 22
			           User aaron
		- chmod 600 ~/.ssh/config
	- **SSH Keys**
	  collapsed:: true
		- Generate a private and public key on client side
		- `ssh-keygen`   // can use options with it, but this commands work
		- private key is save at ~./ssh/ its saved as `id_rsa`
		- public key is saved as `id_rsa.pub`
		- Now we have to copy the public key to the server we want to login
		- How to copy ? Multiple ways
		  1. ssh-copy-id username@severip  //content of public key will be moved to username's home directory on the server and stored in `.ssh/authorized_keys`
		  2. Other way is edit the authorized keys manually the contents of public key to this file
		- whoever has private key to this public key can login
		-
		-
		-
		-
	- **HTTPS PROXY**
		- Commonly used proxy daemon available is squid.
		- Restrict access to the http proxy server
		- `sudo dnf install squid`
		- `sudo systemctl start squid` and enable the service as well.
		- add firewall rule -> `sudo firewall-cmd --add-service=squid --permanent`
		- `sudo vim /etc/squid/squid.conf` --> check access control list
		- acl localnet src xyz ---->
		- acl localnet src 10.11.12.0
		- acl external src 203.0.113.0/24
		- They don't actually any rules, they are defined filters but do not apply it
		- Deny request to unsafe ports `http_access deny !Safe_ports`
		- To apply changes reload --> `sudo systemctl reload squid.service`
		- This is graceful , restart is abruptive
	- ****
	-
	-
- **Storage**
	- **fdisk and cfdisk**
	  collapsed:: true
		- List, create, delete and modify physical storage partitions.
		  collapsed:: true
			- To see what partitions exist on a linux system -> `lsblk`
				- What we see in output are block devices. Places where linux can store data.
				- Only ones that have word part are partitions.
				- Devices in focus sda and its two partitions sda1 and sda2
				- s comes from serial.
				- last letter gives you hint of how many parts. Last letter makes it easy to know which disk and what partition it.
				- sda is first disk, sda1 is 1st part and sda2 is second partition
				- All block devices are found in `/dev` directory
				-
		- `sudo fdisk --list /dev/sda` --> fdisk is pre installed partition utility
		- sudo is needed to special permissions
		- A storage divided into sector. Sector is divided into 512 bytes
		- Bootloader area 0 to 2047 , first part sector will start from 2048
		- fdisk can be used to delete and create partitions
		- sudo cfdisk /dev/sdb  ---> pick gpt
		- Imagine you want to create two partitions 8 GB and 2 GB
		- Navigate to free space and select NEW button and select 8 GB , navigate up and down and select further for further functions.
		- Press down to remaining free space and parititon that to into 2 GB and hit enter.
		- Navigate to first partition -> go to resize and you can change from 8 GB to 4 GB --> now you will have some free space again and new resized part
		- now you may have sdb1 , sdb2  and sdb3 4 GB, 2GB and 4GB respectively (depends)
		- Go to SORT option and it will reorder the partitions in a natural way sdb1, sdb2 and sdb3 might now look 4G , 4 G and 2G respectively
		- Go to TYPE button after selecting 2G disk. and select SWAP option.
		- Go to WRITE option and write the partition table to DISK. type yes and changes are permanent.
		- QUIT cfdisk
		- Now check lsblk and you can see your changes have been made.
	- **Configure and manage swap space**
		- How to create a swap partition? Swap is area to move temporary some data from memory
		- Create and Manage Swap space -> Use of Swap space same as windows
			- Move unused data from RAM to Swap to free up memory
			- To check if system has any swap areas `swapon --show`
			- We can add more partitions as swap
			- lsblk - check partitions , identify partition with no data
			- `sudo mkswap /dev/vdb3` ---> tells linux that use this as swap
			- `swapon --show`
			- If we reboot , this partition will not be used as swap again.
			- To stop partition to be used as swap ->`swapoff /dev/vdb3`
			- `sudo dd if=/dev/zero of=/swap bs=1M count=128`  --> bs is block size , tells dd to write 1M block 128 times
			- add parameter `status=progress` to see progress
			- `sudo chmod 600 /swap`
			- sudo mkswap /swap
			- sudo swapon /swap
			-
			-
	- **Create and configure file systems**
		- `sudo mkfs.ext4 /dev/sdb1`
		- man mkfs.ext4 and man mkfs.xfs --> read man pages
	- **Configure systems to mount file systems at or during boot**
		- `sudo mount /dev/vdb1 /mnt/` --> to mount FS
		- `sudo umount /mnt`
	- **On Demand Mounting**
		- AutoFS 
		  `sudo dnf install autofs`
		- NFS -> Network File Sharing
		  `sudo dnf install nfs-utils`
			- Tell NFS server which directories to share with network
			- `sudo vim /etc/exports` -> /etc 127.0.0.1(ro) , ro option makes it read only
			- `sudo systemctl reload nsf-server.service`
		- For Auto FS to mount NFS shares
			- `sudo vim /etc/auto.master`
				- `/shares/ /etc/auto.shares --timeout=400`
			- `sudo vim /etc/auto.shares`
				- `mynetworkshare -fstype=auto 127.0.0.1:/etc`
			- `sudo systemctl reload autofs`
	- **Filesystem Features and Options** (Complete later)
	- findmnt -t xfs,ext4
	-
	- **Logical Volume Manager**
		- `sudo pvcreate /dev/sdc /dev/sdd`
		- `sudo pvs` --> see what physical volumes are currently attached
		- `sudo vgcreate my_volume /dev/sdc /dev/sdd` --> adding two disks to volume
		- `sudo pvcreate /dev/sdf`
		- `sudo vgextend my_volume /dev/sdf`
		- `sudo vgreduce my_volume /dev/sdf`
		- `sudo pvremove /dev/sdf`
		- `sudo lvcreate --size 2G --name partition1 my_volume`
		-
		-
		-
	-