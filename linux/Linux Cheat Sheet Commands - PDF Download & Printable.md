Here in this cheat sheet, Linux commands are categorized into different sections according to its usage. We have designed all the commands in a nice background color.

I have added had both pdf and image (png) format of the cheat sheet.

Download your [linux commands cheat sheet in pdf](https://images.linoxide.com/linux-cheat-sheet.pdf) format and please keep us posted if you have any suggestions or if you find any command that we missed out.

If you are looking to print [Linux commands cheat sheet in A4 size paper](https://images.linoxide.com/linux-commands-cheat-sheet-A4.pdf) its available for download.

[![Linux Commands Cheat Sheet](https://linoxide.com/images/linux-cheat-sheet-612x792.png)](https://linoxide.com/images/linux-cheat-sheet-612x792.png)

## 1) System

<table><tbody><tr><td><span><code>uname</code></span></td><td><span>&nbsp;Displays&nbsp;&nbsp;Linux system information</span></td></tr><tr><td><span><code>uname -r</code></span></td><td><span>Displays&nbsp; kernel release information</span></td></tr><tr><td><span><code>uptime</code></span></td><td><span>Displays how long the system has been running including load average</span></td></tr><tr><td><span><code>hostname</code></span></td><td><span>Shows the system hostname</span></td></tr><tr><td><span><code>hostname -i</code></span></td><td><span>Displays the IP address of the system</span></td></tr><tr><td><span><code>last reboot</code></span></td><td><span>Shows system reboot history</span></td></tr><tr><td><span><code>date</code></span></td><td><span>Displays current system date and time</span></td></tr><tr><td><span><code>timedatectl</code></span></td><td><span>Query and change the System clock</span></td></tr><tr><td><span><code>cal</code></span></td><td><span>Displays the current calendar month and day</span></td></tr><tr><td><span><code>w</code></span></td><td><span>Displays currently&nbsp; logged in users in the system</span></td></tr><tr><td><span><code>whoami</code></span></td><td><span>Displays who you are logged in as</span></td></tr><tr><td><span><code>finger username</code></span></td><td><span>Displays information about the user</span></td></tr></tbody></table>

## 2) Hardware

<table><tbody><tr><td><span><code>dmesg</code></span></td><td><span>Displays bootup messages</span></td></tr><tr><td><span><code>cat /proc/cpuinfo</code></span></td><td><span>Displays more information about CPU e.g model, model name, cores, vendor id</span></td></tr><tr><td><span><code>cat /proc/meminfo</code></span></td><td><span>Displays more information about hardware memory e.g. Total and Free memory</span></td></tr><tr><td><span><code>lshw</code></span></td><td><span>Displays information about system's hardware configuration</span></td></tr><tr><td><span><code>lsblk</code></span></td><td><span>Displays block devices related information</span></td></tr><tr><td><span><code>free -m</code></span></td><td><span>Displays free and used memory in the system (-m flag indicates memory in MB)</span></td></tr><tr><td><span><code>lspci -tv</code></span></td><td><span>Displays PCI devices in a tree-like&nbsp;diagram</span></td></tr><tr><td><span><code>lsusb&nbsp;-tv</code></span></td><td><span>Displays USB devices in a tree-like diagram</span></td></tr><tr><td><span><code>dmidecode</code></span></td><td><span>Displays hardware information from the BIOS</span></td></tr><tr><td><span><code>hdparm&nbsp;-i /dev/xda</code></span></td><td><span>Displays information about disk data</span></td></tr><tr><td><span><code>hdparm&nbsp;-tT /dev/xda&nbsp;&lt;:code&gt;</code></span></td><td><span>Conducts a read speed test on device xda</span></td></tr><tr><td><span><code>badblocks&nbsp;-s /dev/xda</code></span></td><td><span>Tests&nbsp; for unreadable blocks on disk</span></td></tr></tbody></table>

## 3) Users

<table><tbody><tr><td><span><code>id</code></span></td><td><span>Displays the details of the active user e.g. uid, gid, and groups</span></td></tr><tr><td><span><code>last</code></span></td><td><span>Shows the last logins in the system</span></td></tr><tr><td><span><code>who</code></span></td><td><span>Shows who is logged in to the system</span></td></tr><tr><td><span><code>groupadd "admin"</code></span></td><td><span>Adds the group 'admin'</span></td></tr><tr><td><span><code>adduser "Sam"</code></span></td><td><span>Adds user Sam</span></td></tr><tr><td><span><code>userdel "Sam"</code></span></td><td><span>Deletes user Sam</span></td></tr><tr><td><span><code>usermod</code></span></td><td><span>Used for changing / modifying user information</span></td></tr></tbody></table>

## 4) File Commands

<table><tbody><tr><td><span><code>ls -al</code></span></td><td><span>Lists files - both regular &amp;&nbsp; hidden files and their permissions as well.</span></td></tr><tr><td><span><code>pwd</code></span></td><td><span>Displays the current directory file path</span></td></tr><tr><td><span><code>mkdir 'directory_name'</code></span></td><td><span>Creates a new directory</span></td></tr><tr><td><span><code>rm file_name</code></span></td><td><span>Removes a file</span></td></tr><tr><td><span><code>rm -f filename</code></span></td><td><span>Forcefully removes a file</span></td></tr><tr><td><span><code>rm -r directory_name</code></span></td><td><span>Removes a directory recursively</span></td></tr><tr><td><span><code>rm -rf directory_name</code></span></td><td><span>Removes a directory forcefully and recursively</span></td></tr><tr><td><span><code>cp file1 file2</code></span></td><td><span>Copies the contents of file1 to file2</span></td></tr><tr><td><span><code>cp -r dir1 dir2</code></span></td><td><span>Recursively Copies dir1 to dir2. dir2 is created if it does not exist</span></td></tr><tr><td><span><code>mv file1 file2</code></span></td><td><span>Renames file1 to file2</span></td></tr><tr><td><span><code>ln -s /path/to/file_name&nbsp; &nbsp;link_name</code></span></td><td><span>Creates a symbolic link to file_name</span></td></tr><tr><td><span><code>touch file_name</code></span></td><td><span>Creates a new file</span></td></tr><tr><td><span><code>cat &gt; file_name</code></span></td><td><span>Places standard input into a file</span></td></tr><tr><td><span><code>more file_name</code></span></td><td><span>Outputs the contents of a file</span></td></tr><tr><td><span><code>head file_name</code></span></td><td><span>Displays the first 10 lines of a file</span></td></tr><tr><td><code><span>tail file_name</span></code></td><td><span>Displays the last 10 lines of a file</span></td></tr><tr><td><span><code>gpg -c file_name</code></span></td><td><span>Encrypts a file</span></td></tr><tr><td><span><code>gpg file_name.gpg</code></span></td><td><span>Decrypts a file</span></td></tr><tr><td><span><code>wc</code></span></td><td><span>Prints the number of bytes, words and lines in a file</span></td></tr><tr><td><span><code>xargs</code></span></td><td><span>Executes commands from standard input</span></td></tr></tbody></table>

## 5) Process Related

<table><tbody><tr><td><span><code>ps</code></span></td><td><span>Display currently active processes</span></td></tr><tr><td><span><code>ps aux | grep 'telnet'</code></span></td><td><span>Searches for the id of the process 'telnet'</span></td></tr><tr><td><span><code>pmap</code></span></td><td><span>Displays memory map of processes</span></td></tr><tr><td><span><code>top</code></span></td><td><span>&nbsp;Displays all running processes</span></td></tr><tr><td><span><code>kill pid</code></span></td><td><span>Terminates process with a given pid</span></td></tr><tr><td><span><code>killall proc</code></span></td><td><span>Kills / Terminates all processes named proc</span></td></tr><tr><td><span><code>pkill process-name</code></span></td><td><span>Sends&nbsp;a signal to a process with its name</span></td></tr><tr><td><span><code>bg</code></span></td><td><span>Resumes suspended jobs in the background</span></td></tr><tr><td><span><code>fg</code></span></td><td><span>Brings suspended jobs to the foreground</span></td></tr><tr><td><span><code>fg n</code></span></td><td><span>job n to the foreground</span></td></tr><tr><td><span><code>lsof</code></span></td><td><span>Lists files that are open by processes</span></td></tr><tr><td><span><code>renice 19 PID</code></span></td><td><span>makes a process run with very low priority</span></td></tr><tr><td><span><code>pgrep firefox</code></span></td><td><span>find Firefox process ID</span></td></tr><tr><td><span><code>pstree</code></span></td><td><span>visualizing processes in tree model</span></td></tr></tbody></table>

## 6) File Permission

<table><tbody><tr><td><span><code>chmod octal filename</code> &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Change file permissions of the file to octal</span></td></tr><tr><td><span>&nbsp;</span></td><td>&nbsp;</td></tr><tr><td><strong><span>Example</span></strong></td><td><span>&nbsp;</span></td></tr><tr><td><span><code>chmod 777 /data/test.c</code> &nbsp; &nbsp; &nbsp;</span></td><td><span>Set rwx permissions to owner, group and everyone (everyone else who has access to the server)</span></td></tr><tr><td><span><code>chmod 755 /data/test.c</code> &nbsp; &nbsp; &nbsp;</span></td><td><span>Set rwx to the owner and r_x to group and everyone</span></td></tr><tr><td><span><code>chmod&nbsp;766 /data/test.c</code>&nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Sets rwx for owner, rw for group and everyone</span></td></tr><tr><td><span><code>chown owner user-file</code> &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Change ownership of the file</span></td></tr><tr><td><span><code>chown&nbsp;owner-user:owner-group file_name </code>&nbsp; &nbsp; &nbsp;</span></td><td><span>Change owner and group owner of the file</span></td></tr><tr><td><span><code>chown owner-user:owner-group directory</code> &nbsp;</span></td><td><span>Change owner and group owner of the directory</span></td></tr></tbody></table>

## 7) Network

<table><tbody><tr><td><span><code>ip addr show</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Displays IP addresses and all the network interfaces</span></td></tr><tr><td><span><code>ip address add 192.168.0.1/24 dev eth0</code>&nbsp; &nbsp;</span></td><td><span>Assigns IP address 192.168.0.1 to interface eth0</span></td></tr><tr><td><span><code>ifconfig&nbsp;</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Displays IP addresses of all network interfaces</span></td></tr><tr><td><span><code>ping&nbsp; host</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>ping command sends an ICMP echo request to establish a connection to server / PC</span></td></tr><tr><td><span><code>whois domain</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Retrieves more information about a domain name</span></td></tr><tr><td><span><code>dig domain</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;</span></td><td><span>Retrieves DNS information about the domain</span></td></tr><tr><td><span><code>dig -x host&nbsp;</code> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Performs reverse lookup on a domain</span></td></tr><tr><td><span><code>host google.com&nbsp;</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Performs an IP lookup for the domain name</span></td></tr><tr><td><span><code>hostname -i</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Displays local IP address</span></td></tr><tr><td><span><code>wget file_name</code>&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Downloads a file from an online source</span></td></tr><tr><td><span><code>netstat -pnltu</code>&nbsp; &nbsp; &nbsp;</span></td><td><span>Displays all active listening ports</span></td></tr></tbody></table>

## 8) Compression/Archives

<table><tbody><tr><td><span><code>tar -cf home.tar home&lt;:code&gt;</code></span></td><td><span>Creates archive file called 'home.tar' from file 'home'</span></td></tr><tr><td><span><code>tar -xf files.tar</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Extract archive file 'files.tar'</span></td></tr><tr><td><span><code>tar -zcvf home.tar.gz source-folder</code>&nbsp; &nbsp;</span></td><td><span>Creates gzipped tar archive file from the source folder</span></td></tr><tr><td><span><code>gzip file</code>&nbsp;</span></td><td><span>Compression a file with .gz extension</span></td></tr></tbody></table>

## 9) Install Packages

<table><tbody><tr><td><span><code>rpm -i pkg_name.rpm</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Install an rpm package</span></td></tr><tr><td><span><code>rpm -e pkg_name</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Removes an rpm package</span></td></tr><tr><td><span><code>dnf install pkg_name</code></span></td><td><span>Install package using dnf utility</span></td></tr></tbody></table>

## 10) Install Source (Compilation)

<table><tbody><tr><td><span><code>./configure</code></span></td><td><span>Checks your system for the required software needed to build the program. It will build the Makefile containing the instructions required to effectively build the project</span></td></tr><tr><td><span><code>make</code></span></td><td><span>It reads the Makefile to compile the program with the required operations. The process may take some time, depending on your system and the size of the program</span></td></tr><tr><td><span><code>make install</code></span></td><td><span>The command installs the binaries in the default/modified paths after the compilation</span></td></tr></tbody></table>

## 11) Search

<table><tbody><tr><td><span><code>grep 'pattern' files</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Search for a given pattern in files</span></td></tr><tr><td><span><code>grep -r pattern dir</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Search recursively for a pattern in a given directory</span></td></tr><tr><td><span><code>locate file</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Find all instances of the file</span></td></tr><tr><td><span><code>find /home/ -name "index"&nbsp;</code> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Find file names that begin with 'index' in /home folder</span></td></tr><tr><td><span><code>find /home -size +10000k</code></span></td><td><span>Find files greater than 10000k in the home folder</span></td></tr></tbody></table>

## 12) Login

<table><tbody><tr><td><span><code>ssh user@host</code> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Securely connect to host as user</span></td></tr><tr><td><span><code>ssh -p port_number user@host&nbsp;</code> &nbsp; &nbsp;</span></td><td><span>Securely connect to host using a specified port</span></td></tr><tr><td><span><code>ssh host</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Securely connect to the system via SSH default port 22</span></td></tr><tr><td><span><code>telnet host</code>&nbsp;</span></td><td><span>Connect to host via telnet default port 23</span></td></tr></tbody></table>

## 13) File Transfer

<table><tbody><tr><td><span><code>scp file1.txt server2/tmp</code>&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Securely copy file1.txt to server2 in /tmp directory</span></td></tr><tr><td><span><code>rsync -a /home/apps&nbsp; /backup/</code>&nbsp;</span></td><td><span>Synchronize contents in /home/apps directory with /backup&nbsp; directory</span></td></tr></tbody></table>

## 14) Disk Usage

<table><tbody><tr><td><span><code>df&nbsp; -h</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Displays free space on mounted systems</span></td></tr><tr><td><span><code>df&nbsp; -i&nbsp;</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Displays free inodes on filesystems</span></td></tr><tr><td><span><code>fdisk&nbsp; -l</code>&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Shows disk partitions, sizes, and types</span></td></tr><tr><td><span><code>du&nbsp; -sh</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Displays disk usage in the current directory in a human-readable format</span></td></tr><tr><td><span><code>findmnt</code> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Displays target mount point for all filesystems</span></td></tr><tr><td><span><code>mount device-path mount-point</code></span></td><td><span>Mount a device</span></td></tr></tbody></table>

## 15) Directory Traverse

<table><tbody><tr><td><span><code>cd ..</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span></td><td><span>Move up one level in the directory tree structure</span></td></tr><tr><td><span><code>cd</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;</span></td><td><span>Change directory to $HOME directory</span></td></tr><tr><td><span><code>cd /test</code>&nbsp;</span></td><td><span>Change directory to /test directory</span></td></tr></tbody></table>

### Read Also:

-   [38 Basic Linux Commands to Learn with Examples](https://linoxide.com/essential-linux-basic-commands/)
-   [A Brief Outline of 106 Linux Commands with Examples](https://linoxide.coms-brief-outline-examples/)